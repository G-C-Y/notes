## 方法
```java
/*
	对于一个java程序来说，如果没有“方法”，会存在什么问题？
		代码无法得到复用。（怎么提高复用性，可以定义方法，然后需要
		使用该功能的时候，直接调用一下方法即可。这样代码就得到复用了。）
*/
public class MethodTest01{
	// 入口主方法。
	public static void main(String[] args){

		// 需求1：请编写程序，计算100和200的求和。
		int x = 100;
		int y = 200;
		int z = x + y;
		System.out.println(x + "+" + y + "=" + z);

		// 需求2：请编写程序，计算666和888的求和。
		// 这个需求2实际上和需求1是完全相同的，只不过具体求和时的“数据不同”
		int a = 666;
		int b = 888;
		int c = a + b;
		System.out.println(a + "+" + b + "=" + c);

		// 需求3：请编写程序，计算111和222的和
		int m = 111;
		int n = 222;
		int k = m + n;
		System.out.println(m + "+" + n + "=" + k);

		/*
			需求1和需求2本质上相同，只不过参与运算的数值不同，
			代码编写了两份，显然代码没有得到重复利用，专业术语
			叫做“复用性”差。

			功能/业务逻辑既然相同，为什么要重复编写代码，代码能不能
			写一次，以后要是需要再次使用该“业务/需求”的时候，直接调用
			就可以了。

			如果想达到代码复用，那么需要学习java语言中的方法机制。
		*/

	}

}
```
```java
public class MethodTest02{

	// 方法定义在类体当中。
	// 方法定义的先后顺序没有关系。都可以。
	/*
	public static void sumInt(int x, int y){ // 自上而下的顺序依次逐行执行。
		int z = x + y;
		System.out.println(x + "+" + y + "=" + z);
	}
	*/


	// 主方法。入口。
	public static void main(String[] args){ // 自上而下依次逐行执行。
		// 需求1：请编写程序，计算100和200的求和。
		sumInt(100, 200);
		// 需求2：请编写程序，计算666和888的求和。
		sumInt(666, 888);
		// 需求3：请编写程序，计算111和222的和
		sumInt(111, 222);
	}

	// 专门在这个类体当中定义一个方法，这个方法专门来完成求和。
	// x y z在以下的sumInt方法中都属于局部变量
	// 局部变量有一个特点：方法结束之后，局部变量占用的内存会自动释放。
	public static void sumInt(int x, int y){ // 自上而下的顺序依次逐行执行。
		int z = x + y;
		System.out.println(x + "+" + y + "=" + z);
	}

	public static void sum(){
		//System.out.println(x);
		//System.out.println(y); 
		//错误: 找不到符号
		//System.out.println(z);
	}

}
```
```java
/*
	1、方法怎么定义，语法机制是什么？

		[修饰符列表] 返回值类型 方法名(形式参数列表){
			方法体; 
		}

		注意：
			[] 符号叫做中括号，以上中括号[]里面的内容表示不是必须的，是可选的。
			方法体由Java语句构成。
			方法定义之后需要去调用，不调用是不会执行的。
		
		1.1、关于修饰符列表：
			修饰符列表不是必选项，是可选的。目前为止，大家统一写成：public static
			后面你就理解应该怎么写了。

		1.2、关于返回值类型：

			第一：返回值类型可以是任何类型，只要是java中合法的数据类型就行，数据
			类型包括基本数据类型和引用数据类型，也就是说返回值类型可以是：byte short
			int long float double boolean char String......

			第二：什么是返回值？
				返回值一般指的是一个方法执行结束之后的结果。
				结果通常是一个数据，所以被称为“值”，而且还叫
				“返回值”。
				方法就是为了完成某个特定的功能，方法结束之后
				大部分情况下都是有一个结果的，而体现结果的一般
				都是数据。数据得有类型。这就是返回值类型。

				main{
					// 调用a方法
					a();..如果a方法执行结束之后有返回值，这个返回值返回给main了。
				}

				a(){}

				方法执行结束之后的返回值实际上是给调用者了。谁调用就返回给谁。
			
			第三：当一个方法执行结束不返回任何值的时候，返回值
			类型也不能空白，必须写上void关键字。所以void表示该
			方法执行结束后不返回任何结果。

			第四：如果返回值类型“不是void”，那么你在方法体执行结束的时候必须使用
			"return 值;"这样的语句来完成“值”的返回，如果没有“return 值;”这样的语句
			那么编译器会报错。
				return 值; 这样的语句作用是什么？作用是“返回值”，返回方法的执行结果。
			
			第五：只要有“return”关键字的语句执行，当前方法必然结束。
			return只要执行，当前所在的方法结束，记住：不是整个程序结束。

			第六：如果返回值类型是void，那么在方法体当中不能有“return 值;”这样的
			语句。但是可以有“return;”语句。这个语句“return;”的作用就是用来终止当前
			方法的。

			第七：除了void之外，剩下的都必须有“return 值;”这样的语句。

		1.3、方法名
			方法名要见名知意。（驼峰命名方式）
			方法名在标识符命名规范当中，要求首字母小写，后面每个单词首字母大写。
			只要是合法的标识符就行。
		
		1.4、形式参数列表
			简称：形参
			注意：形式参数列表中的每一个参数都是“局部变量”，方法结束之后内存释放。
			形参的个数是：0~N个。
			public static void sumInt(){}
			public static void sumInt(int x){}
			public static void sumInt(int x, int y){}
			public static void sum(int a, int b, double d, String s){}
			形参有多个的话使用“逗号,”隔开。逗号是英文的。
			形参的数据类型起决定性作用，形参对应的变量名是随意的。
		
		1.5、方法体：
			由Java语句构成。java语句以“;”结尾。
			方法体当中编写的是业务逻辑代码，完成某个特定功能。
			在方法体中的代码遵循自上而下的顺序依次逐行执行。
			在方法体中处理业务逻辑代码的时候需要数据，数据来源就是这些形参。
	
	2、方法定义之后怎么调用呢？
		方法必须调用才能执行。
		怎么调用，语法是什么？
			类名.方法名(实际参数列表);
		
		实参和形参的类型必须一一对应，另外个数也要一一对应。

*/
public class MethodTest03{

	//方法定义在这里可以。

	// main方法结束之后不需要给JVM返回任何执行结果。
	public static void main(String[] args){
		// 调用方法
		//错误: 不兼容的类型: String无法转换为int
		//MethodTest03.divide("abc", 200); // int a = "abc";

		//错误原因: 实际参数列表和形式参数列表长度不同
		//MethodTest03.divide();

		// (10, 2)叫做实际参数列表，简称实参。
		// 注意：实参和形参必须一一对应，类型要对应，个数要对应。
		MethodTest03.divide(10, 2);

		// 调用sum方法
		// 怎么去接收这个方法的返回结果？？？？
		// 使用变量来接收这个方法的返回值。
		// 注意：变量的定义需要指定变量的数据类型。
		// 变量的数据类型是什么呢？
		int jieGuo = MethodTest03.sum(100, 200);
		System.out.println(jieGuo); //300

		// jieGuo变量可以是double类型吗？
		// double是大容量。int是小容量。自动类型转换。
		double jieGuo2 = MethodTest03.sum(100, 200);
		System.out.println(jieGuo2); //300.0

		// 对于没有返回值的方法，变量能接收吗？
		// divide方法结束没有返回值。不能接收。
		// 错误: 不兼容的类型: void无法转换为int
		//int i = MethodTest03.divide(100, 50);

		// 当一个方法有返回值的时候，我可以选择不接收吗？
		// 你可以返回值，但是我可以选择不要你这个值。这是允许的。
		// 只不过这样没有意义，一般程序返回了执行结果，都是需要接收这个结果的。
		// 我们可以不接收，但是这个返回值该返回还是会返回的。只不过不用变量接收。
		// 以下代码虽然没有使用变量接收这个返回值，但是这个值还是返回了。
		// 返回之后内存马上释放，因为没有使用变量接收。
		MethodTest03.sum(100, 200);

		byte b1 = 10;
		//int a = b1;
		byte b2 = 20;
		int result = sum(b1, b2); // (b1,b2)是实参。自动类型转换。
		System.out.println(result);

	}

	// 计算两个int类型数据的和
	/*
	public static String sum(int a, int b){
		// 错误: 不兼容的类型: int无法转换为String
		return a + b;
	}
	*/

	public static int sum(int a, int b){
		return a + b;
	}

	// 方法定义到这里也可以。没有顺序要求。
	// 业务是什么？计算两个int类型数据的商
	// 方法执行结束之后返回执行结果。

	//错误: 缺少返回语句
	/*
	public static int divide(int x, int y){
		int z = x / y;
	}
	*/

	//错误: 不兼容的类型: String无法转换为int
	/*
	public static int divide(int x, int y){
		int z = x / y;
		return "abc";
	}
	*/

	//可以
	/*
	public static int divide(int x, int y){
		int z = x / y;
		return z;
	}
	*/

	//可以
	/*
	public static int divide(int x, int y){
		return x / y;
	}
	*/

	// 可以
	/*
	public static int divide(int a, int b){
		return a / b;
	}
	*/

	// 如果我不需要执行结束之后的返回值？
	// 这个结果我希望直接输出。
	//错误: 不兼容的类型: 意外的返回值
	/*
	public static void divide(int a, int b){
		return a / b;
	}
	*/

	//可以
	/*
	public static void divide(int a, int b){
		return; // 用来终止这个方法的
	}
	*/

	// 可以
	/*
	public static void divide(int a, int b){
	}
	*/

	// 可以
	public static void divide(int a, int b){
		System.out.println(a / b); // 5
	}
}
```
```java

/*
	在方法调用的时候，什么时候“类名.”是可以省略的。什么时候不能省略？
		a()方法调用b()方法的时候，a和b方法都在同一个类中，“类名.”可以
		省略。如果不在同一个类中“类名.”不能省略。
*/

// 类1
public class MethodTest04{

	public static void daYin3(){
		System.out.println("动力节点-口口相传的Java黄埔军校！");
	}
	
	// 入口
	public static void main(String[] args){
		// 调用println()方法。
		MethodTest04.daYin();
		MethodTest04.daYin2();
		MethodTest04.daYin3();

		// “类名. ”可以省略吗？
		daYin();
		daYin2();
		daYin3();

		// 第一次跨类调用。
		// 像这种情况下：“类名.”就不能省略了。
		MyClass.daYin();
		//daYin();
	}

	public static void daYin(){
		System.out.println("hello world!");
	}

	public static void daYin2(){
		System.out.println("hello world2!!!");
	}
}

// 类2
class MyClass{

	public static void daYin(){
		System.out.println("打印1");
	}

	public static void daYin2(){
		System.out.println("打印2");
	}

	public static void daYin3(){
		System.out.println("打印3");
	}
}
```
```java

// 别自乱阵脚：任何一个方法体当中的代码都是遵循自上而下的顺序依次逐行执行的。
// 自上而下的顺序
/*
	推测执行结果：
		main begin
		m1 begin
		m2 begin
		m3 begin
		T's m3 method execute!
		m3 over
		m2 over
		m1 over
		main over

		main方法最先执行，并且main方法是最后一个结束。
		main结束，整个程序就结束了。

*/
public class MethodTest05{

	public static void main(String[] args){
		System.out.println("main begin");
		// 调用m1方法
		m1();	
		System.out.println("main over");
	}

	public static void m1(){
		System.out.println("m1 begin");
		// 调用程序不一定写到main方法中，不要把main方法特殊化。
		// main方法也是一个普通方法。
		m2();

		System.out.println("m1 over");
	}

	// m2方法可以调用T类的m3()方法吗？
	public static void m2(){
		System.out.println("m2 begin");
		T.m3();
		System.out.println("m2 over");
	}
}

class T{
	public static void m3(){
		System.out.println("m3 begin");
		System.out.println("T's m3 method execute!");
		System.out.println("m3 over");
	}
}
```
```java
/*
	break;语句和return;语句有什么区别？
		不是一个级别。
		break;用来终止switch和离它最近的循环。
		return;用来终止离它最近的一个方法。
*/
public class MethodTest06{

	//main方法的返回值类型是void，表示没有返回值。
	public static void main(String[] args){

		for(int i = 0; i < 10; i++){
			if(i == 5){
				//break; // 终止for循环
				return; // 终止当前的方法，和break;不是一个级别的。
				//错误: 不兼容的类型: 意外的返回值
				//return 10;
			}
			System.out.println("i = " + i);
		}

		System.out.println("Hello World!");
	}


}
```
### 方法重载
```java
/*
	方法重载机制？
		1、以下程序先不使用方法重载机制，分析程序的缺点？？？
			以下程序没有语法错误，运行也是正常的，你就分析一下代码风格存在什么缺点!

			sumInt、sumLong、sumDouble不是功能“相同”，是功能“相似”。

			三个方法功能不同，但是相似，分别起了三个不同的名字，有什么缺点？

			缺点包括两个：
				第一个：代码不美观（不好看、不整齐）。【这是次要的】
				第二个：程序员需要记忆更多的方法名称，程序员比较累。

*/
public class OverloadTest01{
	//主方法
	public static void main(String[] args){
		int x = sumInt(10, 20);
		System.out.println(x);

		long y = sumLong(10L, 20L);
		System.out.println(y);

		double z = sumDouble(10.0, 20.0);
		System.out.println(z);
	}

	// 定义一个计算int类型数据的求和方法
	public static int sumInt(int a, int b){
		return a + b;
	}

	// 定义一个计算long类型数据的求和方法
	public static long sumLong(long a, long b){
		return a + b;
	}

	// 定义一个计算double类型数据的求和方法
	public static double sumDouble(double a, double b){
		return a + b;
	}
}

```

```java

/*
使用方法重载机制。解决之前的两个缺点。
优点1：代码整齐美观。
优点2：“功能相似”的，可以让“方法名相同”，更易于以后的代码编写。

在java语言中，是怎么进行方法区分的呢？
	首先java编译器会通过方法名进行区分。
	但是在java语言中允许方法名相同的情况出现。
	如果方法名相同的情况下，编译器会通过方法的参数类型进行方法的区分。
*/
public class OverloadTest02{
	public static void main(String[] args){
		// 对于程序员来说，只需要记忆一个方法名即可。
		System.out.println(sum(10, 20));
		System.out.println(sum(10L, 20L));
		System.out.println(sum(10.0, 20.0));
	}
	// 定义一个计算int类型数据的求和方法
	public static int sum(int a, int b){
		System.out.println("int求和");
		return a + b;
	}

	// 定义一个计算long类型数据的求和方法
	public static long sum(long a, long b){
		System.out.println("long求和");
		return a + b;
	}

	// 定义一个计算double类型数据的求和方法
	public static double sum(double a, double b){
		System.out.println("double求和");
		return a + b;
	}
}
```
```java
/*
	方法重载（overload）:

		什么时候需要考虑使用方法重载？
			在同一个类当中，如果“功能1”和“功能2”它们的功能是相似的，
			那么可以考虑将它们的方法名一致，这样代码既美观，又便于
			后期的代码编写（容易记忆，方便使用）。

			注意：方法重载overload不能随便使用，如果两个功能压根不相干，
			不相似，根本没关系，此时两个方法使用重载机制的话，会导致
			编码更麻烦。无法进行方法功能的区分。

		什么时候代码会发生方法重载？	 
			条件1：在同一个类当中
			条件2：方法名相同
			条件3：参数列表不同
						参数的个数不同算不同
						参数的类型不同算不同
						参数的顺序不同算不同

			只要同时满足以上3个条件，那么我们可以认定方法和方法之间发生了
			重载机制。
	
	注意：
		不管代码怎么写，最终一定能让java编译器很好的区分开这两个方法。

		方法重载和方法的“返回值类型”无关。
		方法重载和方法的“修饰符列表”无关。
*/
public class OverloadTest03{
	public static void main(String[] args){
		m1();
		m1(100);

		m2(10, 3.14);
		m2(3.14, 10);

		m3(100);
		m3(3.14);

	}

	public static void m1(){
		System.out.println("m1无参数的执行！");
	}
	
	// 这个方法的参数个数和上面的方法的参数个数不同。
	public static void m1(int a){
		System.out.println("m1有一个int参数执行！");
	}

	public static void m2(int x, double y){
		System.out.println("m2(int x, double y)");
	}

	// 参数的顺序不同，也算不同。
	public static void m2(double y, int x){
		System.out.println("m2(double y, int x)");	
	}

	public static void m3(int x){
		System.out.println("m3(int x)");
	}

	// 参数的类型不同。
	public static void m3(double d){
		System.out.println("m3(double d)");
	}

	//分析：以下两个方法有没有发生重载？
	// 编译器报错了，不是重载，这是重复了：呵呵。
	/*
	public static void m4(int a, int b){
	
	}
	public static void m4(int x, int y){
	
	}
	*/

	// 这两个方法有没有发生重载呢？
	// 这不是重载，这是方法重复了。
	/*
	public static int m5(){
		return 1;
	}
	public static double m5(){
		return 1.0;
	}
	*/

	//这两个方法重载了吗？
	// 这个方法没有修饰符列表
	// 这不是重载，是重复了。
	/*
	void m6(){
	
	}
	// 这个有修饰符列表
	public static void m6(){
	
	}
	*/

}

class MyClass{
	// 不在同一个类当中，不能叫做方法重载。
	public static void m1(int x, int y){
	
	}
}
```
```java
public class OverloadTest04{
	public static void main(String[] args){
		// 大家是否承认：println是一个方法名。
		// println我承认是方法名了，但是这个方法谁写的？SUN公司的java团队写的。
		// 你直接用就行。
		// println()方法肯定是重载了。（不信，你可以翻阅一下SUN公司写的源代码看看。）
		// 对于println()方法来说，我们只需要记忆这一个方法名就行。
		// 参数类型可以随便传。这说明println()方法重载了。
		System.out.println(10);
		System.out.println(3.14);
		System.out.println(true);
		System.out.println('a');
		System.out.println("abc");

		System.out.println(100L);
		System.out.println(3.0F);

		// 调用m方法
		m(100);
	}

	public static void m(int i){
		
	}

}
```
```java
// 目前我们正在学习的一个内容是：方法重载机制（overload）

public class S{
	// 以下所有的p()方法构成了方法的重载。
	// 换行的方法
	public static void p(){
		System.out.println();
	}
	// 输出byte
	public static void p(byte b){
		System.out.println(b);
	}
	// 输出short
	public static void p(short s){
		System.out.println(s);
	}
	// 输出int
	public static void p(int i){
		System.out.println(i);
	}
	// 输出long
	public static void p(long l){
		System.out.println(l);
	}
	// 输出float
	public static void p(float f){
		System.out.println(f);
	}
	// 输出double
	public static void p(double d){
		System.out.println(d);
	}
	// 输出boolean
	public static void p(boolean b){
		System.out.println(b);
	}
	// 输出char
	public static void p(char c){
		System.out.println(c);
	}
	// 输出String
	public static void p(String s){
		System.out.println(s);
	}
}
```
### 方法递归
```java
/*
	方法递归？
		1、什么是方法递归？
			方法自己调用自己，这就是方法递归。

		2、当递归时程序没有结束条件，一定会发生：
			栈内存溢出错误：StackOverflowError
			所以：递归必须要有结束条件。（这是一个非常重要的知识点。）

			JVM发生错误之后只有一个结果，就是退出JVM。

		3、递归假设是有结束条件的，就一定不会发生栈内存溢出错误吗？
			假设这个结束条件是对的，是合法的，递归有的时候也会出现栈内存溢出错误。
			因为有可能递归的太深，栈内存不够了。因为一直在压栈。
		
		4、在实际的开发中，不建议轻易的选择递归，能用for循环while循环代替的，尽量
		使用循环来做。因为循环的效率高，耗费的内存少。递归耗费的内存比较大，另外
		递归的使用不当，会导致JVM死掉。
		(但在极少数的情况下，不用递归，这个程序没法实现。)
		所以：递归我们还是要认真学习的。

		5、在实际的开发中，假设有一天你真正的遇到了：StackOverflowError
		你怎么解决这个问题，可以谈一下你的思路吗？
			我来谈一下我的个人思路：
				首先第一步：
					先检查递归的结束条件对不对。如果递归结束条件不对，
					必须对条件进一步修改，直到正确为止。

				第二步：假设递归条件没问题，怎么办？
					这个时候需要手动的调整JVM的栈内存初始化大小。
					可以将栈内存的空间调大点。（可以调整大一些。）
				
				第三步：调整了大小，如果运行时还是出现这个错误，
				没办法，只能继续扩大栈的内存大小。
				
				(java -X)这个可以查看调整堆栈大小的参数
*/
public class RecursionTest01{
	// 入口
	public static void main(String[] args){
		doSome();
	}

	public static void doSome(){
		System.out.println("doSome begin");
		// 调用方法：doSome()既然是一个方法，那么doSome方法可以调用吗？当然可以。
		// 目前这个递归是没有结束条件的，会出现什么问题？
		doSome();
		// 这行代码永远执行不到。
		System.out.println("doSome over");
	}

	/*
		public static void doSome(){
		// 假设突然有一天，一个条件成立了，这个doSome结束了
		if(某个条件成立了){
			return;
		}
	}
	*/
}
```
```java

// 先不使用递归，请编写程序，计算1~n的和。
public class RecursionTest02{
	public static void main(String[] args){
		// 1~10的和
		int retValue1 = sum(10);
		System.out.println(retValue1);

		// 1~3的和
		int retValue2 = sum(3);
		System.out.println(retValue2); // 6 (1 + 2 + 3)
	}

	// 单独编写一个计算1~n和的方法
	public static int sum(int n){
		int result = 0;
		for(int i = 1; i <= n; i++){
			result += i;
		}
		return result;
	}
}
```
```java

// 使用递归，请编写程序，计算1~n的和。
public class RecursionTest03{
	public static void main(String[] args){
		// 1~3的和
		int n = 3;
		int r = sum(n);
		System.out.println(r); // 6
	}

	// 大家努力的去看，去听，自己写不出来没关系，关键是能不能看懂。
	// 单独编写一个计算1~n和的方法
	// 这个代码修改为递归的方式。
	// 3 + 2 + 1
	public static int sum(int n){
		//n最初等于3
		// 3 + 2 (2是怎么的出来的：n - 1)
		//sum(n - 1); 
		if(n == 1){
			return 1;
		}
		// 程序能执行到此处说明n不是1
		return n + sum(n-1);
	}
}
```
```java
// 使用递归的方式计算N的阶乘
// 5的阶乘：5 * 4 * 3 * 2 * 1

// 用递归的方式实现一个。
// 使用for循环的方式实现一个。
public class RecursionTest04{

	public static void main(String[] args){
		int n = 5;
		int jieGuo = jieCheng(n);
		System.out.println(jieGuo); // 120

		System.out.println(jieCheng2(5));
	}

	public static int jieCheng2(int n){
		int result = 1;
		for(int i = 2; i <= n; i++){
			result *= i;
		}
		return result;
	}

	public static int jieCheng(int n){
		// 5 * 4 * 3 * 2 * 1
		if(n == 1){
			return 1;
		}
		/*
		int result = n * jieCheng(n - 1);
		return result;
		*/

		return n * jieCheng(n - 1);
	}
}
```
### 方法调用时的参数传递
```java
// 分析程序的输出结果。
// java中规定：参数传递的时候，和类型无关，不管是基本数据类型还是引用数据类型
// 统一都是将盒子中保存的那个“值”复制一份，传递下去。

// java中只有一个规定：参数传递的时候，一定是将“盒子”中的东西复制一份传递过去。

// 内存地址也是值，也是盒子中保存的一个东西。
public class Test1{
	public static void main(String[] args){

		int x = 100;
		int y = x; // x赋值给y，是怎么传递的？将x变量中保存的100这个值复制一份传给y

		// 局部变量，域是main
		int i = 10;
		// 将i变量中保存的10复制一份，传给add方法。
		add(i); 
		System.out.println("main ---> " + i); //10
	}

	/*
	public static void add(int i){ // i是局部变量，域是add
		i++;
		System.out.println("add ----> " + i); //11
	}
	*/

	public static void add(int k){ 
		k++;
		System.out.println("add ----> " + k); 
	}
}

```
```java

/*
	java中关于方法调用时参数传递实际上只有一个规则：
		不管你是基本数据类型，还是引用数据类型，实际上在传递的时候都是
		将变量中保存的那个“值”复制一份，传过去。

		int x = 1;
		int y = x; 把x中保存1复制一份传给y
		x和y都是两个局部变量。

		Person p1 = 0x1234;
		Person p2 = p1; 把p1中保存的0x1234复制一份传给p2
		p1和p2都是两个局部变量。

		你和你媳妇，都有你家大门上的钥匙，钥匙是两把。
		但是都可以打开你家的大门。

*/

public class Test2{
	public static void main(String[] args){
		Person p = new Person();
		p.age = 10;
		add(p);
		System.out.println("main--->" + p.age); //11
	}
	// 方法的参数可以是基本数据类型，也可以是引用数据类型，只要是合法的数据类型就行。
	public static void add(Person p){ // p是add方法的局部变量。
		p.age++;
		System.out.println("add--->" + p.age); //11
	}
}

class Person{
	// 年龄属性，成员变量中的实例变量。
	int age;
}
```
### 
## 类
```java
/*
1、观察学生对象的共同特征（只观察属性）
	有哪些共同特征：
		学号：采用int类型
		姓名：采用String类型
		年龄：采用int类型
		性别：采用char或者boolean类型
		住址：采用String类型

		注意：属性是成员变量。
		
2、以上是分析总结的结果，可以开始写代码了：
	定义XueSheng类，编写成员变量作为属性。

3、变量有一个特点：
	必须先声明，再赋值，才能访问。
	成员变量可以不手动赋值？？？？？？？？？？

XueSheng既是一个类名，同时又是一个“类型名”，属于引用数据类型。
*/
public class XueSheng{ // 这个程序编译之后，会生成XueSheng.class字节码文件。

	// 属性

	// 学号（成员变量）
	int xueHao;
	
	

	// 姓名
	String xingMing;

	// 年龄
	int nianLing;

	// 性别
	boolean xingBie;

	// 住址
	String zhuZhi;

}
```
```java

/*
	对象的创建和使用。
*/
public class XueShengTest{
	public static void main(String[] args){

		int i = 100;
		System.out.println("i = " + i);
		
		// 在这里可以访问XueSheng类吗？
		// 当然可以。
		/*
			创建对象的语法是什么？
				目前死记硬背，先记住。后面你就理解了。
					new 类名();
			类是模板，通过一个类，是可以创建N多个对象的。
			new是一个运算符。专门负责对象的创建。

			XueSheng s1 = new XueSheng();
			和
			int i = 100;
			解释一下：
				i是变量名
				int是变量的数据类型
				100是具体的数据。
				
				s1是变量名（s1不能叫做对象。s1只是一个变量名字。）
				XueSheng是变量s1的数据类型（引用数据类型）
				new XueSheng() 这是一个对象。（学生类创建出来的学生对象。）
			
			数据类型包括两种：
				基本数据类型：byte short int long float double boolean char
				引用数据类型：String、XueSheng.....

			java中所有的“类”都属于引用数据类型。

		*/
		XueSheng s1 = new XueSheng(); // 和 int i = 10;一个道理。

		// 再通过该类创建一个全新的对象
		XueSheng s2 = new XueSheng();

		// 再创建一个呢？
		XueSheng xsh = new XueSheng();

		// 以上的这个程序就相当于通过XueSheng类实例化了3个XueSheng对象。
		// 创建对象的个数没有限制，可以随意。只要有模板类就行。
		// 3个对象都属于学生类型。

	}
}

```
### 对象
```java
// 住址类
public class Address{

	// 一个家庭住址有3个属性。

	// 城市
	String city; // 实例变量

	// 街道
	String street;

	// 邮编
	String zipcode;
}
```
```java
public class User{

	// 类=属性+方法
	// 以下3个都是属性，都是实例变量。（对象变量。）

	// 用户id
	// int是一种基本数据类型
	int id; // 实例变量

	// 用户名
	// String是一种引用数据类型
	String username; // 实例变量

	// 家庭住址
	// Address是一种引用数据类型
	// addr是成员变量并且还是一个实例变量
	// addr是否是一个引用呢？是。addr是一个引用。
	Address addr; 
}

// 实例变量都存储在哪里？
// 实例变量都在堆内存的对象内部。

// 方法体外，类体内定义的变量叫做：成员变量。
```
```java

/*
	到目前为止，如果什么也没听懂，怎么写代码？
		记住一个知识点就行，可以后期慢慢学习画图。
			记住一句话：里面有什么就能“点”什么。

			所有的实例变量（属性）都是通过“引用.”来访问的。
	
	引用和对象怎么区分？
		“引用”是啥？是存储对象内存地址的一个变量。
		“对象”是啥？堆里new出来的。
	
	通俗一点：
		只要这个变量中保存的是一个对象的内存地址，那么这个变量就叫做“引用”。
	
	思考：
		引用一定是局部变量吗？
			不一定。
*/
public class Test{
	public static void main(String[] args){

		//报错了。id是实例变量，必须先创建对象，通过“引用.”的方式访问。
		/*
			User u = new User();
			u是引用。
		*/
		//System.out.println(User.id);

		

		/*
		int i = 100;
		int j = i; // 原理：会将i中保存的100复制一份，传给j变量。
		*/
		
		// 家庭住址对象
		Address a = new Address();
		a.city = "北京";
		a.street = "大兴区";
		a.zipcode = "121221";
		
		// 用户对象
		User u = new User();
		System.out.println(u.id); // 0
		System.out.println(u.username); // null
		System.out.println(u.addr); // null

		u.id = 11111;
		u.username = "zhangsan";
		u.addr = a;

		// 思考一个问题：
		// 我想直到zhangsan他是哪个城市的，代码应该怎么写？
		System.out.println(u.username + "是"+u.addr.city+"城市的！");

		// u.addr.city 这行代码可否拆分呢？u.addr.city 节省变量。
		// 拆分成以下代码和以上效果完全相同，原理完全相同，不同的是以下代码多了两个变量。
		Address ad = u.addr;
		String zhuZhi = ad.city;

		System.out.println(zhuZhi);

		//-----------------------是否理解以下代码---------------------------
		int x = 100;
		// = 代表赋值运算，“赋值”中有一个“值”
		// x变量中的值是100. 将100复制一份给y
		// 表示：将x变量中保存的值100复制一份给y
		int y = x;

		//-----------------------是否理解以下代码---------------------------
		Address k = new Address(); // Address k = 0x1111;
		Address m = k; // 这里表示将k变量中保存的0x1111复制了一份传给了m变量。

	}
}
```
### 空指针
```java
/*
	空指针异常。（NullPointerException）

	关于垃圾回收器：GC
		在java语言中，垃圾回收器主要针对的是堆内存。
		当一个java对象没有任何引用指向该对象的时候，
		GC会考虑将该垃圾数据释放回收掉。
	
	出现空指针异常的前提条件是？
		"空引用"访问实例【对象相关】相关的数据时，都会出现空指针异常。
*/
public class NullPointerTest{
	public static void main(String[] args){
		// 创建客户对象
		Customer c = new Customer();
		// 访问这个客户的id
		System.out.println(c.id); // 0

		// 重新给id赋值
		c.id = 9521; // 终身代号
		System.out.println("客户的id是=" + c.id);

		c = null;
		// NullPointerException
		// 编译器没问题，因为编译器只检查语法，编译器发现c是Customer类型，
		// Customer类型中有id属性，所以可以：c.id。语法过了。
		// 但是运行的时候需要对象的存在，但是对象没了，尴尬了，就只能出现一个异常。
		System.out.println(c.id);
	}
}

class Customer{
	// 客户id
	int id; // 成员变量中的实例变量，应该先创建对象，然后通过“引用.”的方式访问。
}
```
```java
/*
学生类
	学号：int
	姓名：String
	年龄：int
	性别：boolean
	住址：String


变量必须先声明，再赋值才能访问。

注意：对于成员变量来说，没有手动赋值时，系统默认赋值。
赋的值都是默认值，那么默认值是什么？

类型				默认值
---------------------
byte				0
short				0
int				0
long				0L
float				0.0F
double			0.0
boolean			false
char				\u0000
引用数据类型	null

null是一个java关键字，全部小写，表示空。是引用类型的默认值。

分析：对于成员变量来说，是不是应该一个对象有一份。
	李四有李四的学号
	张三有张三的学号
	李四和张三的学号不一样。所以应该有两块不同的内存空间。

*/
public class Student{

	// 属性（描述状态），在java程序中以“成员变量”的形式存在。

	// 学号
	// 一个对象一份。
	int no; // 这种成员变量又被称为“实例变量”。

	// 姓名
	String name;

	// 年龄
	int age;

	// 性别
	boolean sex;

	// 住址
	String addr;

}

```
```java
/*
	对象的创建和使用。
*/
public class StudentTest{

	public static void main(String[] args){

		//局部变量
		//错误: 可能尚未初始化变量k
		/*
		int k;
		System.out.println(k);
		*/

		//访问学生姓名可以直接通过类名吗？
		// 学生姓名是一个实例变量。实例变量是对象级别的变量。
		// 是不是应该先有对象才能说姓名的事儿。
		// 不能通过“类名”来直接访问“实例变量”。
		//System.out.println(Student.name);
		
		// i属于局部变量吗？当然是。
		// 局部变量存储在栈内存当中。（栈主要存储局部变量。）
		//int i = 100;

		// 创建学生对象1
		// s1属于局部变量吗？当然是。
		// s1这个局部变量叫做引用
		Student s1 = new Student();
		// 怎么访问实例变量？
		// 语法：引用.实例变量名
		System.out.println(s1.no);
		System.out.println(s1.name);
		System.out.println(s1.age);
		System.out.println(s1.sex);
		System.out.println(s1.addr);

		System.out.println("-----------------------------");


		// 创建学生对象2
		// s2也是局部变量。
		// s2也叫做引用。
		Student s2 = new Student();
		System.out.println(s2.no);
		System.out.println(s2.name);
		System.out.println(s2.age);
		System.out.println(s2.sex);
		System.out.println(s2.addr);

		// 程序执行到此处我可以修改s1这个学生的学号吗？
		// 通过“=”赋值的方式将内存中实例变量的值修改一下。
		s1.no = 110;
		s1.name = "张三";
		s1.age = 20;
		s1.sex = true;
		s1.addr = "深圳宝安区";

		System.out.println("学号=" + s1.no);
		System.out.println("姓名=" + s1.name);
		System.out.println("年龄=" + s1.age);
		System.out.println("性别=" + s1.sex);
		System.out.println("住址=" + s1.addr);

		// 再次赋值
		s1.addr = "北京大兴区";
		System.out.println("住址：" + s1.addr);

	}

	public static void method(){
		// i s1 s2都是main方法中的局部变量，在这里是无法访问的。
		/*
		System.out.println(i);
		System.out.println(s1);
		System.out.println(s2);
		*/
	}
}
```
```java
// 把这个内存图画出来。一定要按照程序的执行顺序一步一步画。
public class T{
	A o1; // 成员变量中的实例变量。必须先创建对象，通过“引用”来访问。

	public static void main(String[] args){
		D d = new D();
		C c = new C();
		B b = new B();
		A a = new A();
		T t = new T();

		//这里不写代码会出现NullPointerException异常。（空指针异常。）
		c.o4 = d;
		b.o3 = c;
		a.o2 = b;
		t.o1 = a;

		// 编写代码通过t来访问d中的i
		//System.out.println(T.a); //错误的。
		System.out.println(t.o1.o2.o3.o4.i);
	}
}
class A{
	B o2;
}
class B{
	C o3;
}
class C{
	D o4;
}
class D{
	int i;
}
```
```java
/*
	User类：用户类
*/
public class User{
	// 用户id
	// 访问id不能这样：User.id （这是错误的，实例变量不能用类名访问。）
	// id的访问必须先造对象，然后对象有了，才能访问对象的id
	int id; //成员变量，实例变量（对象变量，一个对象一份。）
	// 用户名
	String username; // 成员变量可以不手动赋值，系统赋默认值。
	// 密码
	String password;
}

/*
class 人类{
	// 成员变量，实例变量，对象级别变量，先造对象才能访问。
	double 身高;
}
*/

// byte short int long float double boolean char :这些默认值偏向0，false也是0
// 引用类型：null

```
```java

// 第一步：类加载
// 第二步：调用UserTest类的main方法（方法调用要压栈。）
public class UserTest{

	// 方法体外声明的变量叫做成员变量。
	//User u1; //成员变量。（实例变量）

	public static void main(String[] args){
		//int i = 100;

		// 方法体当中声明的变量叫做局部变量
		User u1 = new User();
		// 实例变量怎么访问（属性怎么访问）？
		// 语法是：“引用.属性名”
		System.out.println(u1.id); //0
		System.out.println(u1.username); //null
		System.out.println(u1.password); //null

		u1.id = 11111;
		u1.username = "zhangsan";
		u1.password = "123";

		System.out.println(u1.id);
		System.out.println(u1.username);
		System.out.println(u1.password);
		
		User u2 = new User();
		u2.id = 22222;
		u2.username = "lisi";
		u2.password = "456";

		System.out.println(u2.id);
		System.out.println(u2.username);
		System.out.println(u2.password);
	}
}
```
```java

/*
空指针异常导致的最本质的原因是？
	空引用访问“实例相关的数据”，会出现空指针异常。

	实例相关的包括：实例变量 + 实例方法。
*/
public class NullPointerTest{
	public static void main(String[] args){
		User u = new User();
		System.out.println(u.id); // 0
		u.doSome();

		// 引用变成空null
		u = null;

		// id的访问，需要对象的存在。
		//System.out.println(u.id); // 空指针异常

		// 一个实例方法的调用也必须有对象的存在。
		//u.doSome(); // 空指针异常。
	}
}


// 类 = 属性 + 方法
// 属性描述状态
// 方法描述行为动作
class User{

	// 实例变量
	int id;

	// 实例方法（对象相关的方法，对象级别的方法，应该是一个对象级别的行为。）
	// 方法模拟的是对象的行为动作。
	public void doSome(){
		System.out.println("do some!");
	}

	// 考试的行为，由于每一个人考试之后的分数不一样，所以考试行为应该必须有对象的参与。
	public void exam(){
		
	}
}
```
## 封装
```java
//带有static的方法
//没有static的方法
//分别怎么调用？
	//带有static的方法怎么调用？通过“类名.”的方式访问。

//对象被称为实例。
//实例相关的有：实例变量、实例方法。
//实例变量是对象变量。实例方法是对象方法。
//实例相关的都需要先new对象，通过“引用.”的方式去访问。
public class MethodTest{

	/*
	public MethodTest(){
	
	}
	*/

	public static void main(String[] args){
		MethodTest.doSome();
		//类名. 可以省略（在同一个类中。）
		doSome();
		// 尝试使用“类名.”的方式访问“实例方法”
		// 错误的
		//MethodTest.doOther();
		
		// 创建对象
		MethodTest mt = new MethodTest();
		// 通过"引用."的方式访问实例方法。
		mt.doOther();

	}	

	// 带有static
	public static void doSome(){
		System.out.println("do some!");
	}

	//这个方法没有static，这样的方法被称为：实例方法。（对象方法，对象级别的方法）
	//这个没法解释，大家目前死记硬背。
	public void doOther(){
		System.out.println("do other....");
	}

}
```
```java
/*
	Person表示人类：
		每一个人都有年龄这样的属性。
		年龄age，int类型。
	
	我这里先不使用封装机制，分析程序存在什么缺点？
		Person类的age属性对外暴露，可以在外部程序中随意访问，导致了不安全。
	
	怎么解决这个问题？
		封装。
*/

// 这是没有封装的Person。
/*
public class Person{

	// 实例变量(属性)
	int age; //age属性是暴露的，在外部程序中可以随意访问。导致了不安全。

}
*/

// 尝试封装一下
// 不再对外暴露复杂的数据，封装起来
// 对外只提供简单的操作入口。
// 优点：第一数据安全了。第二调用者也方便了。
public class Person{
	// private 表示私有的，被这个关键字修饰之后，该数据只能在本类中访问。
	// 出了这个类，age属性就无法访问了。私有的。
	private int age; // 每一个人年龄值不同，对象级别的属性。

	// 对外提供简单的访问入口(电视机的遥控器就相当于是电视机的访问入口，简单明了。)
	// 外部程序只能通过调用以下的代码来完成访问
	// 思考：你应该对外提供几个访问入口?
	// 思考：这些操作入口是否应该是方法呢？
	// 写一个方法专门来完成读。(get)
	// 写一个方法专门来完成写。(set)
	// get和set方法应该带有static，还是不应该有static,get和set方法应该定义为实例方法吗？
	// get读年龄，set改年龄，这个读和改都是操作的一个对象的年龄。（没有对象何来年龄）
	// 封装的第二步：对外提供公开的set方法和get方法作为操作入口。并且都不带static。都是实例方法。
	/*
		[修饰符列表] 返回值类型 方法名(形式参数列表){
		}

		注意：
			java开发规范中有要求，set方法和get方法要满足以下格式。
				get方法的要求：
					public 返回值类型 get+属性名首字母大写(无参){
						return xxx;
					}
				set方法的要求：
					public void set+属性名首字母大写(有1个参数){
						xxx = 参数;
					}
			
			大家尽量按照java规范中要求的格式提供set和get方法。
			如果不按照这个规范格式来，那么你的程序将不是一个通用的程序。

	*/
	// get方法
	public int getAge(){
		return age;
	}

	// set方法
	public void setAge(int nianLing){
		// 能不能在这个位置上设置关卡！！！！
		if(nianLing < 0 || nianLing > 150){
			System.out.println("对不起，年龄值不合法，请重新赋值！");
			return; //直接终止程序的执行。
		}
		//程序能够执行到这里，说明年龄一定是合法的。
		age = nianLing;
	}

}
```
```java

// 在外部程序中访问Person这个类型中的数据。
public class PersonTest{
	public static void main(String[] args){
		// 创建Person对象
		Person p1 = new Person();
		// 访问人的年龄
		// 访问一个对象的属性，通常包括两种操作，一种是读数据，一种是改数据。
		// 读数据
		System.out.println(p1.age); //读（get表示获取）

		// 修改数据（set表示修改/设置）
		p1.age = 50;
		
		//再次读取
		System.out.println(p1.age);

		// 在PersonTest这个外部程序中目前是可以随意对age属性进行操作的。
		// 一个人的年龄值不应该为负数。
		// 程序中给年龄赋值了一个负数，按说是不符合业务要求的，但是程序目前还是让它通过了。
		// 其实这就是一个程序的bug。
		p1.age = -100; //改（随意在这里对Person内部的数据进行访问，导致了不安全。）
		System.out.println("您的年龄值是：" + p1.age); //读
	}
}
```
```java
public class PersonTest02{
	public static void main(String[] args){
		// 创建对象
		Person p1 = new Person();

		// Person的age，彻底在外部不能访问了。但是这难免有点太安全了。
		// age不能访问，这个程序就意义不大了。
		/*
		// 读age属性的值
		System.out.println(p1.age);

		// 修改age属性的值
		p1.age = 20;

		// 读age
		System.out.println(p1.age);
		*/

		// 通过“类名.”可以调用set和get方法吗？不行。
		// 只有方法修饰符列表中有static的时候，才能使用“类名.”的方式访问
		// 错误的。
		//Person.getAge();

		//读调用getAge()方法
		//int nianLing = p1.getAge();
		//System.out.println(nianLing); //0
		//以上代码联合
		System.out.println(p1.getAge()); //0

		//改调用setAge()方法
		p1.setAge(20);

		System.out.println(p1.getAge()); //20

		// 你折腾半天了，这不是结果还是没控制住吗？？？？？？
		p1.setAge(-100);
		//System.out.println(p1.getAge()); // -100
		System.out.println(p1.getAge()); // 20

	}
}
```
### 构造方法
```java
/*
	构造方法
		1、什么是构造方法，有什么用？
			构造方法是一个比较特殊的方法，通过构造方法可以完成对象的创建，
			以及实例变量的初始化。换句话说：构造方法是用来创建对象，并且
			同时给对象的属性赋值。（注意：实例变量没有手动赋值的时候，系统
			会赋默认值。）

		2、重点（需要记忆）：当一个类没有提供任何构造方法，系统会默认提供
		一个无参数的构造方法。（而这个构造方法被称为缺省构造器。）

		3、调用构造方法怎么调用呢？
			使用哪个运算符呢？
				使用new运算符来调用构造方法。
				语法格式：
					new 构造方法名(实际参数列表);
		
		4、构造方法的语法结构是？

			[修饰符列表] 构造方法名(形式参数列表){
				构造方法体;
				通常在构造方法体当中给属性赋值，完成属性的初始化。
			}

			注意：
				第一：修饰符列表目前统一写：public。千万不要写public static。

				第二：构造方法名和类名必须一致。

				第三：构造方法不需要指定返回值类型，也不能写void，写上void
				表示普通方法，就不是构造方法了。

			普通方法的语法结构是？
				[修饰符列表] 返回值类型 方法名(形式参数列表){
					方法体;
				}
*/
public class ConstructorTest01{
	public static void main(String[] args){

		// 调用Student类的无参数构造方法
		new Student();

		// 调用普通方法
		ConstructorTest01.doSome();
		doSome();

		// 创建Student类型的对象
		Student s1 = new Student();

		// 输出“引用”
		//只要输出结果不是null，说明这个对象一定是创建完成了。
		// 此处的输出结果大家目前是看不懂的，后期再说。
		System.out.println(s1); //Student@54bedef2

		// 这是调用另一个有参数的构造方法。
		Student s3 = new Student(100);
		System.out.println(s3); //Student@5caf905d
	}

	public static void doSome(){
		System.out.println("do some!!!!");
	}
}
```
```java
public class Student{

	// 学号
	int no;

	// 姓名
	String name;

	// 年龄
	int age;

	// 当前的Student这个类当中并没有定义任何构造方法。
	// 但是系统实际上会自动给Student类提供一个无参数的构造方法。
	// 将无参数的构造方法（缺省构造器）写出来
	public Student(){
		System.out.println("无参数的构造方法执行了！");
	}

	// 定义一个有参数的构造方法
	public Student(int i){
	
	}

	/*
		编译器检测到该方法名“Studen”，发现这个名字和类名不一致，
		编译器会认为该方法是一个普通方法，普通方法应该有返回值
		但是没有写返回值类型，所以报错了。
		 错误: 方法声明无效; 需要返回类型
	*/
	/*
	public Studen(String name){
	
	}
	*/

	// 第一种修改方式
	//public void Studen(String name){}

	// 第二种修改方式
	public Student(String name){
	
	}
}
```
```java

/*
	1、id,name,age都有默认值对吗？
		对。

	2、id的默认值是：0 
	name的默认值是：null
	age的默认值是：0
	
	3、思考：实例变量没有手动赋值的时候，实际上系统会默认赋值，
	那么这个默认赋值操作是在什么时间进行的？
		是在类加载的时候给这些实例变量赋值吗？
			不是，实例变量是在构造方法执行的过程中完成初始化的，完成赋值的。
*/
public class User{
	// 3个属性，3个实例变量【对象变量】
	// 用户id
	int id; //System.out.println(User.id);错误的。需要先new对象，只有对象有了才能谈id

	// 用户名
	String name;

	// 年龄
	int age;

	// 手动定义有参数的构造方法，无参数构造方法将消失。
	public User(int a){

	}

	public User(){
		//这里实际上有三行代码你看不见。
		// 无参数构造方法体当中虽然什么代码都没写，
		// 但是实际上是在这个方法体里面进行的实例变量默认值初始化
		/*
		id = 0;
		name = null;
		age = 0;
		*/
		
		// 这就表示不再采用系统默认值，手动赋值了。
		id = 111;
		name = "lisi";
		age = 30;

	}
}
```
```java
public class Vip{

	// 会员号
	long no;

	// 会员姓名
	String name;

	// 生日
	String birth;

	// 性别
	boolean sex;

	//无参数构造方法
	public Vip(){

	}

	//有参数构造方法
	public Vip(long huiYuanHao, String xingMing){
		// 给实例变量赋值【初始化实例变量，初始化属性】
		no = huiYuanHao;
		name = xingMing;
		// 实际上这里还有两行代码（没有手动赋值，系统都会默认赋值。）
		//birth = null;
		//sex = false;
	}

	//有参数构造方法
	public Vip(long huiYuanHao,String xingMing, String shengRi){
		no = huiYuanHao;
		name = xingMing;
		birth = shengRi;
		// 实际上这里有一行默认的代码
		//sex = false;
	}

	//有参数的构造方法
	public Vip(long huiYuanHao,String xingMing,String shengRi,boolean xingBie){
		no = huiYuanHao;
		name = xingMing;
		birth = shengRi;
		sex = xingBie;
	}
}
```
```java

/*
	1、构造方法对应的英语单词：Constructor【构造器】
	2、构造方法作用：
		创建对象，并且创建对象的过程中给属性赋值（初始化。）
*/
public class ConstructorTest02{
	public static void main(String[] args){

		User u = new User();

		System.out.println(u.id); //111
		System.out.println(u.name); //lisi
		System.out.println(u.age); //30

		User u2 = new User(1111111);
		System.out.println(u2.id); //0
		System.out.println(u2.name); // null
		System.out.println(u2.age); // 0
	}
}
```
```java
public class ConstructorTest03{
	public static void main(String[] args){
		//调用不同的构造方法创建对象
		Vip v1 = new Vip();
		System.out.println(v1.no); //0
		System.out.println(v1.name); // null
		System.out.println(v1.birth); // null
		System.out.println(v1.sex); // false

		Vip v2 = new Vip(11111L, "大灰狼");
		System.out.println(v2.no); // 11111L
		System.out.println(v2.name); // "大灰狼"
		System.out.println(v2.birth); // null
		System.out.println(v2.sex); // false

		Vip v3 = new Vip(22222L, "小绵羊", "2000-10-10");
		System.out.println(v3.no); // 22222L
		System.out.println(v3.name); //"小绵羊"
		System.out.println(v3.birth); // "2000-10-10"
		System.out.println(v3.sex); // false

		Vip v4 = new Vip(33333L, "钢铁侠", "1980-10-11", true);
		System.out.println(v4.no); // 33333L
		System.out.println(v4.name); //"钢铁侠"
		System.out.println(v4.birth); //"1980-10-11"
		System.out.println(v4.sex); //true
	}

}
```
```java

//构造方法、构造器、Constructor【构造函数】
// 只能用new来调用构造方法。
public class Student{

	String no;
	String name;

	// 无参数的构造方法
	public Student(){
	}
	public Student(String s){
		no = s;
	}
	/*
	public Student(String mingZi){
		name = mingZi;
		
	}
	*/
	public Student(String s1, String s2){
		no = s1;
		name = s2;
	}
}

//构造方法两个作用：创建对象  给属性赋值。

class StudentTest{
	public static void main(String[] args){
		Student s = new Student();
		Student s1 = new Student("100");
	}
}
```
## static关键字
```java
/*
	static:
		1、static翻译为“静态”
		2、所有static关键字修饰的都是类相关的，类级别的。
		3、所有static修饰的，都是采用“类名.”的方式访问。
		4、static修饰的变量：静态变量
		5、static修饰的方法：静态方法
	
	变量的分类：
		变量根据声明的位置进行划分：
			在方法体当中声明的变量叫做：局部变量。
			在方法体外声明的变量叫做：成员变量。
		
		成员变量又可以分为：
			实例变量
			静态变量
*/

class VarTest{

	// 以下实例的，都是对象相关的，访问时采用“引用.”的方式访问。需要先new对象。
	// 实例相关的，必须先有对象，才能访问，可能会出现空指针异常。
	// 成员变量中的实例变量
	int i;

	// 实例方法
	public void m2(){
		// 局部变量
		int x = 200;
	}


	// 以下静态的，都是类相关的，访问时采用“类名.”的方式访问。不需要new对象。
	// 不需要对象的参与即可访问。没有空指针异常的发生。
	// 成员变量中的静态变量
	static int k;

	// 静态方法
	public static void m1(){
		// 局部变量
		int m = 100;
	}
	
}
```
```java
/*
	什么时候变量声明为实例的，什么时候声明为静态的？
		如果这个类型的所有对象的某个属性值都是一样的，
		不建议定义为实例变量，浪费内存空间。建议定义
		为类级别特征，定义为静态变量，在方法区中只保留
		一份，节省内存开销。
	
	一个对象一份的是实例变量。
	所有对象一份的是静态变量。
*/
/*
public class StaticTest02{
	public static void main(String[] args){
		Chinese c1 = new Chinese("1231456456456456","张三","中国");
		System.out.println(c1.idCard);
		System.out.println(c1.name);
		System.out.println(c1.country);

		Chinese c2 = new Chinese("7897897896748564","李四","中国");
		System.out.println(c2.idCard);
		System.out.println(c2.name);
		System.out.println(c2.country);
	}
}

// 定义一个类：中国人
class Chinese{

	// 身份证号
	// 每一个人的身份证号不同，所以身份证号应该是实例变量，一个对象一份。
	String idCard; 

	// 姓名
	// 姓名也是一个人一个姓名，姓名也应该是实例变量。
	String name;

	// 国籍
	// 对于“中国人”这个类来说，国籍都是“中国”，不会随着对象的改变而改变。
	// 显然国籍并不是对象级别的特征。
	// 国籍属于整个类的特征。整个族的特征。
	// 假设声明为实例变量，内存图是怎样的？
	// 假设声明为静态变量，内存图又是怎样的?
	String country;

	// 无参数
	public Chinese(){
	
	}

	// 有参数
	public Chinese(String s1,String s2, String s3){
		idCard = s1;
		name = s2;
		country = s3;
	}
}
*/

public class StaticTest02{
	public static void main(String[] args){
		// 访问中国人的国籍
		// 静态变量应该使用类名.的方式访问
		System.out.println(Chinese.country);

		Chinese c1 = new Chinese("1231456456456456","张三");
		System.out.println(c1.idCard);
		System.out.println(c1.name);

		Chinese c2 = new Chinese("7897897896748564","李四");
		System.out.println(c2.idCard);
		System.out.println(c2.name);

		// idCard是实例变量，必须先new对象，通过“引用.” 访问
		// 错误: 无法从静态上下文中引用非静态 变量 idCard
		//System.out.println(Chinese.idCard);
	}
}

// 定义一个类：中国人
class Chinese{

	// 身份证号
	// 每一个人的身份证号不同，所以身份证号应该是实例变量，一个对象一份。
	String idCard; 

	// 姓名
	// 姓名也是一个人一个姓名，姓名也应该是实例变量。
	String name;

	// 国籍
	// 重点重点五颗星：加static的变量叫做静态变量
	// 静态变量在类加载时初始化，不需要new对象，静态变量的空间就开出来了。
	// 静态变量存储在方法区。
	static String country = "中国";

	// 无参数
	public Chinese(){
	
	}

	// 有参数
	public Chinese(String s1,String s2){
		idCard = s1;
		name = s2;
	}
}
```
```java

/*
	实例的：一定需要使用“引用.”来访问。

	静态的：
		建议使用“类名.”来访问，但使用“引用.”也行（不建议使用"引用."）。
		静态的如果使用“引用.”来访问会让程序员产生困惑：程序员以为是实例的呢。
	
	结论：
		空指针异常只有在什么情况下才会发生呢?
			只有在“空引用”访问“实例”相关的，都会出现空指针异常。
*/
public class StaticTest03{
	public static void main(String[] args){
		// 通过"类名."的方式访问静态变量
		System.out.println(Chinese.country);
		// 创建对象
		Chinese c1 = new Chinese("1111111", "张三");
		System.out.println(c1.idCard); // 1111111
		System.out.println(c1.name); // 张三
		System.out.println(c1.country); // 中国

		// c1是空引用
		c1 = null;
		// 分析这里会不会出现空指针异常？
		// 不会出现空指针异常。
		// 因为静态变量不需要对象的存在。
		// 实际上以下的代码在运行的时候，还是：System.out.println(Chinese.country);
		System.out.println(c1.country);

		// 这个会出现空指针异常，因为name是实例变量。
		//System.out.println(c1.name);
	}
}

class Chinese{

	// 实例变量
	String idCard;
	String name;

	// 静态变量
	static String country = "中国";

	//构造方法
	public Chinese(String x, String y){
		idCard = x;
		name = y;
	}
}
```
```java

public class StaticTest04{
	public static void main(String[] args){

		// 这是比较正规的方式，静态方法采用“类名.”
		StaticTest04.doSome();

		//对象
		StaticTest04 st = new StaticTest04();
		// 用“引用.”访问
		st.doSome();

		// 空引用
		st = null;
		// 不会出现空指针异常
		st.doSome(); // 这个代码在最终执行的时候还是会转变为：StaticTest04.doSome();

		// 实例方法doOther()
		// 对象级别的方法（先new对象，通过“引用.”来访问）
		//错误: 无法从静态上下文中引用非静态 方法 doOther()
		//StaticTest04.doOther();

		StaticTest04 st2 = new StaticTest04();
		st2.doOther();

		// 空引用
		st2 = null;
		// 空引用调用实例方法会出现什么问题？空指针异常。
		//st2.doOther();

	}

	// 静态方法（静态方法不需要new对象，直接使用“类名.”来访问）
	// 但是也可以使用“引用.”来访问，不建议用。（因为其他程序员会感到困惑。）
	public static void doSome(){
		System.out.println("静态方法doSome()执行了！");
	}

	// 实例方法（实例相关的都需要new对象，使用"引用."来访问。）
	public void doOther(){
		System.out.println("实例方法doOther执行了！");
	}
}

// 从第一天开始讲解HelloWorld到目前为止，一个类当中一共就写过这些东西。
/*
类{
	// 实例相关的都是需要new对象的，通过"引用."访问。
	实例变量;
	实例方法;

	// 静态相关的都是采用“类名.”访问。也可以使用“引用.”，只不过不建议。
	静态变量;
	静态方法;
}
*/
```
```java
/*
	关于方法来说，什么时候定义为实例方法？什么时候定义为静态方法？
		有没有参考标准。

		此方法一般都是描述了一个行为，如果说该行为必须由对象去触发。
		那么该方法定义为实例方法。

		参考标准：
			当这个方法体当中，直接访问了实例变量，这个方法一定是实例方法。

			我们以后开发中，大部分情况下，如果是工具类的话，工具类当中的方法
			一般都是静态的。(静态方法有一个优点，是不需要new对象，直接采用类名
			调用，极其方便。工具类就是为了方便，所以工具类中的方法一般都是static的。)

			什么是工具类？？？？？
				以后讲。（工具类就是为了方便编程而开发的一些类。）
	
	类 = 属性 + 方法
		属性描述的是：状态
		方法描述的是：行为动作
	
	一个方法代表了一个动作。

	什么时候方法定义为实例方法？
		张三考试，得分90
		李四考试，得分100
		不同的对象参加考试的结果不同。
		我们可以认定“考试”这个行为是与对象相关的行为。
		建议将“考试”这个方法定义为实例方法。
*/
public class StaticTest05{
	public static void main(String[] args){
		User u = new User();
		System.out.println(u.getId()); //0

		//User.getId();

		User.printName2();

		User x = new User();
		x.printName1();

		// 访问T的id怎么访问
		/*
		T t = new T();
		System.out.println(t.id);
		*/

		User y = new User();
		y.printName1();
	}
}

class T{
	// 实例变量
	int id;
}

// 我之前怎么说的？实例变量访问的语法机制是什么？
// 语法：引用.实例变量名
class User{

	// 实例变量，需要对象
	private int id;

	// 实例变量
	private String name; // 首先先分析的是，这个name是对象级别的，一个对象一份。

	//分析这个方法应该定义为实例方法还是静态方法呢？
	// 打印用户的名字这样的一个方法。
	public void printName1(){ 
		System.out.println(name);
	}

	public static void printName2(){
		// 输出的是一个对象的name
		//System.out.println(name);
	}

	public void setId(int i){
		id = i;
	}

	public int getId(){
		return id;
	}

	/*
	public static int getId(){
		return id;
	}
	*/
}
```
```java
public class StaticTest06{

	// 静态代码块（特殊的时机：类加载时机。）
	static {
		System.out.println("A");
	}

	// 一个类当中可以编写多个静态代码块
	static {
		System.out.println("B");
	}

	// 入口
	public static void main(String[] args){
		System.out.println("Hello World!");
	}

	// 编写一个静态代码块
	static{
		System.out.println("C");
	}
}

```
```java
/*
	栈：方法只要执行，会压栈。（局部变量）
	堆：new出来的对象都在堆中。垃圾回收器主要针对。（实例变量）
	方法区：类的信息，字节码信息，代码片段。（静态变量）

	方法的代码片段放在方法区，但是方法执行过程当中需要的内存在栈中。
*/
public class StaticTest07{
	
	// 静态变量在什么时候初始化？类加载时初始化。
	// 静态变量存储在哪里？方法区
	static int i = 100;

	// 静态代码块什么时候执行？类加载时执行。
	static {
		// 这里可以访问i吗？
		System.out.println("i = " + i);
	}

	// 实例变量
	int k = 111; // k变量是实例变量，在构造方法执行时内存空间才会开辟。

	static {
		//k变量可以访问吗？
		// static静态代码块在类加载时执行，并且只执行一次。
		// 类加载时，k变量空间还没有开辟出来呢。
		//错误: 无法从静态上下文中引用非静态 变量 k
		//System.out.println("k = " + k);

		// 这里可以访问name吗？
		//错误: 非法前向引用
		// 静态代码块和静态变量都在类加载的时候执行，时间相同，只能靠代码的顺序来决定谁先谁后。
		//System.out.println("name = " + name);
	}

	// 静态变量在静态代码块下面。
	static String name = "zhangsan";


	//入口(main方法执行之前实际上执行了很多代码)
	public static void main(String[] args){
		System.out.println("main begin");
		System.out.println("main over");
	}
}
```
```java
//判断以下程序的执行顺序
public class CodeOrder{
	
	// 静态代码块
	static{
		System.out.println("A");
	}

	// 入口
	// A X Y C B Z
	public static void main(String[] args){
		System.out.println("Y");
		new CodeOrder();
		System.out.println("Z");
	}

	// 构造方法
	public CodeOrder(){
		System.out.println("B");
	}

	// 实例语句块
	{
		System.out.println("C");
	}

	// 静态代码块
	static {
		System.out.println("X");
	}

}
```

```java
public class InstanceCode{

	//入口
	public static void main(String[] args){
		System.out.println("main begin");
		new InstanceCode();
		new InstanceCode();

		new InstanceCode("abc");
		new InstanceCode("xyz");
	}


	//实例语句块
	{
		System.out.println("实例语句块执行！");	
	}

	// Constructor
	public InstanceCode(){
		System.out.println("无参数构造方法");
	}

	// Constructor
	public InstanceCode(String name){
		System.out.println("有参数的构造方法");
	}

}
```
## this关键字
```java
/*
	this：
		1、this是一个关键字，全部小写。
		2、this是什么，在内存方面是怎样的？
			一个对象一个this。
			this是一个变量，是一个引用。this保存当前对象的内存地址，指向自身。
			所以，严格意义上来说，this代表的就是“当前对象”
			this存储在堆内存当中对象的内部。

		3、this只能使用在实例方法中。谁调用这个实例方法，this就是谁。
		所以this代表的是：当前对象。

		4、“this.”大部分情况下是可以省略的。

		5、为什么this不能使用在静态方法中？？？？？？
			this代表当前对象，静态方法中不存在当前对象。
*/
public class ThisTest01{
	public static void main(String[] args){

		Customer c1 = new Customer("张三");
		c1.shopping();

		Customer c2 = new Customer("李四");
		c2.shopping();

		Customer.doSome();
	}
}

// 顾客类
class Customer{

	// 属性
	// 实例变量（必须采用“引用.”的方式访问）
	String name;   

	//构造方法
	public Customer(){
	
	}
	public Customer(String s){
		name = s;
	}

	// 顾客购物的方法
	// 实例方法
	public void shopping(){
		// 这里的this是谁？this是当前对象。
		// c1调用shopping(),this是c1
		// c2调用shopping(),this是c2
		//System.out.println(this.name + "正在购物!");

		// this. 是可以省略的。
		// this. 省略的话，还是默认访问“当前对象”的name。
		System.out.println(name + "正在购物!");
	}

	// 静态方法
	public static void doSome(){
		// this代表的是当前对象，而静态方法的调用不需要对象。矛盾了。
		// 错误: 无法从静态上下文中引用非静态 变量 this
		//System.out.println(this);
	}
}


class Student{

	// 实例变量，怎么访问？必须先new对象，通过“引用.”来访问。
	String name = "zhangsan";

	// 静态方法
	public static void m1(){
		//System.out.println(name);

		// this代表的是当前对象。
		//System.out.println(this.name);

		// 除非你这样
		Student s = new Student();
		System.out.println(s.name);

	}

	//为什么set和get方法是实例方法？
	public static void setName(String s){
		name = s;
	}
	public String getName(){
		return name;
	}

	// 什么时候方法定义为实例方法，什么时候定义为静态方法？
	// 如果方法中直接访问了实例变量，该方法必须是实例方法。
}
```
```java

// 分析：i变量在main方法中能不能访问？？？？

public class ThisTest02{

	// 实例变量
	int i = 100; // 这个i变量是不是必须先new对象才能访问。

	// 静态变量
	static int k = 111;

	// 静态方法
	public static void main(String[] args){
		// 错误: 无法从静态上下文中引用非静态 变量 i
		// System.out.println(i);

		// 怎么样访问i
		ThisTest02 tt = new ThisTest02();
		System.out.println(tt.i);

		// 静态变量用“类名.”访问。
		System.out.println(ThisTest02.k);

		// 类名. 能不能省略？
		// 可以
		System.out.println(k);
	}
}
```
```java
/*
	1、this除了可以使用在实例方法中，还可以用在构造方法中。
	2、新语法：通过当前的构造方法去调用另一个本类的构造方法，可以使用以下语法格式：
		this(实际参数列表);
			通过一个构造方法1去调用构造方法2，可以做到代码复用。
			但需要注意的是：“构造方法1”和“构造方法2” 都是在同一个类当中。

	3、this() 这个语法作用是什么？
		代码复用。
	
	4、死记硬背：
		对于this()的调用只能出现在构造方法的第一行。
*/
public class ThisTest04{
	public static void main(String[] args){
		// 调用无参数构造方法
		Date d1 = new Date();
		d1.detail();

		// 调用有参数构造方法
		Date d2 = new Date(2008, 8, 8);
		d2.detail();
	}
}

/*
需求：
	1、定义一个日期类，可以表示年月日信息。
	2、需求中要求：
		如果调用无参数构造方法，默认创建的日期为：1970年1月1日。
		当然，除了调用无参数构造方法之外，也可以调用有参数的构造方法来创建日期对象。
*/
class Date{ // 以后写代码都要封装，属性私有化，对外提供setter and getter
	//年
	private int year;
	//月
	private int month;
	//日
	private int day;

	// 构造方法无参
	// 调用无参数构造方法，初始化的日期是固定值。
	public Date(){
		//错误: 对this的调用必须是构造器中的第一个语句
		//System.out.println(11);
		/*
		this.year = 1970;
		this.month = 1;
		this.day = 1;
		*/
		this(1970, 1, 1);
	}
	// 构造方法有参数
	public Date(int year, int month, int day){
		this.year = year;
		this.month = month;
		this.day = day;
	}

	// 提供一个可以打印日期的方法
	public void detail(){
		//System.out.println(year + "年" + month + "月" + day + "日");
		System.out.println(this.year + "年" + this.month + "月" + this.day + "日");
	}

	//setter and getter
	public void setYear(int year){
		// 设立关卡（有时间可以设立关卡）
		this.year = year;
	}
	public int getYear(){
		return year;
	}
	public void setMonth(int month){
		// 设立关卡（有时间可以设立关卡）
		this.month = month;
	}
	public int getMonth(){
		return month;
	}
	public void setDay(int day){
		// 设立关卡（有时间可以设立关卡）
		this.day = day;
	}
	public int getDay(){
		return day;
	}
}
```
```java
public class Review{ // 类
	// 类加载机制中，是这样的：在程序执行之前，凡是需要加载的类全部加载到JVM当中。
	// 先完成加载才会执行main方法。
	static{
		System.out.println("Review类加载时执行！");
	}

	// 入口
	// 静态方法
	public static void main(String[] args){
		// 局部变量
		int i = 100;

		// 完成一个对象的一连串动作。
		// 一个学生在教室先学习，学习完成之后去餐厅吃饭。
		Student s1 = new Student();

		// 先学习，所有调用学习这个实例方法。
		s1.study();

		Student s2 = new Student();
	}

}

// 学生类
class Student{

	static{
		System.out.println("Student类加载时执行！");
	}

	// 学号
	private int no; // 实例变量
	// 姓名
	private String name;

	// 学生有静态变量吗？
	// 类级别的属性
	static String job = "学习";

	{
		System.out.println("实例语句块，构造方法执行一次，这里就执行一次！");
	}

	// 构造方法
	public Student(){
		// 假设调用无参数的构造方法，默认创建的学生学号是100，名字是zhangsan
		this(100, "zhangsan"); // this() 在这里也使用了。
	}
	public Student(int no, String name){
		this.no = no; // 这里使用了this
		this.name = name;
	}

	// 封装
	// setter and getter方法
	public void setName(String name){
		this.name = name;
	}
	public String getName(){
		return name;
	}
	public void setNo(int no){
		this.no = no;
	}
	public int getNo(){
		return no;
	}

	// 提供两个实例方法
	public void study(){
		// 私有的是可以在本类中访问的。在其它类中必须使用set和get方法。
		//System.out.println(this.name + "正在努力的学习!");
		//System.out.println(name + "正在努力的学习!");

		// 在实例方法中调用本类其它的实例方法。
		System.out.println(this.getName() + "正在努力的学习!");
		//System.out.println(getName() + "正在努力的学习!");

		// 方法执行到此处表示学习完成了，去吃饭。
		//this.eat();		
		// this.可以省略
		// 编译器检测到eat()方法是实例方法，会自动在eat()方法前添加 this.
		eat();
	}
	
	public void eat(){ // 实例方法
		System.out.println(this.getName() + "在餐厅吃饭呢！！！");

		// 调用静态m1()方法
		// 静态方法使用“类名.”的方式访问
		// Student.m1();

		// 类名. 可以省略吗？可以。
		// java编译器会自动在m1()方法之前添加“类名.”，因为检测到m1()方法是一个静态方法。
		m1();
	}


	// 提供两个静态方法
	public static void m1(){
		System.out.println("Student's m1 method execute!");
		// 调用m2()方法
		//Student.m2();
		m2();
	}

	public static void m2(){
		System.out.println("Student's m2 method execute!");
		System.out.println("工作性质：" + job);
		// 编译器检测到job是一个静态变量，所以这里会自动在job前添加：Student.
		//System.out.println("工作性质：" + Student.job);
	}
}

```
```java

/*
	程序再怎么变化，万变不离其宗，有一个固定的规律：
		所有的实例相关的都是先创建对象，通过“引用.”来访问。
		所有的静态相关的都是直接采用“类名.”来访问。
	
	你有发现一些问题吗？
		总有一些是需要记忆的，在这些记忆的基础之上进行分析。
	
	大结论：
		只要负责调用的方法a和被调用的方法b在同一个类当中：
			this. 可以省略
			类名. 可以省略
*/
public class Review02{

	int i = 100;

	static int j = 1000;

	public void m1(){

		// 访问其他类的静态方法
		T.t1();

		// 访问其他类的实例方法
		T t = new T();
		t.t2();
	}

	public void m2(){}

	// 实例方法
	public void x(){ // 这个方法是实例方法，执行这个方法的过程中，当前对象是存在的。
		m1();
		m2();

		m3();
		m4();

		System.out.println(i); // System.out.println(this.i);
		System.out.println(j); // System.out.println(Review02.i);
	}

	public static void m3(){}

	public static void m4(){}

	// 问？你怎么分析这个程序？
	/*
		第一步：
			main方法是静态的，JVM调用main方法的时候直接采用的是“类名.”的方式。
			所以main方法中没有this。

		第二步：
			m1() 和 m2() 方法是实例方法，按照java语法规则来说，实例方法必须先
			new对象，通过“引用.”的方式访问。
	*/
	public static void main(String[] args){
		// 编译报错。
		//m1();
		//m2();

		m3(); // 编译器会自动识别m3()静态方法，结果是：Review02.m3();
		m4(); // Review02.m4();

		//System.out.println(i); // 报错
		System.out.println(j); // 可以

		// 想访问m1() m2()还有i，你在static方法中只能自己new
		Review02 r = new Review02();
		System.out.println(r.i);
		r.m1();
		r.m2();

		// 局部变量，局部变量访问的时候是不需要“xxx.”的
		int k = 10000;
		System.out.println(k);
	}
}


class T{
	// 静态方法
	public static void t1(){
	
	}

	//实例方法
	public void t2(){
	
	}
}

```
## 继承
```java

// 使用继承机制来解决代码复用问题。
// 继承也是存在缺点的：耦合度高，父类修改，子类受牵连。
public class ExtendsTest02{
	public static void main(String[] args){
		// 创建普通账户
		Account act = new Account();
		act.setActno("1111111");
		act.setBalance(10000);
		System.out.println(act.getActno() + ",余额" + act.getBalance());

		// 创建信用账户
		CreditAccount ca = new CreditAccount();
		ca.setActno("2222222");
		ca.setBalance(-10000);
		ca.setCredit(0.99);
		System.out.println(ca.getActno() + ",余额" + ca.getBalance() + ",信誉度" + ca.getCredit());
	}
}

// 银行账户类
// 账户的属性：账号、余额
class Account{ // 父类
	// 属性
	private String actno;
	private double balance;

	// 构造方法
	public Account(){
	
	}
	public Account(String actno, double balance){
		this.actno = actno;
		this.balance = balance;
	}

	// setter and getter
	public void setActno(String actno){
		this.actno = actno;
	}
	public String getActno(){
		return actno;
	}
	public void setBalance(double balance){
		this.balance = balance;
	}
	public double getBalance(){
		return balance;
	}
}

// 其它类型的账户：信用卡账户
// 账号、余额、信誉度
class CreditAccount extends Account{ //子类

	// 属性
	private double credit;

	// 构造方法
	public CreditAccount(){
	
	}

	public void doSome(){
		//错误: actno 在 Account 中是 private 访问控制
		//System.out.println(actno);
		// 间接访问
		//System.out.println(this.getActno());
		System.out.println(getActno());
	}

	// setter and getter方法
	public void setCredit(double credit){
		this.credit = credit;
	}
	public double getCredit(){
		return credit;
	}
	
}
```
```java
/*
测试：子类继承父类之后，能使用子类对象调用父类方法吗
	实际上以上的这个问题问的有点蹊跷！！！！！
	哪里蹊跷？“能使用子类对象调用父类方法”
	本质上，子类继承父类之后，是将父类继承过来的方法归为自己所有。
	实际上调用的也不是父类的方法，是他子类自己的方法（因为已经继承过来了
	就属于自己的。）。
		
*/
public class ExtendsTest04{
	public static void main(String[] args){
		// 创建子类对象
		Cat c = new Cat();
		// 调用方法
		c.move();
		// 通过子类对象访问name可以吗？
		System.out.println(c.name);
	}
}

// 父类
//class Animal extends Object {
class Animal{
	// 名字（先不封装）
	String name = "XiaoHua"; //默认值不是null，给一个XiaoHua

	// 提供一个动物移动的方法
	public void move(){
		System.out.println(name + "正在移动！");
	}
}

// Cat子类
// Cat继承Animal，会将Animal中所有的全部继承过来。
class Cat extends Animal{
}
```
```java

// editPlus中蓝色是关键字
// 黑色是标识符
// System.out.println("Hello World!"); 
// 以上代码中：System、out、println都是标识符。
// 在 editplus中的红色字体，表示这个类是SUN的JDK写好的一个类。
public class Test{

	// 静态变量
	static Student stu = new Student();

	// 入口
	public static void main(String[] args){
		
		//拆分为两行
		Student s = Test.stu;
		s.exam();

		//合并代码
		Test.stu.exam();

		System.out.println("Hello World!");
	}
}

class Student{

	// 实例方法
	public void exam(){
		System.out.println("考试。。。。。");
	}
}
```
## 方法覆盖
```java
/*
	回顾一下方法重载！！！！
		什么时候考虑使用方法重载overload？
			当在一个类当中，如果功能相似的话，建议将名字定义的一样，这样
			代码美观，并且方便编程。
		
		什么条件满足之后能够构成方法重载overload？
			条件一：在同一个类当中
			条件二：方法名相同
			条件三：参数列表不同（个数、顺序、类型）

	--------------------------------------------------------------------------------

	什么时候我们会考虑使用“方法覆盖”呢？
		子类继承父类之后，当继承过来的方法无法满足当前子类的业务需求时，
		子类有权利对这个方法进行重新编写，有必要进行“方法的覆盖”。
	
	方法覆盖又叫做：方法重写（重新编写），英语单词叫做：Override、Overwrite，都可以。
	比较常见的：方法覆盖、方法重写、override

	重要结论：
		当子类对父类继承过来的方法进行“方法覆盖”之后，
		子类对象调用该方法的时候，一定执行覆盖之后的方法。

	当我们代码怎么编写的时候，在代码级别上构成了方法覆盖呢？
		条件一：两个类必须要有继承关系。
		条件二：重写之后的方法和之前的方法具有：
					相同的返回值类型、
					相同的方法名、
					相同的形式参数列表。
		条件三：访问权限不能更低，可以更高。（这个先记住。）
		条件四：重写之后的方法不能比之前的方法抛出更多的异常，可以更少。（这个先记住）
	
	这里还有几个注意事项：（这几个注意事项，当学习了多态语法之后自然就明白了！）
		注意1：方法覆盖只是针对于方法，和属性无关。
		注意2：私有方法无法覆盖。
		注意3：构造方法不能被继承，所以构造方法也不能被覆盖。
		注意4：方法覆盖只是针对于“实例方法”，“静态方法覆盖”没有意义。

*/
public class OverrideTest02{
	public static void main(String[] args){
		Bird b = new Bird();
		b.move();
		b.sing(1000); //Animal sing....

		Cat c = new Cat();
		c.move();
	}
}

class Animal{
	public void move(){
		System.out.println("动物在移动！");
	}

	public void sing(int i){
		System.out.println("Animal sing....");
	}
}

class Bird extends Animal{

	// 对move方法进行方法覆盖，方法重写，override
	// 最好将父类中的方法原封不动的复制过来。（不建议手动编写）
	// 方法覆盖，就是将继承过来的那个方法给覆盖掉了。继承过来的方法没了。
	public void move(){
		System.out.println("鸟儿在飞翔！！！");
	}

	//protected表示受保护的。没有public开放。
	// 错误：正在尝试分配更低的访问权限; 以前为public
	/*
	protected void move(){
		System.out.println("鸟儿在飞翔！！！");
	}
	*/

	//错误：被覆盖的方法未抛出Exception
	/*
	public void move() throws Exception{
		System.out.println("鸟儿在飞翔！！！");
	}
	*/

	// 分析：这个sing()和父类中的sing(int i)有没有构成方法覆盖呢？
	// 没有，原因是，这两个方法根本就是两个完全不同的方法。
	// 可以说这两个方法构成了方法重载吗？可以。
	public void sing(){
		System.out.println("Bird sing.....");
	}
}

class Cat extends Animal{

	// 方法重写
	public void move(){
		System.out.println("猫在走猫步！！！");
	}
}
```
```java
//方法覆盖比较经典的案例
//一定要注意：方法覆盖/重写的时候，建议将父类的方法复制粘贴，这样比较保险。
public class OverrideTest03{
	public static void main(String[] args){
		// 创建中国人对象
		// ChinaPeople p1 = new ChinaPeople("张三");// 错误原因：没有这样的构造方法
		ChinaPeople p1 = new ChinaPeople();
		p1.setName("张三");
		p1.speak();

		// 创建美国人对象
		// AmericPeople p2 = new AmericPeople("jack"); // 错误原因：没有这样的构造方法
		AmericPeople p2 = new AmericPeople();
		p2.setName("jack");
		p2.speak();
	}
}

// 人
class People{
	// 属性
	private String name;
	// 构造
	public People(){}
	public People(String name){
		this.name = name;
	}
	//setter and getter
	public void setName(String name){
		this.name = name;	
	}
	public String getName(){
		return name;
	}
	// 人都会说话
	public void speak(){
		System.out.println(name + "....");
	}
}

// 中国人
class ChinaPeople extends People{

	// 中国人说话是汉语
	// 所以子类需要对父类的speak()方法进行重写
	public void speak(){
		System.out.println(this.getName() + "正在说汉语");
	}
}


// 美国人
class AmericPeople extends People{
	// 美国人说话是英语
	// 所以子类需要对父类的speak()方法进行重写
	public void speak(){
		System.out.println(getName() + " speak english!");
	}
}

```
```java
/*
	关于Object类中的toString()方法
		1、toString()方法的作用是什么？
			作用：将“java对象”转换成“字符串的形式”。

		2、Object类中toString()方法的默认实现是什么？
			public String toString() {
				return getClass().getName() + "@" + Integer.toHexString(hashCode());
			}
			toString: 方法名的意思是转换成String
			含义：调用一个java对象的toString()方法就可以将该java对象转换成字符串的表示形式。

		3、那么toString()方法给的默认实现够用吗？
*/
public class OverrideTest04{
	public static void main(String[] args){
		// 创建一个日期对象
		MyDate t1 = new MyDate();
		// 调用toString()方法（将对象转换成字符串形式。）
		// 问：你对这个输出结果满意吗？不满意，希望输出：xxxx年xx月xx日
		// 重写MyDate的toString()方法之前的结果
		//System.out.println(t1.toString()); //MyDate@28a418fc 

		// 重写MyDate的toString()方法之后的结果
		System.out.println(t1.toString());

		// 大家是否还记得：当输出一个引用的时候，println方法会自动调用引用的toString方法。
		System.out.println(t1);

		MyDate t2 = new MyDate(2008, 8, 8);
		System.out.println(t2); //2008年8月8日

		//创建学生对象
		Student s = new Student(1111, "zhangsan");
		// 重写toString()方法之前
		//System.out.println(s); //Student@87aac27
		// 重写toString()方法之后
		// 输出一个学生对象的时候，可能更愿意看到学生的信息，不愿意看到对象的内存地址。
		System.out.println(s.toString());
		System.out.println(s);
	}
}

// 日期类
class MyDate {
	private int year;
	private int month;
	private int day;
	public MyDate(){
		this(1970,1,1);
	}
	public MyDate(int year,int month,int day){
		this.year = year;
		this.month = month;
		this.day = day;
	}
	public void setYear(int year){
		this.year = year;
	}
	public int getYear(){
		return year;
	}
	public void setMonth(int month){
		this.month = month;
	}
	public int getMonth(){
		return month;
	}
	public void setDay(int day){
		this.day = day;
	}
	public int getDay(){
		return day;
	}

	// 从Object类中继承过来的那个toString()方法已经无法满足我业务需求了。
	// 我在子类MyDate中有必要对父类的toString()方法进行覆盖/重写。
	// 我的业务要求是：调用toString()方法进行字符串转换的时候，
	// 希望转换的结果是：xxxx年xx月xx日，这种格式。
	// 重写一定要复制粘贴，不要手动编写，会错的。
	public String toString() {
		return year + "年" + month + "月" + day + "日";
	}
}

class Student{
	int no;
	String name;
	public Student(int no, String name){
		this.no = no;
		this.name = name;
	}
	// 重写  方法覆盖
	public String toString() {
		return "学号：" + no + "，姓名：" + name;
	}
}

```
```java
/*
	1、方法覆盖需要和多态机制联合起来使用才有意义。
		Animal a = new Cat();
		a.move();
		要的是什么效果？
			编译的时候move()方法是Animal的。
			运行的时候自动调用到子类重写move()方法上。
		
		假设没有多态机制，只有方法覆盖机制，你觉得有意义吗？
			没有多态机制的话，方法覆盖可有可无。

			没有多态机制，方法覆盖也可以没有，如果父类的方法无法满足
			子类业务需求的时候，子类完全可以定义一个全新的方法。
		
		方法覆盖和多态不能分开。

	2、静态方法存在方法覆盖吗？
		多态自然就和对象有关系了。
		而静态方法的执行不需要对象。
		所以，一般情况下，我们会说静态方法“不存在”方法覆盖。
		不探讨静态方法的覆盖。

*/
public class OverrideTest05{
	public static void main(String[] args){
		// 静态方法可以使用“引用.”来调用吗？可以
		// 虽然使用“引用.”来调用，但是和对象无关。
		Animal a = new Cat(); //多态
		// 静态方法和对象无关。
		// 虽然使用“引用.”来调用。但是实际运行的时候还是：Animal.doSome()
		a.doSome();
		
		Animal.doSome();
		Cat.doSome();
	}
}

class Animal{
	// 父类的静态方法
	public static void doSome(){
		System.out.println("Animal的doSome方法执行！");
	}
}

class Cat extends Animal{
	// 尝试在子类当中对父类的静态方法进行重写
	public static void doSome(){
		System.out.println("Cat的doSome方法执行！");
	}
}
```
```java

// 经过测试，你记住就行。
// 私有方法不能覆盖。
public class OverrideTest06{

	// 私有方法
	private void doSome(){
		System.out.println("OverrideTest06's private method doSome execute!");
	}

	// 入口
	public static void main(String[] args){
		// 多态
		OverrideTest06 ot = new T();
		ot.doSome(); //OverrideTest06's private method doSome execute!
	}
}

/*
// 在外部类中无法访问私有的。
class MyMain{
	public static void main(String[] args){
		OverrideTest06 ot = new T();
		//错误: doSome() 在 OverrideTest06 中是 private 访问控制
		//ot.doSome();
	}
}
*/

// 子类
class T extends OverrideTest06{
	// 尝试重写父类中的doSome()方法
	// 访问权限不能更低，可以更高。
	public void doSome(){
		System.out.println("T's public doSome method execute!");
	}
}
```
## 多态
```java
/*
	多态的基础语法：
		1、学习多态基础语法之前，我们需要普及两个概念：
			第一个：向上转型
				子 ---> 父（自动类型转换）
			第二个：向下转型
				父 ---> 子（强制类型转换，需要加强制类型转换符）

			注意：
				java中允许向上转型，也允许向下转型。

				*****（五颗星）无论是向上转型，还是向下转型，
						两种类型之间必须有继承关系，没有继承关系编译器报错。
				
				以后在工作过程中，和别人聊天的时候，要专业一些，说
				向上转型和向下转型，不要说自动类型转换，也不要说强制
				类型转换，因为自动类型转换和强制类型转换是使用在基本
				数据类型方面的，在引用类型转换这里只有向上和向下转型。
		
		2、多态指的是：
			父类型引用指向子类型对象。
			包括编译阶段和运行阶段。
			编译阶段：绑定父类的方法。
			运行阶段：动态绑定子类型对象的方法。
			多种形态。
		
		3、个别同学有点混乱了：
			java中只有“类名”或者“引用”才能去“点”
			类名.
			引用.
			万变不离其宗，只要你想“点”，“点”前面要么是一个类名，要么是一个引用。
		
		4、什么时候必须使用“向下转型”？
			不要随便做强制类型转换。
			当你需要访问的是子类对象中“特有”的方法。此时必须进行向下转型。
*/
public class Test01{

	public static void main(String[] args){

		Animal a1 = new Animal();
		a1.move(); //动物在移动！！！

		Cat c1 = new Cat();
		c1.move(); //cat走猫步！

		Bird b1 = new Bird();
		b1.move(); //鸟儿在飞翔！！！

		// 代码可以这样写吗？
		/*
			1、Animal和Cat之间有继承关系吗？有的。
			2、Animal是父类，Cat是子类。
			3、Cat is a Animal，这句话能不能说通？能。
			4、经过测试得知java中支持这样的一个语法：
				父类型的引用允许指向子类型的对象。
				Animal a2 = new Cat();
				a2就是父类型的引用。
				new Cat()是一个子类型的对象。
				允许a2这个父类型引用指向子类型的对象。
		*/
		Animal a2 = new Cat();
		Animal a3 = new Bird();

		
		// 没有继承关系的两个类型之间存在转型吗？
		// 错误: 不兼容的类型: Dog无法转换为Animal
		// Animal a4 = new Dog();

		// 调用a2的move()方法
		/*
			什么是多态？
				多种形态，多种状态。
			分析：a2.move();
				java程序分为编译阶段和运行阶段。
				先来分析编译阶段：
					对于编译器来说，编译器只知道a2的类型是Animal，
					所以编译器在检查语法的时候，会去Animal.class
					字节码文件中找move()方法，找到了，绑定上move()
					方法，编译通过，静态绑定成功。（编译阶段属于静态绑定。）
				再来分析运行阶段：
					运行阶段的时候，实际上在堆内存中创建的java对象是
					Cat对象，所以move的时候，真正参与move的对象是一只猫，
					所以运行阶段会动态执行Cat对象的move()方法。这个过程
					属于运行阶段绑定。（运行阶段绑定属于动态绑定。）

			多态表示多种形态：
				编译的时候一种形态。
				运行的时候另一种形态。
		*/
		a2.move(); //cat走猫步！
		
		// 调用a3的move()方法
		a3.move(); //鸟儿在飞翔！！！

		// ======================================================================
		Animal a5 = new Cat(); // 底层对象是一只猫。

		// 分析这个程序能否编译和运行呢？
		// 分析程序一定要分析编译阶段的静态绑定和运行阶段的动态绑定。
		// 只有编译通过的代码才能运行。没有编译，根本轮不到运行。
		// 错误: 找不到符号
		// why??? 因为编译器只知道a5的类型是Animal，去Animal.class文件中找catchMouse()方法
		// 结果没有找到，所以静态绑定失败，编译报错。无法运行。（语法不合法。）
		//a5.catchMouse(); 
		
		// 假设代码写到了这里，我非要调用catchMouse()方法怎么办？
		// 这个时候就必须使用“向下转型”了。（强制类型转换）
		// 以下这行代码为啥没报错？？？？
		// 因为a5是Animal类型，转成Cat，Animal和Cat之间存在继承关系。所以没报错。
		Cat x = (Cat)a5;
		x.catchMouse(); //猫正在抓老鼠！！！！

		// 向下转型有风险吗？
		Animal a6 = new Bird(); //表面上a6是一个Animal，运行的时候实际上是一只鸟儿。
		/*
			分析以下程序，编译报错还是运行报错？？？
				编译器检测到a6这个引用是Animal类型，
				而Animal和Cat之间存在继承关系，所以可以向下转型。
				编译没毛病。

				运行阶段，堆内存实际创建的对象是：Bird对象。
				在实际运行过程中，拿着Bird对象转换成Cat对象
				就不行了。因为Bird和Cat之间没有继承关系。
			
			运行是出现异常，这个异常和空指针异常一样非常重要，也非常经典：
				java.lang.ClassCastException：类型转换异常。
			
			java.lang.NullPointerException：空指针异常。这个也非常重要。
		*/
		//Cat y = (Cat)a6;
		//y.catchMouse();

		// 怎么避免ClassCastException异常的发生？？？
		/*	
			新的内容，运算符：
				instanceof （运行阶段动态判断）
			第一：instanceof可以在运行阶段动态判断引用指向的对象的类型。
			第二：instanceof的语法：
				(引用 instanceof 类型)
			第三：instanceof运算符的运算结果只能是：true/false
			第四：c是一个引用，c变量保存了内存地址指向了堆中的对象。
				假设(c instanceof Cat)为true表示:
					c引用指向的堆内存中的java对象是一个Cat。
				假设(c instanceof Cat)为false表示:
					c引用指向的堆内存中的java对象不是一个Cat。
			
			程序员要养成一个好习惯：
				任何时候，任何地点，对类型进行向下转型时，一定要使用
				instanceof 运算符进行判断。（java规范中要求的。）
				这样可以很好的避免：ClassCastException
		*/
		System.out.println(a6 instanceof Cat); //false

		if(a6 instanceof Cat){ // 如果a6是一只Cat
			Cat y = (Cat)a6;  // 再进行强制类型转换
			y.catchMouse();
		}
	}
}


```
```java
// 主人类
public class Master{

	/*
	// 假设主人起初的时候只是喜欢养宠物狗狗
	// 喂养宠物狗狗
	public void feed(Dog d){
		d.eat();
	}

	// 由于新的需求产生，导致我们“不得不”去修改Master这个类的代码
	public void feed(Cat c){
		c.eat();
	}
	*/
	
	// 能不能让Master主人这个类以后不再修改了。
	// 即使主人又喜欢养其它宠物了，Master也不需要修改。
	// 这个时候就需要使用：多态机制。
	// 最好不要写具体的宠物类型，这样会影响程序的扩展性。
	public void feed(Pet pet){ 
		// 编译的时候，编译器发现pet是Pet类，会去Pet类中找eat()方法，结果找到了，编译通过
		// 运行的时候，底层实际的对象是什么，就自动调用到该实际对象对应的eat()方法上。
		// 这就是多态的使用。
		pet.eat();
	}

}

/*

	注意这里的分析：
		主人起初的时候只喜欢养宠物狗狗
		随着时间的推移，主人又喜欢上养“猫咪”
		在实际的开发中这就表示客户产生了新的需求。
		作为软件的开发人员来说，必须满足客户的需求。
		我们怎么去满足客户的需求呢？
			在不使用多态机制的前提下，目前我们只能在Master类中添加一个新的方法。
	
	思考：软件在扩展新需求过程当中，修改Master这个类有什么问题？
		一定要记住：软件在扩展过程当中，修改的越少越好。
		修改的越多，你的系统当前的稳定性就越差，未知的风险就越多。

		其实这里涉及到一个软件的开发原则：
			软件开发原则有七大原则（不属于java，这个开发原则属于整个软件业）：
				其中有一条最基本的原则：OCP（开闭原则）

		什么是开闭原则？
			对扩展开放（你可以额外添加，没问题），对修改关闭（最好很少的修改现有程序）。
			在软件的扩展过程当中，修改的越少越好。
	

	高手开发项目不是仅仅为了实现客户的需求，还需要考虑软件的扩展性。

	什么是软件扩展性？
		假设电脑中的内存条部件坏了，我们可以买一个新的插上，直接使用。
		这个电脑的设计就考虑了“扩展性”。内存条的扩展性很好。
	
	面向父类型编程，面向更加抽象进行编程，不建议面向具体编程。
	因为面向具体编程会让软件的扩展力很差。

*/
```
```java
/*
	测试多态在开发中的作用
*/
public class Test{
	public static void main(String[] args){
		// 创建主人对象
		Master zhangsan = new Master();
		// 创建宠物对象
		Dog zangAo = new Dog();
		// 主人喂
		zhangsan.feed(zangAo);
		// 创建宠物对象
		Cat xiaoHua = new Cat();
		// 主人喂
		zhangsan.feed(xiaoHua);
		// 创建宠物对象
		YingWu yingWu = new YingWu();
		// 主人喂
		zhangsan.feed(yingWu);
	}
}
```
## super关键字
```java
/*
	1、super是一个关键字，全部小写。
	2、super和this对比着学习。
		this:
			this能出现在实例方法和构造方法中。
			this的语法是：“this.”、“this()”
			this不能使用在静态方法中。
			this. 大部分情况下是可以省略的。
			this.什么时候不能省略呢？ 在区分局部变量和实例变量的时候不能省略。
				public void setName(String name){
					this.name = name;
				}
			this() 只能出现在构造方法第一行，通过当前的构造方法去调用“本类”中
			其它的构造方法，目的是：代码复用。

		super:
			super能出现在实例方法和构造方法中。
			super的语法是：“super.”、“super()”
			super不能使用在静态方法中。
			super. 大部分情况下是可以省略的。
			super.什么时候不能省略呢？ ？？？？？？？
			super() 只能出现在构造方法第一行，通过当前的构造方法去调用“父类”中
			的构造方法，目的是：创建子类对象的时候，先初始化父类型特征。

	3、super()
		表示通过子类的构造方法调用父类的构造方法。
		模拟现实世界中的这种场景：要想有儿子，需要先有父亲。
	
	4、重要的结论：
		当一个构造方法第一行：
			既没有this()又没有super()的话，默认会有一个super();
			表示通过当前子类的构造方法调用父类的无参数构造方法。
			所以必须保证父类的无参数构造方法是存在的。
	
	5、注意：
		this()和super() 不能共存，它们都是只能出现在构造方法第一行。
	
	6、无论是怎样折腾，父类的构造方法是一定会执行的。（百分百的。）
	
*/
public class SuperTest01{
	public static void main(String[] args){
		// 创建子类对象
		/*
			A类的无参数构造方法！
			B类的无参数构造方法！
		*/
		new B();
	}
}

class A extends Object{

	// 建议手动的将一个类的无参数构造方法写出来。
	public A(){
		//super(); // 这里也是默认有这一行代码的。
		System.out.println("A类的无参数构造方法！");
	}

	// 一个类如果没有手动提供任何构造方法，系统会默认提供一个无参数构造方法。
	// 一个类如果手动提供了一个构造方法，那么无参数构造系统将不再提供。
	public A(int i){
		//super();
		System.out.println("A类的有参数构造方法(int)");
	}
}

class B extends A{
	/*
	public B(){
		super();
		System.out.println("B类的无参数构造方法！");
	}
	*/

	public B(){
		this("zhangsan");
		// 调用父类中有参数的构造方法
		//super(123);
		System.out.println("B类的无参数构造方法！");
	}

	public B(String name){
		super();
		System.out.println("B类的有参数构造方法(String)");
	}
}
```
```java

/*
	判断程序的输出结果
	1
	3
	6
	5
	4

	在java语言中不管是是new什么对象，最后老祖宗的Object类的无参数构造方法
	一定会执行。（Object类的无参数构造方法是处于“栈顶部”）

	栈顶的特点：
		最后调用，但是最先执行结束。
		后进先出原则。
	
	大家要注意：
		以后写代码的时候，一个类的无参数构造方法还是建议大家手动的写出来。
		如果无参数构造方法丢失的话，可能会影响到“子类对象的构建”。

*/
public class SuperTest02{
	public static void main(String[] args){
		new C();

	}
}

/*
class Object{
	public Object(){	
	}
}
*/

class A extends Object{
	public A(){
		System.out.println("1"); //1
	}
}

class B extends A{
	public B(){
		System.out.println("2"); //2
	}
	public B(String name){
		super();
		System.out.println("3"); // 3
	}
}

class C extends B{
	public C(){ // 这个是最先调用的。但是最后结束。
		this("zhangsan");
		System.out.println("4");//4
	}
	public C(String name){
		this(name, 20);
		System.out.println("5");//5
	}
	public C(String name, int age){
		super(name);
		System.out.println("6");//6
	}
}
```
```java
public class SuperTest04{
	public static void main(String[] args){
		Vip v = new Vip("张三");
		v.shopping();
	}
}
class Customer{
	String name;
	public Customer(){}
	public Customer(String name){
		super();
		this.name = name;
	}
}
class Vip extends Customer{
	public Vip(){}
	public Vip(String name){
		super(name);
	}
	// super和this都不能出现在静态方法中。
	public void shopping(){
		// this表示当前对象。
		System.out.println(this.name + "正在购物!");
		// super表示的是当前对象的父类型特征。（super是this指向的那个对象中的一块空间。）
		System.out.println(super.name + "正在购物!");
		System.out.println(name + "正在购物!");
	}
}

```
```java

/*
	1、“this.”和“super.”大部分情况下都是可以省略的。
	2、this. 什么时候不能省略？
		public void setName(String name){
			this.name = name;
		}
	3、super. 什么时候不能省略？
		父中有，子中又有，如果想在子中访问“父的特征”，super. 不能省略。
*/
public class SuperTest05{
	public static void main(String[] args){
		Vip v = new Vip("张三");
		v.shopping();
	}
}
class Customer {
	String name;
	public Customer(){}
	public Customer(String name){
		super();
		this.name = name;
	}

	public void doSome(){
		System.out.println(this.name + " do some!");
		System.out.println(name + " do some!");
		//错误: 找不到符号
		//System.out.println(super.name + " do some!");
	}
}
class Vip extends Customer{

	// 假设子类也有一个同名属性
	// java中允许在子类中出现和父类一样的同名变量/同名属性。
	String name; // 实例变量

	public Vip(){
	}
	public Vip(String name){
		super(name);
		// this.name = null;
	}
	public void shopping(){
		/*
			java是怎么来区分子类和父类的同名属性的？
				this.name：当前对象的name属性
				super.name：当前对象的父类型特征中的name属性。
		*/
		System.out.println(this.name + "正在购物!"); // null 正在购物
		System.out.println(super.name + "正在购物!"); // 张三正在购物
		System.out.println(name + "正在购物!"); //null 正在购物
	}
}

```
```java

/*
	在父和子中有同名的属性，或者说有相同的方法，
	如果此时想在子类中访问父中的数据，必须使用“super.”加以区分。

	super.属性名    【访问父类的属性】
	super.方法名(实参) 【访问父类的方法】
	super(实参)  【调用父类的构造方法】
*/
public class SuperTest07{
	public static void main(String[] args){
		/*
			Cat move!
			Cat move!
			Animal move!
		*/
		Cat c = new Cat();
		c.yiDong();
	}
}

class Animal{
	public void move(){
		System.out.println("Animal move!");
	}
}

class Cat extends Animal{
	// 对move进行重写。
	public void move(){
		System.out.println("Cat move!");
	}

	// 单独编写一个子类特有的方法。
	public void yiDong(){
		this.move();
		move();
		// super. 不仅可以访问属性，也可以访问方法。
		super.move();
	}
}
```
