# Spring Cloud 教程
Spring Cloud是什么
1、Spring Cloud是一个一站式的开发分布式系统的框架，为开发者提供了一系列的构建分布式系统的工具集;
2、Spring Cloud为开发人员提供了快速构建分布式系统中一些常见模式的工具(比如：配置管理，服务发现，断路器，智能路由、微代理、控制总线、全局锁、决策竞选、分布式会话和集群状态管理等);
3、开发分布式系统都需要解决一系列共同关心的问题，而使用Spring Cloud可以快速地实现这些分布式开发共同关心的问题，并能方便地在任何分布式环境中部署与运行。
4、Spring Cloud这个一站式地分布式开发框架，被近年来流行的“微服务”架构所大力推崇，成为目前进行微服务架构的优先选择工具;
5、Spring Cloud基于Spring Boot框架构建微服务架构，学习Spring Cloud需要先学习Spring Boot;
6、SpringCloud官网：http://spring.io
## Spring Cloud的版本
Spring Cloud最早是从2014年推出的，在推出的前期更新迭代速度非常快，频繁发布新版本，目前更趋于稳定，变化稍慢一些;
Spring Cloud的版本并不是传统的使用数字的方式标识，而是使用诸如：Angel、Brixton、Camden......等伦敦的地名来命名版本，版本的先后顺序使用字母表A-Z的先后来标识,，现在已经进入F版本;
Spring Cloud与Spring Boot版本匹配关系

| Finchley                       | 兼容Spring Boot 2.0.x，不兼容Spring Boot 1.5.x |
| --- | --- |
| Edgware           | 兼容Spring Boot 1.5.x，不兼容Spring Boot 2.0.x |
| Dalston | 兼容Spring Boot 1.5.x，不兼容Spring Boot 2.0.x |
| Camden | 兼容Spring Boot 1.4.x，也兼容Spring Boot 1.5.x |
| Brixton | 兼容Spring Boot 1.3.x，也兼容Spring Boot 1.4.x |
| Angel | 兼容Spring Boot 1.2.x |

Spring Cloud并不是从0开始开发一整套微服务解决方案，而是集成各个开源软件，构成一整套的微服务解决方案，这其中有非常著名的Netflix公司的开源产品;
Netflix公司成立于1997年，是目前美国最大的版权视频交易网站;
Netflix公司在不断发展的过程中，也成为了一家云计算公司，并积极参与开源项目，Netflix OSS(Open Source)就是由Netflix公司主持开发的一套代码框架和库，github地址：https://github.com/Netflix;
Spring Cloud 所包含的众多组件中，Spring Cloud Netflix就是其中一组不可忽视的组件，由netflix公司开发后又并入Spring Cloud 大家庭;
目前Netflix公司贡献的活跃项目包括：
spring-cloud-netflix-eureka
spring-cloud-netflix-hystrix
spring-cloud-netflix-stream
spring-cloud-netflix-archaius
spring-cloud-netflix-ribbon
spring-cloud-netflix-zuul
## Spring Cloud开发环境
SpringBoot 2.0.x
Spring Cloud Finchley RC2
Maven 3.5.3
JDK 1.8.152
IntelliJ IDEA
## Spring Cloud的整体架构
![](https://images.cherryfloris.eu.org/2021/1633934589300-cb876523-7c1c-4c93-916b-a1520cbf57bf.png)
Service Provider： 暴露服务的服务提供方。
Service Consumer：调用远程服务的服务消费方。
EureKa Server： 服务注册中心和服务发现中心。
# Spring Cloud快速入门
搭建和配置一个服务提供者
我们知道，SpringCloud构建微服务是基于SpringBoot开发的。
1、 创建一个SpringBoot工程，并且添加SpringBoot的相关依赖;
2、 创建服务提供者的访问方法，也就是后续消费者如何访问提供者;
Spring Cloud是基于rest的访问，所以我们添加一个Controller，在该Controller中提供一个访问入口：
```java
@RestController
public class HelloController {
    @RequestMapping(value = "/hello", method = RequestMethod.GET)
    public String hello() {
        return "Hello Spring Cloud";
    }
```
3、 启动运行该SpringBoot程序，访问该controller;
## 搭建和配置一个服务消费者
服务消费者也是一个SpringBoot项目，服务消费者主要用来消费服务提供者提供的服务;
1、 创建一个SpringBoot工程，并且添加SpringBoot的相关依赖;
2、开发一个消费者方法，去消费服务提供者提供的服务，这个消费者方法也是一个Controller:
```java
@RestController
public class ConsumerController {
    @Autowired
    private RestTemplate restTemplate;
    @RequestMapping(value="/cloud/hello")
    public String helloController() {
        return restTemplate.getForEntity("http://localhost:9100/hello", String.class).getBody();
    }
}
```
3、启动该SpringBoot程序，测试服务消费者调用服务提供者;
## 走进服务注册中心Eureka
在微服务架构中，服务注册与发现是核心组件之一，手动指定每个服务是很低效的，Spring Cloud提供了多种服务注册与发现的实现方式，例如：Eureka、Consul、Zookeeper。
Spring Cloud支持得最好的是Eureka，其次是Consul，再次是Zookeeper。
### 什么是服务注册?
服务注册：将服务所在主机、端口、版本号、通信协议等信息登记到注册中心上;
### 什么是服务发现?
服务发现：服务消费者向注册中心请求已经登记的服务列表，然后得到某个服务的主机、端口、版本号、通信协议等信息，从而实现对具体服务的调用;
### Eureka是什么?
Eureka是一个服务治理组件，它主要包括服务注册和服务发现，主要用来搭建服务注册中心。
Eureka 是一个基于 REST 的服务，用来定位服务，进行中间层服务器的负载均衡和故障转移;
Eureka是Netflix 公司开发的，Spring Cloud 封装了 Netflix 公司开发的 Eureka 模块来实现服务注册和发现，也就是说Spring Cloud对Netflix Eureka 做了二次封装;
Eureka 采用了C-S(客户端/服务端)的设计架构，也就是Eureka由两个组件组成：Eureka服务端和Eureka客户端。Eureka Server 作为服务注册的服务端，它是服务注册中心，而系统中的其他微服务，使用 Eureka 的客户端连接到 Eureka Server服务端，并维持心跳连接，Eureka客户端是一个Java客户端，用来简化与服务器的交互、负载均衡，服务的故障切换等;
有了Eureka注册中心，系统的维护人员就可以通过 Eureka Server 来监控系统中各个微服务是否正常运行。
## Eureka与Zookeeper的比较
著名的CAP理论指出，一个分布式系统不可能同时满足C(一致性)、A(可用性)和P(分区容错性)。
由于分区容错性在是分布式系统中必须要保证的，因此我们只能在A和C之间进行权衡，在此Zookeeper保证的是CP, 而Eureka则是AP。
### Zookeeper保证CP
在ZooKeeper中，当master节点因为网络故障与其他节点失去联系时，剩余节点会重新进行leader选举，但是问题在于，选举leader需要一定时间, 且选举期间整个ZooKeeper集群都是不可用的，这就导致在选举期间注册服务瘫痪。在云部署的环境下，因网络问题使得ZooKeeper集群失去master节点是大概率事件，虽然服务最终能够恢复，但是在选举时间内导致服务注册长期不可用是难以容忍的。
### Eureka保证AP
Eureka优先保证可用性，Eureka各个节点是平等的，某几个节点挂掉不会影响正常节点的工作，剩余的节点依然可以提供注册和查询服务。而Eureka的客户端在向某个Eureka注册或时如果发现连接失败，则会自动切换至其它节点，只要有一台Eureka还在，就能保证注册服务可用(保证可用性)，只不过查到的信息可能不是最新的(不保证强一致性)。
所以Eureka在网络故障导致部分节点失去联系的情况下，只要有一个节点可用，那么注册和查询服务就可以正常使用，而不会像zookeeper那样使整个注册服务瘫痪，Eureka优先保证了可用性。
## 搭建与配置Eureka服务注册中心
Spring Cloud要使用Eureka注册中心非常简单和方便，Spring Cloud中的Eureka服务注册中心实际上也是一个Spring Boot工程，我们只需通过引入相关依赖和注解配置就能让Spring Boot构建的微服务应用轻松地与Eureka进行整合。
具体步骤如下：
1、 创建一个SpringBoot项目，并且添加SpringBoot的相关依赖;
03-springcloud-eureka-server
2、 添加eureka的依赖：
```java
<!--Spring Cloud的eureka-server起步依赖-->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
</dependency>
```
3、 在Spring Boot的入口类上添加一个@EnableEurekaServer注解，用于
开启Eureka注册中心服务端
4、 在application.properties文件中配置Eureka服务注册中心信息：
```java
#内嵌定时tomcat的端口
server.port=8761
#设置该服务注册中心的hostname
eureka.instance.hostname=localhost
#由于我们目前创建的应用是一个服务注册中心，而不是普通的应用，默认情况下，这个应用会向注册中心（也是它自己）注册它自己，设置为false表示禁止这种自己向自己注册的默认行为
eureka.client.register-with-eureka=false
#表示不去检索其他的服务，因为服务注册中心本身的职责就是维护服务实例，它不需要去检索其他服务
eureka.client.fetch-registry=false
#指定服务注册中心的位置
eureka.client.service-url.defaultZone=http://${eureka.instance.hostname}:${server.port}/eureka
```
启动与测试Eureka服务注册中心
1、完成上面的项目搭建后，我们就可以启动SpringBoot程序，main方法运行;
2、启动成功之后，通过在浏览器地址栏访问我们的注册中心;
## 向Eureka服务注册中心注册服务
我们前面搭建了服务提供者项目，接下来我们就可以将该服务提供者注册到Eureke注册中心，步骤如下：
1、在该服务提供者中添加eureka的依赖，因为服务提供者向注册中心注册服务，需要连接eureka，所以需要eureka客户端的支持;
```java
<!--SpringCloud集成eureka客户端的起步依赖-->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
```
2、激活Eureka中的EnableEurekaClient功能：
在Spring Boot的入口函数处，通过添加@EnableEurekaClient注解来表明自己是一个eureka客户端，让我的服务提供者可以连接eureka注册中心;
3、配置服务名称和注册中心地址
```java
spring.application.name=02-springcloud-service-provider
eureka.client.service-url.defaultZone=http://localhost:8761/eureka
```
4、启动服务提供者SpringBoot程序的main方法运行;
5、启动运行之后，通过在浏览器地址栏访问我们之前搭建好的eureka注册中心，就可以看到有一个服务已经注册成功了;
## 从Eureka服务注册中心发现与消费服务
我们已经搭建一个服务注册中心，同时也向这个服务注册中心注册了服务，接下来我们就可以发现和消费服务了，这其中服务的发现由eureka客户端实现，而服务的消费由Ribbon实现，也就是说服务的调用需要eureka客户端和Ribbon两者配合起来才能实现;
### Eureka客户端是什么?
Eureka客户端是一个Java客户端，用来连接Eureka服务端，与服务端进行交互、负载均衡，服务的故障切换等;
### Ribbon是什么?
Ribbon是一个基于HTTP 和 TCP 的客户端负载均衡器，当使用Ribbon对服务进行访问的时候，它会扩展Eureka客户端的服务发现功能，实现从Eureka注册中心中获取服务端列表，并通过Eureka客户端来确定服务端是否己经启动。Ribbon在Eureka客户端服务发现的基础上，实现了对服务实例的选择策略，从而实现对服务的负载均衡消费。
接下来我们来让服务消费者去消费服务：
我们前面搭建了服务消费者项目，接下来我们就可以使用该服务消费者通过注册中心去调用服务提供者，步骤如下：
1、在该消费者项目中添加eureka的依赖，因为服务消费者从注册中心获取服务，需要连接eureka，所以需要eureka客户端的支持;
```java
<!--SpringCloud集成eureka客户端的起步依赖-->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
```
2、激活Eureka中的EnableEurekaClient功能：
在Spring Boot的入口函数处，通过添加@EnableEurekaClient注解来表明自己是一个eureka客户端，让我的服务消费者可以使用eureka注册中心;
3、配置服务的名称和注册中心的地址：
```java
spring.application.name=03-springcloud-web-consumer
eureka.client.service-url.defaultZone=http://localhost:8761/eureka
```
4、前面我介绍了服务的发现由eureka客户端实现，而服务的真正调用由ribbon实现，所以我们需要在调用服务提供者时使用ribbon来调用：
```java
@LoadBalanced
@Bean
public RestTemplate restTemplate () {
    return new RestTemplate();
}
```
加入了ribbon的支持，那么在调用时，即可改为使用服务名称来访问：
```java
restTemplate.getForEntity("http://01-SPRINGCLOUD-SERVICE-PROVIDER/cloud/hello", String.class).getBody();
```
5、完成上面的步骤后，我们就可以启动消费者的SpringBoot程序，main方法运行;
6、启动成功之后，通过在浏览器地址栏访问我们的消费者，看是否可以正常调用远程服务提供者提供的服务;
# Spring Cloud Eureka服务注册中心
Eureka注册中心高可用集群概述
在微服务架构的这种分布式系统中，我们要充分考虑各个微服务组件的高可用性问题，不能有单点故障，由于注册中心eureka本身也是一个服务，如果它只有一个节点，那么它有可能发生故障，这样我们就不能注册与查询服务了，所以我们需要一个高可用的服务注册中心，这就需要通过注册中心集群来解决。
eureka服务注册中心它本身也是一个服务，它也可以看做是一个提供者，又可以看做是一个消费者，我们之前通过配置：
eureka.client.register-with-eureka=false 让注册中心不注册自己，但是我们可以向其他注册中心注册自己;
Eureka Server的高可用实际上就是将自己作为服务向其他服务注册中心注册自己，这样就会形成一组互相注册的服务注册中心，进而实现服务清单的互相同步，往注册中心A上注册的服务，可以被复制同步到注册中心B上，所以从任何一台注册中心上都能查询到已经注册的服务，从而达到高可用的效果。
![](https://images.cherryfloris.eu.org/2021/1633940426350-7b5ce3d7-518a-4b36-b73d-2da8fa35c927.png)
## Eureka注册中心高可用集群搭建
我们知道，Eureka注册中心高可用集群就是各个注册中心相互注册，所以：
1、在8761的配置文件中，让它的service-url指向8762，在8762的配置文件中让它的service-url指向8761
2、由于8761和8762互相指向对方，实际上我们构建了一个双节点的服务注册中心集群
```java
eureka.client.service-url.defaultZone=http://eureka8762:8762/eureka/
eureka.client.service-url.defaultZone=http://eureka8761:8761/eureka/
```
然后在本地hosts文件配置：C:\Windows\System32\drivers\etc\hosts
```java
127.0.0.1 eureka8761
127.0.0.1 eureka8762
```
运行时，在运行配置项目Program Arguments 中配置：
```java
--spring.profiles.active=eureka8761 
--spring.profiles.active=eureka8762 
```
分别启动两个注册中心，访问两个注册中心页面，观察注册中心页面是否正常;
## Eureka注册中心高可用集群测试
在要进行注册的服务中配置：
```java
eureka.client.service-url.defaultZone=http://eureka8761:8761/eureka/,http://eureka8762:8762/eureka/
```
启动服务提供者服务，然后观察注册中心页面，可以看到服务会在两个注册中心上都注册成功;
## Eureka服务注册中心自我保护机制
自我保护机制是Eureka注册中心的重要特性，当Eureka注册中心进入自我保护模式时，在Eureka Server首页会输出如下警告信息：
EMERGENCY! EUREKA MAY BE INCORRECTLY CLAIMING INSTANCES ARE UP WHEN THEY'RE NOT. RENEWALS ARE LESSER THAN THRESHOLD AND HENCE THE INSTANCES ARE NOT BEING EXPIRED JUST TO BE SAFE.
emergency! eureka may be incorrectly claiming instances are up when they're not. renewals are lesser than threshold and hence the instances are not being expired just to be safe.
在没有Eureka自我保护的情况下，如果Eureka Server在一定时间内没有接收到某个微服务实例的心跳，Eureka Server将会注销该实例，但是当发生网络分区故障时，那么微服务与Eureka Server之间将无法正常通信，以上行为可能变得非常危险了——因为微服务本身其实是正常的，此时不应该注销这个微服务，如果没有自我保护机制，那么Eureka Server就会将此服务注销掉。
Eureka通过“自我保护模式”来解决这个问题——当Eureka Server节点在短时间内丢失过多客户端时(可能发生了网络分区故障)，那么就会把这个微服务节点进行保护。一旦进入自我保护模式，Eureka Server就会保护服务注册表中的信息，不删除服务注册表中的数据(也就是不会注销任何微服务)。当网络故障恢复后，该Eureka Server节点会再自动退出自我保护模式。
所以，自我保护模式是一种应对网络异常的安全保护措施，它的架构哲学是宁可同时保留所有微服务(健康的微服务和不健康的微服务都会保留)，也不盲目注销任何健康的微服务，使用自我保护模式，可以让Eureka集群更加的健壮、稳定。
当然也可以使用配置项：eureka.server.enable-self-preservation = false 禁用自我保护模式。
但是Eureka Server 自我保护模式也会给我们带来一些困扰，如果在保护期内某个服务提供者刚好非正常下线了，此时服务消费者就会拿到一个无效的服务实例，此时会调用失败，对于这个问题需要服务消费者端具有一些容错机制，如重试，断路器等。
Eureka的自我保护模式是有意义的，该模式被激活后，它不会从注册列表中剔除因长时间没收到心跳导致注册过期的服务，而是等待修复，直到心跳恢复正常之后，它自动退出自我保护模式。这种模式旨在避免因网络分区故障导致服务不可用的问题。
例如，两个微服务客户端实例A和B之间有调用的关系，A是消费者，B是提供者，但是由于网络故障，B未能及时向Eureka发送心跳续约，这时候Eureka 不能简单的将B从注册表中剔除，因为如果剔除了，A就无法从Eureka 服务器中获取B注册的服务，但是这时候B服务是可用的;
所以，Eureka的自我保护模式最好还是开启它。
关于自我保护常用几个配置如下：
服务器端配置：
#测试时关闭自我保护机制，保证不可用服务及时踢出
eureka.server.enable-self-preservation=false
客户配置：
#每间隔2s，向服务端发送一次心跳，证明自己依然"存活"
eureka.instance.lease-renewal-interval-in-seconds=2
#告诉服务端，如果我10s之内没有给你发心跳，就代表我故障了，将我踢出掉
eureka.instance.lease-expiration-duration-in-seconds=10
# Spring Cloud Ribbon客户端负载均衡
Spring Cloud中的Ribbon是什么?
我们通常说的负载均衡是指将一个请求均匀地分摊到不同的节点单元上执行，负载均和分为硬件负载均衡和软件负载均衡：
**硬件负载均衡：**比如 F5、深信服、Array 等;
**软件负载均衡：**比如 Nginx、LVS、HAProxy 等;
硬件负载均衡或是软件负载均衡，他们都会维护一个可用的服务端清单，通过心跳检测来剔除故障的服务端节点以保证清单中都是可以正常访问的服务端节点。当客户端发送请求到负载均衡设备的时候，该设备按某种算法(比如轮询、权重、 最小连接数等)从维护的可用服务端清单中取出一台服务端的地址，然后进行转发。
Ribbon是Netflix发布的开源项目，主要功能是提供客户端的软件负载均衡算法，是一个基于HTTP和TCP的客户端负载均衡工具。
Spring Cloud对Ribbon做了二次封装，可以让我们使用RestTemplate的服务请求，自动转换成客户端负载均衡的服务调用。
Ribbon支持多种负载均衡算法，还支持自定义的负载均衡算法。
Ribbon只是一个工具类框架，比较小巧，Spring Cloud对它封装后使用也非常方便，它不像服务注册中心、配置中心、API网关那样需要独立部署，Ribbon只需要在代码直接使用即可;
Ribbon 与 Nginx 的区别
Ribbon是客户端的负载均衡工具，而客户端负载均衡和服务端负载均衡最大的区别在于服务清单所存储的位置不同，在客户端负载均衡中，所有客户端节点下的服务端清单，需要自己从服务注册中心上获取，比如Eureka服务注册中心。同服务端负载均衡的架构类似，在客户端负载均衡中也需要心跳去维护服务端清单的健康性，只是这个步骤需要与服务注册中心配合完成。在Spring Cloud中，由于Spring Cloud对Ribbon做了二次封装，所以默认会创建针对Ribbon的自动化整合配置;
在Spring Cloud中，Ribbon主要与RestTemplate对象配合起来使用，Ribbon会自动化配置RestTemplate对象，通过@LoadBalanced开启RestTemplate对象调用时的负载均衡。
![](https://images.cherryfloris.eu.org/2021/1633940711673-24a4a65e-4694-4717-a03f-099fd0184913.png)
## Ribbon实现客户端负载均衡
由于Spring Cloud Ribbon的封装， 我们在微服务架构中使用客户端负载均衡调用非常简单， 只需要如下两步：
1、启动多个服务提供者实例并注册到一个服务注册中心或是服务注册中心集群。
2、服务消费者通过被@LoadBalanced注解修饰过的RestTemplate来调用服务提供者。
这样，我们就可以实现服务提供者的高可用以及服务消费者的负载均衡调用。
## Ribbon负载均衡策略
Ribbon的负载均衡策略是由IRule接口定义, 该接口由如下实现：
![](https://images.cherryfloris.eu.org/2021/1633940711876-f4e44735-16e3-4b5a-ae6d-6b01654eb687.png)

| RandomRule | 随机 |
| --- | --- |
| RoundRobinRule | 轮询 |
| AvailabilityFilteringRule | 先过滤掉由于多次访问故障的服务，以及并发连接数超过阈值的服务，然后对剩下的服务按照轮询策略进行访问； |
|                                                                   WeightedResponseTimeRule                                                                                     | 根据平均响应时间计算所有服务的权重，响应时间越快服务权重就越大被选中的概率即越高，如果服务刚启动时统计信息不足，则使用RoundRobinRule策略，待统计信息足够会切换到该WeightedResponseTimeRule策略； |
| RetryRule | 先按照RoundRobinRule策略分发，如果分发到的服务不能访问，则在指定时间内进行重试，分发其他可用的服务； |
| BestAvailableRule | 先过滤掉由于多次访问故障的服务，然后选择一个并发量最小的服务； |
| ZoneAvoidanceRule | 综合判断服务节点所在区域的性能和服务节点的可用性，来决定选择哪个服务； |

## Rest请求模板类解读
当我们从服务消费端去调用服务提供者的服务的时候，使用了一个极其方便的对象叫RestTemplate，当时我们只使用了RestTemplate中最简单的一个功能getForEntity发起了一个get请求去调用服务端的数据，同时，我们还通过配置@LoadBalanced注解开启客户端负载均衡，RestTemplate的功能非常强大，那么接下来我们就来详细的看一下RestTemplate中几种常见请求方法的使用。
在日常操作中，基于Rest的方式通常是四种情况，它们分表是：
GET请求 --查询数据
POST请求 –添加数据
PUT请求 – 修改数据
DELETE请求 –删除数据
下面我们逐一解读。
## RestTemplate的GET请求
有两种方式：
第一种：getForEntity
该方法返回一个ResponseEntity对象，ResponseEntity是Spring对HTTP请求响应的封装，包括了几个重要的元素，比如响应码、contentType、contentLength、响应消息体等;
```java
ResponseEntity<String> responseEntity = restTemplate.getForEntity("http://01-SPRINGCLOUD-SERVICE-PROVIDER/service/hello", String.class);
String body = responseEntity.getBody();
HttpStatus statusCode = responseEntity.getStatusCode();
int statusCodeValue = responseEntity.getStatusCodeValue();
HttpHeaders headers = responseEntity.getHeaders();

System.out.println(body);
System.out.println(statusCode);
System.out.println(statusCodeValue);
System.out.println(headers);
```
以上代码：
getForEntity方法第一个参数为要调用的服务的地址，即服务提供者提供的http://01-SPRINGCLOUD-SERVICE-PROVIDER/service/hello接口地址，注意这里是通过服务名调用而不是服务地址，如果改为服务地址就无法使用Ribbon实现客户端负载均衡了。
getForEntity方法第二个参数String.class表示希望返回的body类型是String类型，如果希望返回一个对象，也是可以的，比如User对象;
另外两个重载方法：
```java
public <T> ResponseEntity<T> getForEntity(String url, Class<T> responseType, Object... uriVariables) throws RestClientException
```
比如：
```java
restTemplate.getForEntity("http://01-SPRINGCLOUD-SERVICE-PROVIDER/service/hello?id={1}&name={2}", String.class, "{1, '张无忌'}").getBody();
```
```java
public <T> ResponseEntity<T> getForEntity(String url, Class<T> responseType, Map<String, ?> uriVariables) throws RestClientException
```
比如：
```java
Map<String, Object> paramMap = new ConcurrentHashMap<>();
paramMap.put("id", 1);
paramMap.put("name", "张无忌");
restTemplate.getForEntity("http://01-SPRINGCLOUD-SERVICE-PROVIDER/service/hello?id={id}&name={name}", String.class, paramMap).getBody(); 
```
第二种：getForObject()
与getForEntity使用类似，只不过getForObject是在getForEntity基础上进行了再次封装，可以将http的响应体body信息转化成指定的对象，方便我们的代码开发;
当你不需要返回响应中的其他信息，只需要body体信息的时候，可以使用这个更方便;
它也有两个重载的方法，和getForEntity相似;
```java
<T> T getForObject(URI url, Class<T> responseType) throws RestClientException;

<T> T getForObject(String url, Class<T> responseType, Object... uriVariables) throws RestClientException;

<T> T getForObject(String url, Class<T> responseType, Map<String, ?> uriVariables) throws RestClientException;
```
RestTemplate的POST请求：
Post与Get请求非常类似：
```java
restTemplate.postForObject()
restTemplate.postForEntity()
restTemplate.postForLocation()
```
RestTemplate的PUT请求：
restTemplate.put();
## RestTemplate的DELETE请求：
restTemplate.delete();
# Spring Cloud Hystrix服务熔断
Hystrix是什么
在微服务架构中，我们是将一个单体应用拆分成多个服务单元，各个服务单元之间通过注册中心彼此发现和消费对方提供的服务，每个服务单元都是单独部署，在各自的服务进程中运行，服务之间通过远程调用实现信息交互，那么当某个服务的响应太慢或者故障，又或者因为网络波动或故障，则会造成调用者延迟或调用失败，当大量请求到达，则会造成请求的堆积，导致调用者的线程挂起，从而引发调用者也无法响应，调用者也发生故障。
比如电商中的用户下订单，我们有两个服务，一个下订单服务，一个减库存服务，当用户下订单时调用下订单服务，然后下订单服务又调用减库存服务，如果减库存服务响应延迟或者没有响应，则会造成下订单服务的线程挂起等待，如果大量的用户请求下订单，或导致大量的请求堆积，引起下订单服务也不可用，如果还有另外一个服务依赖于订单服务，比如用户服务，它需要查询用户订单，那么用户服务查询订单也会引起大量的延迟和请求堆积，导致用户服务也不可用。
所以在微服务架构中，很容易造成服务故障的蔓延，引发整个微服务系统瘫痪不可用。
为了解决此问题，微服务架构中引入了一种叫熔断器的服务保护机制。
熔断器也有叫断路器，他们表示同一个意思，最早来源于微服务之父Martin Fowler的论文CircuitBreaker一文。“熔断器”本身是一种开关装置，用于在电路上保护线路过载，当线路中有电器发生短路时，能够及时切断故障电路，防止发生过载、发热甚至起火等严重后果。
微服务架构中的熔断器，就是当被调用方没有响应，调用方直接返回一个错误响应即可，而不是长时间的等待，这样避免调用时因为等待而线程一直得不到释放，避免故障在分布式系统间蔓延;
Spring Cloud Hystrix实现了熔断器、线程隔离等一系列服务保护功能。该功能也是基于Netflix的开源框架Hystrix实现的，该框架的目标在于通过控制那些访问远程系统、服务和第三方库的节点，从而对延迟和故障提供更强大的容错能力。Hystrix具备服务降级、服务熔断、线程和信号隔离、请求缓存、请求合并以及服务监控等强大功能。
## Hystrix快速入门
在SpringCloud中使用熔断器Hystrix是非常简单和方便的，只需要简单两步即可：
1、添加依赖
```java
<!--Spring Cloud熔断器起步依赖-->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-hystrix</artifactId>
    <version>1.4.4.RELEASE</version>
</dependency>
```
2、在入口类中使用@EnableCircuitBreaker注解开启断路器功能，也可以使用一个名为@SpringCloudApplication的注解代替主类上的三个注解;
3、在调用远程服务的方法上添加注解：@HystrixCommand(fallbackMethod="error")
## 服务消费者Hystrix测试
hystrix默认超时时间是1000毫秒，如果你后端的响应超过此时间，就会触发断路器;
修改hystrix的默认超时时间：
```java
@HystrixCommand(fallbackMethod="error", commandProperties={
        @HystrixProperty(name="execution.isolation.thread.timeoutInMilliseconds", value="1500")}) //熔断器，调用不通，回调error()方法
public String webHello () {
```
Hystrix的服务降级
有了服务的熔断，随之就会有服务的降级，所谓服务降级，就是当某个服务熔断之后，服务端提供的服务将不再被调用，此时由客户端自己准备一个本地的fallback回调，返回一个默认值来代表服务端的返回;
这种做法，虽然不能得到正确的返回结果，但至少保证了服务的可用，比直接抛出错误或服务不可用要好很多，当然这需要根据具体的业务场景来选择;
## Hystrix的异常处理
我们在调用服务提供者时，我们自己也有可能会抛异常，默认情况下方法抛了异常会自动进行服务降级，交给服务降级中的方法去处理;
当我们自己发生异常后，只需要在服务降级方法中添加一个Throwable类型的参数就能够获取到抛出的异常的类型，如下：
```java
public String error(Throwable throwable) {
    System.out.println(throwable.getMessage());
    return "error";
}
```
此时我们可以在控制台看到异常的类型;
如果远程服务有一个异常抛出后我们不希望进入到服务降级方法中去处理，而是直接将异常抛给用户，那么我们可以在@HystrixCommand注解中添加忽略异常，如下：
```java
@HystrixCommand(fallbackMethod="error", ignoreExceptions = Exception.class)
```
自定义Hystrix请求的服务异常熔断处理
我们也可以自定义类继承自HystrixCommand来实现自定义的Hystrix请求，在getFallback方法中调用getExecutionException方法来获取服务抛出的异常;
com.netflix.hystrix.HystrixCommand.Setter.withGroupKey(HystrixCommandGroupKey.Factory.asKey(""))
## Hystrix仪表盘监控
Hystrix仪表盘(Hystrix Dashboard)，就像汽车的仪表盘实时显示汽车的各项数据一样，Hystrix仪表盘主要用来监控Hystrix的实时运行状态，通过它我们可以看到Hystrix的各项指标信息，从而快速发现系统中存在的问题进而解决它。
要使用Hystrix仪表盘功能，我们首先需要有一个Hystrix Dashboard，这个功能我们可以在原来的消费者应用上添加，让原来的消费者应用具备Hystrix仪表盘功能，但一般地，微服务架构思想是推崇服务的拆分，Hystrix Dashboard也是一个服务，所以通常会单独创建一个新的工程专门用做Hystrix Dashboard服务;
### 搭建一个Hystrix Dashboard服务的步骤：
第一步：创建一个普通的Spring Boot工程
比如创建一个名为springcloud-hystrix-dashboard的Spring Boot工程，建立好基本的结构和配置;
第二步：添加相关依赖
在创建好的Spring Boot项目的 pom.xml文件中添加相关依赖，如下：
```java
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-hystrix-dashboard</artifactId>
    <version>1.4.5.RELEASE</version>
</dependency>
```
第三步：入口类上添加注解
添加好依赖之后，在入口类上添加@EnableHystrixDashboard注解开启仪表盘功能，如下：
```java
@SpringBootApplication
@EnableHystrixDashboard
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}
```
第四步：属性配置
最后，我们可以根据个人习惯配置一下application.properties文件，如下：server.port=3721
至此，我们的Hystrix监控环境就搭建好了;

![](https://images.cherryfloris.eu.org/2021/1633943460692-7d163b0d-24fe-4944-b89e-83a75d07b890.png)
Hystrix仪表盘工程已经创建好了，现在我们需要有一个服务，让这个服务提供一个路径为/actuator/hystrix.stream接口，然后就可以使用Hystrix仪表盘来对该服务进行监控了;
我们改造消费者服务，让其能提供/actuator/hystrix.stream接口，步骤如下：
1、消费者项目需要有hystrix的依赖：
```java
<!--Spring Cloud熔断器起步依赖-->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-hystrix</artifactId>
    <version>1.4.5.RELEASE</version>
</dependency>
```
2、需要有一个spring boot的服务监控依赖：
```java
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```
3、配置文件需要配置spring boot监控端点的访问权限：
management.endpoints.web.exposure.include=*
这个是用来暴露 endpoints 的，由于 endpoints 中会包含很多敏感信息，除了 health 和 info 两个支持直接访问外，其他的默认不能直接访问，所以我们让它都能访问，或者指定：
management.endpoints.web.exposure.include=hystrix.stream
4、访问入口 http://localhost:8081/actuator/hystrix.stream
注意：这里有一个细节需要注意，要访问/hystrix.stream接口，首先得访问consumer工程中的任意一个其他接口，否则直接访问/hystrix.stream接口时会输出出一连串的ping: ping: …，先访问consumer中的任意一个其他接口，然后再访问/hystrix.stream接口即可;
## Hystrix仪表盘监控数据解读
![](https://images.cherryfloris.eu.org/2021/1633943509872-222d3605-cb2c-44a8-becc-040fcab367c1.png)
# Spring Cloud Feign声明式服务消费
Feign是什么
Feign是Netflix公司开发的一个声明式的REST调用客户端;
Ribbon负载均衡、Hystrix服务熔断是我们Spring Cloud中进行微服务开发非常基础的组件，在使用的过程中我们也发现它们一般都是同时出现的，而且配置也都非常相似，每次开发都有很多相同的代码，因此Spring Cloud基于Netflix Feign整合了Ribbon和Hystrix两个组件，让我们的开发工作变得更加简单，就像Spring Boot是对Spring+SpringMVC的简化一样，Spring Cloud Feign对Ribbon负载均衡、Hystrix服务熔断进行简化，在其基础上进行了进一步的封装，不仅在配置上大大简化了开发工作，同时还提供了一种声明式的Web服务客户端定义方式;
## 使用Feign实现消费者
使用Feign实现消费者，我们通过下面步骤进行：
### 第一步：创建普通Spring Boot工程
首先我们来创建一个普通的Spring Boot工程，取名为：05-springcloud-service-feign;
### 第二步：添加依赖
要添加的依赖主要是spring-cloud-starter-netflix-eureka-client和spring-cloud-starter-feign，如下：
```java
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-feign</artifactId>
    <version>1.4.5.RELEASE</version>
</dependency>
<!--Spring Cloud熔断器起步依赖-->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-hystrix</artifactId>
    <version>1.4.5.RELEASE</version>
</dependency>
```
第三步：添加注解
在项目入口类上添加@EnableFeignClients注解表示开启Spring Cloud Feign的支持功能;
### 第四步：声明服务
定义一个HelloService接口，通过@FeignClient注解来指定服务名称，进而绑定服务，然后再通过SpringMVC中提供的注解来绑定服务提供者提供的接口，如下：
```java
@FeignClient("01-springcloud-service-provider")
public interface HelloService {
    @RequestMapping("/service/hello")
    public String hello();
}
```
这相当于绑定了一个名叫01-springcloud-service-provider (这里01-springcloud-service-provider大小写01-SPRINGCLOUD-SERVICE-PROVIDER都可以 ) 的服务提供者提供的/service/hello接口;
我们服务提供者提供的接口如下：
```java
@GetMapping("/service/hello")
public String hello() {
    System.out.println("服务提供者1。。。。。。。");
    return "Hello, Spring Cloud，Provider 1";
}
```
第五步：使用Controller中调用服务
接着来创建一个Controller来调用上面的服务，如下：
```java
@RestController
public class FeignController {
    @Autowired
    HelloService helloService;
    @RequestMapping("/web/hello")
    public String hello() {
        return helloService.hello();
    }
}
```
第六步：属性配置
在application.properties中指定服务注册中心、端口号等信息，如下：
```java
server.port=8082
#配置服务的名称
spring.application.name=05-springcloud-service-feign
#配置eureka注册中心地址
eureka.client.service-url.defaultZone=http://eureka8761:8761/eureka/,http://eureka8762:8762/eureka/
```
第七步：测试
依次启动注册中心、服务提供者和feign实现服务消费者，然后访问如下地址：http://localhost:8082/web/hello。
## 使用Feign实现消费者的测试
之前我们为了简化RestTemplate操作，将之封装在一个BookService中，但同时我们也发现BookService中的方法几乎都是模板式的，写起来很枯燥，Spring Cloud Feign对此进行了进一步的封装，简化了我们的封装操作。
Feign的基本使用，在HelloService类中声明接口时，我们发现这里的代码可以直接从服务提供者的Controller中复制过来，这些可以复制的代码Spring Cloud Feign对它进行了进一步的抽象，这里就用到了Feign的继承特性，Feign继承特性的方便之处了，这种方式用起来确实很方面，但是也带来一个问题，就是服务提供者和服务消费者的耦合度太高，此时如果服务提供者修改了一个接口的定义，服务消费者可能也得跟着变化，进而带来很多未知的工作量，因此小伙伴们在使用继承特性的时候，要慎重考虑。
# Spring Cloud API网关Zuul
Spring Cloud的Zuul是什么
通过前面内容的学习，我们已经可以基本搭建出一套简略版的微服务架构了，我们有注册中心 Eureka，可以将服务注册到该注册中心中，我们有 Ribbon 或Feign 可以实现对服务负载均衡地调用，我们有 Hystrix 可以实现服务的熔断，但是我们还缺少什么呢?
我们首先来看一个微服务架构图：
![](https://images.cherryfloris.eu.org/2021/1634027643698-ddafd82f-7bac-434c-9501-2e73919a6024.png)
在上面的架构图中，我们的服务包括：内部服务 Service A 和内部服务 ServiceB，这两个服务都是集群部署，每个服务部署了 3 个实例，他们都会通过 EurekaServer 注册中心注册与订阅服务，而 Open Service 是一个对外的服务，也是集群部署，外部调用方通过负载均衡设备调用 Open Service 服务，比如负载均衡使用 Nginx，这样的实现是否合理，或者是否有更好的实现方式呢?接下来我们主要围绕该问题展开讨论。
1、如果我们的微服务中有很多个独立服务都要对外提供服务，那么我们要如何去管理这些接口?特别是当项目非常庞大的情况下要如何管理?
2、在微服务中，一个独立的系统被拆分成了很多个独立的服务，为了确保安全，权限管理也是一个不可回避的问题，如果在每一个服务上都添加上相同的权限验证代码来确保系统不被非法访问，那么工作量也就太大了，而且维护也非常不方便。
为了解决上述问题，微服务架构中提出了 API 网关的概念，它就像一个安检站一样，所有外部的请求都需要经过它的调度与过滤，然后 API 网关来实现请求路由、负载均衡、权限验证等功能;
那么 Spring Cloud 这个一站式的微服务开发框架基于 Netflix Zuul 实现了Spring Cloud Zuul，采用 Spring Cloud Zuul 即可实现一套 API 网关服务。
## 使用Zuul构建API网关
1、创建一个普通的 Spring Boot 工程名为 06-springcloud-api-gateway，然后添加相关依赖，这里我们主要添加两个依赖 zuul 和 eureka 依赖：
```java
<!--添加spring cloud的zuul的起步依赖-->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-zuul</artifactId>
</dependency>
<!--添加spring cloud的eureka的客户端依赖-->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
```
2、在入口类上添加@EnableZuulProxy 注解，开启 Zuul 的 API 网关服务功能：
```java
@EnableZuulProxy //开启Zuul的API网关服务功能
@SpringBootApplication
public class Application {
        public static void main(String[] args) {
           SpringApplication.run(Application.class, args);
        }
}

```
3、在 application.properties 文件中配置路由规则：
```java
#配置服务内嵌的Tomcat端口
server.port=8080

#配置服务的名称
spring.application.name=06-springcloud-api-gateway 

#配置路由规则
zuul.routes.api-wkcto.path=/api-wkcto/** 
zuul.routes.api-wkcto.serviceId=05-springcloud-service-feign 

#配置API网关到注册中心上，API网关也将作为一个服务注册到eureka-server上
eureka.client.service-url.defaultZone=http://eureka8761:8761/eureka/,http:/
/eureka8762:8762/eureka/
```
以上配置，我们的路由规则就是匹配所有符合/api-wkcto/**的请求，只要路径中带有/api-wkcto/都将被转发到 05-springcloud-service-feign 服务上，至于05-springcloud-service-feign 服务的地址到底是什么则由 eureka-server 注册中心去分析，我们只需要写上服务名即可。
以我们目前搭建的项目为例，请求 http://localhost:8080/api-wkcto/web/hello 接口则相当于请求 http://localhost:8082/web/hello(05-springcloud-service-feign 服务的地址为 http://localhost:8082/web/hello)，路由规则中配置的 api-wkcto 是路由的名字，可以任意定义，但是一组 path 和serviceId 映射关系的路由名要相同。
如果以上测试成功，则表示们的 API 网关服务已经构建成功了，我们发送的符合路由规则的请求将自动被转发到相应的服务上去处理。
## Zuul进行请求过滤
我们知道 Spring cloud Zuul 就像一个安检站，所有请求都会经过这个安检站，所以我们可以在该安检站内实现对请求的过滤，下面我们以一个权限验证案例说这一点：
1、我们定义一个过滤器类并继承自 ZuulFilter，并将该 Filter 作为一个 Bean：
```java
@Component 
public class AuthFilter extends ZuulFilter { 
    @Override 
    public String filterType() { 
        return "pre"; 
    } 
    @Override 
    public int filterOrder() { 
        return 0; 
    } 
    @Override 
    public boolean shouldFilter() { 
        return true; 
    } 
    @Override 
    public Object run() throws ZuulException { 
        RequestContext ctx = RequestContext.getCurrentContext(); 
        HttpServletRequest request = ctx.getRequest(); 
        String token = request.getParameter("token"); 
        if (token == null) { 
            ctx.setSendZuulResponse(false); 
            ctx.setResponseStatusCode(401); 
            
ctx.addZuulResponseHeader("content-type","text/html;charset=utf-8"); 
            ctx.setResponseBody("非法访问"); 
        } 
        return null; 
    } 
} 
```
（1）filterType 方法的返回值为过滤器的类型，过滤器的类型决定了过滤器在哪个生命周期执行，pre 表示在路由之前执行过滤器，其他值还有 post、error、route 和 static，当然也可以自定义。
（2）filterOrder 方法表示过滤器的执行顺序，当过滤器很多时，我们可以通过该方法的返回值来指定过滤器的执行顺序。
（3）shouldFilter 方法用来判断过滤器是否执行，true 表示执行，false 表示不执行。
（4）run 方法则表示过滤的具体逻辑，如果请求地址中携带了 token 参数的话，则认为是合法请求，否则为非法请求，如果是非法请求的话，首先设置ctx.setSendZuulResponse(false); 表示不对该请求进行路由，然后设置响应码和响应值。这个 run 方法的返回值目前暂时没有任何意义，可以返回任意值。
2、通过 http://localhost:8080/api-wkcto/web/hello 地址访问，就会被过滤器过滤。
## Zuul的路由规则
1、 在前面的例子中：
```java
#配置路由规则
zuul.routes.api-wkcto.path=/api-wkcto/**
zuul.routes.api-wkcto.serviceId=05-springcloud-service-feign

当访问地址符合/api-wkcto/**规则的时候，会被自动定位到05-springcloud-service-feign  服务上，不过两行代码有点麻烦，还可以简化为：

zuul.routes.05-springcloud-service-feign=/api-wkcto/**
zuul.routes  后面跟着的是服务名，服务名后面跟着的是路径规则，这种配置方式更简单。
```
2、 如果映射规则我们什么都不写，系统也给我们提供了一套默认的配置规则默认的配置规则如下：
```java
#默认的规则
zuul.routes.05-springcloud-service-feign.path=/05-springcloud-service-feign/**
zuul.routes.05-springcloud-service-feign.serviceId=05-springcloud-service-feign
```
3、默认情况下，Eureka 上所有注册的服务都会被 Zuul 创建映射关系来进行路由。
但是对于我这里的例子来说，我希望：05-springcloud-service-feign 提供服务;而01-springcloud-service-provider 作为服务提供者只对服务消费者提供服务，不对外提供服务。
如果使用默认的路由规则，则 Zuul 也会自动为01-springcloud-service-provider 创建映射规则，这个时候我们可以采用如下方式来让 Zuul 跳过 01-springcloud-service-provider 服务，不为其创建路由规则：
```java
#忽略掉服务提供者的默认规则
zuul.ignored-services=01-springcloud-service-provider
```
不给某个服务设置映射规则，这个配置我们可以进一步细化，比如说我不想给/hello 接口路由，那我们可以按如下方式配置：
```java
#忽略掉某一些接口路径
zuul.ignored-patterns=/**/hello/**
```
此外，我们也可以统一的为路由规则增加前缀，设置方式如下：
```java
#配置网关路由的前缀
zuul.prefix=/myapi
```
此时我们的访问路径就变成了 http://localhost:8080/myapi/web/hello
4、 路由规则通配符的含义：

| 通配符 | 含义 | 举例 | 说明 |
| --- | --- | --- | --- |
| ? | 匹配任意单个字符 | /05-springcloud-service-feign/? | 匹配
/05-springcloud-service-feign/a,
/05-springcloud-service-feign/b,
/05-springcloud-service-feign/c 等 |
| * | 匹配任意数量的字符 | /05-springcloud-service-feign/* | 匹配
/05-springcloud-service-feign/aaa,
/05-springcloud-service-feign/bbb,
/05-springcloud-service-feign/ccc 等，
无法匹配
/05-springcloud-service-feign/a/b/c |
| ** | 匹配任意数量的字符 | /05-springcloud-service-feign/** | 匹配
/05-springcloud-service-feign/aaa,
/05-springcloud-service-feign/bbb,
/05-springcloud-service-feign/ccc 等，
也可以匹配
/05-springcloud-service-feign/a/b/c |

5、一般情况下 API 网关只是作为各个微服务的统一入口，但是有时候我们可能也需要在 API 网关服务上做一些特殊的业务逻辑处理，那么我们可以让请求到达 API 网关后，再转发给自己本身，由 API 网关自己来处理，那么我们可以进行如下的操作：
在 06-springcloud-api-gateway 项目中新建如下 Controller：
```java
@RestController 
public class GateWayController { 
    @RequestMapping("/api/local") 
    public String hello() { 
        return "exec the api gateway."; 
    } 
} 
```
然后在 application.properties 文件中配置：
```java
zuul.routes.gateway.path=/gateway/**
zuul.routes.gateway.url=forward:/api/local
```
Zuul的异常处理
Spring Cloud Zuul 对异常的处理是非常方便的，但是由于 Spring Cloud 处于迅速发展中，各个版本之间有所差异，本案例是以 Finchley.RELEASE 版本为例，来说明 Spring Cloud Zuul 中的异常处理问题。
首先我们来看一张官方给出的 Zuul 请求的生命周期图：
![](https://images.cherryfloris.eu.org/2021/1634027899764-d1e00720-5d5d-46fe-982b-c4be1e31b0f0.png)
1、正常情况下所有的请求都是按照 pre、route、post 的顺序来执行，然后由 post返回 response。
2、在 pre 阶段，如果有自定义的过滤器则执行自定义的过滤器。
3、pre、routing、post 的任意一个阶段如果抛异常了，则执行 error 过滤器。
我们可以有两种方式统一处理异常：
（1）禁用 zuul 默认的异常处理 SendErrorFilter 过滤器，然后自定义我们自己的Errorfilter 过滤器
```java
zuul.SendErrorFilter.error.disable=true
@Component 
public class ErrorFilter extends ZuulFilter { 
    private static final Logger logger = 
LoggerFactory.getLogger(ErrorFilter.class); 
    @Override 
    public String filterType() { 
        return "error"; 
    } 
    @Override 
    public int filterOrder() { 
        return 1; 
    } 
    @Override 
    public boolean shouldFilter() { 
        return true; 
    } 
    @Override 
    public Object run() throws ZuulException { 
        try { 
            RequestContext context = RequestContext.getCurrentContext(); 
            ZuulException exception = (ZuulException)context.getThrowable(); 
            logger.error("进入系统异常拦截", exception); 
            HttpServletResponse response = context.getResponse(); 
            response.setContentType("application/json; charset=utf8"); 
            response.setStatus(exception.nStatusCode); 
            PrintWriter writer = null; 
            try { 
                writer = response.getWriter(); 
                writer.print("{code:"+ exception.nStatusCode +",message:\""+ 
exception.getMessage() +"\"}"); 
            } catch (IOException e) { 
                e.printStackTrace(); 
            } finally { 
                if(writer!=null){ 
                    writer.close(); 
                } 
            } 
        } catch (Exception var5) { 
            ReflectionUtils.rethrowRuntimeException(var5); 

        } 
        return null; 
    } 
} 
```
（2）自定义全局 error  错误页面
```java
@RestController 
public class ErrorHandlerController implements ErrorController { 
    /** 
     * 出异常后进入该方法，交由下面的方法处理
     */ 
    @Override 
    public String getErrorPath() { 
        return "/error"; 
    } 
    @RequestMapping("/error") 
    public Object error(){ 
        RequestContext ctx = RequestContext.getCurrentContext(); 
        ZuulException exception = (ZuulException)ctx.getThrowable(); 
        return exception.nStatusCode + "--" + exception.getMessage(); 
    } 
} 
```
# Spring Cloud Config配置中心
Spring Cloud Config配置中心是什么
在分布式系统中，尤其是当我们的分布式项目越来越多，每个项目都有自己的配置文件，对配置文件的统一管理就成了一种需要，而 Spring Cloud  Config  就提供了对各个分布式项目配置文件的统一管理支持。Spring Cloud Config  也叫分布式配置中心，市面上开源的分布式配置中心有很多，比如国内的， 360  的QConf、淘宝的 diamond、百度的 disconf  都是解决分布式系统配置管理问题，国外也有很多开源的配置中心 Apache 的 Apache Commons Configuration、owner、cfg4j  等等；
Spring Cloud Config 是一个解决分布式系统的配置管理方案。它包含 Client和 Server 两个部分，Server 提供配置文件的存储、以接口的形式将配置文件的内容提供出去，Client 通过接口获取数据、并依据此数据初始化自己的应用。
Spring cloud 使用 git 或 svn 存放配置文件，默认情况下使用 git。
## 构建Spring cloud config配置中心
构建一个 spring cloud config 配置中心按照如下方式进行：
1、创建一个普通的 Spring Boot 项目
2、在 pom.xml 文件中添加如下依赖：
```java
<dependency>
<groupId>org.springframework.cloud</groupId>
<artifactId>spring-cloud-config-server</artifactId>
</dependency>
```
3、在入口类，也就是 main 方法的类上添加注解 @EnableConfigServer
4、在 application.properties 中配置一下 git 仓库信息，此处我们使用 GitHub( 也可以使用码云 gitee ) ， 首先在我的 Github 上创建一个名为spring-cloud-config 的项目，创建之后，再做如下配置：
```java
server.port=3721
spring.application.name=07-springcloud-config-server
spring.cloud.config.server.git.uri=https://github.com/myspring/sprin
g-cloud-config.git
spring.cloud.config.server.git.search-paths=config-center
spring.cloud.config.server.git.username=xxxx@163.com
spring.cloud.config.server.git.password=xxxx123456
```
其中：
● uri 表示配置中心所在仓库的位置
● search-paths 表示仓库下的子目录
● username 表示你的 GitHub 用户名
● password 表示你的 GitHub 密码
至此我们的配置中心服务端就创建好了。
## 构建Springcloud config配置中心仓库
接下来我们需要在 github 上设置好配置中心，首先在本地创建一个文件夹叫wkcto，然后在里面创建一个文件夹叫 config-center，然后在 config-center中创建四个配置文件，如下：
```java
application.properties
application-dev.properties
application-test.properties
application-online.properties
```
在四个文件里面分别写上要测试的内容：
```java
url=http://www.wkcto.com
url=http://dev.wkcto.com
url=http://test.wkcto.com
url=http://online.wkcto.com
```
然后回到 wkcto 目录下，依次执行如下命令将本地文件同步到 Github 仓库中：
说明：在使用命令之前先从 https://git-scm.com/ 网站下载安装 git 的 window 客户端
1、添加提交人的账号信息，git 需要知道提交人的信息作为标识;
```java
git config --global user.name 'junge'
git config --global user.email 'junge@163.com'
```
2、将该目录变为 git 可以管理的目录;
```java
git init
```
3、将文件添加到暂存区
```java
git add config-center/
```
4、把文件提交到本地仓库;
```java
git commit -m 'add config-center'
```
5、添加远程主机;
```java
git remote add origin https://github.com/hnylj/spring-cloud-config.git
```
6、将本地的 master 分支推送到 origin 主机;
```java
git push -u origin master
```
至此，我们的配置文件就上传到 GitHub 上了。
此时启动我们的配置中心，通过/{application}/{profile}/{label}就能访问到我们的配置文件了;
其中：
```java
{application}表示配置文件的名字，对应的配置文件即application，
{profile}表示环境，有dev、test、online及默认，
{label}
```
通过浏览器上访问 http://localhost:3721/application/dev/master
返回的 JSON 格式的数据：
name 表示配置文件名 application 部分，profiles 表示环境部分，label 表示分支，version 表示 GitHub 上提交时产生的版本号，同时当我们访问成功后，在控制台会打印了相关的日志信息;当访问成功后配置中心会通过 git clone 命令将远程配置文件在本地也保存一份，以确保在 git 仓库故障时我们的应用还可以继续正常使用。
## 构建Spring cloud config配置中心客户端
前面已经搭建好了配置中心的服务端，接下来我们来看看如何在客户端应用中使用。
1、创建一个普通的 Spring Boot 工程 08-springcloud-config-client，并添加如下依赖：
```java
<dependency>
   <groupId>org.springframework.cloud</groupId>
   <artifactId>spring-cloud-starter-config</artifactId>
</dependency>
```
2、创建 bootstrap.properties 文件，用于获取配置信息，文件内容如下：
(注意这些信息一定要放在 bootstrap.properties 文件中才有效)
```java
server.port=3722

spring.application.name=application
spring.cloud.config.profile=dev
spring.cloud.config.label=master
spring.cloud.config.uri=http://localhost:3721/
```
其中：
name 对应配置文件中的 application 部分，profile 对应了 profile 部分，label 对应了 label 部分，uri 表示配置中心的地址。
3、创建一个 Controller 进行测试：
```java
@RestController
@RefreshScope
public class ConfigController {
   @Value("${url}")
   http://www.wkcto.com
   private String url;
   @Autowired
   private Environment env;
   @RequestMapping("/cloud/url")
   public String url () {
      return this.url;
   }
   @RequestMapping("/cloud/url2")
   public String url2 () {
      return env.getProperty("url");
   }
}
```
我们可以直接使用@Value 注解注入配置的属性值，也可以通过 Environment对象来获取配置的属性值。
## Spring cloud config配置中心客户端测试
通过客户端应用测试是否能够获取到配置中心配置的数据;
## Spring cloud config的工作原理
Spring cloud Config Server 的工作过程如下图所示：
![](https://images.cherryfloris.eu.org/2021/1634028377336-5ed21c72-36ea-4f63-9983-cc7617dc74c0.png)
1、首先需要一个远程 Git 仓库，平时测试可以使用 GitHub，在实际生产环境中，需要自己搭建一个 Git 服务器，远程 Git 仓库的主要作用是用来保存我们的配置文件;
2、除了远程 Git 仓库之外，我们还需要一个本地 Git 仓库，每当 Config Server访问远程 Git 仓库时，都会克隆一份到本地，这样当远程仓库无法连接时，就直接使用本地存储的配置信息;
3、微服务 A、微服务 B 则是我们的具体应用，这些应用在启动的时会从 ConfigServer 中获取相应的配置信息;
4.当微服务 A、微服务 B 尝试从 Config Server 中加载配置信息的时候，ConfigServer 会先通过 git clone 命令克隆一份配置文件保存到本地;
5、由于配置文件是存储在 Git 仓库中，所以配置文件天然具有版本管理功能;
## Spring cloud config的安全保护
生产环境中我们的配置中心肯定是不能随随便便被人访问的，我们可以加上适当的保护机制，由于微服务是构建在 Spring Boot 之上，所以整合 Spring Security是最方便的方式。
1、在 springcloud config server 项目添加依赖：
```java
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```
2、在 springcloud config server 项目的 application.properties 中配置用户名密码：
```java
spring.security.user.name=wkcto
spring.security.user.password=123456
```
3、在 springcloud config client 上 bootstrap.properties 配置用户名和密码：
```java
spring.cloud.config.username=wkcto
spring.cloud.config.password=123456
```
4、最后测试验证;
