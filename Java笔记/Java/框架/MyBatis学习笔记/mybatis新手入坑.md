## 遇到的bug与解决方法：
### 1、在执行codegenerator时执行成功但没有生成想要的类文件，遇到如下警告：
![image.png](https://images.cherryfloris.eu.org/2021/1629180231819-a0faa96b-9609-4109-941d-90f0850d3629.png)
于是按照告警提示去网上搜解决办法，改路径，refresh刷新，换依赖版本，全部都试过仍然没有反应，想到同事跟我用的代码一样，都没有任何错误，开始思考自己是不是漏掉点什么操作。然后发现自己生成了建表语句之后就没有再管，导致本地没有数据库，codegenerator没有索引到，于是将生成的建表语句导入到Navicat，然后文件顺利生成。
### 2.解决在idea中springboot项目通过@Autowired注解使mapper注入成功，但出现红色下划线错误问题。
开始说明下，虽然出现红色下划线，但是程序是能跑的通的。既然能正常运行就这样好了，但是身为一个有强迫症又喜欢提问题又好学的程序员，忍不了！所以自己分析了一下出错情况，首先程序运行正常，说明代码没为题，但既然没问题那为什么有报错呢？错误原因是什么呢？会不会是idea识别有问题？所以针对以上问题，网上查了资料，给出以下几种答案，个人觉得除了第一种，其他几种都是正解。

#### 第一种方法，降低idea对代码的审查级别。
这也是网上最普遍的解决方法，没有之一。但是，我不建议使用，为什么下面再说。
首先把鼠标放到出错的代码上会出现一个小灯泡，然后点击下灯泡的三角，会出现下图的菜单，最后点击Edit inspection profile setting
![image.png](https://images.cherryfloris.eu.org/2021/1629880073036-9f9c8662-dc46-4221-b619-3cda159b6817.png)
然后会出现下方的弹窗，接着将级别从Error改为Warning，点击ok，设置成功，红色下划线会消失。
![image.png](https://images.cherryfloris.eu.org/2021/1629880091999-be6fe03d-2cf5-4585-be51-86b540b1c8b7.png)
#### 第二种方式，添加注解的方式，解决该问题。
首先查看出错原因：
![image.png](https://images.cherryfloris.eu.org/2021/1629880108125-02cdd4d3-2c5f-455c-bf01-87429d1cc5d3.png)
出错信息提示说：不能自动装配，UserMapper这个bean没有被找到。这就说明idea或者说是spring认为UserMapper没有注入，所以它找不到故而报错（也是这个原因，不建议使用第一种方法解决）。那这就简单了，那我告诉你我注入了bean就好了啊。所以在mapper或者dao上使用注解@Component或者@Repository来告诉spring我已经把这个bean注入进来了，你自己看着办吧。
![image.png](https://images.cherryfloris.eu.org/2021/1629880120749-61c674a5-32c7-4924-beb9-520b7f976ab9.png)
#### 第三种方法，将@Autowired替换成@Resource效果一样，也能解决红色下划线问题。
![image.png](https://images.cherryfloris.eu.org/2021/1629880139805-ce003e78-c3cf-401e-a7d8-6766f43702fc.png)
（至于@Autowired和@Resource的区别自行百度。）
[
](https://blog.csdn.net/it_erge/article/details/93597711)
