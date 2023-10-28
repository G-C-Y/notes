## 环境搭建
```java
/*
	1、什么是注释，有什么用？
		注释是对java源代码的解释说明。
		注释可以帮程序员更好的理解程序。

	2、注释信息只保存在java源文件当中，java源文件编译生成的字节码class文件，
	这个class文件中是没有这些注释信息的。

	3、在实际的开发中，一般项目组都要求积极的编写注释。这也是一个java软件工程师
	的基本素养。

	4、注释不是写的越多越好，精简，主线清晰，每个注释都应该是点睛之笔。（以后慢慢锻炼）
*/

// 这种注释属于单行注释，只注释两个斜杠后面的

/**
* 类的注释信息
* @version 1.0
* @author bjpowernode-dujubin
* ....
*/
public class HelloWorld{ // 这是一个类，类名叫做HelloWorld
	public static void main(String[] args){
		System.out.println("Hello World");
		System.out.println("动力节点-口口相传的Java黄埔军校");
	}
}

/*
	在这里可以编写多行注释
	这是一行注释
	这是第二行注释
	这是第三行注释
*/
```

---

```java
/*
	1、在java中任何有效的代码必须写到“类体”当中，最外层必须是一个类的定义。

	2、public表示公开的，class表示定义一个类，Test是一个类名。类名后面必须是
	一对大括号，这一对大括号被称为“类体”

	3、大括号必须是成对的。并且建议都要成对编写，这样才不会丢掉。
		{}
		[]
		()

	4、什么时候代码缩进？
		我包着你，你就比我低一级。你就需要缩进。
		没有合理的缩进，代码可读性很差。
		或者也可以这样所，大括号里的都需要缩进。
		缩进就是可读性问题，不缩进也不影响程序的编译和执行。
		
*/

public class Test{ // 声明/定义一个公开的类，起个名字叫Test


	// 类体


	// 整个这一块的代码被称为：main方法（程序的入口，SUN公司java语言规定的）
	// 也就是说：JVM在执行程序的时候，会主动去找这样一个方法。没有这个规格的方法，程序是无法执行的。
	// main方法也可以叫做主方法。
	// 注意：方法必须放到“类体”中，不能放到“类体”外面。
	// 任何一个程序都要有一个入口，没有入口进不来，无法执行。
	public static void main(String[] args){ //这是一个入口方法。
		
		// 方法体
		// 注意：方法体由一行一行的“java语句”构成
		// 并且非常重要的是：任何一条java语句必须以“;”结尾，并且这个分号还得是英文的，不能用中文分号。
		// ";" 代表一条语句的结束。
		// 非常非常重要的是：方法体中的代码遵循自上而下的顺序依次逐行执行。

		System.out.println("Test1");

		// System.out.println();这行代码的作用是向控制台输出一句话。就是这个作用。
		// 注意：如果println后面小括号里的内容是一个“字符串”的话，必须使用英文双引号括起来。
		// 双引号也要成对儿写。
		System.out.println("Test2");
	}

	
	// 能再来一个一模一样的入口吗？
	// 不行，有语法错误
	/*
	public static void main(String[] args){
	
	}
	*/

	// 方法2
	// 现在不执行不代表以后不执行，以后我们可以学习其它语法让他执行。
	public static void main2(String[] args){
		System.out.println("hehe");
	}

	// 方法3

	// 方法4

}
```

---

```java
/*
D:\course\JavaProjects\02-JavaSE\chapter01>java Test2
错误: 在类 Test2 中找不到 main 方法, 请将 main 方法定义为:
   public static void main(String[] args)

以下程序可以编译通过，但是无法运行，符合语法规则。
*/
public class Test2{

}
```

---

```java
/*
没有语法错误，能够编译通过，但是不能运行，因为没有main方法。

错误: 在类 Test3 中找不到 main 方法, 请将 main 方法定义为:
   public static void main(String[] args)
*/
public class Test3{
	static void main(String[] args){
	
	}
}
```

---

```java
public class Test4{
	// 注意：args可以改名字，随意，对于主方法来说只有这个位置可以改，其它位置不能动
	public static void main(String[] fdsafdsafdsafdsa){
		System.out.println("hello world");
	}
}
```

---

```java
// 以下程序符合java语法规则吗？
// 不是不运行，是编译报错。编译过不去，运行肯定不行。

public class Test5{

	// 类体当中应该是方法，而不是直接的java语句
	// 这里可以写吗？
	System.out.println("hello1");
	
	// 主方法，入口
	public static void main(String[] args){
	
	}

	// 这里可以写吗？
	System.out.println("hello2");
}
```

---

```java
// main方法中什么也不写行吗？
// 以下程序编译和运行可以吗？

public class Test6{

	// 入口
	public static void main(String[] args){
	
	}

}
```

---

```java
// main方法中什么也不写行吗？
// 以下程序编译和运行可以吗？

//可以

public class Test6{

	// 入口
	public static void main(String[] args){
	
	}

}
```

---

```java
public class Test7{
	
	public static void main(String[] args){

		// 这个不加双引号行吗？
		// 可以，因为它是数字。
		System.out.println(100);

		// 是数字，加双引号行吗？
		System.out.println("100");

		// 以上性质一样吗？
		// 不一样：一个是字符串，一个是数字。
		// 但最终输出到控制台上一个样子，没啥区别。

		// 这里扩展一下：对于数字来说能进行加减乘除吗？
		// + 能用吗？
		// - 能用吗？
		// / 能用吗？
		// * 能用吗？
		// 可以
		System.out.println(100 + 200); // 300
		System.out.println(200 - 100); // 100
		System.out.println(200 * 100); // 20000
		System.out.println(200 / 100); // 2

	}
}
```

---


```java

/*
	1、这个内容没有为什么，只能经过测试，然后根据测试结果进行记忆。

	2、第一个结论？
		一个java源文件中可以定义多个class。
	
	3、第二个结论？
		public的类不是必须的。可以没有。

	4、第三个结论？
		在源文件中只要有一个class的定义，那么必然会对应生成一个class文件。
	
	5、第四个结论？
		public的类可以没有，但如果有的话，public修饰的类名必须和源文件名保持一致。
	
	6、第五个结论？
		public的类有也只能有1个。
*/
class A{

}

/*
	Test8.java:20: 错误: 类 B 是公共的, 应在名为 B.java 的文件中声明
	public class B{
			 ^
	1 个错误
*/
/*
public class B{

}
*/

// 如果定义public的类你只能这样写
public class Test8{
}

class C{

}

class D{

}

//错误: 类重复: Test8
/*
public class Test8{
}
*/
```

---

```java
// 编译通过了
// 能执行吗？
// 想从哪个入口进去执行，你就加载哪个类就行了！！！
// 例如：java T1
// 例如：java T2
// 例如：java T3

// 测试不代表以后就这样写，一般一个软件的执行入口是一个。不会出现多个的。
// 以下只是一个测试罢了。
class T1{
	// 想从这个入口进去执行怎么办？
	public static void main(String[] args){
		System.out.println("T1.....");
	}
}

class T2{
	// 想从这个入口进去执行怎么办？
	public static void main(String[] args){
		System.out.println("T2.....");
	}
}

class T3{
	// 想从这个入口进去执行怎么办？
	public static void main(String[] args){
		System.out.println("T3.....");
	}
}
```

---

## 标识符和关键字
```java
class T{
}

// 在123.java文件中定义public的类可以吗？
// 因为之前有一条规则是这样说的：public的类可以没有
// 但如果有public的类，也只能有1个，并且public的类的
// 名字必须和源文件名保持一致。
//public class 123 { // 但是最终尴尬了，因为123不能做标识符。是错误的标识符。
//}
```
```java

/*
	1、在java程序当中，使用EditPlus工具进行代码编写的时候，
	有一些单词是蓝色，有的是红色，有的绿色，有的是黑色，有
	的是紫色，有的是粉色....

	2、注意：在java源代码当中，在EditPlus工具中显示的高亮颜色为黑色时，
	这个单词属于标识符。

	3、标识符可以标识什么？
		可以标识：
			类名
			方法名
			变量名
			接口名
			常量名
			......
	
	4、到底什么是标识符呢？
		一句话搞定：凡是程序员自己有权利命名的单词都是标识符。
	
	5、标识符可以随意编写吗，有命名规则吗？有
		什么是命名规则？
			命名规则属于语法机制，必须遵守，不遵守命名规则标识不符合语法，
			这样，编译器会报错。

		规则1：标识符只能由数字、字母（包括中文）、下划线_、美元符号$组成，
		不能含有其它符号。

		规则2：标识符不能以数字开头

		规则3：关键字不能做标识符。例如：public class static void 这些蓝色的字体
		都是关键字，关键字是不能做标识符的。

		规则4：标识符是严格区分大小写的。大写A和小写a不一样。

		规则5：标识符理论上是没有长度限制的。
		
*/
public class BiaoShiFuTest{
	// main是一个方法的名称，属于标识符
	// 但是这个标识符不能修改，因为这个main是SUN固定死的。
	public static void main(String[] args){
	}

	//doSome是一个方法名，可以改成其他的名字
	public static void doSome(){
		// k是一个变量名
		int k = 100;
		// nianLing 是一个变量名
		int nianLing = 20;
	}
}

/*
	编译报错，错误信息是：
		错误: 需要<标识符>
		错误原因：编译器检测到class这个单词，那么编译器会从class这个
		单词后面找类名，而类名是标识符，编译器找了半天没有找到标识符，
		因为123ABC不是标识符，所以编译器提示的错误信息是：需要<标识符>

		解决办法：
			将123ABC修改为合法的标识符。
*/
class Y123ABC{
}

// 类名是标识符，标识符“中”不能有空格
/*
编译器错误信息是：
	错误: 需要'{'
	编译器检测到class，然后找class后面的标识符，编译器找到了一个合法的标识符
	叫做“Hello”，然后编译器继续往后找“{”，结果没有找到“{”，所以报错了。

	解决办法：
		办法1：是把World删除
		办法2：把空格删除
*/
/*
class Hello World{
}
*/

class Hello{
}

class HelloWorld                   {
}

class _A{
}

class _$1Aa你{
}

// 错误: 需要<标识符>
// 关键字不能做标识符
/*
class public {
}
*/

// 这个可以，因为 public1 不是关键字，可以用。
class public1 {
}

class b {
}

class B {
}


// 虽然java中的标识符严格区分大小写
// 但是对于类名来说，如果一个java源文件中同时出现了：A类和a类
// 那么谁在前就生成谁。大家以后最好不要让类名“相同”。
// 最好类名是不同的。
class HelloWorld2{
}

class helloWorld2{
}

```
```java

/*
	1、在java程序当中，使用EditPlus工具进行代码编写的时候，
	有一些单词是蓝色，有的是红色，有的绿色，有的是黑色，有
	的是紫色，有的是粉色....

	2、注意：在java源代码当中，在EditPlus工具中显示的高亮颜色为黑色时，
	这个单词属于标识符。

	3、标识符可以标识什么？
		可以标识：
			类名
			方法名
			变量名
			接口名
			常量名
			......
	
	4、到底什么是标识符呢？
		一句话搞定：凡是程序员自己有权利命名的单词都是标识符。
	
	5、标识符可以随意编写吗，有命名规则吗？有
		什么是命名规则？
			命名规则属于语法机制，必须遵守，不遵守命名规则标识不符合语法，
			这样，编译器会报错。

		规则1：标识符只能由数字、字母（包括中文）、下划线_、美元符号$组成，
		不能含有其它符号。

		规则2：标识符不能以数字开头

		规则3：关键字不能做标识符。例如：public class static void 这些蓝色的字体
		都是关键字，关键字是不能做标识符的。

		规则4：标识符是严格区分大小写的。大写A和小写a不一样。

		规则5：标识符理论上是没有长度限制的。
		
*/
public class BiaoShiFuTest{
	// main是一个方法的名称，属于标识符
	// 但是这个标识符不能修改，因为这个main是SUN固定死的。
	public static void main(String[] args){
	}

	//doSome是一个方法名，可以改成其他的名字
	public static void doSome(){
		// k是一个变量名
		int k = 100;
		// nianLing 是一个变量名
		int nianLing = 20;
	}
}

/*
	编译报错，错误信息是：
		错误: 需要<标识符>
		错误原因：编译器检测到class这个单词，那么编译器会从class这个
		单词后面找类名，而类名是标识符，编译器找了半天没有找到标识符，
		因为123ABC不是标识符，所以编译器提示的错误信息是：需要<标识符>

		解决办法：
			将123ABC修改为合法的标识符。
*/
class Y123ABC{
}

// 类名是标识符，标识符“中”不能有空格
/*
编译器错误信息是：
	错误: 需要'{'
	编译器检测到class，然后找class后面的标识符，编译器找到了一个合法的标识符
	叫做“Hello”，然后编译器继续往后找“{”，结果没有找到“{”，所以报错了。

	解决办法：
		办法1：是把World删除
		办法2：把空格删除
*/
/*
class Hello World{
}
*/

class Hello{
}

class HelloWorld                   {
}

class _A{
}

class _$1Aa你{
}

// 错误: 需要<标识符>
// 关键字不能做标识符
/*
class public {
}
*/

// 这个可以，因为 public1 不是关键字，可以用。
class public1 {
}

class b {
}

class B {
}


// 虽然java中的标识符严格区分大小写
// 但是对于类名来说，如果一个java源文件中同时出现了：A类和a类
// 那么谁在前就生成谁。大家以后最好不要让类名“相同”。
// 最好类名是不同的。
class HelloWorld2{
}

class helloWorld2{
}

```
```java

	题目：
		创建一个java文件，起名 123.java可以吗？
			可以，完全可以，在windows操作系统中文件名叫做：123.java没毛病。
		123其实并不是标识符。只是一个文件名。
		只不过在123.java文件中无法定义public的类。
	
	标识符除了命名规则之外，还有命名规范：
		1、命名规则和命名规范有什么区别？
			命名规则是语法，不遵守就会编译报错。
			命名规范只是说，大家尽量按照统一的规范来进行命名，不符合规范也行，
			代码是可以编译通过的，但是你的代码风格和大家不一样，这个通常也是
			不允许的。

			规则类似于：现实世界中的法律。
			规范类似于：现实世界中的道德。

			统一按照规范进行的话，代码的可读性很好。
			代码很容易让其它开发人员理解。

		2、具体的命名规范是哪些？

			规范1：见名知意（这个标识符在起名的时候，最好一看这个单词就知道啥意思。）

			规范2：遵循驼峰命名方式，什么是驼峰（一高一低，一高一低...）
				驼峰有利于单词与单词之间很好的进行分隔
				BiaoShiFuTest，这个很好，一眼就能看出来是4个单词。

			规范3：类名、接口名有特殊要求
				类名和接口名首字母大写，后面每个单词首字母大写。
					StudentTest、UserTest ，这是类名、接口名。

			规范4：变量名、方法名有特殊要求
				变量名和方法名首字母小写，后面每个单词首字母大写。
					nianLing（NianLing这样就不符合了。）
					mingZi（MingZi这样也不符合了。）
			
			规范5：所有“常量”名：全部大写，并且单词和单词之间采用下划线衔接。
				USER_AGE ：用户年龄
				MATH_PI：固定不变的常量3.1415926.....
*/
public class IdentifierTest{
	public static void main(String[] args){
		// 主要看两个汉语拼音，可读性很强。
		// nianLing和mingZi都是黑色字体的标识符。
		int nianLing = 20;
		String mingZi = "zhangsan";
	}
}
```
## 变量
```java
/*
	变量的第一个测试程序：Var是变量

	1、关于程序当中的数据？
		开发软件是为了解决现实世界中的问题。
		而现实世界当中，有很多问题都是使用数据进行描述的。
		所以软件执行过程中最主要就是对数据的处理。

		软件在处理数据之前需要能够表示数据，在java代码中
		怎么去表示数据呢？在java中有这样的一个概念：字面量。

		注意：在java语言中“数据”被称为“字面量”。
		10
		1.23
		true
		false
		'a'
		"abc"
		以上这些都是数据，在程序中都被叫做“字面量”。

		字面量可以分为很多种类：
			整数型字面量：1 2 3 100 -100 -20 ....
			浮点型字面量：1.3 1.2 3.14.....
			布尔型字面量：true、false没有其它值了，表示真和假,true表示真，false表示假

			字符型字面量：'a'、'b'、'中'
			字符串型字面量："abc"、"a"、"b"、"中国"

			其中字符型和字符串型都是描述了现实世界中的文字：
				需要注意的是：
					所有的字符型只能使用单引号括起来。
					所有的字符串型只能使用双引号括起来。
				
				字符型一定是单个字符才能成为“字符型”

				在语法级别上怎么区分字符型和字符串型？
					主要看是双引号还是单引号。
					单引号的一定是字符型。
					双引号的一定是字符串型。

	2、什么是变量？
		
*/
public class VarTest01{
	public static void main(String[] args){
		System.out.println(100);
		System.out.println(3.14);
		System.out.println(true);
		System.out.println(false);
		System.out.println('a');
		System.out.println('中');
		System.out.println("abc");
		System.out.println("国"); // 这不属于字符型，因为使用双引号括起来了，所以它是字符串。

		// 编译报错。ab是一个串，不是字符型，不能用单引号。
		//System.out.println('ab');

		System.out.println('好'); // 属于字符型
		System.out.println("好"); // 属于字符串型
		System.out.println("1"); //属于整数型吗？不是，是字符串。
		System.out.println("true"); // 属于布尔型吗？不是，是字符串。
		System.out.println("3.14"); // 字符串型

		System.out.println(1); // 整数型
		System.out.println(3.14); // 浮点型
		System.out.println(true); // 布尔型
		System.out.println(false); // 布尔型

		//分析一下：如果只有字面量，没有变量机制的话，有什么问题？
		// 10 是一个整数型数据，在内存中占有一定的空间（CPU 内存 硬盘）
		// 10 + 20 = 30
		// 在内存中找一块空间存储10，再找一块空间存储20，CPU负责“+”运算，算完
		// 之后的结果是30，那么这个30也会在内存当中找一块临时的空间存储起来。
		// 思考：以下的三个10在内存当中是一块空间，还是三块不同的空间呢？
		// 以下虽然都是10，但是这3个10占用三块不同的内存空间。
		System.out.println(10);
		System.out.println(10);
		System.out.println(10); // 只有“字面量”机制的话，是远远不够的，因为只有字面量内存是无法重复利用的。

		// 定义/声明一个变量，起名i
		int i = 1000;
		// 以下这5次访问都是访问的同一块内存空间。（这样使用变量之后，内存空间就得到了复用。）
		System.out.println(i);
		System.out.println(i);
		System.out.println(i);
		System.out.println(i);
		System.out.println(i);

		// 以下程序表示访问的是字符i以及字符串i，以下的这两个i和以上的i变量没有任何关系。
		System.out.println('i');
		System.out.println("i");

	}

}
```
```java
/**
* 变量测试类2
* @author 杜聚宾
* @version 1.5
* @since 1.0
*/
/*
	什么是变量？
		变量其实就是内存当中存储数据的最基本的单元。
		变量就是一个存储数据的盒子。

	在java语言当中任何数据都是有数据类型的，其中整数型是：int
		没有为什么，java中规定的，整数型就是：int
	
	当然，在java中除了数据类型int之外，还有其它的类型，例如带小数的：double等。。。

	数据类型有什么用呢？
		记住：不同的数据类型，在内存中分配的空间大小不同。
		也就是说，Java虚拟机到底给这个数据分配多大的空间，主要还是看这个变量的数据类型。
		根据不同的类型，分配不同大小的空间。
	
	对于int这种整数类型，JVM会自动给int分配4个字节大小的空间。

	1个字节=8个比特位
	1个比特位就是一个1或0. 注意：比特位是二进制位。
	int是占用多少个二进制位？1个int占有32个二进制位（bit位）

	int i = 1; 实际上在内存中是这样表示的：
		00000000 00000000 00000000 00000001
	int i = 2;
		00000000 00000000 00000000 00000010
	
	二进制位就是：满2进1位（0 1 10 11 100 101....）
	十进制位就是：满10进1位（1 2 3 4 5 6 7 8 9 10）

	对于一个变量来说，包括三要素：
		变量的数据类型
		变量的名字
		变量中保存的值

		类型+名字+值
			类型决定空间的大小。
			起个名字是为了以后方便访问。（以后在程序中访问这个数据是通过名称来访问的。）
			值是变量保存的数据。

	变量名属于标识符吗？
		变量名命名规范中是怎么说的？
			首字母小写，后面每个单词首字母大写，遵循驼峰命名方式，见名知意。
	
	变量怎么声明/定义，语法格式是什么？
		数据类型 变量名;
		例如：
			int nianLing;
	
	在java语言中有一个规定，变量必须先声明，再赋值才能访问。（没有值相当于这个空间没有开辟。）

	在java语言中怎么给一个变量赋值呢，语法格式是什么？
		记住：使用一个运算符，叫做“=”，这个运算符被称为赋值运算符。
		赋值运算符“=”的运算特点是：等号右边先执行，执行完之后赋值给左边的变量。
	
	变量可以声明的时候赋值吗？可以的。
	
*/
public class VarTest02{

	/**
	* 这是一个程序的入口
	* @param args是main方法的参数
	*/
	public static void main(String[] args){

		// 定义一个int类型的变量，起名nianLing，该变量用来存储人的年龄。
		int nianLing;
		
		// 变量声明之后，没有手动赋值，可以直接访问吗？
		// 编译报错：错误: 可能尚未初始化变量nianLing
		//System.out.println(nianLing);

		// 给变量赋值
		nianLing = 45;
		System.out.println(nianLing); // 这是访问变量。

		System.out.println("nianLing"); // 这是访问字符串。

		// 变量：可以变化的量。
		// 重新赋值
		nianLing = 80;
		System.out.println(nianLing);

		// 再次重新赋值
		nianLing = 90;
		System.out.println(nianLing);

		// 体重80kg
		int tiZhong = 80;
		System.out.println(tiZhong);
	}
}
```
```java
public class VarTest03{
	public static void main(String[] args){
		// 在这里可以访问k变量吗？
		// 注意：方法体当中的代码遵循自上而下的顺序依次逐行执行。
		// 所以以下程序编译报错。
		System.out.println(k); //错误: 找不到符号

		// 只有执行了这一行代码，k变量在内存中才会开辟空间。
		int k = 10;
	}
}
```
```java

// 重要的结论：在同一个域当中（这个域怎么理解，后面讲），变量名不能重名，不能重复声明。
// 变量可以重新赋值，但在同一个域当中，不能重复声明。
public class VarTest04{
	public static void main(String[] args){
		// 声明一个整数型的变量起名nianLing，存储值20
		int nianLing = 20;
		System.out.println(nianLing);

		// 给变量重新赋值
		nianLing = 30;
		System.out.println(nianLing);

		// 这个可以吗？不行
		// 错误信息:错误: 已在方法 main(String[])中定义了变量 nianLing
		/*
		int nianLing = 100;
		System.out.println(nianLing); 
		*/
	}
}
```
```java
// 编译报错：i变量重复定义了。（和类型没有关系。不能同名。）
public class VarTest05{
	public static void main(String[] args){

		// 整数型
		int i = 100;	

		System.out.println(i);

		// 浮点型（带小数的）
		// 错误: 已在方法 main(String[])中定义了变量 i
		double i = 1.2;

		System.out.println(i);

	}
}
```
```java
// 一行上可以同时声明多个变量吗？
// 答案：可以一行声明多个变量。
public class VarTest06{
	public static void main(String[] args){
		// 声明三个变量，都是int类型，起名a,b,c
		// 通过测试得出结论是：a,b没有赋值，c赋值100
		int a, b, c = 100;

		// 变量必须先声明，再赋值，才能访问，a,b两个变量赋值了吗？
		//错误: 可能尚未初始化变量a
		//System.out.println(a);
		//错误: 可能尚未初始化变量b
		//System.out.println(b);
		System.out.println(c);

		// 给a赋值
		a = 200;
		// 给b赋值
		b = 300;
		System.out.println(a);
		System.out.println(b);
		
	}
}
```
```java
// 一行上可以同时声明多个变量吗？
// 答案：可以一行声明多个变量。
public class VarTest06{
	public static void main(String[] args){
		// 声明三个变量，都是int类型，起名a,b,c
		// 通过测试得出结论是：a,b没有赋值，c赋值100
		int a, b, c = 100;

		// 变量必须先声明，再赋值，才能访问，a,b两个变量赋值了吗？
		//错误: 可能尚未初始化变量a
		//System.out.println(a);
		//错误: 可能尚未初始化变量b
		//System.out.println(b);
		System.out.println(c);

		// 给a赋值
		a = 200;
		// 给b赋值
		b = 300;
		System.out.println(a);
		System.out.println(b);
		
	}
}
```
```java
/*
	1、关于变量的一个分类（这个需要“死记硬背”。）
		变量根据出现的位置进行划分：
			在方法体当中声明的变量：局部变量。
			在方法体之外，类体内声明的变量：成员变量。

			重点依据是：声明的位置。

	2、注意：局部变量只在方法体当中有效，方法体执行结束该变量的内存就释放了。
*/
public class VarTest07{

	// 这里可以定义变量吗？可以的
	// 成员变量
	int i = 100;

	// 主方法
	public static void main(String[] args){
		// 局部变量
		int k = 100; // main方法结束k内存空间释放。
	}

}
```
```java

/*
	变量的作用域？
		1、什么是作用域？
			变量的有效范围。
		2、关于变量的作用域，大家可以记住一句话：
			出了大括号就不认识了。（死记这句话。）
		3、java中有一个很重要的原则：
			就近原则。（不仅java中是这样，其它编程语言都有这个原则。）
			哪个离我近，就访问哪个。
*/

public class VarTest08{

	// 成员变量
	int i = 10000;

	public static void main(String[] args){
		// 局部变量
		int i = 100; // 这个i的有效范围是main方法。
		System.out.println(i); // 这个i是多少？

		// 同一个域当中，这是不允许的。
		//int i = 90;  

		for(int n = 0; n < 10; n++){ // 这里声明的n变量只属于for域。for结束后n释放没了。
			// 这里没有编写代码。
		}

		// for循环执行结束之后，在这里访问n变量可以吗？
		//System.out.println(n);  //错误: 找不到符号

		int k; // 属于main域。
		for(k = 0; k < 10; k++){

		}
		// 能否继续访问k呢？
		System.out.println(k);
	}

	public static void x(){
		// 在这个位置上能访问i吗？
		// 错误: 找不到符号
		// System.out.println(i); // i是无法访问的。

		// 可以定义一个变量起名i吗？
		// 这个i的有效范围是x方法。
		// 局部变量
		int i = 200; // 所以这个i和main方法中的i不在同一个域当中。不冲突。
	}
}
```
## 数据类型
```java
/*
	1、在java语言中boolean类型只有两个值，没有其他值：
		true和false。
		不像C或者C++，C语言中1和0也可以表示布尔类型。

	2、boolean类型在实际开发中使用在哪里呢？
		使用在逻辑判断当中，通常放到条件的位置上（充当条件）
*/
public class BooleanTest01{
	public static void main(String[] args){
		//错误: 不兼容的类型: int无法转换为boolean
		//boolean xingBie = 1;

		// 需求规定：如果为true则表示男，为false则表示女。
		//boolean sex = true;
		boolean sex = false;

		int a = 10;
		int b = 20;
		System.out.println(a < b); // true
		System.out.println(a > b); // false

		//boolean flag = a < b;
		boolean flag = (a < b); // 运算符是有优先级的，不确定可以加小括号。加了小括号就一定是先执行的。
		System.out.println(flag); // true

		// 后面我们会学习if语句
		// if语句是一个条件语句
		// 可以实现什么功能呢？例如：如果A账户的钱充足，才可以向B账户转账。
		// 例如：如果这个布尔型值是true，则表示男性，为false则表示女性。
		if(sex){
			System.out.println("男");
		}else{
			System.out.println("女");
		}

	}
}
```
```java
/*
	字符型：
		char

		1、char占用2个字节。
		2、char的取值范围：[0-65535]
		3、char采用unicode编码方式。
		4、char类型的字面量使用单引号括起来。
		5、char可以存储一个汉字。
*/
public class CharTest01{
	public static void main(String[] args){
		// char可以存储1个汉字吗？
		// 可以的，汉字占用2个字节，java中的char类型占用2个字节，正好。
		char c1 = '中';
		System.out.println(c1);

		char c2 = 'a';
		System.out.println(c2);

		// 0如果加上单引号的话，0就不是数字0了，就是文字0，它是1个字符。
		char c3 = '0';
		System.out.println(c3);

		// 错误: 不兼容的类型: String无法转换为char
		//char c4 = "a";

		// 错误: 未结束的字符文字    两个字符为字符串
		//char c5 = 'ab';

		// 错误: 未结束的字符文字    为字符串
		//char c6 = '1.08';

	}
}
```
```java
/*
	关于java中的转义字符
		java语言中“\”负责转义。
			\t 表示制表符tab
*/
public class CharTest02{
	public static void main(String[] args){

		// 普通的't'字符
		char c1 = 't';
		System.out.println(c1);
		
		//char x = 'ab';

		// 根据之前所学，以下代码应该报错。
		// 经过测试以下代码 \t 实际上是1个字符，不属于字符串
		// 两个字符合在一起表示一个字符，其中 \t 表示“制表符tab”
		char c2 = '\t'; //相当于键盘上的tab键

		System.out.println("abcdef");
		System.out.println("abctdef");
		// \的出现会将紧挨着的后面的字符进行转义。\碰到t表示tab键。
		System.out.println("abc\tdef");
		
		/*
			System.out.println(); 换行
			System.out.print(); 不换行
		*/
		System.out.print("HelloWorld");
		System.out.println("123abcdef");

		System.out.print("abc");
		//char c3 = 'n'; // 普通的n字符
		char c3 = '\n'; // 换行符
		//System.out.print(c3);
		System.out.println(c3);
		System.out.println("def"); 

		// 假设现在想在控制台输出一个 ' 字符怎么办？
		// 错误: 空字符文字
		//System.out.println(''');
		// \' 表示一个普通不能再普通的单引号字符。（\'联合起来表示一个普通的 '）
		System.out.println('\'');

		// 假设现在想在控制台输出一个 \ 字符怎么办？
		//错误: 未结束的字符文字
		//System.out.println('\');
		// 在java中两个反斜杠代表了一个“普通的反斜杠字符”
		System.out.println('\\');

		// 双引号括起来的是字符串
		System.out.println("test");
		// 希望输出的结果是："test"
		// 错误: 需要')'
		//System.out.println(""test"");
		System.out.println("“test”"); //内部的双引号我用中文的行吗？可以。

		System.out.println("");
		// 编译报错。
		//System.out.println(""");
		//System.out.println("\"");
		System.out.println("\"test\"");

		// 这个可以输出吗？
		// 这个不需要专门进行转义。
		// 这个 ' 在这里只是一个普通的字符，不具备特殊含义。
		System.out.println("'");

		//以下都有问题
		//System.out.println(''');
		//System.out.println(""");

		// 可以的。
		System.out.println("'这样呢'");

		// 编译报错，因为：4e2d 是一个字符串
		// 错误: 未结束的字符文字
		//char x = '4e2d';

		// 反斜杠u表示后面的是一个字符的unicode编码。
		// unicode编码是十六进制的。
		char x = '\u4e2d';
		System.out.println(x); // '中'
	}
} 
/*
十六进制，满16进1位：
	1 2 3 4 5 6 7 8 9 a b c d e f 10
	11 12 13 14 15 16 17 18 19 1a 1b 1c 1d 1e 1f 20...

八进制：
	0 1 2 3 4 5 6 7 10 11 12 13 14 15 16 17 20.....
*/
```
```java
/*
	1、整数能否直接赋值给char
	2、char x = 97;
		这个java语句是允许的，并且输出的结果是'a'
		经过这个测试得出两个结论：
			第一个结论：当一个整数赋值给char类型变量的时候，会自动转换成char字符型，
			最终的结果是一个字符。

			第二个结论：当一个整数没有超出byte short char的取值范围的时候，
			这个整数可以直接赋值给byte short char类型的变量。
*/
public class CharTest03{
	public static void main(String[] args){
	
		char c1 = 'a';
		System.out.println(c1);

		// 这里会做类型转换吗？
		// 97是int类型（这是java中规定，默认当做int处理）
		// c2是char类型
		//char c2 = (char)97; // 不需要这样做。
		char c2 = 97;
		System.out.println(c2); // 'a'

		// char类型取值范围：[0~65535]
		char c3 = 65535; // 实际上最终是一个“看不懂”的字符。
		System.out.println(c3);

		//错误: 不兼容的类型: 从int转换到char可能会有损失
		//char c4 = 65536;

		// 怎么解决以上问题？
		char c4 = (char)65536;

		byte x = 1;
		short s = 1;
		char c = 1;

	}
}
```
```java
/*
	关于java语言中的浮点型数据
		浮点型包括：
			float			4个字节
			double		8个字节
		
		float是单精度
		double是双精度

		double更精确

		比如说：
			10.0 / 3 如果采用float来存储的话结果可能是：3.33333
			10.0 / 3 如果采用double来存储的话结果可能是：3.3333333333333
		
		但是需要注意的是，如果用在银行方面或者说使用在财务方面，double
		也是远远不够的，在java中提供了一种精度更高的类型，这种类型专门
		使用在财务软件方面：java.math.BigDecimal （不是基本数据类型，属于
		引用数据类型。）
	
		float和double存储数据的时候都是存储的近似值。
		为什么？
			因为现实世界中有这种无线循环的数据，例如：3.3333333333333....
			数据实际上是无限循环，但是计算机的内存有限，用一个有限的资源
			表示无限的数据，只能存储近似值。
		
		long类型占用8个字节。
		float类型占用4个字节。
		哪个容量大？
			注意：任意一个浮点型都比整数型空间大。
			float容量 > long容量。
	
	java中规定，任何一个浮点型数据默认被当做double来处理。
	如果想让这个浮点型字面量被当做float类型来处理，那么
	请在字面量后面添加F/f。
		1.0 那么1.0默认被当做double类型处理。
		1.0F 这才是float类型。（1.0f）
*/
public class FloatTest01{
	public static void main(String[] args){

		// 这个不存在类型转换
		// 3.1415926是double类型
		// pi是double类型
		double pi = 3.1415926;
		System.out.println(pi);

		// 这个可以吗？
		//错误: 不兼容的类型: 从double转换到float可能会有损失
		//float f = 3.14;

		// 怎么修改以上的代码呢？
		// 第一种方式:在字面量后面添加F/f
		//float f = 3.14f;
		//float f = 3.14F;

		// 第二种方式：强制类型转换，但可能损失精度。谨慎使用。
		float f = (float)3.14;
		System.out.println(f);

		// 分析这个程序，可以编译通过吗？
		// 错误: 不兼容的类型: 从double转换到int可能会有损失
		// 原理：先将5转换成double类型，然后再做运算，结果是double
		// 大容量无法直接赋值给小容量，需要强转。
		//int i = 10.0 / 5;

		// 怎么修改
		int i = (int)10.0 / 5;
		System.out.println(i); // 2

		// 可以这样修改吗？强转的时候只留下整数位。
		int x = (int)(10.0 / 5);
		System.out.println(x); // 2
	}
}
```
```java

/*
	整数型在java语言中共4种类型：
		byte	1个字节  最大值127
		short	2个字节  最大值32767
		int	4个字节  2147483647是int最大值，超了这个范围可以使用long类型。
		long	8个字节

		1个字节 = 8个二进制位
		1byte = 8bit

		对于以上的四个类型来说，最常用的是int。
		开发的时候不用斤斤计较，直接选择使用int就行了。
	
	在java语言中整数型字面量有4种表示形式：
		十进制：最常用的。
		二进制
		八进制
		十六进制
*/
public class IntTest01{
	public static void main(String[] args){
		// 十进制
		int a = 10; 
		System.out.println(a); // 10

		// 八进制
		int b = 010;
		System.out.println(b); // 8

		// 十六进制
		int c = 0x10;
		System.out.println(c); // 16

		int x = 16; //十进制方式
		System.out.println(x);

		// 二进制（JDK8的新特性，低版本不支持。）
		int d = 0b10;
		System.out.println(d); // 2
	}
}
```
```java
/*
	在java中有一条非常重要的结论，必须记住：
		在任何情况下，整数型的“字面量/数据”默认被当做int类型处理。（记住就行）
		如果希望该“整数型字面量”被当做long类型来处理，需要在“字面量”后面添加L/l
		建议使用大写L，因为小写l和1傻傻分不清。
*/
public class IntTest02{
	public static void main(String[] args){

		// 分析这个代码存在类型转换吗，以下代码什么意思？
		// 不存在类型转换
		// 100 这个字面量被当做int类型处理
		// a变量是int类型，所以不存在类型的转换。
		// int类型的字面量赋值给int类型的变量。
		int a = 100;
		System.out.println(a);

		// 分析这个程序是否存在类型转换？
		// 分析：200这个字面量默认被当做int类型来处理
		// b变量是long类型，int类型占4个字节，long类型占8个字节
		// 小容量可以自动转换成大容量，这种操作被称为：自动类型转换。
		long b = 200;
		System.out.println(b);

		// 分析这个是否存在类型转换？
		// 这个不存在类型转换。
		// 在整数型字面量300后面添加一个L之后，300L联合起来就是一个long类型的字面量
		// c变量是long类型，long类型赋值给long类型不存在类型转换。
		long c = 300L;
		System.out.println(c);

		// 题目：
		// 可以吗？存在类型转换吗？
		// 2147483647默认被当做int来处理
		// d变量是long类型，小容量可以自动赋值给大容量，自动类型转换
		long d = 2147483647; // 2147483647是int最大值。
		System.out.println(d);

		// 编译器会报错吗？为什么？
		// 在java中，整数型字面量一上来编译器就会将它看做int类型
		// 而2147483648已经超出了int的范围，所以在没有赋值之前就出错了。
		// 记住，不是e放不下2147483648，e是long类型，完全可以容纳2147483648
		// 只不过2147483648本身已经超出了int范围。
		// 错误: 整数太大
		//long e = 2147483648;

		// 怎么解决这个问题呢？
		long e = 2147483648L;
		System.out.println(e);

	}
}
```
```java

/*
	1、小容量可以直接赋值给大容量，称为自动类型转换。

	2、大容量不能直接赋值给小容量，需要使用强制类型转换符进行强转。
	但需要注意的是：加强制类型转换符之后，虽然编译通过了，但是运行
	的时候可能会损失精度。
*/
public class IntTest03{
	public static void main(String[] args){
		
		// 不存在类型转换
		// 100L是long类型字面量，x是long类型字面量。
		long x = 100L;

		// x是long类型，占用8个字节，而y变量是int类型，占用4个字节
		// 在java语言中，大容量可以“直接”赋值给小容量吗？不允许，没有这种语法。
		// 编译错误信息：错误: 不兼容的类型: 从long转换到int可能会有损失
		//int y = x;

		// 大容量转换成小容量，要想编译通过，必须加强制类型转换符，进行强制类型转换。
		// 底层是怎么进行强制类型转换的呢？
		// long类型100L：00000000 00000000 00000000 00000000 00000000 00000000 00000000 01100100
		// 以上的long类型100L强转为int类型，会自动将“前面”的4个字节砍掉：00000000 00000000 00000000 01100100
		int y = (int)x; // 这个(int)就是强制类型转换符，加上去就能编译通过。
							 // 但是要记住：编译虽然过了，但是运行时可能损失精度。
		System.out.println(y); // 100


		// 定义变量a int类型，赋值100
		int a = 100;
		System.out.println(a);

		int b = a; // 将变量a中保存的值100复制一份给b变量。
		System.out.println(b);

	}
}
```
```java
/*
	java中有一个语法规则：
		当这个整数型字面量没有超出byte的取值范围，那么这个
		整数型字面量可以直接赋值给byte类型的变量。
	
	这种语法机制是为了方便写代码，而存在的。
*/
public class IntTest04{
	public static void main(String[] args){
		// 分析：以下代码编译可以通过吗？
		// 300 被默认当做int类型
		// b变量是byte类型
		// 大容量转换成小容量，要想编译通过，必须使用强制类型转换符
		// 错误: 不兼容的类型: 从int转换到byte可能会有损失
		//byte b = 300;

		// 要想让以上的程序编译通过，必须加强制类型转换符
		// 虽然编译通过了，但是可能精度损失。
		// 300这个int类型对应的二进制：00000000 00000000 00000001 00101100
		// byte占用1个字节，砍掉前3个字节，结果是：00101100 (44)
		byte b = (byte)300;
		System.out.println(b); // 44

		// 这个编译能通过吗？
		// 1是int类型，默认被当做int类型来看。
		// x是byte类型，1个字节，大容量无法直接转换成小容量。
		// 按说是编译报错的。
		byte x = 1;
		byte y = 127;
		// 错误: 不兼容的类型: 从int转换到byte可能会有损失
		byte z = 128;

		// 当整数型字面量没有超出short类型取值范围的时候，该字面量可以直接赋值给short
		// 类型的变量。
		short s = 1;
		short s1 = 32767;
		// 错误: 不兼容的类型: 从int转换到short可能会有损失
		//short s2 = 32768;
		System.out.println(s);

	}
}
```
```java
/*
	1、计算机在任何情况下都只能识别二进制
	2、计算机在底层存储数据的时候，一律存储的是“二进制的补码形式”
		计算机采用补码形式存储数据的原因是：补码形式效率最高。
	3、什么是补码呢？
		实际上是这样的，二进制有：原码 反码 补码 
	4、记住：
		对于一个正数来说：二进制原码、反码、补码是同一个，完全相同。
			int i = 1;
			对应的二进制原码：00000000 00000000 00000000 00000001
			对应的二进制反码：00000000 00000000 00000000 00000001
			对应的二进制补码：00000000 00000000 00000000 00000001
		对于一个负数来说：二进制原码、反码、补码是什么关系呢？
			byte i = -1;
			对应的二进制原码：10000001
			对应的二进制反码（符号位不变，其它位取反）：11111110
			对应的二进制补码（反码+1）：11111111
	5、分析 byte b = (byte)150;
		这个b是多少？
			int类型的4个字节的150的二进制码是什么？
				00000000 00000000 00000000 10010110
			将以上的int类型强制类型转为1个字节的byte，最终在计算机中的二进制码是：
				10010110
		
		千万要注意：计算机永远存储的都是二进制补码形式。也就是说上面
		10010110 这个是一个二进制补码形式，你可以采用逆推导的方式推算出
		这个二进制补码对应的原码是啥！！！！！！
			10010110 ---> 二进制补码形式
			10010101 ---> 二进制反码形式
			11101010 ---> 二进制原码形式 
*/
public class IntTest05{
	public static void main(String[] args){

		// 编译报错：因为150已经超出了byte取值范围，不能直接赋值，需要强转
		//byte b = 150;
		byte b = (byte)150;

		// 这个结果会输出多少呢？
		System.out.println(b); // -106
	}
}
```
```java
public class IntTest05{
	public static void main(String[] args){

		// 编译报错：因为150已经超出了byte取值范围，不能直接赋值，需要强转
		//byte b = 150;
		byte b = (byte)150;

		// 这个结果会输出多少呢？
		System.out.println(b); // -106
	}
}
```
```java
/*
	结论：byte、char、short做混合运算的时候，各自先转换成int再做运算。
*/
public class IntTest06{
	public static void main(String[] args){

		char c1 = 'a';
		byte b = 1;

		// 注意：这里的"+"是负责求和的
		System.out.println(c1 + b); // 98

		// 错误: 不兼容的类型: 从int转换到short可能会有损失
		//short s = c1 + b; // 编译器不知道这个加法最后的结果是多少。只知道是int类型。

		// 这样修改行吗？
		//错误: 不兼容的类型: 从int转换到short可能会有损失
		//short s = (short)c1 + b;

		short s = (short)(c1 + b);

		//short k = 98;

		int a = 1;
		//错误: 不兼容的类型: 从int转换到short可能会有损失
		// short x = 1; 可以
		short x = a; // 不可以，编译器只知道a是int类型，不知道a中存储的是哪个值。
		System.out.println(x);
	}
}
```
```java
/*
	结论：多种数据类型做混合运算的时候，最终的结果类型是“最大容量”对应的类型。

	char+short+byte 这个除外。
	因为char + short + byte混合运算的时候，会各自先转换成int再做运算。
*/
public class IntTest07{
	public static void main(String[] args){
		
		long a = 10L;
		char c = 'a';
		short s = 100;
		int i = 30;

		// 求和
		System.out.println(a + c + s + i); //237

		// 错误: 不兼容的类型: 从long转换到int可能会有损失
		// 计算结果是long类型
		//int x = a + c + s + i;

		int x = (int)(a + c + s + i);
		System.out.println(x);

		// 以下程序执行结果是？
		// java中规定，int类型和int类型最终的结果还是int类型。
		int temp = 10 / 3; // / 是除号。（最终取整）
		System.out.println(temp); // 3.33333吗？结果是：3

		// 在java中计算结果不一定是精确的。
		int temp2 = 1 / 2;
		System.out.println(temp2); // 0

	}
}
```
```java
public class TypeTransferTest{
	public static void main(String[] args){
		// 编译报错，因为1000已经超出范围了。
		//byte b1 = 1000;
		// 可以
		byte b2 = 20;
		// 可以
		short s = 1000;
		// 可以
		int c = 1000;
		// 可以
		long d = c;
		// 编译报错
		//int e = d;
		// 可以
		int f = 10 / 3;
		// 可以
		long g = 10;
		// 编译报错
		//int h = g / 3;
		// 可以
		long m = g / 3;
		// 编译报错
		//byte x = (byte)g / 3;
		// 可以
		short y = (short)(g / 3);
		// 可以
		short i = 10;
		// 可以
		byte j = 5;
		// 编译报错
		//short k = i + j;
		// 可以
		int n = i + j;
		// 可以
		char cc = 'a';
		System.out.println(cc); // a
		System.out.println((byte)cc); // 97
		// cc 会先自动转换成int类型，再做运算
		int o = cc + 100;
		System.out.println(o); // 197
	}
}
```
## 运算符
```java

// 大家讨论最多的一个问题。
// 如果只是针对于面试题的话，建议死记硬背。
public class Homework01{
	public static void main(String[] args){
		int i = 10;
		i = i++;
		// 大部分同学都会认为这个i一定是11
		// 这个i变量最终的结果是10（惊讶）
		// 首先，第一点：这种代码以后不会有人写。
		// 其次：第二点：没必要讨论这个问题，因为在C++中运行结果确实是11.
		// java中运行结果是10
		// c++中运行结果是11
		// 为什么？因为java和c++的编译器是不同的人开发的。原理不同。
		System.out.println(i);
		
		// 在java语言中i++，这种表达式在执行的时候，会提前先将i变量找一个临时
		// 变量存储一下。(C++中并没有这样做。)
		/*
		int k = 10;
		k = k++;
		*/
		int k = 10;
		// k = k++;对应的是下面三行代码
		int temp = k;
		k++;
		k = temp;
		System.out.println(k);
	}
}
```
```java
public class Homework02{
	public static void main(String[] args){
		int x = 10;
		int a = x + x++; // 该行代码只要结束，x就是11
		System.out.println("a =" + a); // 20 （x走到这里就变成11了）
		System.out.println("x =" + x); // 11
		int b = x + ++x; // 23 该行代码结束之后，x就是12
		System.out.println("b =" + b); // 23
		System.out.println("x =" + x); // 12
		int c = x + x--; // 该行代码执行结束之后，x就是11
		System.out.println("c =" + c); // 24
		System.out.println("x =" + x); // 11
		int d = x + --x; // 该行代码只要执行结束，x就是10了。
		System.out.println("d =" + d); // 21
		System.out.println("x =" + x); // 10
	}
}
```
```java

/*
	+ 运算符：
		1、+ 运算符在java语言中有两个作用。
			作用1：求和
			作用2：字符串拼接

		2、什么时候求和？什么时候进行字符串的拼接呢？
			当 + 运算符两边都是数字类型的时候，求和。
			当 + 运算符两边的“任意一边”是字符串类型，那么这个+会进行字符串拼接操作。

		3、一定要记住：字符串拼接完之后的结果还是一个字符串。
*/
public class OperatorTest06{

	public static void main(String[] args){

		// 定义一个年龄的变量。
		int nianLing = 35;

		// + 在这里会进行字符串的拼接操作。
		System.out.println("年龄=" + nianLing); // "年龄=35"

		int a = 100;
		int b = 200;
		// 这里的 + 两边都是数字，所以加法运算
		int c = a + b;
		System.out.println(c); // 300

		// 注意：当一个表达式当中有多个加号的时候
		// 遵循“自左向右”的顺序依次执行。（除非额外添加了小括号，小括号的优先级高）
		// 第一个+先运算，由于第一个+左右两边都是数字，所以会进行求和。
		// 求和之后结果是300，代码就变成了：System.out.println(300 + "110");
		// 那么这个时候，由于+的右边是字符串"110"，所以此时的+会进行字符串拼接。
		System.out.println(a + b + "110"); // 最后一定是一个字符串："300110"

		// 先执行小括号当中的程序：b + "110"，这里的+会进行字符串的拼接，
		// 拼接之后的结果是："200110"，这个结果是一个字符串类型。
		// 代码就变成了：System.out.println(a + "200110");
		// 这个时候的+还是进行字符串的拼接。最终结果是："100200110"
		System.out.println(a + (b + "110"));

		// 在控制台上输出"100+200=300"
		System.out.println("100+200=300"); // 不是这个意思。

		// 以下有效的运算符加号一共有4个，这4个加号都是字符串拼接操作。
		System.out.println(a + "+" + b + "=" + c);
		
		// 分析这个结果是多少？
		// 以下表达式中没有小括号，所以遵循自左向右的顺序依次执行。
		// 第1,2,3,4个加号都是进行字符串拼接，拼接之后的结果是："100+200=100"
		// 前4个加号运行之后是一个字符串"100+200=100"
		// 然后这个字符串再和最后一个b变量进行字符串的拼接："100+200=100200"
		System.out.println(a + "+" + b + "=" + a + b);

		// 和上面程序不一样的地方是：最后一个加号先执行，并且会先进行求和运算。
		System.out.println(a + "+" + b + "=" + (a + b));

		// 在java语言中怎么定义字符串类型的变量呢？
		// int是整数型 i 是变量名 10是字面量
		//int i = 10;
		// String是字符串类型，并且String类型不属于基本数据类型范畴，属于引用类型。
		// name是变量名，只要是合法的标识符就行。
		// "jack" 是一个字符串型字面量。
		String name = "李四"; // String类型是字符串类型，其中S是大写，不是：string

		// 错误：类型不兼容。
		//String name = 100;

		// 会进行字符串的拼接
		//System.out.println("登录成功欢迎" + name + "回来");
		
		
		// 口诀：加一个双引号""，然后双引号之间加两个加号："++"，然后两个加号中间加变量名："+name+"
		System.out.println("登录成功欢迎"+name+"回来");

		System.out.println(a + "+" + b + "=" + c);

	}
}
```
```java
/*
1、输出信息到控制台：
	System.out.println(...);
2、在java中怎么接收键盘的输入呢？
	先声明一下，这个代码看不懂很正常，因为这个代码是面向对象章节学习之后才能够理解。
	这个代码以后复制粘贴就行。

	前提：java.util.Scanner s = new java.util.Scanner(System.in); 
	接收一个整数怎么办？
		int num = s.nextInt();
		
	接收一个字符串怎么办？
		String str = s.next();
*/
public class KeyInput{
	public static void main(String[] args){

		// 创建一个键盘扫描器对象
		// s 变量名，可以修改。其它不能改。 
		java.util.Scanner s = new java.util.Scanner(System.in); //这行代码写一次就行了。

		// 接收用户的输入，从键盘上接收一个int类型的数据
		// 解释这行代码，尽量让大家明白：代码执行到这里的时候，会暂停下来
		// 等待用户的输入，用户可以从键盘上输入一个整数，然后回车，回车之后
		// i变量就有值了。并且i变量中保存的这个值是用户输入的数字。
		// i变量就是接收键盘数据的。
		int i = s.nextInt(); // i是变量名，s是上面的变量名
		System.out.println("您输入的数字是：" + i);

		// 代码执行到此处又会停下来，等待用户的输入。
		// 敲完回车，s.nextInt();代码执行结束。
		int j = s.nextInt();
		System.out.println("您输入的数字是：" + j);

		// 如果输入的不是数字，那么会出异常：InputMismatchException
		int m = s.nextInt();
		System.out.println("您输入的数字是：" + m);

		// 我怎么从键盘上接收一个字符串呢？
		// 程序执行到此处会停下来，等待用户的输入，用户可以输入字符串。
		String str = s.next();
		System.out.println("您输入了：" + str);

		// 完整的。
		System.out.print("请输入用户名：");
		String name = s.next();
		System.out.println("欢迎"+name+"回来");
	}
}
```
```java
import java.util.Scanner;

// 更有交互性
public class KeyInput2{
	public static void main(String[] args){
		// 创建键盘扫描器对象
		Scanner s = new Scanner(System.in);
		// 输出一个欢迎信息
		System.out.println("欢迎使用小型迷你计算器");
		System.out.print("请输入第1个数字：");
		int num1 = s.nextInt();
		System.out.print("请输入第2个数字：");
		int num2 = s.nextInt();
		System.out.println(num1 + "+" + num2 + "=" + (num1 + num2));
	}
}
```
```java
/*
	算术运算符：
		+	求和
		-	相减
		*  乘积
		/  商
		%  求余数（求模）

		++ 自加1
		-- 自减1
	
	对于++运算符来说：
		可以出现在变量前，也可以出现在变量后。
		不管出现在变量前还是后，总之++执行结束之后，变量的值一定会自加1。
	
*/
public class OperatorTest01{
	public static void main(String[] rags){
		int a = 10;
		int b = 3;
		System.out.println(a + b); // 13
		System.out.println(a - b); // 7
		System.out.println(a * b); // 30
		System.out.println(a / b); // 3
		System.out.println(a % b); // 1

		// 重点掌握 ++ 和 --
		// 这里重点讲解 ++，至于-- 大家可以照葫芦画瓢。
		// ++ 自加1（++可以出现在变量前，也可以出现在变量后。）
		int i = 10;

		// i变量自加1
		i++;

		System.out.println(i); //11

		int k = 10;
		// k变量自加1
		++k;
		System.out.println(k); //11

		// 研究：++出现在变量前和变量后有什么区别？
		// 先看++出现在变量后。
		// 语法：当++出现在变量后，会先做赋值运算，再自加1
		int m = 20;
		int n = m++;
		System.out.println(n); // 20
		System.out.println(m); // 21

		// ++出现在变量前呢？
		// 语法规则：当++出现在变量前的时候，会先进行自加1的运算，然后再赋值。
		int x = 100;
		int y = ++x;
		System.out.println(x); // 101
		System.out.println(y); // 101

		// 题目
		int c = 90;
		System.out.println(c++);  // 传，这个“传”在这里有一个隐形的赋值运算。90
		// 把上面代码拆解开
		//int temp = c++;
		//System.out.println(temp);

		System.out.println(c); // 91

		int d = 80;
		System.out.println(++d); //81
		// 拆解
		//int temp2 = ++d;
		//System.out.println(temp2);

		System.out.println(d); // 81

		/*
		int e = 1;
		int f = e; // e赋值给f，表示将e“传”给了f
		*/

		// 自己测试以下 -- 运算符。

	}
}
```
```java

/*
	关系运算符：
		>
		>=
		<
		<=
		==
		!=

		一定要记住一个规则：
			所有的关系运算符的运算结果都是布尔类型，
			不是true就是false，不可能是其他值。
		
		在java语言中:
			= ： 赋值运算符
			== ：关系运算符，判断是否相等。
		
		注意：关系运算符中如果有两个符号的话，两个符号之间不能有空格。
			>= 这是对的, > = 这是不对的。
			== 这是对的，= = 这是不对的。
*/
public class OperatorTest02{
	public static void main(String[] args){
		int a = 10;
		int b = 10;
		System.out.println(a > b); // false
		System.out.println(a >= b); // true
		System.out.println(a < b); // false
		System.out.println(a <= b); // true
		System.out.println(a == b); // true
		System.out.println(a != b); // false
	}
}
```
```java

/*
	逻辑运算符：
		&	逻辑与（可以翻译成并且）
		|	逻辑或（可以翻译成或者）
		!	逻辑非（取反）
		&&	短路与
		||	短路或
	
	用普通话描述的话：100 大于 99 并且 100 大于 98 ，有道理
	用代码描述的话：100 > 99 & 100 > 98 --> true

	true & true --> true

	非常重要：
		逻辑运算符两边要求都是布尔类型，并且最终的运算结果也是布尔类型。
		这是逻辑运算符的特点。
	
	100 & true 不行，语法错误。
	100 & 200 不行，没有这种语法。
	true & false 这样可以。

	100 > 90 & 100 > 101 --> false

	& 两边都是true，结果才是true
	| 有一边是true，结果就是true

*/	
public class OperatorTest03{
	public static void main(String[] args){
		// 对于逻辑与&运算符来说，只要有一边是false，结果就是false。
		// 只有两边同时为true，结果才是true。
		System.out.println(true & true); // true
		System.out.println(true & false); // false
		System.out.println(false & false); // false

		System.out.println(100 > 90 & 100 > 101); // false
		System.out.println((100 > 90) & (100 > 101)); // false

		int a = 100;
		int b = 101;
		int c = 90;
		System.out.println(a < b & a > c); // true

		// 对于逻辑或呢？
		// 只要有一边是true，结果就是true。
		System.out.println(a < b | c > b); // true
		System.out.println(true | false); // true

		System.out.println(true | true); // true
		System.out.println(false | false); // false

		System.out.println(!false); // true
		System.out.println(!true); // false

		// 注意：这里需要加一个小括号。
		System.out.println(!(a > b)); // true

		/*
			关于短路与 &&，短路或 ||
			其中重点学习短路与，短路或照葫芦画瓢。

			短路与&& 和 逻辑与 &有什么区别？
				首先这两个运算符的运算结果没有任何区别，完全相同。
				只不过“短路与&&”会发生短路现象。

			什么是短路现象呢？
				右边表达式不执行，这种现象叫做短路现象。

			什么时候使用&&，什么时候使用& ？
				从效率方面来说，&&比&的效率高一些。
				因为逻辑与&不管第一个表达式结果是什么，第二个表达式一定会执行。

				以后的开发中，短路与&&和逻辑与还是需要同时并存的。
					大部分情况下都建议使用短路与&&
					只有当既需要左边表达式执行，又需要右边表达式执行的时候，才会
					选择逻辑与&。
		*/

		System.out.println(true & true); // true
		System.out.println(true & false); // false
		System.out.println(false & false); // false

		System.out.println(true && true); // true
		System.out.println(true && false); // false
		System.out.println(false && false); // false

		// 接下来需要理解一下什么是短路现象，什么时候会发生“短路”。
		int x = 10;
		int y = 11;
		// 逻辑与&什么时候结果为true（两边都是true，结果才是true）
		// 左边的 x>y 表达式结果已经是false了，其实整个表达式的结
		// 果已经确定是false了，按道理来说右边的表达式不应该执行。
		System.out.println(x > y & x > y++); 

		// 通过这个测试得出：x > y++ 这个表达式执行了。
		System.out.println(y); // 12

		//测试短路与&&
		int m = 10;
		int n = 11;
		// 使用短路与&&的时候，当左边的表达式为false的时候，右边的表达式不执行
		// 这种现象被称为短路。
		System.out.println(m > n && m > n++);
		System.out.println(n); // 11

		// 问题：什么时候发生短路或现象？
		// || 短路或
		// “或”的时候只要有一边是true，结果就是true。
		// 所以，当左边的表达式结果是true的时候，右边的表达式不需要执行，此时会短路。

	}
}
```
```java

/*
	赋值运算符：
		1、赋值运算符包括“基本赋值运算符”和“扩展赋值运算符”：基本的、扩展的。
		2、基本赋值运算符？
			=
		3、扩展的赋值运算符？
			+=
			-=
			*=
			/=
			%=
			注意：扩展赋值运算符在编写的时候，两个符号之间不能有空格。
				+ =  错误的。
				+= 正确的。
		4、很重要的语法机制：
			使用扩展赋值运算符的时候，永远都不会改变运算结果类型。
			byte x = 100;
			x += 1;
			x自诞生以来是byte类型，那么x变量的类型永远都是byte。不会变。
			不管后面是多大的数字。
*/
public class OperatorTest04{
	public static void main(String[] args){

		// 赋值运算符“=”右边优先级比较高，先执行右边的表达式
		// 然后将表达式执行结束的结果放到左边的“盒子”当中。（赋值）
		int i = 10;
		// 重新赋值
		i = 20;

		byte b = 10;
		b = 20;

		/*
			以 += 运算符作为代表，学习扩展赋值运算符。
			其它的运算符，例如：-= *= /= %= 和 += 原理相似。
		*/
		int k = 10;
		k += 20; // k变量追加20
		System.out.println(k); // 30

		int m = 10;
		// += 运算符类似于下面的表达式
		m = m + 20;
		System.out.println(m); // 30

		// 研究：
		// i += 10 和 i = i + 10 真的是完全一样吗？
		// 答案：不一样，只能说相似，其实本质上并不是完全相同。
		byte x = 100; // 100没有超出byte类型取值范围，可以直接赋值
		System.out.println(x); // 100

		// 分析：这个代码是否能够编译通过？
		// 错误: 不兼容的类型: 从int转换到byte可能会有损失
		//x = x + 1; // 编译器检测到x + 1是int类型，int类型可以直接赋值给byte类型的变量x吗？

		// 使用扩展赋值运算符可以吗？
		// 可以的，所以得出结论：x += 1 和 x = x + 1不一样。
		// 其实 x += 1 等同于：x = (byte)(x + 1);
		x += 1;
		System.out.println(x); // 101

		// 早就超出byte的取值范围了。
		x += 199; // x = (byte)(x + 199);
		System.out.println(x); // 44 （当然会自动损失精度了。）

		int y = 100;
		y += 100;
		System.out.println(y); // 200

		y -= 100; // x = x - 100;
		System.out.println(y); // 100

		y *= 10; // x = x * 10;
		System.out.println(y); // 1000

		y /= 30; // x = x / 30;
		System.out.println(y); // 33

		y %= 10; // x = x % 10;
		System.out.println(y); // 3
		
	}
}
```
```java

/*
	条件运算符：（三目运算符。）
		语法格式：
			布尔表达式 ? 表达式1 : 表达式2

		执行原理是什么？
			布尔表达式的结果为true时，表达式1的执行结果作为整个表达式的结果。
			布尔表达式的结果为false时，表达式2的执行结果作为整个表达式的结果。
*/
public class OperatorTest05{
	public static void main(String[] args){

		// 合法的java语句
		// 表示声明一个变量，起名i
		int i = 100;

		// 这里会编译出错吗？
		// 错误: 不是语句
		// 100;

		// 错误: 不是语句
		//'男';

		boolean sex = true;
		
		// 分析以下代码是否存在语法错误？
		// 错误: 不是语句
		//sex ? '男' : '女';

		// 前面的变量的c的类型不能随意编写。
		// 最终的计算结果是字符型，所以变量也需要使用char类型。
		char c = sex ? '男' : '女';
		System.out.println(c);

		// 实际开发中不会这样，故意的
		//错误: 不兼容的类型: 条件表达式中的类型错误
		//char x = sex ? '男' : "女";
		//System.out.println(x);

		// 这样可以吗？可以
		sex = false;
		System.out.println(sex ? '男' : "女");

		//System.out.println(这里很牛，因为这里什么类型的数据都能放);
		/*
		System.out.println(100);
		System.out.println("100");
		System.out.println('a');
		*/
	}
}
```
```java

/*
	+ 运算符：
		1、+ 运算符在java语言中有两个作用。
			作用1：求和
			作用2：字符串拼接

		2、什么时候求和？什么时候进行字符串的拼接呢？
			当 + 运算符两边都是数字类型的时候，求和。
			当 + 运算符两边的“任意一边”是字符串类型，那么这个+会进行字符串拼接操作。

		3、一定要记住：字符串拼接完之后的结果还是一个字符串。
*/
public class OperatorTest06{

	public static void main(String[] args){

		// 定义一个年龄的变量。
		int nianLing = 35;

		// + 在这里会进行字符串的拼接操作。
		System.out.println("年龄=" + nianLing); // "年龄=35"

		int a = 100;
		int b = 200;
		// 这里的 + 两边都是数字，所以加法运算
		int c = a + b;
		System.out.println(c); // 300

		// 注意：当一个表达式当中有多个加号的时候
		// 遵循“自左向右”的顺序依次执行。（除非额外添加了小括号，小括号的优先级高）
		// 第一个+先运算，由于第一个+左右两边都是数字，所以会进行求和。
		// 求和之后结果是300，代码就变成了：System.out.println(300 + "110");
		// 那么这个时候，由于+的右边是字符串"110"，所以此时的+会进行字符串拼接。
		System.out.println(a + b + "110"); // 最后一定是一个字符串："300110"

		// 先执行小括号当中的程序：b + "110"，这里的+会进行字符串的拼接，
		// 拼接之后的结果是："200110"，这个结果是一个字符串类型。
		// 代码就变成了：System.out.println(a + "200110");
		// 这个时候的+还是进行字符串的拼接。最终结果是："100200110"
		System.out.println(a + (b + "110"));

		// 在控制台上输出"100+200=300"
		System.out.println("100+200=300"); // 不是这个意思。

		// 以下有效的运算符加号一共有4个，这4个加号都是字符串拼接操作。
		System.out.println(a + "+" + b + "=" + c);
		
		// 分析这个结果是多少？
		// 以下表达式中没有小括号，所以遵循自左向右的顺序依次执行。
		// 第1,2,3,4个加号都是进行字符串拼接，拼接之后的结果是："100+200=100"
		// 前4个加号运行之后是一个字符串"100+200=100"
		// 然后这个字符串再和最后一个b变量进行字符串的拼接："100+200=100200"
		System.out.println(a + "+" + b + "=" + a + b);

		// 和上面程序不一样的地方是：最后一个加号先执行，并且会先进行求和运算。
		System.out.println(a + "+" + b + "=" + (a + b));

		// 在java语言中怎么定义字符串类型的变量呢？
		// int是整数型 i 是变量名 10是字面量
		//int i = 10;
		// String是字符串类型，并且String类型不属于基本数据类型范畴，属于引用类型。
		// name是变量名，只要是合法的标识符就行。
		// "jack" 是一个字符串型字面量。
		String name = "李四"; // String类型是字符串类型，其中S是大写，不是：string

		// 错误：类型不兼容。
		//String name = 100;

		// 会进行字符串的拼接
		//System.out.println("登录成功欢迎" + name + "回来");
		
		
		// 口诀：加一个双引号""，然后双引号之间加两个加号："++"，然后两个加号中间加变量名："+name+"
		System.out.println("登录成功欢迎"+name+"回来");

		System.out.println(a + "+" + b + "=" + c);

	}
}
```
## 控制语句
### break
```java
/*
	break;语句：
		1、break;语句比较特殊，特殊在：break语句是一个单词成为一个完整的java语句。
		另外：continue也是这样，他俩都是一个单词成为一条语句。

		2、break 翻译为折断、弄断。

		3、break;语句可以用在哪里呢？
			用在两个地方，其它位置不行
			第一个位置：switch语句当中，用来终止switch语句的执行。
				用在switch语句当中，防止case穿透现象，用来终止switch。

			第二个位置：break;语句用在循环语句当中，用来终止循环的执行。
				用在for当中
				用在while当中
				用在do....while..当中。
		
		4、以下程序主要是以for循环为例学习break转向语句。

		5、break;语句的执行并不会让整个方法结束，break;语句主要是用来终止离它最近
		的那个循环语句。

		6、怎么用break;语句终止指定的循环呢？
			第一步：你需要给循环起一个名字，例如：
				a: for(){
					b:for(){
					
					}
				}
			第二步：终止：break a;
*/
public class BreakTest01{

	public static void main(String[] args){

		// 输出0-9
		/*
		for(int i = 0; i < 10; i++){
			System.out.println("i = " + i);
		}
		*/

		for(int i = 0; i < 10; i++){
			if(i == 5){
				// break;语句会让离它最近的循环终止结束掉。
				break; // break;终止的不是if，不是针对if的，而是针对离它最近的循环。
			}
			System.out.println("i = " + i); // 0 1 2 3 4
		}

		// 这里的代码照常执行。break;的执行并不会影响这里。
		System.out.println("Hello World!");

		// 这个for循环两次
		for(int k = 0; k < 2; k++){ // 外层for
			for(int i = 0; i < 10; i++){ // 内层for
				if(i == 5){
					break; // 这个break;语句只能终止离它最近的for
				}
				System.out.println("i ===> " + i); 
			}
		}

		System.out.println("------------------------------------------");

		// 这种语法很少用，了解一下即可。
		a:for(int k = 0; k < 2; k++){ 
			b:for(int i = 0; i < 10; i++){
				if(i == 5){
					break a; // 终止指定的循环。
				}
				System.out.println("i ===> " + i); 
			}
		}

		System.out.println("呵呵");

	}
}


```
### continue
```java
/*
	continue;语句：
		1、continue翻译为：继续
		2、continue语句和break语句要对比着学习
		3、continue语句的作用是：
			终止当前"本次"循环，直接进入下一次循环继续执行。
			for(){
				if(){ // 当这个条件成立时，执行continue语句
					continue; //当这个continue语句执行时，continue下面的代码不执行，直接进入下一次循环执行。
				}
				// 以上的continue一旦执行，以下代码不执行，直接执行更新表达式。
				code1;
				code2;
				code3;
				code4;
			}

		4、continue语句后面可以指定循环吗？
			可以的。
			这里就不再讲了，自己测试以下。
			a:for(;;更新表达式1){
				b:for(;;更新表达式2){
					if(){
						continue a;
					}
					code1;
					code2;
					code3;
				}
			}
*/
public class ContinueTest01{
	public static void main(String[] args){

		/*
			i = 0
			i = 1
			i = 2
			i = 3
			i = 4
		*/
		for(int i = 0; i < 10; i++){
			if(i == 5){
				break;
			}
			System.out.println("i = " + i);
		}

		System.out.println("----------------------------");

		/*
			i = 0
			i = 1
			i = 2
			i = 3
			i = 4
			i = 6
			i = 7
			i = 8
			i = 9
		*/
		for(int i = 0; i < 10; i++){
			if(i == 5){
				continue;
			}
			System.out.println("i = " + i); // 输出i是4
		}

	}
}

```
### do..while
```java

/*
	do..while循环语句的执行原理以及语法机制：
		语法机制：
			do {
				循环体;
			}while(布尔表达式);

		注意：do..while循环最后的时候别漏掉“分号”

		执行原理：
			先执行循环体当中的代码，执行一次循环体之后，
			判断布尔表达式的结果，如果为true，则继续执行
			循环体，如果为false循环结束。
		
		对于do..while循环来说，循环体至少执行1次。循环体的执行次数是：1~n次。
		对于while循环来说，循环体执行次数是：0~n次。
		
*/
public class DoWhileTest01{
	public static void main(String[] args){
		//错误: 需要';'
		/*
		int i = 0;
		do{
			System.out.println(i);
			i++;
		}while(i < 10)
		*/
		
		/*
		int i = 0;
		do{
			System.out.println(i); // 0 1 2 3 ... 8 9
			i++;
		}while(i < 10);
		*/

		/*
		int i = 0;
		do{
			System.out.println(i++); // 0 1 2 3 ... 8 9
		}while(i < 10);
		*/

		int i = 0;
		do{
			//System.out.println(++i); // 1 2 3 ... 8 9 10

			// 把上面那一行代码拆分为以下的两行代码。
			int temp = ++i;
			System.out.println(temp); // 程序执行到此处的时候i是10

		}while(i < 10);

		System.out.println("-----------------------------");
		int k = 100;
		System.out.println(++k); // 101
		System.out.println(k); // 101

		int m = 10;
		System.out.println(m++); // 10
		System.out.println(m); // 11


		// 至少执行1次循环体。
		do{
			System.out.println("Hello World!");
		}while(false);

	}
}
```
### for
```java
/*
	使用for循环，实现1~100所有奇数求和
	至少给出两种解决方案。
*/
public class ForTest04{
	public static void main(String[] args){

		//第一种方案：
		// 思路：先找出1~100所有的奇数，然后再考虑求和的事儿。
		// 第一步：先从1取到100，一个数字一个数字取出来。
		// 第二步：既然可以得到每一个数字，那么我们进一步判断这个数字是否为奇数
		// 奇数对2求余数，结果都是1
		int sum = 0; // 初始值给0
		for(int i = 1; i <= 100; i++){
			// int sum = 0; // 不能在这个循环体中声明，这样会导致“计算器归0”
			//for循环中嵌套了if语句。
			if(i % 2 == 1){ // i为奇数的条件
				//System.out.println("i = " + i);
				sum += i; // 累加 (sum = sum + i;)
			}
		}
		// 一定是在for循环全部结束之后，输出的sum就是最终的结果。
		System.out.println("1~100所有奇数求和结果是：" + sum); // 2500

		//第二种方案：这种方案效率高，因为循环次数比较少。
		// 之前的sum归0.重新求和。
		sum = 0;
		for(int i = 1; i < 100; i += 2){
			//这样写可以保证每一次取出的值都是奇数。不需要判断。
			//System.out.println(i);
			sum += i;
		}
		System.out.println(sum);
		
	}
}
```
```java
/*
	九九乘法表

	1*1=1
	1*2=2 2*2=4
	1*3=3 2*3=6 3*3=9
	1*4=4 2*4=8 3*4=12 4*4=16
	....
	......
	1*9=9 2*9=18.............................9*9=81

	各位，请找一下以上九九乘法表的特点？？？？？
		第一个特点：共9行。
		第二个特点：第1行1个。第2行2个。第n行n个。
	
	最重要的是：不要慌，慢慢的把思路捋出来，再写代码。
*/
public class ForTest06{
	public static void main(String[] args){
		
		// 9行，循环9次。
		for(int i = 1; i <= 9; i++){ // 纵向循环
			//System.out.println(i); // i是行号（1~9）
			// 负责输出一行的。（内部for循环负责将一行上的全部输出。）
			for(int j = 1; j <= i; j++){ // i是行号
				System.out.print(j + "*" + i + "=" + i * j + " ");
			}
			// 换行
			System.out.println();
		}
	}
}
```
### if
```java
public class IfTest01{
	public static void main(String[] args){

		// 定义一个布尔类型的变量，表示性别。
		//boolean sex = true;
		boolean sex = false;

		//业务：当sex为true时表示男，为false时表示女。
		/*
		if(sex == true){ // == 是关系运算符，不是赋值运算符，== 双等号是用来判断是否相等的。
			System.out.println("男");
		}else{
			System.out.println("女");
		}
		*/

		// 改良。
		sex = true;
		if(sex){
			System.out.println("男");
		}else{
			System.out.println("女");
		}

		// 可以再进一步改良
		// 可以使用三目运算符
		sex = false;
		System.out.println(sex ? "男" : "女");

		// 代码可以这样写吗？
		// ()小括号当中最终取的值是sex变量的值。
		// 而sex是布尔类型，所以这个可以通过。
		sex = false;
		if(sex = true){ // 以前sex不管是true还是false，走到这一行sex一定是true。
			System.out.println("男"); // 输出"男"
		}else{
			// 虽然这种语法可以，但是会导致else分支永远不能执行。
			System.out.println("女");
		}

		int i = 100;
		if(i == 100){
			System.out.println("i是100");
		}

		/*
		//错误: 不兼容的类型: int无法转换为boolean
		if(i = 100){ // (i = 100)整体执行完之后是一个int类型，不是布尔类型。
			System.out.println("i是100");
		}
		*/

		// 当分支中只有一条java语句的话，大括号可以省略。
		if(sex) 
			System.out.println("男"); 
		else 
			System.out.println("女");
		
		
		// 判断以下程序会出现问题吗？会出什么问题？第几行代码报错？？？？
		if(sex)
			System.out.println("男");
			System.out.println("HelloWorld!"); // 以上的这3行代码没有问题，合乎语法。
		/*
		else // 这一行编译报错，因为else缺少if
			System.out.println("女");
		*/
		

	}
}
```
```java
/*
	业务要求：
		1、从键盘上接收一个人的年龄。
		2、年龄要求为[0-150]，其它值表示非法，需要提示非法信息。
		3、根据人的年龄来动态的判断这个人属于生命的哪个阶段？
			[0-5] 婴幼儿
			[6-10] 少儿
			[11-18] 少年
			[19-35] 青年
			[36-55] 中年
			[56-150] 老年
		4、请使用if语句完成以上的业务逻辑。
*/
public class IfTest02{
	public static void main(String[] args){
		java.util.Scanner s = new java.util.Scanner(System.in);
		System.out.print("请输入年龄：");
		int age = s.nextInt();
		//System.out.println("测试以下，您输入的年龄是：" + age);
		/*
		if(age < 0 || age > 150){
			System.out.println("对不起，年龄值不合法");
		} else {
			// 能够走到这个分支当中，说明年龄是合法的。
			// 可以进一步使用嵌套的if语句进行判断。
			//if(age >= 0 && age <= 5){}
			// 当前先使用if嵌套的方式，当然，嵌套不是必须的。可以有其它写法。
			//System.out.println("年龄值合法");
			// 年龄值合法的情况下，继续判断年龄属于哪个阶段的！！！！
			//if(age >= 0 && age <= 5){} // 这样写代码比较啰嗦了。
			if(age <= 5){
				System.out.println("婴幼儿");
			} else if(age <= 10){
				System.out.println("少儿");
			} else if(age <= 18){
				System.out.println("少年");
			} else if(age <= 35){
				System.out.println("青年");
			} else if(age <= 55){
				System.out.println("中年");
			} else {
				System.out.println("老年");
			}
		}
		*/

		// 可以不嵌套吗？可以
		/*
		if(age < 0 || age > 150){
			System.out.println("对不起，年龄值不合法");
		} else if(age <= 5){
			System.out.println("婴幼儿");
		} else if(age <= 10){
			System.out.println("少儿");
		} else if(age <= 18){
			System.out.println("少年");
		} else if(age <= 35){
			System.out.println("青年");
		} else if(age <= 55){
			System.out.println("中年");
		} else {
			System.out.println("老年");
		}
		*/

		// 进一步改良
		String str = "老年"; // 字符串变量默认值是“老年”
		if(age < 0 || age > 150){
			System.out.println("对不起，年龄值不合法");
			// 既然不合法，你就别让程序往下继续执行了，怎么终止程序执行
			//return;
		} else if(age <= 5){
			str = "婴幼儿";
		} else if(age <= 10){
			str = "少儿";
		} else if(age <= 18){
			str = "少年";
		} else if(age <= 35){
			str = "青年";
		} else if(age <= 55){
			str = "中年";
		} 
		System.out.println(str);
	
		// 对于初学者来说可能代码会写成这样，这是正常的。
		// 代码的经验需要一步一步的积累，慢慢的代码就会越来越漂亮了。
		// 需要时间，需要积累代码经验。最好的代码是：最少的代码量，最高的效率。
		/*
		if(age >= 0 && age <= 5){
		
		}else if(age >= 6 && age <= 10){
		
		}else if.....
		*/

	}
}
```
```java
/*
	题目：
		1、系统接收一个学生的考试成绩，根据考试成绩输出成绩的等级。

		2、等级：
			优：[90~100]
			良：[80~90) 
			中：[70-80)
			及格：[60~70)
			不及格：[0-60)

		3、要求成绩是一个合法的数字，成绩必须在[0-100]之间，成绩可能带有小数。
*/
public class IfTest03{
	public static void main(String[] args){
		// 键盘扫描器对象
		java.util.Scanner s = new java.util.Scanner(System.in);
		System.out.print("请输入您的考试成绩：");
		// 考试成绩带有小数
		double score = s.nextDouble(); //程序到这里停下了，等待用户的输入。
		// 判断考试成绩
		String str = "优";
		if(score < 0 || score > 100){
			str = "成绩不合法!!!";
		}else if(score < 60){
			str = "不及格";
		}else if(score < 70){
			str = "及格";
		}else if(score < 80){
			str = "中";
		}else if(score < 90){
			str = "良";
		}
		System.out.println(str);
	}
}
```
```java
/*
	题目：
		业务：
			从键盘上接收天气的信息：
				1表示：雨天
				0表示：晴天
			同时从键盘上接收性别的信息：
				1表示：男
				0表示：女
			业务要求：
				当天气是雨天的时候：
					男的：打一把大黑伞
					女的：打一把小花伞
				当天气是晴天的时候：
					男的：直接走起，出去玩耍
					女的：擦点防晒霜，出去玩耍
		
		需要使用if语句以及嵌套的方式展现这个业务。

		可以在程序的开始，接收两个数据，一个数据是天气，一个数据是性别。
		然后将这两个数据保存到变量中。
*/
public class IfTest04{
	public static void main(String[] args){
		// 接收用户键盘输入
		java.util.Scanner s = new java.util.Scanner(System.in);
		// 提示信息
		System.out.print("请输入您的性别，输入1表示男，输入0表示女：");
		// 程序停下来等待用户的输入
		int gender = s.nextInt();
		//System.out.println(gender);
		// 提示信息
		System.out.print("请输入当前的天气，1表示雨天，0表示晴天：");
		// 等待用户的输入
		int weather = s.nextInt();
		// 开发要不断的进行测试，不要期望一次把程序写好。
		//System.out.println(weather);
		if(weather == 1){
			//System.out.println("雨天");
			if(gender == 1){
				// 男
				System.out.println("下雨了，小哥哥，出门的时候记得拿一把大黑伞哦！");
			}else if(gender == 0){
				// 女
				System.out.println("下雨了，小姐姐，出门的时候记得带一把小花伞哦！");
			}
		}else if(weather == 0){
			//System.out.println("晴天");
			if(gender == 1){
				// 男
				System.out.println("外面的天气不错，老铁们出去玩耍吧！");
			}else if(gender == 0){
				// 女
				System.out.println("外面的天气晴朗，小姐姐要保护好皮肤哦，擦点防晒霜！");
			}
		}
	}
}
```
### Switch
```java
/*
	switch语句：
		1、switch语句也是选择语句，也可以叫做分支语句。
		2、switch语句的语法格式

			switch(值){
			case 值1:
				java语句;
				java语句;...
				break;
			case 值2:
				java语句;
				java语句;...
				break;
			case 值3:
				java语句;
				java语句;...
				break;
			default:
				java语句;
			}

			以上是一个完整的switch语句：
				其中：break;语句不是必须的。default分支也不是必须的。

			switch语句支持的值有哪些？
				支持int类型以及String类型。
				但一定要注意JDK的版本，JDK8之前不支持String类型，只支持int。
				在JDK8之后，switch语句开始支持字符串String类型。

				switch语句本质上是只支持int和String，但是byte,short,char也可以
				使用在switch语句当中，因为byte short char可以进行自动类型转换。

				switch语句中“值”与“值1”、“值2”比较的时候会使用“==”进行比较。

		3、switch语句的执行原理
			拿“值”与“值1”进行比较，如果相同，则执行该分支中的java语句，
			然后遇到"break;"语句，switch语句就结束了。

			如果“值”与“值1”不相等，会继续拿“值”与“值2”进行比较，如果相同，
			则执行该分支中的java语句，然后遇到break;语句，switch结束。

			注意：如果分支执行了，但是分支最后没有“break;”，此时会发生case
			穿透现象。

			所有的case都没有匹配成功，那么最后default分支会执行。
*/
public class SwitchTest01{
	public static void main(String[] args){
		
		// 分析这个程序是否能够编译通过？
		// switch只支持int和String类型。
		// 错误: 不兼容的类型: 从long转换到int可能会有损失
		/*
		long x = 100L;
		switch(x){
		
		}
		*/

		/*
		long x = 100L;
		switch((int)x){
		
		}
		*/
		
		/*
		byte b = 100;
		switch(b){
		
		}
		*/

		/*
		short s = 100;
		switch(s){
		
		}
		*/

		/*
		char c = 'a';
		switch(c){
		
		}
		*/

		//switch也支持字符串String类型。
		//switch("abc"){}

		// 写一个完整的switch语句
		// 接收键盘输入，根据输入的数字来判断星期几。
		// 0 星期日
		// 1 星期一
		// ....
		// 假设输入的数字就是正确的。0到6
		java.util.Scanner s = new java.util.Scanner(System.in);
		System.out.print("请输入[0-6]的整数：");
		int num = s.nextInt();

		/*
		switch(num){
		case 0:
			System.out.println("星期日");
			break;
		case 1:
			System.out.println("星期一");
			break;
		case 2:
			System.out.println("星期二");
			break;
		case 3:
			System.out.println("星期三");
			break;
		case 4:
			System.out.println("星期四");
			break;
		case 5:
			System.out.println("星期五");
			break;
		case 6:
			System.out.println("星期六");
		}
		*/

		//case穿透现象
		/*
		switch(num){
		case 0:
			System.out.println("星期日");
			break;
		case 1:
			System.out.println("星期一");
		case 2:
			System.out.println("星期二");
		case 3:
			System.out.println("星期三");
		case 4:
			System.out.println("星期四");
		case 5:
			System.out.println("星期五");
			break;
		case 6:
			System.out.println("星期六");
		}
		*/

		// 关于default语句，当所有的case都没有匹配上的时候，执行default语句。
		/*
		switch(num){
		case 1:
			System.out.println("星期一");
			break;
		case 2:
			System.out.println("星期二");
			break;
		case 3:
			System.out.println("星期三");
			break;
		case 4:
			System.out.println("星期四");
			break;
		case 5:
			System.out.println("星期五");
			break;
		case 6:
			System.out.println("星期六");
			break;
		default:
			System.out.println("星期日");
		}
		*/

		// 关于case合并的问题
		switch(num){
		case 1: case 2: case 3:
			System.out.println("星期一");
			break;
		case 4:
			System.out.println("星期二");
			break;
		case 5:
			System.out.println("星期三");
			break;
		case 6:
			System.out.println("星期四");
			break;
		case 7:
			System.out.println("星期五");
			break;
		case 8:
			System.out.println("星期六");
			break;
		default:
			System.out.println("星期日");
		}


	}
}
```
```java
/*
题目：
		1、系统接收一个学生的考试成绩，根据考试成绩输出成绩的等级。

		2、等级：
			优：[90~100]
			良：[80~90) 
			中：[70-80)
			及格：[60~70)
			不及格：[0-60)

		3、要求成绩是一个合法的数字，成绩必须在[0-100]之间，成绩可能带有小数。

		必须使用switch语句来完成，你该怎么办？
*/
public class SwitchTest02{
	public static void main(String[] args){
		// 提示用户输入学生成绩
		java.util.Scanner s = new java.util.Scanner(System.in);
		System.out.print("请输入学生成绩：");
		double score = s.nextDouble();
		//System.out.println(score);
		if(score < 0 || score > 100){
			System.out.println("您输入的学生成绩不合法，再见！");
			return; // 这个代码的执行，会让main结束。后面会讲。
		}

		// 程序能够执行到这里说明成绩一定是合法的。
		// grade的值可能是：0 1 2 3 4 5 6 7 8 9 10
		// 0 1 2 3 4 5 不及格
		// 6 及格
		// 7 中
		// 8 良
		// 9 10 优
		
		int grade = (int)(score / 10); // 95.5/10结果9.55，强转为int结果是9
		String str = "不及格";
		switch(grade){
		case 10: case 9:
			str = "优";
			break;
		case 8: 
			str = "良";
			break;
		case 7:
			str = "中";
			break;
		case 6:
			str = "及格";
		}
		System.out.println("该学生的成绩等级为：" + str);
	}
}
```
### while
```java
/*
	while循环：
		1、while循环的语法机制以及执行原理
			语法机制：
				while(布尔表达式){
					循环体;
				}
			执行原理：
				判断布尔表达式的结果，如果为true就执行循环体，
				循环体结束之后，再次判断布尔表达式的结果，如果
				还是true，继续执行循环体，直到布尔表达式结果
				为false，while循环结束。

		2、while循环有没有可能循环次数为0次？
			可能。
			while循环的循环次数是：0~n次。
*/
public class WhileTest01{
	public static void main(String[] args){
		// 死循环
		/*
		while(true){
			System.out.println("死循环");
		}
		*/

		// 本质上while循环和for循环原理是相同的。
		/*
			for(初始化表达式; 布尔表达式; 更新表达式){
				循环体;
			}

			初始化表达式;
			while(布尔表达式){
				循环体;
				更新表达式;
			}

			if switch属于分支语句属于选择语句。
			for while do..while..这些都是循环语句。
			可以正常互相嵌套。
		*/
		for(int i = 0; i < 10; i++){
			System.out.println("i --->" + i);
		}
		
		/*
		int i = 0;
		while(i < 10){
			System.out.println("i = " + i);
			i++;
		}
		*/

		// for和while完全可以互换，只不过就是语法格式不一样。
		for(int i = 0; i < 10; ){
			i++;
			System.out.println("i --->" + i); // 1 2 3 .. 9 10
		}

		int i = 0;
		while(i < 10){
			i++;
			System.out.println("i = " + i); // 1 2 3 .. 9 10
		}


	}
}
```
### homework
```java
/*
根据指定月份，打印该月份所属的季节。
	3,4,5 春季 
	6,7,8 夏季 
	9,10,11 秋季 
	12, 1, 2 冬季

	if和switch各写一版
*/
class Homework1{
	public static void main(String[] args){
		java.util.Scanner s = new java.util.Scanner(System.in);
		System.out.print("请输入合法的数字【该数字可以是：1 2 3 4 5 6 7 8 9 10 11 12】:");
		int i = s.nextInt();

		// if版本
		/*
		String str = "输入的数字不合法";
		if(i == 3 || i == 4 || i == 5){
			str = "春季";
		}else if(i == 6 || i == 7 || i == 8){
			str = "夏季";
		}else if(i == 9 || i == 10 || i == 11){
			str = "秋季";
		}else if(i == 12 || i == 1 || i == 2){
			str = "冬季";
		}
		System.out.println(str);
		*/

		// switch版本
		String str = "输入的数字不合法";
		switch(i){
		case 3:case 4:case 5:
			str = "春季";
			break;
		case 6:case 7:case 8:
			str = "夏季";
			break;
		case 9:case 10:case 11:
			str = "秋季";
			break;
		case 12:case 1:case 2:
			str = "冬季";
		}
		System.out.println(str);

	}
}

//从键盘接收一个数字，判断该数字的正负
class Homework2{
	public static void main(String[] args){
		java.util.Scanner s = new java.util.Scanner(System.in);
		System.out.print("请输入一个数字，我可以判断正负哦：");
		// 接收一个数字
		//int value = s.nextInt();
		double value = s.nextDouble();
		// 判断该数字正负
		/*
		if(value < 0){
			System.out.println("负数");
		}else{
			System.out.println("正数");
		}
		*/
		System.out.println(value < 0 ? "负数" : "正数");
	}
}

//从键盘接收一个数字，判断该数字的奇偶。
class Homework3{
	public static void main(String[] args){
		
		//创建一次。
		java.util.Scanner s = new java.util.Scanner(System.in);

		while(true){
			System.out.print("请输入一个数字，可以判断奇数偶数哦（输入0表示退出系统）：");
			int value = s.nextInt();
			if(value == 0){
				// 退出系统，结束程序
				return; //后面讲。
			}
			System.out.println(value % 2 == 0 ? "偶数" : "奇数");
		}
	}
}

/*
整数大小比较：输入两个整数，比较大小，
	若x>y 输出 >
	若x=y 输出 =
	若x<y 输出 <
*/
class Homework4{
	public static void main(String[] args){
		java.util.Scanner s = new java.util.Scanner(System.in);
		System.out.print("请输入第1个数字：");
		int x = s.nextInt();
		System.out.print("请输入第2个数字：");
		int y = s.nextInt();
		if(x > y){
			System.out.println(x + ">" + y);
		}else if(x == y){
			System.out.println(x + "=" + y);
		}else{
			System.out.println(x + "<" + y);
		}
		// 同学们尝试一下使用多个三目运算符如何表述以上程序。
	}
}


/*
编写程序，由键盘输入三个整数分别存入变量num1,num2,num3中，对它们进行排序，
使用if-else结构，并按从小到大的顺序输出
*/
class Homework5{
	public static void main(String[] args){
		java.util.Scanner s = new java.util.Scanner(System.in);
		System.out.print("请输入第1个数字：");
		int x = s.nextInt();
		System.out.print("请输入第2个数字：");
		int y = s.nextInt();
		System.out.print("请输入第3个数字：");
		int z = s.nextInt();

		// 先判断三个值是否都相等
		if(x == y && y == z){
			System.out.println(x);
			System.out.println(y);
			System.out.println(z);
			return; //终止掉程序，后面讲
		}

		// 代码能够走到这里说明x y z不是都相等。
		// x和y相等，但是和z不等 
		if(x == y){
			if(x > z){
				System.out.println(z);
				System.out.println(x);
				System.out.println(y);
			}else{
				System.out.println(x);
				System.out.println(y);
				System.out.println(z);
			}
		}
		// x和z相等，但是和y不等
		if(x == z){ 
			if(x > y){
				System.out.println(y);
				System.out.println(x);
				System.out.println(z);
			}else{
				System.out.println(x);
				System.out.println(z);
				System.out.println(y);
			}
		}
		// y和z相等，但是和x不等
		if(y == z){ // x y z
			if(y > x){
				System.out.println(x);	
				System.out.println(y);	
				System.out.println(z);	
			}else{
				System.out.println(y);	
				System.out.println(z);	
				System.out.println(x);
			}
		}

		// 程序执行到这里说明 x y z 都不相等
		/*
		if(x > y){
			if(y > z){
				System.out.println(z);
				System.out.println(y);
				System.out.println(x);
			}else{ 
				if(x < z){
					System.out.println(y);
					System.out.println(x);
					System.out.println(z);
				}else{
					System.out.println(y);
					System.out.println(z);
					System.out.println(x);
				}
			}
		}else{
			// x < y
			// 50 < 100
		}
		*/

		// 不算相等的，一共有6种情况。
		if(x > y && x > z){ // 假设x是最大的
			if(y > z){
				System.out.println(z);
				System.out.println(y);
			}else{
				System.out.println(y);
				System.out.println(z);
			}
			System.out.println(x);
		}else if(y > x && y > z){ // 假设y是最大的
			if(x > z){
				System.out.println(z);
				System.out.println(x);
			}else{
				System.out.println(x);
				System.out.println(z);
			}
			System.out.println(y);
		}else{ //假设z是最大的
			if(x > y){
				System.out.println(y);
				System.out.println(x);
			}else{
				System.out.println(x);
				System.out.println(y);
			}
			System.out.println(z);
		}
		

	}
}

/*
打车起步价8元（3KM以内）
超过3KM，超出的每公里1.2元
超过5KM，超出的每公里1.5元
请在键盘上接收公里数，得出总价。
*/
class Homework6{
	public static void main(String[] args){
		java.util.Scanner s = new java.util.Scanner(System.in);
		System.out.print("请输入行驶的公里数：");
		int dis = s.nextInt(); 
		if(dis <= 3){
			System.out.println("总价是：" + 8 + "元");
		}else if(dis <= 5){
			System.out.println("总价是：" + ((dis - 3) * 1.2 + 8) + "元");
		}else{
			// 公里超出5KM
			System.out.println("总价是：" + ((8 + 2 * 1.2) + (dis - 5) * 1.5) + "元");
		}
	}
}
```
```java
/*
	应该怎么去编程？？？？？？？

	计算1000以内所有不能被7整除的整数之和
		1、解决一个问题的时候，可以先使用汉语描述思路。（养成好习惯）
		2、复杂的问题可以“一步一步”去实现，没必要一下全部实现。
	
	把上面的题目可以拆分成几步去完成：

		第一步：从1开始循环，循环到1000，先保证每一个数字你都能取到。

		第二步：在以上第一步的循环过程中，一个数字一个数字筛查，判断该数字是否
		是“不能被7整除的整数”。
	
	编程思想/思路，都是一步一步分析，积累出来的。
	编程最主要的是写汉语思路。思路有了，代码就不远了。

	把问题拆开，一个一个去解决一下。

	不断写代码，不断的积累编程“模型”。
*/
public class Homework1{

	public static void main(String[] args){

		// 在外部准备一个变量，用来存储求和的结果
		int sum = 0;

		//循环的时候你能想起来for while do..while
		for(int i = 1; i <= 1000; i++){ //第一步

			// 判断的时候你能想起来使用if
			if(i % 7 != 0){ // 第二步
				// 此时的i是不能被7整除的，这个i应该此时纳入求和/累加。
				//sum += i;
				sum = sum + i;
			}

		}

		// 在for循环结束之后，结果才计算完成，所以在这里输出。
		System.out.println("sum = " + sum); //429429


	}
}
```
```java
// 计算 1+2-3+4-5+6-7....+100的结果
// 找规律：奇数时减法，偶数时加法。
// 第一种思路：(除1之外)所有的偶数求和，所有的奇数求和，然后偶数求和的结果减去奇数求和的结果。
// 第二种思路：循环过程中取出每个值，判断该数是偶数还是奇数，偶数就加，奇数就减。

//写代码养成好习惯是：写一步测试一步。
public class Homework2{
	public static void main(String[] args){
		// 第一步：先别着急着完成，先能从1取到100
		int sum = 1; //sum的初始值不是0，而是1.
		for(int i = 2; i <= 100; i++){ // i从2开始。
			if(i % 2 == 0){ //偶数
				sum += i;
			}else{ // 奇数
				sum -= i; 
			}
		}
		System.out.println("结果=" + sum); // 52
	}
}
```
```java
// 计算 1+2-3+4-5+6-7....+100的结果
// 找规律：奇数时减法，偶数时加法。
// 第一种思路：(除1之外)所有的偶数求和，所有的奇数求和，然后偶数求和的结果减去奇数求和的结果。
// 第二种思路：循环过程中取出每个值，判断该数是偶数还是奇数，偶数就加，奇数就减。

//写代码养成好习惯是：写一步测试一步。
public class Homework2{
	public static void main(String[] args){
		// 第一步：先别着急着完成，先能从1取到100
		int sum = 1; //sum的初始值不是0，而是1.
		for(int i = 2; i <= 100; i++){ // i从2开始。
			if(i % 2 == 0){ //偶数
				sum += i;
			}else{ // 奇数
				sum -= i; 
			}
		}
		System.out.println("结果=" + sum); // 52
	}
}
```
```java
//从控制台输入一个正整数，计算该数的阶乘。例如输入5，阶乘为 5*4*3*2*1
public class Homework3{
	public static void main(String[] args){
		//第一步：怎么从键盘上接收一个正整数。
		java.util.Scanner s = new java.util.Scanner(System.in);
		// 等待用户输入一个正整数。
		System.out.print("请输入一个正整数：");
		int num = s.nextInt();
		// 计算该数的阶乘
		// 5的阶乘：5*4*3*2*1
		// 8的阶乘：8*7*6*5*4*3*2*1
		// 第二步：先不用管乘法的事儿，先实现从8取到1.（递减的方式取）
		//int jieGuo = 0; //初始值不能是0，是0的时候，乘积最后是0.
		int jieGuo = 1; //结果的初始值给1.
		for(int i = num; i > 1; i--){
			jieGuo *= i; // jieGuo = jieGuo * i;
		}
		System.out.println("计算结果 = " + jieGuo);
	}
}
```
```java

/*
从控制台接收一个正整数，判断该数字是否为质数
质数（质数是指在大于1的自然数中，除了1和它本身以外不再有其他因数的自然数）

因数是什么？
	3 * 5 = 15
	3和5都是15的因数。

2 3 4 5 6 7中：2 3 5 7都是质数。

重点题目：
	主要练习，在外部打布尔标记。

*/
public class Homework4{
	public static void main(String[] args){
		// 从控制台接收一个正整数。
		java.util.Scanner s = new java.util.Scanner(System.in);
		System.out.print("请输入一个正整数：");
		int num = s.nextInt(); // 假设输入的是8

		// 判断该数字是否为质数
		// 怎么判断num是不是质数
		// 怎么判断8是不是质数？
		// 思路：8除以2看看能不能整除、8除以3看看能不能整除、8除以4看看能不能整除
		// 一直除下去，直到发现有能够整除的，表示该数一定不是质数。
		/*
			假设输入的是7：
				7 / 1 不用判断
				7 / 2	需要判断
				7 / 3	需要判断
				7 / 4	需要判断（假设这个判断，发现可以整除，就没必要往下判断了。）
				7 / 5	需要判断
				7 / 6	需要判断
				7 / 7 不用判断
		*/

		//可以考虑在外边准备一个布尔类型的标记。
		boolean zhiShu = true; // true表示是质数。

		for(int i = 2; i < num; i++){ // 假设输入的是100
			//System.out.println(i);
			if(num % i == 0){
				// 循环没必要执行了，为了效率，这里要终止循环
				//System.out.println("该数字"+num+"不是质数！");
				zhiShu = false;
				break;
			}
		}

		System.out.println(num + (zhiShu ? "是" : "不是") + "质数");
	}
}
```
```java
/*
从键盘接收一个正整数，该正整数作为行数，输出以下图形
    *
   ***
  *****
 *******
*********
例如：输入5，则打印如上图5行。

空格的规律：
	第1行4个空格(5-1)
	第2行3个空格(5-2)
	第3行2个空格(5-3)
	第4行1个空格(5-4)
	第5行0个空格(5-5)

星号的规律：
	第1行1个
	第2行3个
	第3行5个
	第4行7个
	.....

	行号 * 2 - 1
*/
public class Homework5{
	public static void main(String[] args){
		// 开发需要思路，实现这个功能需要一步一步来。
		// 这个步骤是什么？
		java.util.Scanner s = new java.util.Scanner(System.in);
		System.out.print("请输入一个正整数作为行数：");
		int rows = s.nextInt();
		
		// 6行循环6次
		// n行循环n次
		for(int i = 1; i <= rows; i++){ // 外层循环控制的是总行数。
			
			// 我在这里需要将一行全部输出
			// 这里需要再使用循环，输出空格以及“*”
			// 输出空格的循环
			for(int j = 0; j < rows - i; j++){
				System.out.print(" ");
			}
			// 输出星号*的循环
			for(int k = 0; k < i * 2 - 1; k++){
				System.out.print("*");
			}

			// 以上两个for循环都结束之后，表示一行就结束了
			// 在这里换行
			System.out.println();
		}

	}
}
```
```java
/*
小芳的妈妈每天给她2.5元钱，她都会存起来，但是，每当这一天是存钱的第5天
或者5的倍数的话，她都会花去6元钱，请问，经过多少天，小芳才可以存到100元钱。

这个题目最主要练习是：
	while循环 + 计数。
*/
public class Homework6{
	public static void main(String[] args){

		// 小芳每一天肯定会有2.5元的收入。
		// 小芳即使有一天花了6元，但是2.5元的收入还是有的。
		// 经过分析：总钱数肯定需要是double类型。int类型不行。

		int day = 0; // 天数的默认初始值是0
		double money = 0.0; // 钱的默认初始值是0

		/*
		while(true){
			day++; // 天数加1
			money += 2.5; // 钱加2.5元
			// 如果天数是5的倍数，那么花去6元
			if(day % 5 == 0){
				money -= 6.0;
			}
			// 什么时候循环结束呢？
			// 当money >= 100.0的时候，循环结束。
			if(money >= 100){
				break;
			}
		}
		*/

		// 改造之后的。
		while(money < 100){
			day++; // 天数加1
			money += 2.5; // 钱加2.5元
			// 如果天数是5的倍数，那么花去6元
			if(day % 5 == 0){
				money -= 6.0;
			}
		}

		//小芳通过74天存到了101.0元钱
		System.out.println("小芳通过" + day + "天存到了" + money + "元钱");

	}
}
```
```java

/*
一个数如果恰好等于它的因子之和，这个数就是完数，例如 6 = 1 + 2 + 3，编程
找出1000内所有的完数。

什么是完数？
	一个数如果恰好等于它的因子之和，这个数就是完数。

那么因子怎么找？
	10的因子？
		10 % 1 == 0
		10 % 2 == 0
		10 % 5 == 0
	不算10本身。
	10的因子：
		1 + 2 + 5 = 8

运行结果：
	6
	28
	496
*/
public class Homework7{
	public static void main(String[] args){
		// 1不属于完数。从2开始判断
		// 第一步：先从1到1000，每个数字都取出来
		for(int i = 2; i <= 1000; i++){
			// 第二步：在这里可以拿到i，那么此时应该判断i是否是一个完数。
			// 这个数字有了，找这个数字的因子。
			// 假设现在这个数字就是6，i等于6
			int sum = 0;
			for(int j = 1; j <= i / 2; j++){
				//j取到的值是：1 2 3 4 5
				//但实际上j取到哪儿就行了：1 2 3，取这几个数就行了。
				//取到一半就行。
				if(i % j == 0){
					//此时j就是因子。
					// 记得将因子j追加，累计。
					sum += j;
				}
			}
			// 以上for结束表示：所有因子求和完毕了。
			if(i == sum){
				//i是一个完数
				System.out.println(i);
			}
		}
	}
}
```
