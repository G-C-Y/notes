# Java中Collection集合概述
集合是用来存储引用类型数据的容器
## 集合分为两大类:
● Collection集合: 存储数据时是单个存储的
● Map集合：存储数据时是按<键,值>对的形式一对一对存储的
java.util包中, Collection集合常用类
![](https://images.cherryfloris.eu.org/2021/1633681185928-89a34e7c-7929-4961-84ae-a185469d87cd.png)
# Java中Collection的基本操作
boolean：add(E e) 向集合中添加元素e
boolean：addAll(Collection c) 把集合c中所有元素都添加到当前集合中
void：clear() 清空当前集合中所有的元素
boolean：contains(Object o) 在当前集合中判断是否包含元素o
boolean：containsAll(Collection c) 判断当前集合是否包含集合c中的所有元素
boolean：equals(Object o)
int：hashCode()
boolean：isEmpty() 判断集合是否为空
Iterator：iterator() 返回当前集合的迭代器
boolean：remove(Object o) 从当前集合中删除第一个与o匹配的元素
boolean：removeAll(Collection c) 在当前集合中删除在c集合中出现的所有元素
int：size() 返回集合中元素的个数
Object[]：toArray() 把集合转换为数组
T[]：toArray(T[] a)
```java
package com.wkcto.chapter05.collection;

import java.util.ArrayList;
import java.util.Collection;

/**
 * 演示Collection集合的基本操作
 * @author 蛙课网
 *
 */
public class Test01 {

	public static void main(String[] args) {
		//1)创建Collection集合, Collection是一个接口,需要赋值实现类对象
		Collection	 collection = new ArrayList<>();
		
		//2) 向集合中添加元素, 默认添加Object类型数据
		collection.add("aa");
		collection.add("bb");
		collection.add( 123 ); 		//如果添加基本类型,系统会自动装箱, 把包装类对象添加到集合中
		collection.add( true );
		
		//3) 直接打印, collection引用 的是ArrayList对象, ArrayList的爷爷类AbstractCollection重写了toString()
		System.out.println( collection );  //[aa, bb, 123, true]
		
		//4)判断
		System.out.println( collection.isEmpty() );		//false
		System.out.println( collection.size());			//4
		System.out.println( collection.contains("bb"));	//true
		
		//5)删除
		collection.remove("bb");
		System.out.println( collection );
		
	}

}
```
```java
package com.wkcto.chapter05.collection;

import java.util.ArrayList;
import java.util.Collection;
/**
 * 集合泛型与集合之间的相互操作
 * @author 蛙课网
 *
 */
public class Test02 {

	public static void main(String[] args) {
		//在实际应用中,一个集合中一般只存储同一类型的数据, 可以在定义集合时,通过泛型约束集合中元素的类型
		//Collection后面的尖括弧指定集合元素的类型, 这就是泛型, 泛型就是把数据类型当作参数
		Collection<String> collection = new ArrayList<>();
		
		//在添加元素时, collection集合就只能添加String类型的数据
		collection.add("gg");
		collection.add("jj");
		collection.add("dd");
		collection.add("mm");
		//如果添加的数据不是String类型,编译报错, 这就是泛型的好处,可以在编译时进行数据类型的检查
//		collection.add(123);  
		
		collection.add( "mm");
		collection.add( "jj");
		
		System.out.println( collection );  		//[gg, jj, dd, mm, mm, jj]

		//删除jj, remove()只删除第一个匹配的元素
		collection.remove("jj");
		System.out.println( collection );		//[gg, dd, mm, mm, jj]
		
		//创建第二个集合
		Collection<String> collection22 = new ArrayList<>();
		collection22.addAll(collection);  //把collection中 的所有元素添加到当前集合中
		System.out.println( collection22 );
		collection22.remove("mm");
		System.out.println( collection22 );   //[gg, dd, mm, jj]
		//判断collection集合中是否包含collection22集合中所有的元素
		System.out.println( collection.containsAll(collection22));  	//true
		//判断collection22集合中是否包含collection集合中所有的元素
		System.out.println( collection22.containsAll(collection));		//true
		//在colllection中删除在collection22集合中出现的元素
		collection.removeAll(collection22);
		System.out.println( collection );  		//[]
	}

}
```
```java
package com.wkcto.chapter05.collection;

import java.util.ArrayList;
import java.util.Collection;
import java.util.Iterator;
/**
 * 集合的迭代器
 * @author 蛙课网
 *
 */
public class Test03 {

	public static void main(String[] args) {
		//1)创建一个存储String字符串的Collection集合
		Collection<String> collection = new ArrayList<>();
		
		//2) 添加元素
		collection.add("gg");
		collection.add("jj");
		collection.add("dd");
		collection.add("jj");
		collection.add("dd");
		collection.add("jj");
		//3)直接打印
		System.out.println( collection );   	//[gg, jj, dd, jj, dd, jj]
		
		//4) 遍历集合中的元素
		for (String str : collection) {
			//把collection集合中的每个 元素赋值给局部变量str
			System.out.println( str );
		}
		
		//5)把所有的dd删除
//		collection.remove("dd") ;  		//删除第一个匹配的元素
//		collection.removeAll(c); 		//删除出现在c集合中的所有元素, 依次判断当前集合中每个 元素是否在c集合中,如果存在就删除
		
		//foreach循环仅用于遍历
	/*	for (String string : collection) {
			if ("dd".equals(string)) {
				collection.remove("dd");
			}
		}*/
		
		//6) 迭代器遍历
		//6.1 获得迭代器对象
		Iterator<String> iterator = collection.iterator();
		/*
		 * iterator.hasNext()用于判断是否还有下个元素没访问
		 * iterator.next()返回下个元素, 游标下移
		 * 刚刚获得迭代器时, 迭代器的游标指向第一个元素的前面
		 */
		//6.2迭代遍历
		while( iterator.hasNext() ){
			String str = iterator.next();
			System.out.print( str + "\t");
		}
		System.out.println();
		//循环完成后, iterator游标已经指向最后一个元素的后面, 如果还想要使用iterator迭代器,需要重写获得
		iterator = collection.iterator();   //重新获得迭代器后,游标指向 第一个元素的前面
		//6.3 迭代删除
		while (iterator.hasNext()) {
			String string = iterator.next();
			if ("dd".equals(string)) {
				iterator.remove();  	 	//迭代删除
			}
		}
		System.out.println( collection );
		
		//重新获得迭代器, 游标指向 第一个元素的前面
		iterator = collection.iterator();
		//获得了迭代器后, 如果再通过集合的add()/remove()/clear()等方法修改了集合的结构, 再迭代时,可能会产生异常
		//获得了迭代器后, 不能再通过集合的add()/remove()/clear()等方法修改集合的结构
		// 可以在通过集合的add()/remove()/clear()等方法修改集合的结构后, 重新获得迭代器对象
//		collection.add("dd");
		System.out.println( collection );
		//再迭代遍历
		while (iterator.hasNext()) {
			String string = (String) iterator.next();
//			System.out.print( string + "\t");
			if( "jj".equals(string) ){
//				collection.remove("jj");
			}
		}
	}

}
```
# Java中List集合
List集合的特点：存储的元素是有序/可重复的。
List集合为每个元素指定了一个索引值, 主要增加了针对索引值的操作。

| void | add(int index, E element) 在当前集合的index位置插入元素element |
| --- | --- |
| boolean | addAll(int index, Collection<? extends E> c) 把集合c中的所有元素插到当前集合的index位置 |
| E | [g](http://www.bjpowernode.com/tutorial_java_advance/637.html#get-int-)
et(int index) 返回index位置的元素 |
| int | indexOf(Object o) 返回元素o在集合中第一次出现的位置 |
| int | lastIndexOf(Object o) 返回元素o在集合中最后一次出现的位置 |
| ListIterator<E> | listIterator() 返回List迭代器 |
| E | remove(int index) 删除指定位置的元素 |
| E | set(int index, E element) 修改指定位置的元素 |
| default void | sort(Comparator<? super E> c) 排序 |
| List<E> | subList(int fromIndex, int toIndex) 返回[frominde, toIndex)范围内的子列表 |

```java
package com.wkcto.chapter05.list;

import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;

/**
 * 演示List的基本操作
 * @author 蛙课网
 *
 */
public class Test01 {
	public static void main(String[] args) {
		//1)创建List集合, List接口引用需要赋值实现类对象
		List<String> list = new ArrayList<>();
		
		//2)添加元素
		list.add("gg");
		list.add("jj");
		list.add("dd");
		list.add("mm");
		list.add("jj");
		
		//3)直接打印, List存储元素的顺序就是添加的顺序, 可以存储重复的数据
		System.out.println( list ); 		//[gg, jj, dd, mm, jj]

		//4) 判断
		System.out.println( list.size() );
		System.out.println( list.isEmpty());
		System.out.println( list.contains("jj"));
		
		//5) 删除
		list.remove("gg"); 		//删除第一个匹配的元素
		System.out.println( list ); 		//[jj, dd, mm, jj]
		
		//6) 遍历
		for (String string : list) {
			System.out.print( string + "\t");
		}
		System.out.println( );
		
		//7)迭代遍历
		Iterator<String> iterator = list.iterator();
		while (iterator.hasNext()) {
			String string = (String) iterator.next();
			System.out.print(string + "\t");
		}
		System.out.println( );
		
		//8)迭代删除
		iterator = list.iterator(); 		//重新获得迭代器对象
		while (iterator.hasNext()) {
			String string = (String) iterator.next();
			if ("jj".equals(string)) {
				iterator.remove();
			}
		}
		System.out.println( list );
		
	}
}
```
```java
package com.wkcto.chapter05.list;

import java.util.ArrayList;
import java.util.List;
import java.util.ListIterator;

/**
 * 演示List集合新增的操作
 * @author 蛙课网
 *
 */
public class Test02 {

	public static void main(String[] args) {
		// 1)创建List集合,
		List<String> list = new ArrayList<>();

		// 2)添加元素
		list.add("gg");
		list.add("jj");
		list.add("dd");
		list.add("mm");
		list.add("jj");

		// 3)直接打印, 
		System.out.println(list);		//[gg, jj, dd, mm, jj]
		
		//4) 在指定索引值的位置添加
		list.add(0, "MM");
		list.add(list.size(), "DD");
		System.out.println(list);		//[MM, gg, jj, dd, mm, jj, DD]
		//遇到索引值的位置,需要注意索引值不能越界
//		list.add(20 , "xxx");  		//java.lang.IndexOutOfBoundsException
		
		//5)删除指定位置的元素
		list.remove(0);
		System.out.println( list ); //[gg, jj, dd, mm, jj, DD]
		list.remove(list.size()-1);
		System.out.println( list ); //[gg, jj, dd, mm, jj]
		
		//6)返回指定位置的元素
		System.out.println( list.get(0));
		System.out.println( list.get(list.size()-1));
		
		//7)修改指定位置的元素
		list.set(0, "JJ");
		System.out.println( list );  //[JJ, jj, dd, mm, jj]
		
		//8)返回指定范围的子列表, 注意subList并没有生成新的List列表 ,而是返回原有List列表的一个视图
		List<String> sublist = list.subList(0, 3);
		System.out.println( sublist );  		//[JJ, jj, dd]
		//修改sublist子列表
		sublist.add("DD");
		sublist.set(0, "jj");
		System.out.println( sublist );  		//[jj, jj, dd, DD]
		//对subList进行的修改实际上就是对list进行修改
		System.out.println( list ); 			//[jj, jj, dd, DD, mm, jj]
		
		//9) 返回指定元素在列表中第一次出现的位置
		System.out.println( list.indexOf("jj"));
		System.out.println( list.lastIndexOf("jj"));
		
		//10) ListIterator迭代
		// ListIterator继承了Iterator
		ListIterator<String> listIterator = list.listIterator();
		while (listIterator.hasNext()) {
			String string = (String) listIterator.next();
			System.out.print( string + "\t");
		}
		System.out.println();
		//经过上个while循环后,listIterator游标指向最后,ListIterator还可以向前迭代
		while( listIterator.hasPrevious() ){
			String str = listIterator.previous();
			System.out.print( str + "\t");
		}
		System.out.println();
		//ListIterator不仅可以删除元素,还可以修改/添加元素
		while (listIterator.hasNext()) {
			String string = (String) listIterator.next();
			if (string.equals("mm")) {
				listIterator.remove();  	//删除
			}else if ( "jj".equals(string)) {
				listIterator.add("Dd");
			}else if ("dd".equals(string)) {
				listIterator.set("DD");
			}
		}
		System.out.println( list ); 	//[jj,Dd , jj, Dd, DD, DD, jj, Dd]
	}

}
```
```java
package com.wkcto.chapter05.list;

import java.util.ArrayList;
import java.util.List;

/**
 * List集合存储自定义类型数据
 * 	注意List集合的remove(Object)/contains(Object)方法会调用对象的equals()方法, 如果是自定义需要重写equals()方法 
 * @author 蛙课网
 *
 */
public class Test03 {

	public static void main(String[] args) {
		//创建List集合,存储Person对象
		List<Person> list = new ArrayList<>();
		
		//添加元素
		list.add(new Person("lisi", 18));
		list.add(new Person("feifei", 28));
		list.add(new Person("zhang", 33));
		list.add(new Person("yong", 35));
		
		System.out.println( list );
		
		Person feifei = new Person("feifei", 28);
		System.out.println( list.contains(feifei));
		
		list.remove(feifei);
		System.out.println( list );
	}

}
```
```java
package com.wkcto.chapter05.list;

import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;
/**
 * List集合排序
 * 	sort(Comparator)
 * @author 蛙课网
 *
 */
public class Test04 {

	public static void main(String[] args) {
		//创建List集合,存储Person对象
		List<Person> list = new ArrayList<>();
		
		//添加元素
		list.add(new Person("lisi", 18));
		list.add(new Person("feifei", 28));
		list.add(new Person("zhang", 33));
		list.add(new Person("yong", 35));

		//打印输出的顺序就是添加的顺序
		System.out.println( list );
		//[Person [name=lisi, age=18], Person [name=feifei, age=28], Person [name=zhang, age=33], Person [name=yong, age=35]]

		//对List集合中的元素排序, 想要对List集合中的Person对象按照年龄降序排序
		//调用方法时,传递Comparator的匿名内部类对象, 通过泛型指定比较对象的数据类型
		list.sort(new Comparator<Person>() {
			//在匿名内部类重写接口的抽象方法
			@Override
			public int compare(Person o1, Person o2) {
				//在compare方法中指定比较规则 , 按年龄降序
				return o2.age - o1.age;   //如果o1的年龄大返回负数, o2年龄大返回正数
//				return o1.age - o2.age;   //如果o1的年龄大返回正数, o2年龄大返回负数
			}
		});
		System.out.println( list );
		
		//对List排序, 根据姓名升序
		list.sort(new Comparator<Person>() {
			@Override
			public int compare(Person o1, Person o2) {
//				return o1.name.compareTo(o2.name); 	//姓名升序
				return o2.name.compareTo(o1.name); 	//姓名降序
			}
		});
		System.out.println(list);
	}

}
```
# Java中ArrayList与Vector的区别
ArrayList与Vector底层都是数组, 访问快, 添加/删除慢
● ArrayList与Vector底层都是数组
●  ArrayList与Vector默认初始化容量:10
●  ArrayList扩容: 1.5倍,   Vector扩容:2倍
● Vector提供的方法都使用了synchronized修饰 ,是线程安全的，ArrayList不是线程安全的。

# Java中LinkedList详解
LinkedList底层是双向链表
## 单向链表
![](https://images.cherryfloris.eu.org/2021/1633681552545-c6cd6b13-ff77-4044-8bdd-e48d9e1fc8cd.png)
双向链表
![](https://images.cherryfloris.eu.org/2021/1633681553275-50c3d7ba-d28b-48ae-a9da-67a98171b248.png)
LinkedList新增的方法
主要增加了针对头结点与尾结点进行操作的方法, 即针对第一个元素和最后一个元素进行操作的方法。
void：addFirst(E e) 添加到善
void：addLast(E e) 添加到尾部
E：element()返回第一个元素
E：getFirst() 返回第一个元素
E：getLast()返回最后一个元素
boolean：offer(E e) 把元素添加到尾部
boolean：offerFirst(E e) 添加到状况
boolean：offerLast(E e) 添加到尾部
E：peek() 返回第一个元素
E：peekFirst() 返回第一个元素
E：peekLast() 返回最后一个元素
E：poll() 删除第一个元素并返回
E：pollFirst() 删除第一个元素并返回
E：pollLast() 删除最后一个元素并返回
E：pop()删除第一个元素并返回
void：push(E e) 在头部添加元素
E：removeFirst() 删除第一个元素并返回
E：removeLast() 删除最后一个元素并返回
经常使用push( E ) / pop() 模拟栈, 栈的特点是先进后出/后进先出.   push( E )把元素添加到链表的头部,  pop()把链表头部的元素删除并返回。
使用offer( E ) / poll()  模拟队列,  队列的特点是先进先出, offer( E )添加元素是在链表的尾部添加,  poll() 是把链表的头部元素删除并返回。 
# Java Set集合与HashSet集合特点
Set集合
Set集合特点:** **存储的数据无序,不可重复
无序是指存储的顺序与添加的顺序可能不一样
```java
package com.wkcto.chapter05.set;

import java.util.HashSet;
import java.util.Iterator;
import java.util.Set;
/**
 * Set集合特点:
 * 		无序,不可重复
 * @author 蛙课网
 *
 */
public class Test01 {

	public static void main(String[] args) {
		//1)创建Set集合
		Set<String> set = new HashSet<>();
		
		//2)添加元素
		set.add("666");
		set.add("wkcto");
		set.add("hehehe");
		set.add("abc");
		
		//3)直接打印, 输出的顺序可能与添加的顺序不一致 
		System.out.println( set );   	//[abc, wkcto, 666, hehehe]
		
		//4)添加重复的元素
		set.add("wkcto");
		set.add("666");
		//Set集合中不能存储重复的元素		
		System.out.println( set ); 		//[abc, wkcto, 666, hehehe]
		
		//5)删除
		set.remove("abc");
		System.out.println( set); 		//[wkcto, 666, hehehe]
		
		//6)迭代
		Iterator<String> iterator = set.iterator();
		while (iterator.hasNext()) {
			String string = (String) iterator.next();
			System.out.print( string + "\t");
		}
		System.out.println();
		
	}

}
```
HashSet集合特点
● HashSet底层是HashMap
● 向Hashset中添加元素, 实际上是把这个元素作为键添加到底层的HashMap中
● HashSet实际上就是底层HashMap的键的集合
# Java TreeSet集合
TreeSet集合实现了SortedSet接口, 可以对集合中元素进行自然排序, 要求集合中的元素必须是可比较的。
```java
package com.wkcto.chapter05.set;

import java.util.Comparator;
import java.util.TreeSet;

/**
 * TreeSet集合
 * 		可以对元素进行自然排序, 要求元素必须是可比较的
 * 			1)创建TreeSet集合时,通过构造方法指定Comparator比较器
 * 			2)如果没有指定Comparator比较器, 要求元素的类必须实现Comparable接口
 * @author 蛙课网
 *
 */
public class Test03 {

	public static void main(String[] args) {
		//1) 创建TreeSet集合,存储Person对象, 在构造方法中指定Comparator比较器,按姓名升序排序
		TreeSet<Person> treeSet = new TreeSet<>(new Comparator<Person>() {
			//在匿名内部类中重写接口的抽象方法
			@Override
			public int compare(Person o1, Person o2) {
				//指定一个比较规则
				return o1.name.compareTo(o2.name);   //姓名升序
			}
		});
		
		//2)添加元素
		treeSet.add(new Person("lisi", 18));
		treeSet.add(new Person("feifei", 28));
		treeSet.add(new Person("yong", 35));
		treeSet.add(new Person("bin", 36));
		treeSet.add(new Person("zhang", 33));
		
		//3)直接打印
		System.out.println( treeSet );
		
		//4) 根据已有TreeSet创建新的TreeSet集合
		TreeSet<Person> treeSet22 = new TreeSet<>(treeSet);
		System.out.println( treeSet22 );
		
		//5) 使用TreeSet的无参构造, 没有指定Comparator比较器, 要求Person类实现Comparable接口
		TreeSet<Person> treeSet33 = new TreeSet<>();
		treeSet33.addAll(treeSet);		
		System.out.println( treeSet33);
	}

}
```
TreeSet集合底层是TreeMap，向TreeSet集合添加元素,实际上是把该元素作为键添加到了底层TreeMap中，TreeSet集合实际上就是底层TreeMap的键的集合。
```java
package com.wkcto.chapter05.set;

import java.util.Comparator;
import java.util.TreeSet;
/**
 * 注意:
 * 		在TreeSet集合中, 是根据Comparator/Comparable的比较结果是否为0来判断是否为同一个对象
 * 		如果Comparator的compare()方法/Comparable的compareTo()方法的返回值为0 就认为是同一个对象
 * @author 蛙课网
 *
 */
public class Test04 {

	public static void main(String[] args) {
		//创建TreeSet集合,存储Person对象, 通过构造方法指定Comparator比较器,按年龄降序排序
		TreeSet<Person> treeSet = new TreeSet<>(new Comparator<Person>() {
			@Override
			public int compare(Person o1, Person o2) {
				return o2.age - o1.age;
			}
		});
		
		//当前treeSet是根据年龄比较Person大小的, 在添加Person对象时, 如果年龄相同就认为是同一个对象
		treeSet.add(new Person("lisi", 18));
		treeSet.add(new Person("feifei", 18));
		treeSet.add(new Person("zhang", 18));
		treeSet.add(new Person("yong", 18));
		
		System.out.println( treeSet.size() ); 		// 1
		System.out.println( treeSet );
		System.out.println( treeSet.contains( new Person("wang", 18)));   //true
	}

}
```
# Java Collection集合小结
Collection集合
只能存储引用类型的数据, 单个存储
基本操作:  add(), remove(), contains(), size(), iterator()
## List集合
特点: 存储的元素是有序,可重复的
为每个元素指定一个索引值
增加的方法, 针对索引值的操作, listIterator(),  subList(),  sort(Comparator)
## ArrayList集合
底层是数组, 访问快, 添加/删除效率低
初始化容量: 10,  扩容: 1.5倍
## Vector集合
底层是数组, 它是线程安全的, ArrayList不是线程安全的
初始化容量: 10,  扩容: 2倍
## LinkedList集合
底层是双向链表, 添加/删除效率高, 访问慢
## List集合应用场景
ArrayList适用于以访问为主, 很少添加/删除的情况
LinkedList适用于经常添加/删除的情况
## Set集合
特点: 数据无序,不可重复
## HashSet集合
底层是HashMap, HashSet实际上就是HashMap键的集合
## TreeSet集合
底层是TreeMap, TreeSet实际上就是TreeMap键的集合
TreeSet实现了SortedSet接口, 可以对元素自然排序, 要求元素必须是可比较的：
● 在构造方法中指定Comparator比较器对象
● 如果没有Comparator比较器, 集合元素的类必须实现Comparable接口
## Set集合的应用场景
如果不需要对Set集合进行排序就选择HashSet
如果需要对Set集合的元素进行排序就选择TreeSet
## 注意:
List集合/HashSet集合的contains( e ) / remove( e )等方法需要调用对象的equals()方法, 这些集合中的元素的类需要重写equals()方法
TreeSet集合中contains( e )/  remove( e) 等方法判断是否同一个对象是根据Comparator/Comparable的比较结果是否为0来判断的, 如果比较结果为0表示同一个元素
# Java中Collections工具类
java.util.Collections类, 该工具类中有一组方法, synchronizedXXX( xxx )可以把xxx集合转换为线程安全的集合。
static <T> Collection<T> synchronizedCollection(Collection<T> c) 
static <T> List<T> synchronizedList(List<T> list)  
static <K,V> Map<K,V> synchronizedMap(Map<K,V> m)  
static <T> Set<T> synchronizedSet(Set<T> s)  
但是,在开发多线程程序时, 基本不使用这一组操作, 在多线程环境中：
● 如果使用List集合就直接使用java.util.concurrent.CopyOnWriteArrayList类。
● 如果使用Set集合，不需要排序,使用java.util.concurrent.CopyOnWriteArraySet类, 如果需要排序,使用java.util.concurrent.ConcurrentSkipListSet集合。
# Java泛型详解
在Comparable/Comparator接口中通过泛型指定比较对象的数据类型, 在Collection集合中,通过泛型指定集合元素的类型。
泛型就是把数据类型参数化。
泛型的好处,可以在编译时进行数据类型检查。
**如:**
Collection<String> collection = new ArrayList<>(); 约束collection集合中只能存储String类型的数据。
## 注意:
Collection  collection = new ArrayList<String> ();  如果在定义collection集合时没有指定泛型 ,在创建ArrayList对象时指定了泛型, 是没有作用的, 当前的collection集合依然是存储Object类型的数据。
