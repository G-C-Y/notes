# Java中Map集合概述
Map集合是按<键,值>对的形式存储数据,  如存储员工的姓名及员工的工资, <员工姓名, 员工工资>
## java.util.Map集合的结构图
![](https://images.cherryfloris.eu.org/2021/1632993959573-0a784e52-8804-4013-87e6-be021b11d711.png)
# Java中Map基本操作
void：clear() 清空集合中所有的<键,值>对
boolean：containsKey(Object key) 判断是否包含指定的键
boolean：containsValue(Object value) 判断是否包含指定的值
Set>：entrySet() 返回所有Entry的集合, 一个<键,值>对就是一个Entry
boolean：equals(Object o)
V：get(Object key) 返回键对应的值
boolean：isEmpty() 判断集合是否为空
Set：keySet() 返回键的集合
V：put(K key, V value) 添加对, 如果key键已存在,使用value值替换原来的值
void：putAll(Map m) 把m集合中所有的<键,值>对添加到当前集合中
V：remove(Object key) 只要key匹配就删除对应的<键,值>对
default boolean：remove(Object key, Object value) 删除
default V：replace(K key, V value) 使用value值替换key原来的值
int：size() 返回<键,值>对的数
Collection：values() 返回所有值的集合
```java
package com.wkcto.chapter05.map;

import java.util.HashMap;
import java.util.Map;

/**
 * 演示Map的基本操作
 * @author 蛙课网
 *
 */
public class Test01 {

	public static void main(String[] args) {
		//1) 创建Map集合, 用来保存<员工姓名,员工工资>
		//Map是一个接口,需要赋值实现类对象
		Map<String, Integer>  map = new HashMap<>();
		
		//2) 添加数据
		map.put("feifei", 30000);
		map.put("bin", 40000);
		map.put("zhang", 50000);
		map.put("yong", 100000);
		
		//3) 直接打印, 存储顺序与添加顺序可能不一致
		System.out.println( map );
		//{bin=40000, yong=100000, zhang=50000, feifei=30000}
		
		//4)添加重复的键, 如果键重复,会使用新的value值替换原来的值, Map中的键不能重复的
		map.put("bin", 40001);
		System.out.println( map );
		
		//5)修改
		map.replace("feifei", 30002); 
		map.replace("yan", 6666);			//替换时, 如果键不存在,替换不成功
		System.out.println( map );
		
		//6)判断
		System.out.println( map.isEmpty() );
		System.out.println( map.size());
		System.out.println( map.containsKey("feifei"));
		System.out.println( map.containsValue(100000));
		System.out.println( map.get("yong"));
		System.out.println( map.get("cui"));  		//如果键不存在, 返回null
		
		//7) 删除
		map.remove("bin", 40000); 		//删除<"bin", 40000>对,  要求键与值都匹配才能删除
		System.out.println( map ); 		//{bin=40001, yong=100000, zhang=50000, feifei=30002}
		map.remove("yong");				//只要键匹配就删除
		System.out.println( map );
		
	}

}
```
```java
package com.wkcto.chapter05.map;

import java.util.Collection;
import java.util.HashMap;
import java.util.Iterator;
import java.util.Map;
import java.util.Map.Entry;
import java.util.Set;
/**
 * Map的遍历
 * @author 蛙课网
 *
 */
public class Test02 {

	public static void main(String[] args) {
		//1)创建Map集合
		Map<String, Integer>  map = new HashMap<>();
		
		//2) 添加数据
		map.put("feifei", 30000);
		map.put("bin", 40000);
		map.put("zhang", 50000);
		map.put("yong", 100000);
		
		//3) 获得所有键的集合, 
		Set<String> keySet = map.keySet();
		System.out.println( keySet );
		
		//4) 所有值的集合
		Collection<Integer> values = map.values();
		Iterator<Integer> iterator = values.iterator();
		while (iterator.hasNext()) {
			Integer integer = (Integer) iterator.next();
			System.out.print( integer + "\t");
		}
		System.out.println();
		
		//5)所有entry的集合, 一个Entry就是一个<键,值>对
		Set<Entry<String, Integer>> entrySet = map.entrySet();
		for (Entry<String, Integer> entry : entrySet) {
			System.out.println( entry.getKey() + " : " + entry.getValue());
		}
		
	}

}
```
**练习**
```java
package com.wkcto.chapter05.map;

import java.util.HashMap;
import java.util.Map;
import java.util.Map.Entry;
import java.util.Set;

/**
 * 统计字符串中每个 字符出现的次数
 * 	a : 12
 * 	c : 5
 * 	d : 23
 * 
 * @author 蛙课网
 *
 */
public class Test03 {

	public static void main(String[] args) {
		String  text = "afdfasfafasfdaczadsfazcvafdfcvfdfdaadvavdavfdaav zcvafdafadfvczxvzvafdafad";
		
		//1) 定义一个Map保存<字符, 出现的次数>结果
		Map<Character, Integer> map = new HashMap<>();
		
		//2) 遍历字符串中的每个 字符
		for( int i = 0  ; i < text.length(); i++){
			char cc = text.charAt(i); 			//取出对应的字符
			//如果字符不是第一次出现, 把原来的次数 加 1
			if ( map.containsKey(cc) ) { 		//Map集合中的键包含cc这个字符
				Integer count = map.get(cc); 	//把cc字符原来的次数取出来
				map.replace(cc, count + 1 ); 	//把cc字符的次数加1, 保存到map中
			}else{
				//如果是第一次出现,  把<字符, 1 > 保存到集合中
				map.put(cc, 1);
			}
		}
		//3) 打印结果
		Set<Entry<Character, Integer>> entrySet = map.entrySet();
		for (Entry<Character, Integer> entry : entrySet) {
			System.out.println( entry.getKey() + " : " + entry.getValue());
		}
	}

}
```
# Java HashMap底层实现原理
HashMap底层是哈希表(散列表)，哈希就是一个数组，数组的每个元素是一个单向链表。
![](https://images.cherryfloris.eu.org/2021/1632994102112-5c78a01d-6fa2-40fe-a55d-5e659fe638e9.png)
● 在第一次执行put方法时,给哈希表的数组(哈希桶)默认初始化,容量: 16
● hashMap加载因子是0.75
● 当hashMap中<键,值>对的数量  > 哈希桶容量 * 加载因子时,  哈希桶(数组)要扩容  , 按2倍大小扩容
● HashMap可以指定初始化容量, 系统会自动调整为2的幂次方,  可以快速的计算数组的下标
● 如果单向链表中结点的个数超过8个时, 系统会自动的把单向链表转换为树形结构
# HashTable和HashMap的区别
● 与HashMap一样,底层也是哈希表, 但是HashTable是线程安全的
● HashMap默认初始化容量: 16,  HashTable默认初始化容量:11
● 加载因子: 0.75,  当键,值对的数量大于加载因子*哈希桶容量时, 要扩容
● HashMap默认按2倍大小扩容,  HashTable默认按  2倍 + 1  大小扩容
● HashMap可以指定初始化容量, 系统会自动调整为2的幂次方,  HashTable也能指定初始化容量, 系统不会自动调整
● HashMap中的键与值都可以为null, HashTable中的键与值都不能为null
● HashMap的父类是AbstractMap  ,  HashTable的父类是Dictionary

# Map<String, Object> map=new HashMap＜String,Object＞详解
**Map是一个接口，即Interface Map<K,V>，其中K-key类型和V-value的类型**
它的每个元素包含一个key对象和一个value对象，且在这两个对象之间存在一种映射的对应关系，所有从Map集合中访问元素时，只有指定了key就可以找到对应的value，因此key必须是唯一的且不能重复，当key相同时，后面的value值会覆盖之前的value值。
### Map定义的一些通用的方法
![image.png](https://images.cherryfloris.eu.org/2021/1632983146006-65587273-44cc-42ed-b857-a23e5c1ff511.png)
### Map接口有很多实现类，如TreeMap，Hashtable，SortedMap，HashMap。
HashMap，即Class HashMap<K,V>，是基于哈希表的Map接口实现。
  此实现提供所有可选的映射操作，并允许空值和空键。这个类不保证地图的顺序，特别是它不保证该顺序会随着时间的推移保持不变。
#### （1）HashMap的数据结构
  在Java编程语言中，最基本的结构就是两种，一个是数组，另外一个是指针（引用），HashMap就是通过这两个数据结构进行实现。HashMap实际上是一个“链表散列”的数据结构，即数组和链表的结合体。HashMap底层就是一个数组结构，数组中的每一项又是一个链表。当新建一个HashMap的时候，就会初始化一个数组。
  HashMap在底层将key-value当成一个整体进行处理，这个整体就是一个Entry对象。HashMap底层采用一个Entry[]数组来保存所有的key-value对，当需要存储一个Entry对象时，会根据hash算法来决定器在数组中的存储位置，再根据equals方法决定其在该数组位置上的链表中的存储位置；当需要取出一个Entry时，也会根据hash算法找到其在数组中存储位置，再根据equals方法从该位置上的链表中取出该Entry。
#### （2）HashMap的两个影响其性能的参数：初始容量和负载因子。
  容量是在哈希表中桶的数量，初始容量是简单地在创建哈希表中的时间的能力。负载因子衡量的是一个散列表的空间的使用速度，负载因子越大表示散列表的装填程度越高，反之越小。当哈希表中的条目数超过加载因子和当前容量的乘积时，哈希表将被重新哈希（重建内部数据结构），以便哈希表具有大约两倍的桶数。作为一般规则，默认加载因子（0.75）在时间和空间成本之间提供了良好的权衡。较高的值会减少空间开销，但会增加查找成本（体现在HashMap类的大多数类操作中，包括get和put）。在设置其初始容量时，应考虑映射中的预期条目数及其加载因子，以便最小化重新散列操作的数量。如果初始容量大于最大条目数除以加载因子，则不会发生重新加载操作。
**例子**
```sql
Map<String,Object> map = new HashMap<String,Object>();//创建Map对象，Object是所有类型的父类
map.put("publish",publish);//存储key和value
map.put("status",status);
map.get("publish");//获取相应key的值
```
# Java Properties类
Properties继承了HashTable, 它的键与值都是String类型。
经常使用Properties设置/读取系统的属性值
```java
package com.wkcto.chapter05.map;

import java.util.Properties;

/**
 * Properties一般用来设置/读取系统属性值
 * @author 蛙课网
 *
 */
public class Test06 {

	public static void main(String[] args) {
		//1)创建Properties, 不需要通过泛型约束键与值的类型, 都是String
		Properties properties = new Properties();
		//2)设置属性值
		properties.setProperty("username", "wkcto");
		properties.setProperty("password", "666");
		//3)读取属性值
		System.out.println( properties.getProperty("username"));
		System.out.println( properties.getProperty("password"));
		
	}

}
```
```java
package com.wkcto.chapter05.map;

import java.io.IOException;
import java.io.InputStream;
import java.util.Properties;

/**
 * 使用Properties读取配置文件
 * 1) 配置文件保存什么内容?
 * 		经常在配置文件中保存系统属性
 * 2) 如何添加配置文件?
 * 		一般情况下,会在项目中单独创建一个包, 在该包中添加一个配置文件,配置文件的扩展名是:.properties
 * 		在src目录中的.java源文件自动编译为.class保存到bin目录中,  src目录中的非.java源文件,Eclipse会自动复制到bin目录中
 * 3)可以使用Properties读取配置文件内容
 * @author 蛙课网
 *
 */
public class Test07 {

	public static void main(String[] args) throws IOException {
		//1)先创建Properties
		Properties properties = new Properties();
		
		//2)加载配置文件
		/*
		 * 把一组小狗抽象为Dog类, 把一组小猫抽象为Cat类,把一组人抽象为Person类,
		 * 把Dog/Cat/Person/System/String等所有的类抽象为Class类, Class类描述的是所有类的相同的特征
		 * 每个类都有一个class属性,返回就是该类的Class对象, 即该类运行时类对象, 可以把运行时类对象简单的理解为该类的字节码文件
		 */
//		InputStream in = Test07.class.getResourceAsStream("/resources/config.properties");
		//如果开发多线程程序,
		InputStream in = Thread.currentThread().getContextClassLoader().getResourceAsStream("resources/config.properties");
		properties.load( in );
		//3)读取系统属性
		System.out.println( properties.getProperty("username")); 
		System.out.println( properties.get("password")); 
	}

}
```
resources包中的config.properties配置文件内容如下:
username=wkcto
password:147
```java
package com.wkcto.chapter05.map;

import java.util.ResourceBundle;

/**
 * 使用ResourceBundle读取配置文件
 * @author 蛙课网
 *
 */
public class Test08 {

	public static void main(String[] args) {
		//加载配置文件时,不需要扩展名,(前提是配置文件扩展名是properties)
		ResourceBundle bundle = ResourceBundle.getBundle("resources/config");
		System.out.println( bundle.getString("username"));
		System.out.println( bundle.getString("password"));
	}

}
```
# Java TreeMap排序
TreeMap实现了SortedMap接口, 根据键自然排序, 要求键必须是可比较的，要么指定Comparator比较器，如果没有Comparator比较器, 键要实现Comparable接口。
```java
package com.wkcto.chapter05.map;

import java.util.Comparator;
import java.util.TreeMap;

/**
 * TreeMap
 * @author 蛙课网
 *
 */
public class Test09 {

	public static void main(String[] args) {
		//1)创建TreeMap, 在构造方法中指定Comparator比较器
		TreeMap<String, Integer> treeMap = new TreeMap<>(new Comparator<String>() {
			
			@Override
			public int compare(String o1, String o2) {
				return o2.compareTo(o1); 		//按字符串降序
			}
		});
		
		treeMap.put("feifei", 28);
		treeMap.put("zhang", 36);
		treeMap.put("yong", 35);
		treeMap.put("bin", 34);
		
		//输出结果, 根据键降序排序
		System.out.println( treeMap );
		//{zhang=36, yong=35, feifei=28, bin=34}
		
		
		//2) 创建TreeMap, 没有指定Comparator比较器, 要求键实现Comparable接口
		TreeMap<String, Integer> treeMap22 = new TreeMap<>();
		treeMap22.putAll(treeMap);
		System.out.println( treeMap22 );
		//{bin=34, feifei=28, yong=35, zhang=36}
		
	}

}
```
```java
package com.wkcto.chapter05.map;

import java.util.Comparator;
import java.util.TreeMap;

/**
 * TreeMap中的键必须是可比较的
 * 		要么指定Comparator比较器,要么实现Comparable接口
 * 注意:
 * 	在TreeMap中判断键是否存在,根据Comparator/Comparable的比较结果是否为0进行判断的,如果为0就认为是相同的键
 * 
 * @author 蛙课网
 *
 */
public class Test10 {

	public static void main(String[] args) {
		//创建TreeMap, 存储<Person, String> 表示员工与部门
		//指定Comparator比较器 , 根据年龄升序
		TreeMap<Person, String> treeMap = new TreeMap<>(new Comparator<Person>() {
			@Override
			public int compare(Person o1, Person o2) {
				return o1.age - o2.age;
			}
		});
		
		treeMap.put(new Person("feifei", 28), "教学部");
		treeMap.put(new Person("xixi", 22), "教务部");
		treeMap.put(new Person("hong", 26), "市场部");
		treeMap.put(new Person("yun", 24), "市场部");		
		System.out.println( treeMap );
		//{ [name=xixi, age=22]=教务部,  [name=yun, age=24]=市场部,  [name=hong, age=26]=市场部,  [name=feifei, age=28]=教学部}

		//因为Comparator比较器根据年龄比较大小, 新添加的Person键如果与Map中现在的键年龄相同 就认为是同一个键
		treeMap.put(new Person("mengmeng", 22), "行政");
		System.out.println( treeMap );
		//binbin的年龄与feifei年龄相同, 就认为是同一个键
		System.out.println( treeMap.containsKey(new Person("binbin", 28)));   //true
		
		System.out.println("--------------------------------");
		TreeMap<Person, String>  treeMap2 = new TreeMap<>(treeMap);
		System.out.println( treeMap2 );
		
		TreeMap<Person, String> treeMap3 = new TreeMap<>();
		treeMap3.putAll(treeMap);
		System.out.println( treeMap3 );
		//{ [name=feifei, age=28]=教学部,  [name=hong, age=26]=市场部,  [name=xixi, age=22]=教务部,  [name=yun, age=24]=市场部}

	}

}
```
TreeMap可以根据键自然排序,排序的原理是二叉树原理
![](https://images.cherryfloris.eu.org/2021/1633750664122-c893a509-4230-4180-964d-fe26b240c276.png)
# Java Map集合小结
Map集合
按<键,值>对的形式存储元素
put( k, v),  containsKey( k ),  containsValue( v ) , get( k ),  remove( k )
keyset()  ,  values(),  entrySet()
## HashMap
底层是哈希表(散列表),  哈希表就是一个数组, 数组的每个元素是一个单向链表
## HashTable
底层是哈希表, 它是线程安全的, HashMap不是线程安全的
初始化容量:11, HashMap初始化容量: 16
加载因子: 0.75,  当<键,值>对的数量大于 哈希桶容量 * 加载因子时,  哈希桶扩容
HashTable默认扩容: 2倍 + 1  ,  HashMap扩容: 2倍
HashTable的键与值都不能为null,  HashMap的键与值可以为null
创建HashTable时, 可以指定初始化容量;   HashMap会自动把初始化容量调整为2的幂次方,就是为了快速计算数组的下标
## Properties
继承了HashTable, 键与值都是String类型
经常用于设置/读取系统属性值
一般情况下, 系统属性会保存在配置文件中, 可以通过Properties读取配置文件的内容, 也可以使用ResouceBundle读取配置文件的属性
## TreeMap
实现了SortedMap接口, 可以根据键自然排序, 要求键必须是可比较的
要么指定Comparator比较器, 如果没有Comparator比较器,键需要实现Comparable接口
Comparator比较与Comparable如何选择?
对于TreeMap来说, 先根据Comaparator比较器进行比较大小 , 如果没有Comparator比较器, 再选择Comparable接口。
对于开发人员来说, 一般通过实现Comparable接口定义一个默认的比较规则 , 通过Comparator比较器定义若干不能同的排序规则。
## 如何选择Map?
如果不需要根据键排序就选择HashMap, 如果需要根据键排序就选择TreeMap。
如果在多线程程序中, 使用java.util.concurrent包中的类,如果不需要根据键排序选择ConcurrentHashMap, 如果需要根据键排序选择ConcurrentSkipListMap[

](https://blog.csdn.net/wenchangwenliu/article/details/108194758)
