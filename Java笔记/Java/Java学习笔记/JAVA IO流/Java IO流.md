# Java IO流的分类
流是有起点和终点的有序的字节序列
## 流的分类
输入流/输出流. 是以当前程序为参照, 如果程序从外面读取数据到程序中来就是输入流, 把程序中的数据保存到外面就是输出流。
字节流/字符流. 如果是以字节为单位处理流中的数据就是字节流, 如果是以字符为单位处理流中的数据就是字符流。
节点流/处理流. 如果直接从数据源读写数据就是节点流, 处理流是对节点流的包装。
在程序中, 经常需要读写文件中的数据, 需要使用IO流, Java在jav.io包中定义了相关的流类, 这些类如果是以Stream单词结尾就是字节流, 如果是以Reader结尾就是字符输入流, 如果是以Writer结尾就是字符输出流。
![](https://images.cherryfloris.eu.org/2021/1633760808185-2a13b4ec-1fdf-4620-8446-a9166ffd18af.png)


![](https://images.cherryfloris.eu.org/2021/1633760808230-43eda6a3-6b96-4ef6-ba9f-fa24ff97e065.png)
# Java文件输入输出流
使用这两个类可以读写文件内容, 是以字节为单位
```java
package com.wkcto.chapter06.fileinputstream;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;

/**
 * 以字节为单位读取文件的内容, 循环读取
 * @author 蛙课网
 *
 */
public class Test03 {
	public static void main(String[] args) throws IOException {
		//1)在当前程序与指定的文件之间建立流通道
		//使用FileInputStream类以字节为单位读取文件内容, 通过构造方法指定要访问的文件
		FileInputStream fis = new FileInputStream("d:/abc.txt");
		//该文件内容: ABCabc
		
		//2)读取文件数据, read()方法从文件中读取一个字节 ,并把读到 的字节返回, 如果读到文件末尾返回-1
		int cc = fis.read(); 
		
		while( cc != -1 ){
			//对读到的cc字节进行处理
//			System.out.println( cc ); 		//把读到的字节打印到屏幕上
			System.out.print( (char)cc ); 			//当前文件中都是英文字符,一个字符对应一个字节, 把读到的字节转换为字符再打印
			//继续读取文件中的内容
			 cc = fis.read(); 
		}
				
		//3)关闭流通道
		fis.close();
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
```java
package com.wkcto.chapter06.fileinputstream;

import java.io.FileInputStream;
import java.io.IOException;
/**
 * 一次读取一个字节数组,循环读取
 * @author 蛙课网
 *
 */
public class Test04 {

	public static void main(String[] args) throws IOException {
		//1)建立与文件的流通道
		FileInputStream fis = new FileInputStream("d:/abc.txt");
		//文件内容:ABCabcwkcto
		
		byte[] bytes = new byte[8];
		
		//2)读取数据保存到字节数组中, 返回读到的字节数,如果读到文件末尾返回-1
		int len = fis.read(bytes);
		
		while( len != -1 ){
			//从流中读取了len个字节保存到了字节数组中, 可以对这len个字节 进行处理
			//把读到的len个字节转换为字符串打印到屏幕上
			System.out.print( new String(bytes, 0, len)  );
			
			//继续向下读, 读的字节继续保存到字节中
			len = fis.read(bytes);
		}		
		
		//3)关闭流
		fis.close();
	}

}
```
```java
package com.wkcto.chapter06.fileinputstream;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;

/**
 * 异常处理
 * @author 蛙课网
 *
 */
public class Test05 {

	public static void main(String[] args) {
		
//		readData(); 		//以字节为单位读取文件内容, 异常处理, 手动关闭流
		readData2(); 		//以字节数组为单位读取文件内容, 异常处理, 自动 关闭流, 从JDK7开始
	}

	private static void readData2() {		
		try (
				FileInputStream fis = new FileInputStream("d:/abc.txt");
				) {
			byte [] bytes = new byte[8];  	//字符数组一般情况下是1024的偶数倍
			int len = fis.read(bytes);
			while( len != -1){
				System.out.print( new String(bytes, 0 ,len));
				len = fis.read(bytes);
			}
			
		} catch (Exception e) {
		}
	}
```
```java
private static void readData() {
		
		FileInputStream fis = null;
		try {
			fis = new FileInputStream("d:/abc.txt");
			int cc = fis.read();
			while( cc != -1 ){
				System.out.print( (char)cc );
				cc = fis.read();
			}
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		} finally {
			if ( fis != null) {
				try {
					fis.close();
				} catch (IOException e) {
					e.printStackTrace();
				}				
			}			
		}
		
	}

}
```
```java
package com.wkcto.chapter06.fileinputstream;

import java.io.FileOutputStream;
import java.io.IOException;

/**
 * 演示FileOutputStream, 把程序中的数据保存到文件中
 * @author 蛙课网
 *
 */
public class Test06 {

	public static void main(String[] args) throws IOException {
		//1)建立当前程序与文件之间的流通道, 如果文件不存在,会创建一个新的文件,如果文件已存在,会覆盖原来的内容
//		FileOutputStream fos = new FileOutputStream("d:/def.txt");
		//1)建立当前程序与文件之间的流通道, 如果文件不存在,会创建一个新的文件,如果文件已存在,原文件后面追加新的内容
		FileOutputStream fos = new FileOutputStream("d:/def.txt", true); 	//以追加的方式打开文件
		//2)把数据保存到文件中
		//2.1 可以一次保存一个字节
		fos.write(97);
		fos.write(98);
		fos.write(99);
		//2.2 可以一次保存一个字节数组
		byte[]bytes = "wkcto is a NB Website".getBytes();
		fos.write(bytes);
		//2.3 换行 , 在Windows操作系统中,换行需要\r\n两个 字符
		fos.write('\r');
		fos.write('\n');
		//2.4 保存字节数组中部分字节
		fos.write(bytes, 0, 5);
		
		//3)关闭流通道
		fos.close();
	}

}
```
```java
package com.wkcto.chapter06.fileinputstream;

import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;

/**
 * 以字节流实现文件的复制
 * @author 蛙课网
 *
 */
public class Test07 {

	public static void main(String[] args) {
		String srcFile = "d:/javase/video/6-6 FileOutputStream保存数据到文件.avi"	;
		String destFile = "d:/hehe.avi";
		
//		copyFile1( srcFile, destFile );  		//以字节为单位复制, 异常处理, 手动关闭流
		copyFile2(srcFile ,destFile); 			//以字节数组为单位复制, 异常处理, 自动关闭流
	}

	////以字节数组为单位复制, 异常处理, 自动关闭流
	private static void copyFile2(String srcFile, String destFile) {
		try (
				FileInputStream fis = new FileInputStream(srcFile);
				FileOutputStream fos = new FileOutputStream(destFile);
				) {
			byte [] bytes = new byte[1024];
			int len = fis.read(bytes);
			while( len != -1 ){
				//把读到的len个字节保存到fos输出流中
				fos.write(bytes, 0, len);
				len = fis.read(bytes);
			}
			
		} catch (Exception e) {
		}
	}

	////以字节为单位复制, 异常处理, 手动关闭流
	private static void copyFile1(String srcFile, String destFile) {
		//文件复制,从源文件中读取一个字节, 把该字节保存到目标文件中
		
		FileInputStream fis = null;
		FileOutputStream fos = null;
		try {
			fis = new FileInputStream(srcFile);
			fos = new FileOutputStream(destFile);
			
			int cc = fis.read(); 	//从源文件中读取一个字节
			while( cc != -1 ){
				//把读到的字节cc保存到目标文件中
				fos.write(cc);
				//继续读到源文件的下个字节
				cc = fis.read(); 
			}
		} catch (IOException e) {
			e.printStackTrace();
		}finally {
			if ( fis != null ) {
				try {
					fis.close();
//					fos.close(); 		//不能放在一起
				} catch (IOException e) {
					e.printStackTrace();
				}
			}
			if (fos != null) {
				try {
					fos.close();
				} catch (IOException e) {
					e.printStackTrace();
				}
			}
		}

	}

}
```
# Java缓冲输入输出流
缓冲字节流
默认有8192字节的缓冲区
![](https://images.cherryfloris.eu.org/2021/1633770508106-c2added6-de23-48ed-bf75-39033719c29f.png)
```java
package com.wkcto.chapter06.filterstream;

import java.io.BufferedInputStream;
import java.io.BufferedOutputStream;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;

/**
 * 字节缓冲流
 * 		BufferedInputStream/BufferedOutputStream
 * @author 蛙课网
 *
 */
public class Test01 {

	public static void main(String[] args) throws IOException {
		//1)使用字节缓冲流读取文件内容
//		readData();
		
		//2)使用字节缓冲流保存数据到文件
		writeData();
		
	}

	//使用字节缓冲流保存数据到文件
	private static void writeData() throws IOException {
		//在当前程序与指定的文件间建立字节流通道
		OutputStream out = new FileOutputStream("d:/def.txt");
		//使用字节缓冲流对out字节流进行包装(缓冲)
		BufferedOutputStream bos = new BufferedOutputStream(out);
		
		//使用缓冲流保存数据, 现在是把数据保存到缓冲流的缓冲区中
		bos.write(97);
		
		byte[] bytes = "wkcto is  a good websit".getBytes();
		bos.write(bytes);
		
//		bos.flush(); 	//把缓冲区的数据清空到文件里
		bos.close();
	}

	//使用字节缓冲流读取文件内容
	private static void readData() throws IOException {
		//在当前程序与指定的文件之间建立字节 流通道 
		InputStream in = new FileInputStream("d:/abc.txt");
		//对字节流进行缓冲
		BufferedInputStream bis = new BufferedInputStream(in);
		
		//使用缓冲字节流读取文件内容
		int cc = bis.read();
		while( cc != -1){
			System.out.print( (char)cc );
			cc = bis.read();
		}
		
		bis.close(); 	//关闭缓冲流, 也会把被包装的字节流关闭
	}

}
```
# Java数据输入输出流
```java
package com.wkcto.chapter06.filterstream;

import java.io.DataInputStream;
import java.io.DataOutputStream;
import java.io.FileInputStream;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.io.OutputStream;

/**
 * DataInputStream/DataOutputStream
 * 	可以读写带有数据格式的数据
 * 	不直接对数据源进行操作, 是处理流
 * @author 蛙课网
 *
 */
public class Test02 {

	public static void main(String[] args) throws IOException {
		//1) 保存数据
//		writeData();
		
		//2) 读取文件
		readData();
	}

	//使用DataInputStream读取文件的内容
	private static void readData() throws IOException {
		InputStream in = new FileInputStream("d:/def.txt");
		DataInputStream dis = new DataInputStream(in);
		
		//读取的顺序要与写入的顺序一致 
		int num = dis.readInt();
		double dd = dis.readDouble();
		boolean flag = dis.readBoolean();
		String text = dis.readUTF();
		
		dis.close();
		System.out.println("num=" + num + " ,dd=" + dd + " ,flag=" + flag + " ,text=" + text);
	}

	//使用DataOutputStream保存数据
	private static void writeData() throws IOException {
		OutputStream out = new FileOutputStream("d:/def.txt");
		DataOutputStream dos = new DataOutputStream(out);
		
		dos.writeInt(123);				//保存整数
		dos.writeDouble(3.14);			//保存小数
		dos.writeBoolean(true);			//保存布尔
		dos.writeUTF("wkcto");			//保存字符串
		
		dos.close();
	}

}
```
# Java打印流与Java装饰者设计模式
PrintStream
```java
package com.wkcto.chapter06.filterstream;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.OutputStream;
import java.io.PrintStream;

/**
 * PrintStream
 * 	字节打印流
 * @author 蛙课网
 *
 */
public class Test03 {

	public static void main(String[] args) throws FileNotFoundException {
		//在追加的方式建立与文件的字节流通道
		OutputStream out = new FileOutputStream("d:/log.txt", true);
		//创建打印流
		PrintStream  pStream = new PrintStream(out);
		
		pStream.print("hello");			//打印,不换行
		pStream.println(" wkcto"); 		//打印,换行
		pStream.println("feifei");
		
        
		System.out.println("在屏幕上打印信息, System类的out成员就是一个PrintStream打印流");
		System.out.println("System.out代表系统的标准输出设备,显示器,");
		//修改System.out的打印输出方向
		System.setOut(pStream);
		System.out.println("现在打印的信息就不是显示在屏幕上了, 而是打印到pstream流中,即log.txt文件中");
		
		//有时, 也会把异常信息打印到日志文件中
		try {
			FileInputStream fis = new FileInputStream("F:/abc.txt");
		} catch (Exception e) {
			// 在开发时,一般是把异常打印到屏幕上,方便程序员调试
//			e.printStackTrace();
			// 在部署后, 经常把异常打印到日志文件中
			e.printStackTrace(pStream);
		}
	
		pStream.close();
	}

}
```
装饰者设计模式
设计模式就是别人总结的一套解决方案, 这套解决方案被大多数人熟知与认可
装饰者设计模式是对现有类的现有方法进行功能的扩展
在IO流相关类中,以Filter开头的类采用了装饰者设计模式
# Java对象输入输出流
对象序列化：把一个对象转换为01二进制
对象反序列化：把一组01二进制转换为对象
ObjectOutputStream类可以实现对象序列化, 把对象转换为01序列保存到文件中
ObejctInputStream类实现对象反序列化,从文件中读取01序列转换为对象
## 注意:
对象序列化/反序列化的前提是对象的类必须实现Serializable接口, 该接口是一个标志接口,没有任何方法,只是告诉编译器这个类的对象可以序列化。
```java
package com.wkcto.chapter06.objectstream;

import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.ObjectOutputStream;
import java.io.OutputStream;

/**
 * 使用ObjectOutputStream可以实现对象的序列化, 把对象的01序列保存到文件中
 * 
 * @author 蛙课网
 *
 */
public class Test01 {
	public static void main(String[] args) throws IOException {
		//创建Person对象
		Person lisi = new Person("lisi", 18);
		
		//把lisi对象序列化, 就是把lisi对象保存到文件中
		OutputStream out = new FileOutputStream("d:/obj.txt");
		ObjectOutputStream oos = new ObjectOutputStream(out);
		
		oos.writeObject(lisi); 		//对象序列化
		
		oos.close();
		
	}
}
```
```java
package com.wkcto.chapter06.objectstream;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.io.InputStream;
import java.io.ObjectInputStream;

/**
 * 使用ObjectInputStream类实现对象的反序列化,
 * 		就是从文件中把保存的对象读取出来
 * 
 * @author 蛙课网
 *
 */
public class Test02 {

	public static void main(String[] args) throws IOException, ClassNotFoundException {
		InputStream in = new FileInputStream("d:/obj.txt");
		ObjectInputStream ois = new ObjectInputStream(in);
		
		Object obj = ois.readObject();  	//从文件中读取一个对象, readObject()方法的返回值是Object类型的
		//文件中实际存储的是Person对象, 使用obj引用指向Person对象
		
		System.out.println( obj ); 		//实际上调用的是Person对象的toString()方法
		ois.close();
		
		/*
		 * 在对象序列化之后 ,即把对象已经保存到文件中了,  又在Person类中添加了一个字段,修改了Person类结构,
		 * 	再进行反序列化时, 出现了异常:
		 *  java.io.InvalidClassException:
		 *  	com.wkcto.chapter06.objectstream.Person; local class incompatible: 
		 * 		stream classdesc serialVersionUID = 3479771803741762411, 
		 * 		local class serialVersionUID = 1549311491347595402
		 * 分析原因:
		 * 		流中类的描述信息中 serialVersionUID的值与本地字节码文件中 serialVersionUID字段的值不相等引发的异常
		 * 
		 * 		当类Person实现了Serializable接口后, 系统会自动的在Person类中增加一个serialVersionUID序列化版本号字段
		 * 		在lisi对象序列化时, serialVersionUID字段的值是: 3479771803741762411
		 * 		当序列化后, 又在Person类添加了gender字段, 编译后,在字节码文件中重新生成了一个serialVersionUID的值:1549311491347595402
		 * 		在进行反序列化时, 系统会检查流中serialVersionUID序列化版本号字段与本地字节码文件中serialVersionUID字段的值是否一样
		 * 			如果相等就认为是同一个类的对象, 如果这个serialVersionUID序列化版本号字段的值不相等,就认为是不同类的对象
		 * 解决方法:
		 * 		保证反序列化时流中serialVersionUID字段 的值,与本地字节码文件中serialVersionUID字段的值相等即可
		 * 		可以在Person类实现了Serializable接口后, 手动的添加一个serialVersionUID字段 
		 */
		
	}

}
```
```java
package com.wkcto.chapter06.objectstream;

import java.io.Serializable;
/**
 * Person类的对象要想序列化, Person类必须实现Serializable接口
 * 		Serializable接口是一个标志接口,没有任何方法
 * @author 蛙课网
 *
 */
public class Person implements Serializable{
	String  name;
	int age;
	
	String gender; 		//性别
	
	//手动的添加序列化版本号字段
	 private static final long serialVersionUID = -1345649873215667710L;
	
	
	@Override
	public String toString() {
		return "Person [name=" + name + ", age=" + age + ", gender=" + gender + "]";
	}


	public Person(String name, int age) {
		super();
		this.name = name;
		this.age = age;
	}
	
}
```
# Java文件字符输入输出流
字符流是以字符为单位处理流中的数据, 也可以说是以字符为单位读写文件的内容。
FileReader/FileWriter字符流只能读写纯文本文件, 并且要求文本文件的编码与当前环境的编码要兼容。
```java
package com.wkcto.chapter06.readerwriter;

import java.io.FileReader;
import java.io.IOException;

/**
 * FileReader/FileWriter字符流
 * 	1)只能读写纯文本文件
 * 	2)要求文本文件的编码与当前环境的编码兼容
 * @author 蛙课网
 *
 */
public class Test01 {

	public static void main(String[] args) throws IOException {
		//1)使用FileReader读取文本文件: d:/abc.txt中的内容, 该文件使用GBK编码, 文件中全部是英文字符
//		readFile1();
		
		//2) 读取d:/log.txt文件的内容, 该文件使用UTF-8编码, 文件中有中文也有英文字符
		readFile2();
		
	}

	//使用FileReader读取文件, 一次读取一个字符数组
	private static void readFile2() throws IOException {
		FileReader fReader = new FileReader("d:/log.txt");
//		FileReader fReader = new FileReader("d:/test01.java");   //该文件使用GBK编码,当前环境使用UTF-8编码, 文件中有中文也有英文
		
		char [] contents = new char[8];
		
		//从文件中读取字符保存到字符数组中, 返回读到的字符个数, 如果读到文件末尾返回-1
		int len = fReader.read(contents);
		while( len != -1 ){
			//把读到的len个字符转换为字符串打印到屏幕上
			System.out.print( new String(contents, 0 ,len ));
			len = fReader.read(contents);
		}
		
		fReader.close();
	}

	private static void readFile1() throws IOException {
		FileReader fr = new FileReader("d:/abc.txt");
		
		//read()读取一个字符, 返回该字符的码值, 读到文件末尾返回-1
		int cc = fr.read();
		while( cc != -1 ){
			System.out.print( (char)cc );
			 cc = fr.read();
		}
		
		fr.close();
	}

}
```
```java
package com.wkcto.chapter06.readerwriter;

import java.io.FileWriter;
import java.io.IOException;

/**
 * FileWriter
 * 	可以把字符保存到文本文件中, 该文本文件要与当前环境编码兼容
 * @author 蛙课网
 *
 */
public class Test02 {

	public static void main(String[] args) throws IOException {
//		FileWriter fw = new FileWriter("d:/def.txt"); 		//以覆盖的方式打开 文件,如果原来的文件格式是GBK,写入后文件的格式变为UTF-8
		FileWriter fw = new FileWriter("d:/def.txt", true); //以追加的方式打开 文件,如果原来的文件格式是GBK,写入后文件会出现乱码
		
		//一次写一个字符
		fw.write('A');
		fw.write('中');
		
		//一次写一个字符数组
		char [] contents = "wkcto是一个NB的网站".toCharArray(); 
		fw.write(contents);
		
		fw.write("还可以一次写一个字符串");
		
		fw.write("\r\n"); 		//换行 
		
		fw.close();
	}

}
```
```java
package com.wkcto.chapter06.readerwriter;

import java.io.FileReader;
import java.io.FileWriter;
import java.io.IOException;

/**
 * 使用FileReader/FileWriter实现文本文件的复制
 * 		文本文件的编码要与当前环境的编码兼容
 * @author 蛙课网
 *
 */
public class Test03 {

	public static void main(String[] args) {
		String  srcfile = "d:/test.java";
		String  destfile = "d:/javase/wk.txt"	;
		
//		copyfile( srcfile, destfile) ; 		//逐个字符复制, 异常处理, 手动关闭流
		copyfile2( srcfile, destfile) ; 	//一次复制一个字符数组, 异常处理, 自动关闭流
	}

	//一次复制一个字符数组, 异常处理, 自动关闭流
	private static void copyfile2(String srcfile, String destfile) {
		try (
				FileReader fr = new FileReader(srcfile);
				FileWriter fw = new FileWriter(destfile);
				){
			char [] contents = new char[1024];
			
			int len = fr.read(contents);
			while( len != -1 ){
				fw.write(contents, 0, len);
				len = fr.read(contents);
			}
			
		} catch (Exception e) {
		}
	}

	//逐个字符复制, 异常处理, 手动关闭流
	private static void copyfile(String srcfile, String destfile) {
		FileReader fr = null;
		FileWriter fw = null;
		try {
			fr = new FileReader(srcfile);
			fw = new FileWriter(destfile);
			
			int cc = fr.read();
			while( cc != -1 ){
				//把读到的字符cc保存到fw输出流中
				fw.write(cc);
				//继续读下个字符
				cc = fr.read();
			}
		} catch (IOException e) {
			e.printStackTrace();
		}finally {
			if ( fr != null ) {
				try {
					fr.close();
				} catch (IOException e) {
					e.printStackTrace();
				}
			}
			if (fw != null) {
				try {
					fw.close();
				} catch (IOException e) {
					e.printStackTrace();
				}
			}
		}
		
		
	}

}
```
# Java字符输入输出流
InputStreamReader可以把字节流,以指定的编码转换为字符流。
OutputStreamWriter可以把字符流以指定的编码转换为字节流。
这两个类采用了适配器设计模式, 电源适配器可以把220的交流电转换为20V的直流电,  InputStreamReader把字节流转换为字符流, OutputStreamWriter把字符流转换为字节流。
```java
package com.wkcto.chapter06.readerwriter;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.io.OutputStream;
import java.io.OutputStreamWriter;
import java.io.UnsupportedEncodingException;

/**
 * InputStreamReader/OutputStreamWriter , 转换流类
 * 	当文本文件的编码格式与当前环境的编码格式不兼容时, 使用转换流类读写文件
 * @author 蛙课网
 *
 */
public class Test04 {

	public static void main(String[] args) throws IOException {
		
		//读取文本文件, 文本文件的编码与当前环境编码不兼容
//		readData();
		
		//保存文件, 以指定的编码把数据保存到文件中
		writeData();
	}

	private static void writeData() throws  IOException {
		OutputStream out = new FileOutputStream("d:/def.txt"); 	//以覆盖的方式打开文件
		OutputStreamWriter osw = new OutputStreamWriter(out, "GBK");
		
		osw.write("程序开发环境使用UTF-8编码, 而现在是以GBK的格式把数据保存到文件中");
		osw.close();
	}

	//读取文本文件, 文本文件的编码与当前环境编码不兼容
	private static void readData() throws IOException {
		//在当前程序与d:/test01.java文件之间建立字节流通道 , d:/test01.java文件使用GBK编码, 当前环境是UTF-8编码
		InputStream in = new FileInputStream("d:/test01.java");
		//使用转换流, 把字节流in中的字节,按照指定的编码GBK转换为字符
		InputStreamReader isr = new InputStreamReader(in, "GBK");
		
		//可以读取字符流isr中的字符
		int cc = isr.read();
		while( cc != -1){
			System.out.print( (char)cc);
			cc = isr.read();
		}
		
		isr.close();
	}

}
```
# Java缓冲字符输入输出流
字符缓冲流
默认有8192字符大小的缓冲区
```java
package com.wkcto.chapter06.readerwriter;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.FileInputStream;
import java.io.FileReader;
import java.io.FileWriter;
import java.io.FilterWriter;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Scanner;

/**
 * BufferedReader/BufferedWriter
 * 	字符缓冲流, 对其他字符流进行缓冲, 默认缓冲区大小为8192个字符
 * @author 蛙课网
 *
 */
public class Test05 {

	public static void main(String[] args) throws IOException {
		//1) 使用缓冲字符流读取文件的内容
//		readData();
		//2) 使用缓冲字符流保存数据到文件中
		writeData();
	}
	
	//2) 使用缓冲字符流保存数据到文件中
	private static void writeData() throws IOException {
		FileWriter  fw = new FileWriter("d:/def.txt");
		BufferedWriter bw = new BufferedWriter(fw);
		
		//把数组保存到缓冲流的缓冲区中
		bw.write("hello");
		bw.newLine();
		bw.write("wkcto");
		
		//从键盘上输入数据保存到文件中
//		Scanner sc = new Scanner(System.in);
		//System.in代表系统的标准输入设备,即键盘,  System类的in字段是InputStream字节流
//		String line = sc.nextLine(); 		//从键盘上读取一行
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		String line = br.readLine();
		while( line.length() > 0 ){
			bw.write(line);
			bw.newLine();
//			line = sc.nextLine();
			line = br.readLine();
		}
		
		bw.close(); 		//关闭缓冲流时,会把缓冲区的数据保存到文件中
		
	}
	//1) 使用缓冲字符流读取文件的内容
	private static void readData() throws IOException {
		//创建字符流, d:/test.java文件, 该文件编码为utf-8,与当前环境编码一致
//		FileReader fr = new FileReader("d:/test.java");
		//创建字符流, d:/test01.java文件, 该文件编码为GBK,与当前环境编码不一致
		InputStreamReader fr = new InputStreamReader(new FileInputStream("d:/test01.java"), "GBK");
		//对字符流进行缓冲
		BufferedReader br = new BufferedReader(fr);
		
		//从缓冲字符流中读取数据, readLine()从输入缓冲字符流中读取一行, 读到文件末尾返回null
		String line = br.readLine();
		while( line != null ){
			System.out.println( line);
			line = br.readLine();
		}
		
		br.close();
	}

}
```
# Java File类概述
使用IO流类读写文件的内容, 如果对文件/文件夹进行操作,可以使用File类
```java
package com.wkcto.chapter06.file;

import java.io.File;
import java.io.IOException;

/**
 * 创建File对象
 * @author 蛙课网
 *
 */
public class Test01 {

	public static void main(String[] args) throws IOException {
		//通过File构造方法的参数指定路径 ,File对象既可以是文件夹,也可以是文件
		File  f1 = new File("d:/java1");
		File  f2 = new File("d:/java2");
		f1.mkdir(); 			//创建文件夹
		f2.createNewFile(); 	//创建文件
		
		//通过File构造方法的第一个参数指定上级目录
		File f3 = new File("d:/java1", "sub1");
		File f4 = new File("d:/java1", "sub2");
		f3.mkdir();
		f4.createNewFile();
		
		File  f5 = new File(f3, "sub3");
		File  f6 = new File(f3, "sub3");
		//f5和f6两个对象重名
		f5.mkdir();						//创建了sub3文件夹
		f6.createNewFile();  			//创建sub3文件夹, 出现了重名现象, 创建失败
		
		//在创建File对象,也可以使用相对路径 , 相对于当前项目的路径
		File f7 = new File("folder");
		File f8 = new File("bin/folder2");
		f7.mkdir();
		f8.mkdir();
	}

}
```
```java
package com.wkcto.chapter06.file;

import java.io.File;

/**
 * File文件/路径的分隔符
 * @author 蛙课网
 *
 */
public class Test02 {

	public static void main(String[] args) {
		System.out.println( File.separator);			//\ 在windows系统中文件默认分隔符是反斜杠\
														//在其他操作系统中, 如Linux, 文件分隔符是斜杠 /
		System.out.println( File.pathSeparator);		//; 路径分隔符
	}

}
```
# File类常用操作
boolean：createNewFile() 创建一个新的文件
boolean：delete() 删除File对象
boolean：exists() 判断当前File对象是否存在
File：getAbsoluteFile() 返回File对象的绝对路径形式
String：getAbsolutePath()返回File对象的绝对路径
long：getFreeSpace() 返回指定盘符空闲空间的大小
String：getName() 返回File对象的名称
String：getParent() 返回上一级目录
File：getParentFile()返回上一级目录
String：getPath() 返回路径
long：getTotalSpace() 返回指定盘符总的大小
long：getUsableSpace()返回指定盘符可用空间的大小
boolean：isAbsolute() 判断是否为绝对路径
boolean：isDirectory() 判断是否为文件夹
boolean：isFile() 判断是否为文件
boolean：isHidden() 判断是否为隐藏
long：lastModified() 最后一次修改的时间,是从1970-1-1 00:00:00经过的毫秒数
long：length() 文件长度
String[]：list() 列出文件夹中的内容
String[]：list(FilenameFilter filter) 列出文件夹中的内容,指定文件过滤器
File[]：listFiles()列出文件夹中的内容
File[]：listFiles(FileFilter filter) 列出文件夹中的内容
File[]：listFiles(FilenameFilter filter) 列出文件夹中的内容
staticFile[]：listRoots() 列出根目录
boolean：mkdir() 创建文件夹.如果上一级目录不存在,则文件夹创建失败
boolean：mkdirs()创建文件夹. 如果上一级目录不存在,先创建上一级目录,再创建当前文件夹
boolean：renameTo(File dest) 重命名,如果dest对象和当前File对象不在同一个目录中,相当于文件移动
Path：toPath()
String：toString()
URI：toURI()
```java
package com.wkcto.chapter06.file;

import java.io.File;
import java.io.IOException;
import java.util.Date;

/**
 * 演示文件的相关属性
 * @author 蛙课网
 *
 */
public class Test03 {

	public static void main(String[] args) throws IOException {
//		File f1 = new File("D:\\JavaSE\\video\\5-24 Map集合概述.avi");  		//绝对路径 
		File f1 = new File("hehe.txt");			//相对路径 
		f1.createNewFile();
		
		System.out.println( f1.getAbsolutePath() );
		System.out.println( f1.getPath());
		System.out.println( f1.getParent());
		System.out.println( f1.getName());
		System.out.println( f1.isDirectory());
		System.out.println( f1.isFile());
		System.out.println( f1.length());
		System.out.println( f1.lastModified());
		System.out.println( new Date(f1.lastModified()));
	}

}
```
```java
package com.wkcto.chapter06.file;

import java.io.File;
import java.io.FilenameFilter;

/**
 * 演示文件夹的相关操作
 * @author 蛙课网
 *
 */
public class Test04 {

	public static void main(String[] args) {
		String folder = "d:/java1"	;
		
		//显示指定文件夹的内容
		listsubDir( folder );  
	}

	//显示指定文件夹的内容, 只显示.txt文本文件
	private static void listsubDir(String folder) {		
		File  dir = new File(folder);
		//列出指定文件夹的内容
		File[] listFiles = dir.listFiles(new FilenameFilter() {
			//在匿名内部类对象中重写抽象方法
			@Override
			public boolean accept(File dir, String name) {
				return name.endsWith(".txt") || name.endsWith(".java");
			}
		}) ;

		for (File file : listFiles) {
			System.out.println( file.getAbsolutePath() );
		}	
	}
	//显示指定文件夹的内容
	private static void listsubDir2(String folder) {		
		File  dir = new File(folder);
		//列出指定文件夹的内容
		File[] listFiles = dir.listFiles();
		for (File file : listFiles) {
			System.out.println( file.getAbsolutePath() );
		}	
	}
	//显示指定文件夹的内容
	private static void listsubDir1(String folder) {		
		File  dir = new File(folder);
		//列出指定文件夹的内容
		String[] subdirs = dir.list();
		for (String string : subdirs) {
			System.out.println( string );
		}
	}

}
```
```java
package com.wkcto.chapter06.file;

import java.io.File;
import java.io.FileInputStream;
import java.io.FileOutputStream;
/**
 * 演示文件夹操作的递归调用
 * @author 蛙课网
 *
 */
public class Test05 {

	public static void main(String[] args) {
		String folder = "d:/java1";

		// 显示指定文件夹的内容
//		listsubDir(folder);
		
		//文件夹的复制
		copyDir( folder , "d:/java22");
	}

	//创建方法, 把srcfolder文件夹的内容复制到destFolder文件夹中, 包括子文件夹的内容
	private static void copyDir(String srcFolder, String destFolder) {
		//判断目标文件夹是否存在,如果不目标文件夹不存在,需要创建一个新的文件夹
		File dest = new File(destFolder);
		if ( !dest.exists() ) {
			dest.mkdirs();
		}
		//遍历srcFolder源文件夹的内容, 复制到destFolder目录中
		File src = new File(srcFolder);
		File[] listFiles = src.listFiles();
		for (File file : listFiles) {
			if (file.isFile()) {
//				直接复制文件 , 需要先构建目标文件
				File destFile = new File(destFolder, file.getName());
				copyFile( file, destFile); 		//复制文件
			}else{
				//file是文件夹, 先在destFolder文件夹下创建一个与file同名的文件夹
				File destSubDir = new File(destFolder, file.getName() );
//				destSubDir.mkdir();
				
				//再把file文件夹的内容复制到destFoler/file目录下
				copyDir(file.getAbsolutePath(), destSubDir.getAbsolutePath());
			}
		}
		
	}
	
	//文件复制
	private static void copyFile(File srcfile, File destFile) {
		try(
				FileInputStream fis = new FileInputStream(srcfile);
				FileOutputStream fos = new FileOutputStream(destFile);
				) {
			byte [] bytes = new byte[1024];
			int len = fis.read(bytes);
			while ( len != -1){
				fos.write(bytes, 0, len);
				 len = fis.read(bytes);
			}
			
		} catch (Exception e) {
			// TODO: handle exception
		}
	}

	// 显示指定文件夹的内容, 包括子文件夹的内容
	private static void listsubDir(String folder) {
		File dir = new File(folder);
		// 列出指定文件夹的内容
		File[] listFiles = dir.listFiles();
		for (File file : listFiles) {
			System.out.println(file.getAbsolutePath());
			//判断file对象如果是文件夹, 把file子文件夹的内容也显示出来
			if (file.isDirectory() ) {
				listsubDir( file.getAbsolutePath() );  		//递归调用
			}
		}
	}

}
```
总结:
必须掌握FileInputStrea/FileOutputStream字节流实现文件的读写
掌握FileReader/FileWriter字符流实现文件的读写
理解对象序列化与反序列化
