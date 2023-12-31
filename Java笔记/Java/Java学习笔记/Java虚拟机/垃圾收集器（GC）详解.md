### 七种经典的垃圾回收器
- 串行回收器：Serial、Serial Old
- 并行回收器：ParNew、Parallel Scavenge、Parallel old
- 并发回收器：CMS、G1

按工作的内存区间分，可分为新生代垃圾回收器和老年代垃圾回收器。
JVM针对新生代和老年代提供了不同的垃圾收集器。 Sun HotSpot 虚拟机的垃圾收集器如下：
![image.png](https://images.cherryfloris.eu.org/2022/1664157824429-457f82de-8f11-4f4d-84b9-9e605f4dddae.png)
> （红色虚线）由于维护和兼容性测试的成本，在JDK 8时将Serial+CMS、ParNew+Serial Old这两个组合声明为废弃（JEP173），并在JDK9中完全取消了这些组合的支持（JEP214），即：移除。
> （绿色虚线）JDK14中：弃用Parallel Scavenge和Serialold GC组合（JEP366）
> （绿色虚框）JDK14中：删除CMS垃圾回收器（JEP363）

#### 垃圾收集器组合总结：
Serial + Serial Old
ParNew + CMS + Serial Old
Parallel Scavenge + Parallel Old （吞吐量优先） JDK8中默认的垃圾收集器组合
Serial + CMS (JDK8，声明为废弃，JDK9取消) （CMS JDK14 被删除）
ParNew + Serial Old (JDK8，声明为废弃，JDK9取消)
G1 （JDK9 成为默认的垃圾收集器）
Parallel Scavenge + Serial old（JDK14弃用）
#### 查看默认垃圾收集器
-XX:+PrintCommandLineFlags：查看命令行相关参数（包含使用的垃圾收集器）
使用命令行指令：jinfo -flag 相关垃圾回收器参数 进程ID
#### 新生代
##### Serial垃圾收集器（单线程、 复制算法）
最基本的垃圾收集器，使用复制算法，单线程，虽然收集垃圾时需要暂停其他所有的工作线程，但简单高效，是 java 虚拟机运行在 Client 模式下默认的新生代垃圾收集器

- 在HotSpot虚拟机中，使用-XX:+UseSerialGC参数可以指定年轻代和老年代都使用串行收集器。等价于新生代用Serial GC，且老年代用Serial Old GC
##### ParNew 垃圾收集器 （Serial的多线程版本、 复制算法）
是 Serial 收集器的多线程版本 ，除了多线程进行GC外，其他与Serial一样，默认开启和 CPU 数目相同的线程数 。是很多 java虚拟机运行在 Server 模式下新生代的默认垃圾收集器。

- 可以通过选项"-XX:+UseParNewGC"手动指定使用ParNew收集器执行内存回收任务。它表示年轻代使用并行收集器，不影响老年代
- 这里的多线程指的是垃圾收集时，多线程并行，并不是垃圾收集与程序运行并行
- 收集垃圾时，也需要暂停其他所有工作线程，然后多线程收集垃圾。
- 单CPU环境下，因为线程切换，性能较差。
##### Parallel Scavenge 收集器（多线程复制算法、高效）

- 关注程序的吞吐量，即吞吐量优先。主要适用于在后台运算而不需要太多交互的任务。 自适应调节策略也是 ParallelScavenge 收集器与 ParNew 收集器的一个重要区别。
- 吞吐量=运行用户代码时间/(运行用户代码时间+垃圾收集时间) ； 吞吐量优先，意味着在单位时间内，STW的时间最短；与之相对应的 低延迟 就是暂停时间优先，尽可能让单次STW时间最短；这两个无法同时实现。
- 收集垃圾时，也需要暂停其他所有工作线程，然后多线程收集垃圾。
```java
参数配置
-XX:+UseParallelGC 手动指定年轻代使用Parallel并行收集器执行内存回收任务。 

-XX:+UseParallelOldGC 手动指定老年代都是使用并行回收收集器。 
  分别适用于新生代和老年代。默认jdk8是开启的。
  上面两个参数，默认开启一个，另一个也会被开启。（互相激活）
  
-XX:ParallelGCThreads 设置年轻代并行收集器的线程数。一般地，最好与CPU数量相等，以避免过多的线程数影响垃圾收集性能。  
-XX:MaxGCPauseMillis 设置垃圾收集器最大停顿时间（即STw的时间）。单位是毫秒。 
  为了尽可能地把停顿时间控制在MaxGCPauseMills以内，收集器在工作时会调整Java堆大小或者其他一些参数。
  对于用户来讲，停顿时间越短体验越好。但是在服务器端，我们注重高并发，整体的吞吐量。所以服务器端适合Parallel，进行控制。
  该参数使用需谨慎。
  
-XX:GCTimeRatio 垃圾收集时间占总时间的比例（=1/（N+1））。用于衡量吞吐量的大小。 
  取值范围（0, 100）。默认值99，也就是垃圾回收时间不超过1%。
  与前一个-XX:MaxGCPauseMillis参数有一定矛盾性。暂停时间越长，Radio参数就容易超过设定的比例。
  
-XX:+UseAdaptivesizePolicy 设置Parallel Scavenge收集器具有自适应调节策略 
  在这种模式下，年轻代的大小、Eden和Survivor的比例、晋升老年代的对象年龄等参数会被自动调整，已达到在堆大小、吞吐量和停顿时间之间的平衡点。
  在手动调优比较困难的场合，可以直接使用这种自适应的方式，仅指定虚拟机的最大堆、目标的吞吐量（GCTimeRatio）和停顿时间（MaxGCPauseMills，让虚拟机自己完成调优工作。

```
#### 老年代
##### Serial Old（单线程、标记整理算法）
是Serial的老年代版本，收集垃圾时也需要暂停其他所有的工作线程。

- 是Client模式下默认的老年代垃圾收集器
- Server模式下，搭配新生代的Parallel Scavenge 收集器使用（在 JDK1.5 之前版本中）。同时也作为老年代中使用 CMS 收集器的后备垃圾收集方案（当CMS发生Concurrent Mode Failure）。
##### Parallel Old收集器（多线程、标记整理算法）
Parallel Scavenge的老年代版本

- 吞吐量优先，意味着在单位时间内，STW的时间最短；与之相对应的 低延迟 就是暂停时间优先，尽可能让单次STW时间最短；这两个无法同时实现。
- 若相同对于吞吐量要求较高，可以Parallel Scavenge搭配Parallel Old使用。
##### CMS详解(Concurrent mark sweep)收集器（多线程、标记清除算法 低延迟）
主要目标为获取最短垃圾回收停顿时间（这里的停顿是指停止用户线程），可以为交互较高的程序提高用户体验。多用于服务器端。另外，标记清除算法会产生大量的空间碎片，可能出现空间足够大，但是没有足够的连续空间用来分配对象。回收过程分为以下四个阶段：
![image.png](https://images.cherryfloris.eu.org/2022/1664158228048-8931f3eb-25e8-4137-b153-e892cfcb7270.png)

- 初始标记：只是标记一下 GC Roots 能直接关联的对象以及「年轻代」指向「老年代」的对象，速度很快，需要暂停所有的工作线程（stop-the-world STW）。但是速度很快
- 并发标记：进行 GC Roots 跟踪的过程，和用户线程一起工作，标记出根对象的可达路径。不需要暂停工作线程
- 重新标记：由于在并发标记阶段中，程序的工作线程会和垃圾收集线程同时运行或者交叉运行，因此为了修正在并发标记期间，因用户程序继续运行而导致标记产生变动的那一部分对象的标记记录，需要暂停所有的工作线程。（stop-the-world STW）
- 并发清除：清除 GC Roots 不可达对象，和用户线程一起工作，不需要暂停工作线程 （会产生浮动垃圾，留到下次GC清除）
- 并发标记与并发清除最耗时，但是不用STW。所以整体的回收的底停顿的。
- 另外，由于在垃圾收集阶段用户线程没有中断，所以在CMS回收过程中，还应该确保应用程序用户线程有足够的内存可用。因此，CMS收集器不能像其他收集器那样等到老年代几乎完全被填满了再进行收集，而是当堆内存使用率达到某一阈值时，便开始进行回收，以确保应用程序在CMS工作过程中依然有足够的空间支持应用程序运行。要是CMS运行期间预留的内存无法满足程序需要，就会出现一次“Concurrent Mode Failure” 失败，这时虚拟机将启动后备预案：临时启用Serial Old收集器来重新进行老年代的垃圾收集，这样停顿时间就很长了。
> CMS为什么采用标记清除算法而不是标记整理算法呢？
> 因为当并发清除的时候，用标记整理算法整理内存的话，原来的用户线程使用的内存还怎么用呢？要保证用户线程能继续执行，前提的它运行的资源不受影响嘛。标记整理算法更适合“Stop the World” 这种场景下使用

**设置的参数**

- -XX:+UseConcMarkSweepGC手动指定使用CMS收集器执行内存回收任务。
开启该参数后会自动将-xx:+UseParNewGC打开。即：ParNew（Young区用）+CMS（Old区用）+ Serial Old的组合。
- -XX:CMSInitiatingOccupanyFraction 设置堆内存使用率的阈值，一旦达到该阈值，便开始进行回收。
   - JDK5及以前版本的默认值为68，即当老年代的空间使用率达到68%时，会执行一次CMS回收。JDK6及以上版本默认值为92%。
   - 如果内存增长缓慢，则可以设置一个稍大的值，大的阀值可以有效降低CMS的触发频率，减少老年代回收的次数可以较为明显地改善应用程序性能。反之，如果应用程序内存使用率增长很快，则应该降低这个阈值，以避免频繁触发老年代串行收集器。因此通过该选项便可以有效降低Ful1Gc的执行次数。
- -XX:+UseCMSCompactAtFullCollection 用于指定在执行完Full GC后对内存空间进行压缩整理，以此避免内存碎片的产生。不过由于内存压缩整理过程无法并发执行，所带来的问题就是停顿时间变得更长了。
- -XX:CMSFullGCsBeforeCompaction 设置在执行多少次Full GC后对内存空间进行压缩整理。
- -XX:ParallelcMSThreads 设置CMS的线程数量。
   - CMS默认启动的线程数是（ParallelGCThreads+3）/4，ParallelGCThreads是年轻代并行收集器的线程数。当CPU资源比较紧张时，受到CMS收集器线程的影响，应用程序的性能在垃圾回收阶段可能会非常糟糕。	
#### 垃圾回收器选择小结

- 如果你想要最小化地使用内存和并行开销，请选Serial GC；
- 如果你想要最大化应用程序的吞吐量，请选Parallel GC；
- 如果你想要最小化GC的中断或停顿时间，请选CMS GC。
#### 空间分配担保
在发生Minor GC之前，虚拟机会先检查老年代最大可用的连续空间是否大于新生代所有对象总空间，如果这个条件成立，那么Minor GC可以确保是安全的。当大量对象在Minor GC后仍然存活，就需要老年代进行空间分配担保，把Survivor无法容纳的对象直接进入老年代。如果老年代判断到剩余空间不足（根据以往每一次回收晋升到老年代对象空间的平均值作为经验值），则进行一次Full GC。
#### G1(Garbage first)收集器
目前垃圾收集器理论发展最前沿的成果，对比CMS收集器有两点改进：一是采用标记整理算法，不产生内存碎片，二是可以精确控制停顿时间，在不牺牲吞吐量的前提下，减少垃圾回收停顿。使用-XX:+UseG1GC来启用。
G1收集器将堆内存划分为大小固定的几个区域(局部压缩)，以分区为单位进行回收，将存活对象复制到另一个空闲空间。并且跟踪这些区域的垃圾收集进度，同时在后台维护一个优先级列表，每次根据所允许的收集时间， 优先回收垃圾最多的区域。区域划分和优先级区域回收机制，确保 G1 收集器可以在有限时间获得最高的垃圾收集效率
内存分区上不存在老年代和新生代的区别，只是在逻辑上有分代的概念，随着G1的运行，每个分区都可能在不同代之间切换。
G1的收集都是STW，属于混合收集的方式，每次收集时可能只收集年轻代的区域，也可能收集年轻代的同时，也包含部分老年代区域。
G1内存模型如下，对于老年代和新生代只有逻辑上的分代。heap被划分为一系列大小相等的“小堆区”，也称为region。

- 将整个Java堆划分成约2048个大小相同的独立Region块，每个Region块大小根据堆空间的实际大小而定，整体被控制在1MB到32MB之间，且为2的N次幂，即1MB，2MB，4MB，8MB，16MB，32MB。可以通过-XX:G1HeapRegionSize设定。所有的Region大小相同，且在JVM生命周期内不会被改变。
- 每个Region都是通过指针碰撞来分配空间

G1垃圾收集器还增加了一种新的内存区域，叫做Humongous内存区域，如图中的H块。主要用于存储大对象，如果超过1.5个region，就放到H。
设置H的原因：对于堆中的对象(Eden放不下的大对象)，默认直接会被分配到老年代，但是如果它是一个短期存在的大对象就会对垃圾收集器造成负面影响。为了解决这个问题，G1划分了一个Humongous区，它用来专门存放大对象。如果一个H区装不下一个大对象，那么G1会寻找连续的H区来存储。为了能找到连续的H区，有时候不得不启动Full GC。G1的大多数行为都把H区作为老年代的一部分来看待。
![image.png](https://images.cherryfloris.eu.org/2022/1664158658724-1bd0a800-b972-4ab0-af5f-54e9481ff349.png)
**可预测的停顿时间模型（即：软实时soft real-time）**
这是G1相对于CMS的另一大优势，G1除了追求低停顿外，还能建立可预测的停顿时间模型，能让使用者明确指定在一个长度为M毫秒的时间片段内，消耗在垃圾收集上的时间不得超过N毫秒。

- 由于分区的原因，G1可以只选取部分区域进行内存回收，这样缩小了回收的范围，因此对于全局停顿情况的发生也能得到较好的控制。
- G1跟踪各个Region里面的垃圾堆积的价值大小（回收所获得的空间大小以及回收所需时间的经验值），在后台维护一个优先列表，每次根据允许的收集时间，优先回收价值最大的Region。保证了G1收集器在有限的时间内可以获取尽可能高的收集效率。
- 相比于CMSGC，G1未必能做到CMS在最好情况下的延时停顿，但是最差情况要好很多。
##### G1的垃圾收集过程
G1GC的垃圾回收过程主要包括如下三个环节：

- 年轻代GC（Young GC）
- 老年代并发标记过程（Concurrent Marking）
- 混合回收（Mixed GC）

当年轻代的Eden区用尽时开始年轻代回收过程；G1的年轻代收集阶段是一个并行的独占式收集器。在年轻代回收期，G1GC暂停所有应用程序线程，启动多线程执行年轻代回收。然后从年轻代区间移动存活对象到Survivor区间或者老年区间，也有可能是两个区间都会涉及。
当堆内存使用达到一定值（默认45%）时，开始老年代并发标记过程。
标记完成马上开始混合回收过程。对于一个混合回收期，G1 GC从老年区间移动存活对象到空闲区间，这些空闲区间也就成为了老年代的一部分。和年轻代不同，老年代的G1回收器和其他GC不同，G1的老年代回收器不需要整个老年代被回收，一次只需要扫描/回收一小部分老年代的Region就可以了。同时，这个老年代Region是和年轻代一起被回收的。
###### Remembered Set
一个对象被不同区域引用的问题
一个Region不可能是孤立的，一个Region中的对象可能被其他任意Region中对象引用，判断对象存活时，是否需要扫描整个Java堆才能保证准确？
在其他的分代收集器，也存在这样的问题（而G1更突出）回收新生代也不得不同时扫描老年代？
这样的话会降低MinorGC的效率；
解决方法：
无论G1还是其他分代收集器，JVM都是使用Remembered Set来避免全局扫描：
每个Region都有一个对应的Remembered Set；
每次Reference类型数据写操作时，都会产生一个Write Barrier暂时中断操作；
然后检查将要写入的引用指向的对象是否和该Reference类型数据在不同的Region（其他收集器：检查老年代对象是否引用了新生代对象）；
如果不同，通过CardTable把相关引用信息记录到引用指向对象的所在Region对应的Remembered Set中；
当进行垃圾收集时，在GC根节点的枚举范围加入Remembered Set；就可以保证不进行全局扫描，也不会有遗漏
![image.png](https://images.cherryfloris.eu.org/2022/1664158864682-55b173a7-cf2e-4379-a590-077a543a30c5.png)
###### G1回收过程一：年轻代GC
JVM启动时，G1先准备好Eden区，程序在运行过程中不断创建对象到Eden区，当Eden空间耗尽时，G1会启动一次年轻代垃圾回收过程。
年轻代垃圾回收只会回收Eden区和Survivor区。
首先G1停止应用程序的执行（Stop-The-World），G1创建回收集（Collection Set），回收集是指需要被回收的内存分段的集合，年轻代回收过程的回收集包含年轻代Eden区和Survivor区所有的内存分段。
![image.png](https://images.cherryfloris.eu.org/2022/1664158912615-436bf469-1ffc-4d2f-94aa-f9a7a469bae1.png)
然后开始如下回收过程：
第一阶段，**扫描根**。根是指static变量指向的对象，正在执行的方法调用链条上的局部变量等。根引用连同RSet记录的外部引用作为扫描存活对象的入口。
第二阶段，**更新RSet**。处理dirty card queue（见备注）中的card，更新RSet。此阶段完成后，RSet可以准确的反映老年代对所在的内存分段中对象的引用。
第三阶段，**处理RSet**。识别被老年代对象指向的Eden中的对象，这些被指向的Eden中的对象被认为是存活的对象。
第四阶段，**复制对象**。此阶段，对象树被遍历，Eden区内存段中存活的对象会被复制到Survivor区中空的内存分段，Survivor区内存段中存活的对象如果年龄未达阈值，年龄会加1，达到阀值会被会被复制到Old区中空的内存分段。如果Survivor空间不够，Eden空间的部分数据会直接晋升到老年代空间。
第五阶段，**处理引用**。处理Soft，Weak，Phantom，Final，JNI Weak 等引用。最终Eden空间的数据为空，GC停止工作，而目标内存中的对象都是连续存储的，没有碎片，所以复制过程可以达到内存整理的效果，减少碎片。
###### G1回收过程二：并发标记过程
**初始标记**阶段：标记从根节点直接可达的对象。这个阶段是STW的，并且会触发一次年轻代GC。
**根区域扫描**（Root Region Scanning）：G1 GC扫描Survivor区直接可达的老年代区域对象，并标记被引用的对象。这一过程必须在YoungGC之前完成。
**并发标记**（Concurrent Marking）：在整个堆中进行并发标记（和应用程序并发执行），此过程可能被YoungGC中断。在并发标记阶段，若发现区域对象中的所有对象都是垃圾，那这个区域会被立即回收。同时，并发标记过程中，会计算每个区域的对象活性（区域中存活对象的比例）。
**重新标记**（Remark）：由于应用程序持续进行，需要修正上一次的标记结果。是STW的。G1中采用了比CMS更快的初始快照算法：snapshot-at-the-beginning（SATB）。
**独占清理**（cleanup，STW）：计算各个区域的存活对象和GC回收比例，并进行排序，识别可以混合回收的区域。为下阶段做铺垫。是STW的。这个阶段并不会实际上去做垃圾的收集
**并发清理**阶段：识别并清理完全空闲的区域。
###### G1回收过程三：混合回收
当越来越多的对象晋升到老年代o1d region时，为了避免堆内存被耗尽，虚拟机会触发一个混合的垃圾收集器，即Mixed GC，该算法并不是一个Old GC，除了回收整个Young Region，还会回收一部分的Old Region。这里需要注意：是一部分老年代，而不是全部老年代。可以选择哪些Old Region进行收集，从而可以对垃圾回收的耗时时间进行控制。也要注意的是Mixed GC并不是Full GC。
![image.png](https://images.cherryfloris.eu.org/2022/1664159023621-e9f8ef9b-266f-465a-bdea-001e0356c6a0.png)
并发标记结束以后，老年代中百分百为垃圾的内存分段被回收了，部分为垃圾的内存分段被计算了出来。默认情况下，这些老年代的内存分段会分8次被回收（可以通过-XX:G1MixedGCCountTarget设置）
混合回收的回收集（Collection Set）包括八分之一的老年代内存分段，Eden区内存分段，Survivor区内存分段。混合回收的算法和年轻代回收的算法完全一样，只是回收集多了老年代的内存分段。具体过程请参考上面的年轻代回收过程。
由于老年代中的内存分段默认分8次回收，G1会优先回收垃圾多的内存分段。垃圾占内存分段比例越高的，越会被先回收。并且有一个阈值会决定内存分段是否被回收，-XX:G1MixedGCLiveThresholdPercent，默认为65%，意思是垃圾占内存分段比例要达到65%才会被回收。如果垃圾占比太低，意味着存活的对象占比高，在复制的时候会花费更多的时间。
混合回收并不一定要进行8次。有一个阈值-XX:G1HeapWastePercent，默认值为10%，意思是允许整个堆内存中有10%的空间被浪费，意味着如果发现可以回收的垃圾占堆内存的比例低于10%，则不再进行混合回收。因为GC会花费很多的时间但是回收到的内存却很少。
###### G1回收可选的过程四：Full GC
G1的初衷就是要避免Full GC的出现。但是如果上述方式不能正常工作，G1会停止应用程序的执行（Stop-The-World），使用单线程的内存回收算法进行垃圾回收，性能会非常差，应用程序停顿时间会很长。
要避免Full GC的发生，一旦发生需要进行调整。什么时候会发生Full GC呢？比如堆内存太小，当G1在复制存活对象的时候没有空的内存分段可用，则会回退到Full GC，这种情况可以通过增大内存解决。
导致G1 Full GC的原因可能有两个：

- Evacuation的时候没有足够的to-space来存放晋升的对象；
- 并发处理过程完成之前空间耗尽。

[垃圾回收器之 G1 垃圾回收器_嘿，鱼骨头^O^的博客-CSDN博客_g1垃圾回收器](https://blog.csdn.net/qq_50313418/article/details/122932952)

1. Serial GC：Full GC整个过程STW，Young GC整个过程STW

2. Parallel GC：Full GC整个过程STW，Young GC整个过程STW
3. CMS GC：Full GC整个过程STW，Young GC整个过程STW，Old GC只有两个小阶段STW
4. G1 GC：Full GC整个过程STW，Young GC整个过程STW，Mixed GC由全局并发标记和对象复制组成，全局并发标记其中两个小阶段STW，其它并发
5. Shenandoah GC/ZGC：它们都是回收堆的一部分，所以没有Full GC（Full GC是指回收整个堆，与之相对的是Partial GC，比如CMS GC的Old GC和G1的Mixed GC均属于此类）的概念
如果书上写的是
如果有“Full”，说明这次GC是发生了STW
那是没有问题的，因为所有垃圾回收器的Full GC都会整个过程STW
#### 总结
| **垃圾收集器** | **分类** | **作用位置** | **使用算法** | **特点** | **适用场景** |
| --- | --- | --- | --- | --- | --- |
| Serial | 串行 | 新生代 | 复制算法 | 响应速度优先 | 适用于单CPU环境下的client模式 |
| ParNew | 并行 | 新生代 | 复制算法 | 响应速度优先 | 多CPU环境Server模式下与CMS配合使用 |
| Parallel | 并行 | 新生代 | 复制算法 | 吞吐量优先 | 适用于后台运算而不需要太多交互的场景 |
| Serial Old | 串行 | 老年代 | 标记-整理(压缩)算法 | 响应速度优先 | 适用于单CPU环境下的Client模式 |
| Paraller Old | 并行 | 老年代 | 标记-整理(压缩)算法 | 吞吐量优先 | 适用于后台运算而不需要太多交互的场景 |
| CMS | 并发 | 老年代 | 标记-清除算法 | 响应速度优先 | 适用于互联网或B／S业务 |
| G1 | 并发、并行 | 新生代、老年代 | 标记-整理(压缩)算法 | 响应速度优先 | 响应速度优先 |

原文链接：[https://blog.csdn.net/weixin_46115362/article/details/122383160](https://blog.csdn.net/weixin_46115362/article/details/122383160)



