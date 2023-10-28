### 前言
对象的内存分配，往大的方向上讲，就是在堆上分配，少数情况下也可能会直接分配在老年代中，分配的规则并不是百分之百固定的，其细节决定于当前使用的是哪种垃圾收集器组合，当然还有虚拟机中与内存相关的参数。垃圾收集器组合一般就是Serial+Serial Old和Parallel+Serial Old，前者是Client模式下的默认垃圾收集器组合，后者是Server模式下的默认垃圾收集器组合，文章使用对比学习法对比Client模式下和Server模式下同一条对象分配原则有什么区别。
### TLAB
首先讲讲什么是TLAB。内存分配的动作，可以按照线程划分在不同的空间之中进行，即每个线程在Java堆中预先分配一小块内存，称为本地线程分配缓冲（Thread Local Allocation Buffer，TLAB）。哪个线程需要分配内存，就在哪个线程的TLAB上分配。虚拟机是否使用TLAB，可以通过-XX:+/-UseTLAB参数来设定。这么做的目的之一，也是为了并发创建一个对象时，保证创建对象的线程安全性。TLAB比较小，直接在TLAB上分配内存的方式称为快速分配方式，而TLAB大小不够，导致内存被分配在Eden区的内存分配方式称为慢速分配方式。
#### 一、对象优先在Eden区分配
对象通常在新生代的Eden区进行分配，当Eden区没有足够空间进行分配时，虚拟机将发起一次Minor GC，与Minor GC对应的是Major GC、Full GC。
##### Minor GC:指发生在新生代的垃圾收集动作，非常频繁，速度较快。
##### Major GC:指发生在老年代的GC，出现Major GC，经常会伴随一次Minor GC，同时Minor GC也会引起Major GC，一般在GC日志中统称为GC，不频繁。
##### Full GC:指发生在老年代和新生代的GC，速度很慢，需要Stop The World。
来看下面一段代码，虚拟机参数为“-verbose:gc -XX:+PrintGCDetails -Xms20M -Xmx20M -Xmn10M -XX:SurvivorRatio=8”，即10M新生代，10M老年代，10M新生代中8M的Eden区，两个Survivor区各1M。
```java
public class EdenAllocationTest
{
    private static final int _1MB = 1024 * 1024;
    
    public static void main(String[] args)
    {
        byte[] allocation1 = new byte[2 * _1MB];
        byte[] allocation2 = new byte[2 * _1MB];
        byte[] allocation3 = new byte[2 * _1MB];
        byte[] allocation4 = new byte[4 * _1MB];
    }
}
```
Client模式下：
```java
[GC [DefNew: 6487K->194K(9216K), 0.0042856 secs] 6487K->6338K(19456K), 0.0043281 secs] [Times: user=0.00 sys=0.00, real=0.00 secs] 
Heap
 def new generation   total 9216K, used 4454K [0x0000000005180000, 0x0000000005b80000, 0x0000000005b80000)
  eden space 8192K,  52% used [0x0000000005180000, 0x00000000055a9018, 0x0000000005980000)
  from space 1024K,  18% used [0x0000000005a80000, 0x0000000005ab0810, 0x0000000005b80000)
  to   space 1024K,   0% used [0x0000000005980000, 0x0000000005980000, 0x0000000005a80000)
 tenured generation   total 10240K, used 6144K [0x0000000005b80000, 0x0000000006580000, 0x0000000006580000)
   the space 10240K,  60% used [0x0000000005b80000, 0x0000000006180048, 0x0000000006180200, 0x0000000006580000)
 compacting perm gen  total 21248K, used 2982K [0x0000000006580000, 0x0000000007a40000, 0x000000000b980000)
   the space 21248K,  14% used [0x0000000006580000, 0x0000000006869890, 0x0000000006869a00, 0x0000000007a40000)
No shared spaces configured.
```
Server模式下：
```java
Heap
 PSYoungGen      total 9216K, used 6651K [0x000000000af20000, 0x000000000b920000, 0x000000000b920000)
  eden space 8192K, 81% used [0x000000000af20000,0x000000000b59ef70,0x000000000b720000)
  from space 1024K, 0% used [0x000000000b820000,0x000000000b820000,0x000000000b920000)
  to   space 1024K, 0% used [0x000000000b720000,0x000000000b720000,0x000000000b820000)
 PSOldGen        total 10240K, used 4096K [0x000000000a520000, 0x000000000af20000, 0x000000000af20000)
  object space 10240K, 40% used [0x000000000a520000,0x000000000a920018,0x000000000af20000)
 PSPermGen       total 21248K, used 2972K [0x0000000005120000, 0x00000000065e0000, 0x000000000a520000)
  object space 21248K, 13% used [0x0000000005120000,0x0000000005407388,0x00000000065e0000)
```
看到在**Client模式下，最后分配的4M在新生代中，先分配的6M在老年代中；在Server模式下，最后分配的4M在老年代中，先分配的6M在新生代中**。说明不同的垃圾收集器组合对于对象的分配是有影响的。讲下两者差别的原因：
1、Client模式下，新生代分配了6M，虚拟机在GC前有6487K，比6M也就是6144K多，多主要是因为TLAB和EdenAllocationTest这个对象占的空间，TLAB可以通过“-XX:+PrintTLAB”这个虚拟机参数来查看大小。OK，6M多了，然后来了一个4M的，Eden+一个Survivor总共就9M不够分配了，这时候就会触发一次Minor GC。但是触发Minor GC也没用，因为allocation1、allocation2、allocation3三个引用还存在，另一块1M的Survivor也不够放下这6M，那么这次Minor GC的效果其实是通过分配担保机制将这6M的内容转入老年代中。然后再来一个4M的，由于此时Minor GC之后新生代只剩下了194K了，够分配了，所以4M顺利进入新生代。
2、Server模式下，前面都一样，但是在GC的时候有一点区别。在GC前还会进行一次判断，如果要分配的内存>=Eden区大小的一半，那么会直接把要分配的内存放入老年代中。要分配4M，Eden区8M，刚好一半，而且老年代10M，够分配，所以4M就直接进入老年代去了。为了验证一下结论，我们把3个2M之后分配的4M改为3M看一下
```java
public class EdenAllocationTest
{
    private static final int _1MB = 1024 * 1024;
    
    public static void main(String[] args)
    {
        byte[] allocation1 = new byte[2 * _1MB];
        byte[] allocation2 = new byte[2 * _1MB];
        byte[] allocation3 = new byte[2 * _1MB];
        byte[] allocation4 = new byte[3 * _1MB];
    }
}
```
运行结果为：
```java
[GC [PSYoungGen: 6487K->352K(9216K)] 6487K->6496K(19456K), 0.0035661 secs] [Times: user=0.00 sys=0.00, real=0.00 secs] 
[Full GC [PSYoungGen: 352K->0K(9216K)] [PSOldGen: 6144K->6338K(10240K)] 6496K->6338K(19456K) [PSPermGen: 2941K->2941K(21248K)], 0.0035258 secs] [Times: user=0.02 sys=0.00, real=0.00 secs] 
Heap
 PSYoungGen      total 9216K, used 3236K [0x000000000af40000, 0x000000000b940000, 0x000000000b940000)
  eden space 8192K, 39% used [0x000000000af40000,0x000000000b269018,0x000000000b740000)
  from space 1024K, 0% used [0x000000000b740000,0x000000000b740000,0x000000000b840000)
  to   space 1024K, 0% used [0x000000000b840000,0x000000000b840000,0x000000000b940000)
 PSOldGen        total 10240K, used 6338K [0x000000000a540000, 0x000000000af40000, 0x000000000af40000)
  object space 10240K, 61% used [0x000000000a540000,0x000000000ab70858,0x000000000af40000)
 PSPermGen       total 21248K, used 2982K [0x0000000005140000, 0x0000000006600000, 0x000000000a540000)
  object space 21248K, 14% used [0x0000000005140000,0x0000000005429890,0x0000000006600000)
```
看到3M在新生代中，6M通过分配担保机制进入老年代了。
#### 二、大对象直接进入老年代
需要大量连续内存空间的Java对象称为大对象，大对象的出现会导致提前触发垃圾收集以获取更大的连续的空间来进行大对象的分配。虚拟机提供了-XX:PretenureSizeThreadshold参数来设置大对象的阈值，超过阈值的对象直接分配到老年代。
看下面的代码，虚拟机参数为“-XX:+PrintGCDetails -Xms20M -Xmx20M -Xmn10M -XX:SurvivorRatio=8 -XX:PretenureSizeThreshold=3145728”，最后那个参数表示大于这个设置值的对象直接在老年代中分配，这样做的目的是为了避免在Eden区和两个Survivor区之间发生大量的内存复制。
```java
public class OldTest
{
    private static final int _1MB = 1024 * 1024;
    
    public static void main(String[] args)
    {
         byte[] allocation = new byte[4 * _1MB];
    }
}
```
Client模式下
```java
Heap
 def new generation   total 9216K, used 507K [0x0000000005140000, 0x0000000005b40000, 0x0000000005b40000)
  eden space 8192K,   6% used [0x0000000005140000, 0x00000000051bef28, 0x0000000005940000)
  from space 1024K,   0% used [0x0000000005940000, 0x0000000005940000, 0x0000000005a40000)
  to   space 1024K,   0% used [0x0000000005a40000, 0x0000000005a40000, 0x0000000005b40000)
 tenured generation   total 10240K, used 4096K [0x0000000005b40000, 0x0000000006540000, 0x0000000006540000)
   the space 10240K,  40% used [0x0000000005b40000, 0x0000000005f40018, 0x0000000005f40200, 0x0000000006540000)
 compacting perm gen  total 21248K, used 2972K [0x0000000006540000, 0x0000000007a00000, 0x000000000b940000)
   the space 21248K,  13% used [0x0000000006540000, 0x00000000068272a0, 0x0000000006827400, 0x0000000007a00000)
No shared spaces configured.
```
Server模式下
```java
Heap
 PSYoungGen      total 9216K, used 4603K [0x000000000afc0000, 0x000000000b9c0000, 0x000000000b9c0000)
  eden space 8192K, 56% used [0x000000000afc0000,0x000000000b43ef40,0x000000000b7c0000)
  from space 1024K, 0% used [0x000000000b8c0000,0x000000000b8c0000,0x000000000b9c0000)
  to   space 1024K, 0% used [0x000000000b7c0000,0x000000000b7c0000,0x000000000b8c0000)
 PSOldGen        total 10240K, used 0K [0x000000000a5c0000, 0x000000000afc0000, 0x000000000afc0000)
  object space 10240K, 0% used [0x000000000a5c0000,0x000000000a5c0000,0x000000000afc0000)
 PSPermGen       total 21248K, used 2972K [0x00000000051c0000, 0x0000000006680000, 0x000000000a5c0000)
  object space 21248K, 13% used [0x00000000051c0000,0x00000000054a72a0,0x0000000006680000)
```
看到Client模式下Eden空间几乎没有被使用，而老年代的10MB空间被使用了40%，也就是4MB的allocation对象直接就分配在老年代中，这是因为 PretenureSizeThreshold 被设置为3MB（就是3145728，这个参数不能像-Xmx 之类的参数一样直接写3MB），因此超过3MB的对象都会直接在老年代进行分配。**Server模式下4M还在新生代中**。产生这个差别的原因是**“-XX:PretenureSizeThreshold”这个参数对Serial+Serial Old垃圾收集器组合有效而对Parallel+Serial Old垃圾收集器组合无效**。
#### 三、长期存活的对象进入老年代
每个对象有一个对象年龄计数器，与前面的对象的存储布局中的GC分代年龄对应。对象出生在Eden区、经过一次Minor GC后仍然存活，并能够被Survivor容纳，设置年龄为1，对象在Survivor区每次经过一次Minor GC，年龄就加1，当年龄达到一定程度（默认15），就晋升到老年代，虚拟机提供了-XX:MaxTenuringThreshold来进行设置。
具体代码如下：
```java
public class AllocationTest {
    private static final int _1MB = 1024 * 1024;
    
    /*
     *     -Xms20M -Xmx20M -Xmn10M 
        -XX:SurvivorRatio=8 
        -XX:+PrintGCDetails
        -XX:+UseSerialGC
        -XX:MaxTenuringThreshold=1
        -XX:+PrintTenuringDistribution
     * */
    public static void testTenuringThreshold() {
        byte[] allocation1, allocation2, allocation3;
        allocation1 = new byte[_1MB / 4];
        allocation2 = new byte[4 * _1MB];
        allocation3 = new byte[4 * _1MB];
        allocation3 = null;
        allocation3 = new byte[4 * _1MB];
    }
    
    public static void main(String[] args) {
        testPretenureSizeThreshold();
    }
}
```
运行结果：
```java
[GC (Allocation Failure) [DefNew
Desired survivor size 524288 bytes, new threshold 1 (max 1)
- age   1:     790400 bytes,     790400 total
: 5174K->771K(9216K), 0.0050541 secs] 5174K->4867K(19456K), 0.0051088 secs] [Times: user=0.00 sys=0.00, real=0.00 secs] 
[GC (Allocation Failure) [DefNew
Desired survivor size 524288 bytes, new threshold 1 (max 1)
: 4867K->0K(9216K), 0.0015279 secs] 8963K->4867K(19456K), 0.0016327 secs] [Times: user=0.00 sys=0.00, real=0.00 secs] 
Heap
 def new generation   total 9216K, used 4260K [0x00000000fec00000, 0x00000000ff600000, 0x00000000ff600000)
  eden space 8192K,  52% used [0x00000000fec00000, 0x00000000ff0290e0, 0x00000000ff400000)
  from space 1024K,   0% used [0x00000000ff400000, 0x00000000ff400000, 0x00000000ff500000)
  to   space 1024K,   0% used [0x00000000ff500000, 0x00000000ff500000, 0x00000000ff600000)
 tenured generation   total 10240K, used 4867K [0x00000000ff600000, 0x0000000100000000, 0x0000000100000000)
   the space 10240K,  47% used [0x00000000ff600000, 0x00000000ffac0d30, 0x00000000ffac0e00, 0x0000000100000000)
 Metaspace       used 2562K, capacity 4486K, committed 4864K, reserved 1056768K
  class space    used 275K, capacity 386K, committed 512K, reserved 1048576K
```
说明：发生了两次Minor GC，第一次是在给allocation3进行分配的时候会出现一次Minor GC，此时survivor区域不能容纳allocation2，但是可以容纳allocation1，所以allocation1将会进入survivor区域并且年龄为1，达到了阈值，将在下一次GC时晋升到老年代，而allocation2则会通过担保机制进入老年代。第二次发生GC是在第二次给allocation3分配空间时，这时，allocation1的年龄加1，晋升到老年代，此次GC也可以清理出原来allocation3占据的4MB空间，将allocation3分配在Eden区。所以，最后的结果是allocation1、allocation2在老年代，allocation3在Eden区。
#### 四、动态对象年龄判断
对象的年龄到达了MaxTenuringThreshold可以进入老年代，同时，如果在survivor区中相同年龄所有对象大小的总和大于survivor区的一半，年龄大于等于该年龄的对象就可以直接进入老年代。无需等到MaxTenuringThreshold中要求的年龄。
具体代码如下：
```java
public class AllocationTest {
    private static final int _1MB = 1024 * 1024;
    
    /*
     *     -Xms20M -Xmx20M -Xmn10M 
        -XX:SurvivorRatio=8 
        -XX:+PrintGCDetails
        -XX:+UseSerialGC
        -XX:MaxTenuringThreshold=15
        -XX:+PrintTenuringDistribution
     * */
    
    public static void testTenuringThreshold2() {
        byte[] allocation1, allocation2, allocation3, allocation4;
        allocation1 = new byte[_1MB / 4];
        allocation2 = new byte[_1MB / 4];
        allocation3 = new byte[4 * _1MB];
        allocation4 = new byte[4 * _1MB];
        allocation4 = null;
        allocation4 = new byte[4 * _1MB];
    }
    
    public static void main(String[] args) {
        testPretenureSizeThreshold2();
    }
}
```
运行结果：
```java
[GC (Allocation Failure) [DefNew
Desired survivor size 524288 bytes, new threshold 1 (max 15)
- age   1:    1048576 bytes,    1048576 total
: 5758K->1024K(9216K), 0.0049451 secs] 5758K->5123K(19456K), 0.0049968 secs] [Times: user=0.01 sys=0.00, real=0.00 secs] 
[GC (Allocation Failure) [DefNew
Desired survivor size 524288 bytes, new threshold 15 (max 15)
: 5120K->0K(9216K), 0.0016442 secs] 9219K->5123K(19456K), 0.0016746 secs] [Times: user=0.00 sys=0.00, real=0.00 secs] 
Heap
 def new generation   total 9216K, used 4178K [0x00000000fec00000, 0x00000000ff600000, 0x00000000ff600000)
  eden space 8192K,  51% used [0x00000000fec00000, 0x00000000ff014930, 0x00000000ff400000)
  from space 1024K,   0% used [0x00000000ff400000, 0x00000000ff400000, 0x00000000ff500000)
  to   space 1024K,   0% used [0x00000000ff500000, 0x00000000ff500000, 0x00000000ff600000)
 tenured generation   total 10240K, used 5123K [0x00000000ff600000, 0x0000000100000000, 0x0000000100000000)
   the space 10240K,  50% used [0x00000000ff600000, 0x00000000ffb00f80, 0x00000000ffb01000, 0x0000000100000000)
 Metaspace       used 2568K, capacity 4486K, committed 4864K, reserved 1056768K
  class space    used 275K, capacity 386K, committed 512K, reserved 1048576K
```
结果说明：发生了两次Minor GC，第一次发生在给allocation4分配内存时，此时allocation1、allocation2将会进入survivor区，而allocation3通过担保机制将会进入老年代。第二次发生在给allocation4分配内存时，此时，survivor区的allocation1、allocation2达到了survivor区容量的一半，将会进入老年代，此次GC可以清理出allocation4原来的4MB空间，并将allocation4分配在Eden区。最终，allocation1、allocation2、allocation3在老年代，allocation4在Eden区。
#### 五、空间分配担保
在发生Minor GC时，虚拟机会检查老年代连续的空闲区域是否大于新生代所有对象的总和，若成立，则说明Minor GC是安全的，否则，虚拟机需要查看HandlePromotionFailure的值，看是否运行担保失败，若允许，则虚拟机继续检查老年代最大可用的连续空间是否大于历次晋升到老年代对象的平均大小，若大于，将尝试进行一次Minor GC；若小于或者HandlePromotionFailure设置不运行冒险，那么此时将改成一次Full GC，以上是JDK Update 24之前的策略，之后的策略改变了，只要老年代的连续空间大于新生代对象总大小或者历次晋升的平均大小就会进行Minor GC，否则将进行Full GC。
冒险是指经过一次Minor GC后有大量对象存活，而新生代的survivor区很小，放不下这些大量存活的对象，所以需要老年代进行分配担保，把survivor区无法容纳的对象直接进入老年代。
具体的流程图如下：
![](https://images.cherryfloris.eu.org/2022/1664034546478-b1f03470-65f7-4d40-96b5-6d61ff7f13c4.png)
![](https://images.cherryfloris.eu.org/2022/1664034546474-44735af9-18b3-47ec-af73-35f99d45ef94.png)
具体代码如下：
```java
public class AllocationTest {
    private static final int _1MB = 1024 * 1024;
    
    /*
     *     -Xms20M -Xmx20M -Xmn10M 
        -XX:SurvivorRatio=8 
        -XX:+PrintGCDetails
        -XX:+UseSerialGC
        -XX:+HandlePromotionFailure
     * */
    
    public static void testHandlePromotion() {
        byte[] allocation1, allocation2, allocation3, allocation4, allocation5, allocation6, allocation7,
        allocation8;
        allocation1 = new byte[2 * _1MB];
        allocation2 = new byte[2 * _1MB];
        allocation3 = new byte[2 * _1MB];
        allocation1 = null;
        allocation4 = new byte[2 * _1MB];
        allocation5 = new byte[2 * _1MB];
        allocation6 = new byte[2 * _1MB];
        allocation4 = null;
        allocation5 = null;
        allocation6 = null;
        allocation7 = new byte[2 * _1MB];
    }
    
    public static void main(String[] args) {
        testHandlePromotion();
    }
}
```
运行结果：
```java
[GC (Allocation Failure) [DefNew
Desired survivor size 524288 bytes, new threshold 1 (max 15)
- age   1:     528280 bytes,     528280 total
: 7294K->515K(9216K), 0.0040766 secs] 7294K->4611K(19456K), 0.0041309 secs] [Times: user=0.00 sys=0.00, real=0.01 secs] 
[GC (Allocation Failure) [DefNew
Desired survivor size 524288 bytes, new threshold 15 (max 15)
: 6818K->0K(9216K), 0.0012444 secs] 10914K->4611K(19456K), 0.0012760 secs] [Times: user=0.00 sys=0.00, real=0.00 secs] 
Heap
 def new generation   total 9216K, used 2130K [0x00000000fec00000, 0x00000000ff600000, 0x00000000ff600000)
  eden space 8192K,  26% used [0x00000000fec00000, 0x00000000fee14930, 0x00000000ff400000)
  from space 1024K,   0% used [0x00000000ff400000, 0x00000000ff400000, 0x00000000ff500000)
  to   space 1024K,   0% used [0x00000000ff500000, 0x00000000ff500000, 0x00000000ff600000)
 tenured generation   total 10240K, used 4611K [0x00000000ff600000, 0x0000000100000000, 0x0000000100000000)
   the space 10240K,  45% used [0x00000000ff600000, 0x00000000ffa80d58, 0x00000000ffa80e00, 0x0000000100000000)
 Metaspace       used 2568K, capacity 4486K, committed 4864K, reserved 1056768K
  class space    used 275K, capacity 386K, committed 512K, reserved 1048576K
```
说明：发生了两次GC，第一次发生在给allocation4分配内存空间时，由于老年代的连续可用空间大于存活的对象总和，所以allocation2、allocation3将会进入老年代，allocation1的空间将被回收，allocation4分配在新生代；第二次发生在给allocation7分配内存空间时，此次GC将allocation4、allocation5、allocation6所占的内存全部回收。最后，allocation2、allocation3在老年代，allocation7在新生代。
