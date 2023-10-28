首先，数组和集合的区别：

- 数组是大小固定的
- 集合可以存储和操作数目不固定的一组数据，集合只能存放引用类型的的数据，不能存放基本数据类型
## 特性
### List

- 允许重复
- 有序
- 继承自Connection
### Set

- 不允许重复
- 无序
- 继承自Connection
### Map

- 键值对
- 区别与List和Set，既没有继承也没有实现Connection
## 场景
三者各自适用什么样的场景？
### List

- 使用索引对元素进行访问 ArrayList适合快速查找，LinkedList适合增删元素
- 对有序有需求
### Set

- 确保元素的唯一性 常用的Set有：HashSet、LinkedHashSet和 TreeSet。其中，TreeSet中的元素可以使用Comparator 或者 Comparable 进行排序；LinkedHashSet也按照元素的插入顺序对它们进行存储
### Map

- 希望以键值对的形式存在 常用的Map有：HashMap、LinkedHashSet和TreeMap。其中HashMap是无序的，LinkedHashSet有序，TreeMap可通过Comparator 或者 Comparable 进行排序 另外HashTable也可以实现键值对，并且相对于HashMap是线程安全的，但是由于JAVA5以上 ConcurrentHashMap是线程安全的，但现在已经基本被HashMap取代

**怎么让HashMap同步？**

- synchronizeMap

Map m = Collections.synchronizeMap(hashMap);
复制

- JAVA5以上 ConcurrentHashMap是HashTable的替代 (即线程安全的）
# 关于List＜Map＜String, Object＞＞理解
首先map<String,Object>是定义了一个Map集合变量，然后list<map<String,Object>>是定义了一个List的集合变量，是map的一个集合；map是那个list的其中一个值。 List<Map<String,Object> list=new ArrayList<Map<String,Object>>; Map<String,Object> map=new HashMap<String,Object>; list.add(map);//map是list中的其中一个值。
List集合中的对象是一个Map对象,而这个Map对象的键是String类型,值是Object类型
```java
package com.test;

import java.util.*;

public class MyTest01 {
public static void main(String[] args) {

List<Map<String, Object>> listMaps = new ArrayList<Map<String, Object>>();

Map<String, Object> map1 = new HashMap<String, Object>();
map1.put("1", "a");
map1.put("2", "b");
map1.put("3", "c");
listMaps.add(map1);

Map<String, Object> map2 = new HashMap<String, Object>();
map2.put("11", "aa");
map2.put("22", "bb");
map2.put("33", "cc");
listMaps.add(map2);

for (Map<String, Object> map : listMaps) {
for (String s : map.keySet()) {
System.out.print(map.get(s) + " ");
}
}
System.out.println();
System.out.println("========================");
for (int i = 0; i < listMaps.size(); i++) {
Map<String, Object> map = listMaps.get(i);
Iterator iterator = map.keySet().iterator();
while (iterator.hasNext()) {
String string = (String) iterator.next();
System.out.println(map.get(string));
}
}
System.out.println("++++++++++++++++++++++++++++");
for (Map<String, Object> map : listMaps) {
for (Map.Entry<String, Object> m : map.entrySet()) {
System.out.print(m.getKey() + " ");
System.out.println(m.getValue());
}
}
System.out.println("-----------------------------");
}
}
```
# List＜Map＜String, Object＞＞存放的对象问题
一、提出问题 代码一：
```java
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class Test {
public static void main(String args[]) {
List<Map<String, Object>> list = new ArrayList<Map<String,Object>>(); 
Map<String, Object> map = new HashMap<String, Object>(); 
for(int i=0;i<5;i++) {
//    Map<String, Object> map = new HashMap<String, Object>(); 
map.put("a", i); 
map.put("b", i); 
list.add(map); 
} 
System.out.println(list);
}
}
```
代码二：
```java
import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class Test {
public static void main(String args[]) {
List<Map<String, Object>> list = new ArrayList<Map<String,Object>>(); 
//    Map<String, Object> map = new HashMap<String, Object>(); 
for(int i=0;i<5;i++) {
Map<String, Object> map = new HashMap<String, Object>(); 
map.put("a", i); 
map.put("b", i); 
list.add(map); 
} 
System.out.println(list);
}
}
 
```
二、给出答案 猜猜看代码一二运行的结果分别是啥？
没错，就是：
代码一：
[{a=4,b=4},{a=4,b=4},{a=4,b=4},{a=4,b=4},{a=4,b=4}] 代码二：
[{a=0,b=0},{a=1,b=1},{a=2,b=2},{a=3,b=3},{a=4,b=4}] 
三、问题分析 代码一中，List<Map<String, Object>>里面存放的是map对象的地址，尽管循环了五次，但是每次的map对象对应的都是同一个地址，即listMap里面存放的是五个同样的map对象。 代码二中，每次循环的时候都实例化一个新的map对象，这样list在执行add方法的时候，每次都是存的不一样的map对象。 可以通过debug来观察list存放的map对象对应的id。如图：
代码一：
![](https://images.cherryfloris.eu.org/2022/1661398956808-89e362be-d608-48da-adba-ea181d7cccd0.png)
代码二：
![](https://images.cherryfloris.eu.org/2022/1661398956996-942d1f44-8c44-43df-85de-bb704b5f771f.png)
四、总结 通过上面的分析，我们可以知道，以后需要创建不同的map对象的时候，需要在循环里面进行map的创建。
而不是在循环体外面，因为List<Map<String, Object>>指向的是map对象的地址。 

 
