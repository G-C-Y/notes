# SpringBoot教程
SpringBoot是由Pivotal团队提供的全新框架，其设计目的是用来简化新Spring应用的初始搭建以及开发过程。该框架使用了特定的方式来进行配置，从而使开发人员不再需要定义样板化的配置。通过这种方式，SpringBoot致力于在蓬勃发展的快速应用开发领域(rapid application development)成为领导者。
## SpringBoot简介
SpringBoot是Spring家族中的一个全新的框架，它用来简化Spring应用程序的创建和开发过程，也可以说SpringBoot能简化我们之前采用SpringMVC + Spring + MyBatis框架进行开发的过程。
在以往我们采用SpringMVC + Spring + MyBatis框架进行开发的时候，搭建和整合三大框架，我们需要做很多工作，比如配置web.xml，配置Spring，配置MyBatis，并将它们整合在一起等，而SpringBoot框架对此开发过程进行了革命性的颠覆，完全抛弃了繁琐的xml配置过程，采用大量的默认配置简化我们的开发过程。
所以采用SpringBoot可以非常容易和快速地创建基于Spring框架的应用程序，它让编码变简单了，配置变简单了，部署变简单了，监控变简单了。正因为 SpringBoot 它化繁为简，让开发变得极其简单和快速，所以在业界备受关注。
SpringBoot在国内的关注趋势图：http://t.cn/ROQLquP
## SpringBoot的特性
● 能够快速创建基于Spring的应用程序
● 能够直接使用java main方法启动内嵌的Tomcat服务器运行SpringBoot程序，不需要部署war包文件
● 提供约定的starter POM来简化Maven配置，让Maven的配置变得简单
● 自动化配置，根据项目的Maven依赖配置，Springboot自动配置Spring、Spring mvc等
● 提供了程序的健康检查等功能
● 基本可以完全不使用XML配置文件，采用注解配置
## SpringBoot四大核心
● 自动配置
针对很多Spring应用程序和常见的应用功能，SpringBoot能自动提供相关配置
● 起步依赖
告诉SpringBoot需要什么功能，它就能引入需要的依赖库
● Actuator
让你能够深入运行中的SpringBoot应用程序，一探SpringBoot程序的内部信息
● 命令行界面
这是SpringBoot的可选特性，主要针对Groovy语言使用；
Groovy是一种基于JVM(Java虚拟机) 的敏捷开发语言，它结合了Python、Ruby和Smalltalk的许多强大的特性，Groovy 代码能够与Java代码很好地结合，也能用于扩展现有代码，由于其运行在JVM上的特性，Groovy可以使用其他Java语言编写的库。
## SpringBoot开发版本推荐
● Springboot目前分为两大版本系列，1.x系列和2.x系列
● 如果是使用eclipse，推荐安装Spring Tool Suite (STS)插件
● 如果使用IDEA旗舰版，自带了SpringBoot插件
● 推荐使用Maven 3.3+，Maven目前最新版本为3.6.0(2019.01)
● 推荐使用Java 8，SpringBoot 1.x系列的版本兼容Java 6，SpringBoot 2.x系列需要至少Java8
## SpringBoot重要策略
SpringBoot框架中还有两个非常重要的策略：开箱即用和约定优于配置。开箱即用，Outofbox，是指在开发过程中，通过在MAVEN项目的pom文件中添加相关依赖包，然后使用对应注解来代替繁琐的XML配置文件以管理对象的生命周期。这个特点使得开发人员摆脱了复杂的配置工作以及依赖的管理工作，更加专注于业务逻辑。约定优于配置，Convention over configuration，是一种由SpringBoot本身来配置目标结构，由开发者在结构中添加信息的软件设计范式。这一特点虽降低了部分灵活性，增加了BUG定位的复杂性，但减少了开发人员需要做出决定的数量，同时减少了大量的XML配置，并且可以将代码编译、测试和打包等工作自动化。
SpringBoot应用系统开发模板的基本架构设计从前端到后台进行说明：前端常使用模板引擎，主要有FreeMarker和Thymeleaf，它们都是用Java语言编写的，渲染模板并输出相应文本，使得界面的设计与应用的逻辑分离，同时前端开发还会使用到Bootstrap、AngularJS、JQuery等；在浏览器的数据传输格式上采用Json，非xml，同时提供RESTfulAPI；SpringMVC框架用于数据到达服务器后处理请求；到数据访问层主要有Hibernate、MyBatis、JPA等持久层框架；数据库常用MySQL；开发工具推荐IntelliJIDEA。
## 安装步骤
从最根本上来讲，SpringBoot就是一些库的集合，它能够被任意项目的构建系统所使用。简便起见，该框架也提供了命令行界面，它可以用来运行和测试Boot应用。框架的发布版本，包括集成的CLI（命令行界面），可以在Spring仓库中手动下载和安装。一种更为简便的方式是使用Groovy环境管理器（Groovy enVironment Manager，GVM），它会处理Boot版本的安装和管理。Boot及其CLI可以通过GVM的命令行gvm install springboot进行安装。在OS X上安装Boot可以使用Homebrew包管理器。为了完成安装，首先要使用brew tap pivotal/tap切换到Pivotal仓库中，然后执行brew install springboot命令。
要进行打包和分发的工程会依赖于像Maven或Gradle这样的构建系统。为了简化依赖图，Boot的功能是模块化的，通过导入Boot所谓的“starter”模块，可以将许多的依赖添加到工程之中。为了更容易地管理依赖版本和使用默认配置，框架提供了一个parent POM，工程可以继承它。
# 第一个SpringBoot项目
**开发步骤**
项目名称：000-springboot-first
1.创建一个Module，选择类型为Spring Initializr快速构建
![](https://images.cherryfloris.eu.org/2021/1634029805941-aa8b6592-479c-4aa7-aebd-7906f7c9eb9a.png)
2.设置GAV坐标及pom配置信息
![](https://images.cherryfloris.eu.org/2021/1634029805943-6df90815-5899-47c3-975c-d365bdf48b73.png)
3.选择SpringBoot版本及依赖
会根据选择的依赖自动添加起步依赖并进行自动配置
![](https://images.cherryfloris.eu.org/2021/1634029806215-ae647db4-2767-4d45-a386-80ae659f5de0.png)
4.设置模块名称、Content Root路径及模块文件的目录
![](https://images.cherryfloris.eu.org/2021/1634029805973-9e3fac74-f467-417a-ac7f-869f70c51f44.png)
点击Finish，如果是第一次创建，在右下角会提示正在下载相关的依赖
5.项目创建完毕，如下：
![](https://images.cherryfloris.eu.org/2021/1634029806450-fdb44319-89d8-4d79-8182-c02537c7b1cf.png)
# SpringBoot项目案例
SpringBoot入门案例
项目名称：002-springboot-springmvc
1.创建一个新的Module，选择类型为Spring Initializr
![](https://images.cherryfloris.eu.org/2021/1634030449364-ab23bbea-d066-4a59-b7d4-ec45907aa32b.png)
2.指定GAV及pom配置信息
![](https://images.cherryfloris.eu.org/2021/1634030449372-484c7596-472e-46a5-87e9-553365cbbd03.png)
3.选择Spring Boot版本及依赖
会根据选择的依赖自动添加起步依赖并进行自动配置
![](https://images.cherryfloris.eu.org/2021/1634030449369-562df309-af1e-414c-b335-c041e3cb5175.png)
4.修改Content Root路径及文件所在目录
![](https://images.cherryfloris.eu.org/2021/1634030449398-3f1fc6c8-17af-440e-b97c-e5ff6f25a882.png)
5.对POM.xml文件进行解释
```java
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <!--继承SpringBoot框架的一个父项目，所有自己开发的Spring Boot都必须的继承-->
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.1.5.RELEASE</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>

    <!--当前项目的GAV坐标-->
    <groupId>com.bjpowernode.springboot</groupId>
    <artifactId>002-springboot-springmvc</artifactId>
    <version>1.0.0</version>

    <!--maven项目名称，可以删除-->
    <name>002-springboot-springmvc</name>
    <!--maven项目描述，可以删除-->
    <description>Demo project for Spring Boot</description>

    <!--maven属性配置，可以在其它地方通过${}方式进行引用-->
    <properties>
        <java.version>1.8</java.version>
    </properties>


    <dependencies>
        <!--SpringBoot框架web项目起步依赖，通过该依赖自动关联其它依赖，不需要我们一个一个去添加了-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

        <!--SpringBoot框架的测试起步依赖，例如：junit测试，如果不需要的话可以删除-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <!--SpringBoot提供的打包编译等插件-->
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>
</project>
```
6.对SpringBoot项目结构进行说明
![](https://images.cherryfloris.eu.org/2021/1634030578625-c11fdfb9-5bbb-422a-b494-1f797d60b92e.png)
• mvn|mvnw|mvnw.cmd：使用脚本操作执行maven相关命令，国内使用较少，可删除
• gitignore：使用版本控制工具git的时候，设置一些忽略提交的内容
• static|templates：后面模板技术中存放文件的目录
• application.properties：SpringBoot的配置文件，很多集成的配置都可以在该文件中进行配置，例如：Spring、springMVC、Mybatis、Redis等。目前是空的
• Application.java：SpringBoot程序执行的入口，执行该程序中的main方法，SpringBoot就启动了
7.创建一个Spring MVC的SpringBootController
SpringBootController类所在包：com.bjpowernode.springboot.web
```java
package com.bjpowernode.springboot.web;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

/**
 * ClassName:SpringBootController
 * Package:com.bjpowernode.springboot.web
 * Description:<br/>
 */
@Controller
public class SpringBootController {

    @RequestMapping(value = "/springBoot/say")
    public @ResponseBody String say() {
        return "Hello,springBoot!";
    }
}
```
注意：新创建的类一定要位于Application同级目录或者下级目录，否则SpringBoot加载不到。 
8.在IDEA中右键，运行Application类中的main方法
通过在控制台的输出，可以看到启动SpringBoot框架，会启动一个内嵌的tomcat，端口号为8080，上下文根为空
![](https://images.cherryfloris.eu.org/2021/1634030631139-273c3f25-5c47-433e-9cbd-01ea47946f6e.png)
9.在浏览器中输入http://localhost:8080/springBoot/say访问
![](https://images.cherryfloris.eu.org/2021/1634030631126-cf6f76e6-e8cc-4dd4-9d8f-120bdb30e993.png)
## SpringBoot入门案例分析
1.Spring Boot的父级依赖spring-boot-starter-parent配置之后，当前的项目就是Spring Boot项目
2.spring-boot-starter-parent是一个Springboot的父级依赖，开发SpringBoot程序都需要继承该父级项目，它用来提供相关的Maven默认依赖，使用它之后，常用的jar包依赖可以省去version配置
3.Spring Boot提供了哪些默认jar包的依赖，可查看该父级依赖的pom文件
4.如果不想使用某个默认的依赖版本，可以通过pom.xml文件的属性配置覆盖各个依赖项，比如覆盖Spring版本
```java
<properties>
    		<spring.version>5.0.0.RELEASE</spring.version>
</properties>
```
5.**@SpringBootApplication注解是Spring Boot项目的核心注解，主要作用是开启Spring自动配置，如果在Application类上去掉该注解，那么不会启动SpringBoot程序**
6.main方法是一个标准的Java程序的main方法，主要作用是作为项目启动运行的入口
7.@Controller 及 @ResponseBody 依然是我们之前的Spring MVC，因为Spring Boot的里面依然是使用我们的Spring MVC + Spring + MyBatis 等框架
