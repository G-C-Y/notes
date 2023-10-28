一   查询
1   语句的查询顺序
![image.png](https://images.cherryfloris.eu.org/2021/1638266355931-9dc58005-3526-41f6-a23a-570d93de4049.png)
二  基本查询
1   基本查询
1)  show function ;      查询所有的函数
2)  desc function "函数名"  ;      查看某个函数具体的语法(怎么用)
2   常用函数
1)   求总行数(count) : hive (default)> select count(*) cnt from emp;   ---cnt 是总行数的别名
2)  求工资的最大值 : hive (default)> select max(sal) max_sal from emp;   ---max_sal 是最大值的别名
3)  求工资最小值 : hive (default)> select min(sal) min_sal from emp;   ---min_sal 是最小值的别名
4)  求工资总和 : hive (default)> select sum(sal) sum_sal from emp; 
5)  求工资平均值 : hive (default)> select avg(sal) avg_sal from emp;
3   Limit 语句
典型的查询会返回多行数据 .Limit 子句用于限制返回的行数
hive (default)> select * from emp limit 5;   ----每一页5条数据
-------参数1  起始的行数 0开始计数  
-------参数2  每页显示的条数
hive (default)> select * from emp limit 2, 5;
三   Where 语句
1  使用 where 子句 ,将不满足条件的行过滤掉
2   where 子句紧随 from 子句后面
1   比较运算符(between..and.. / is null / in)
1.1  案例实操 : 
1) 查询出工资等于10000的所有员工的信息-------where 基本用法

hive (default)> select * from where  sal=10000;

2) 查询出薪水水平在7000到9000之间的员工信息

hive (default)> select * from where  sal between 7000 and 9000;

3) 查询提成为空的员工信息

hive (default)> select * from where  commission is null;

4) 查询工资是15000或者20000的员工信息

hive (default)> select * from where  sal =15000 or sal =20000 ;

hive (default)> select * from where  sal in(15000,20000) ;

2  like 和 rlike

2.1  like 运算符表示类似的值

2.2  选择条件可以包含字符或者数字(%代表0个或者多个字符/任意个字符 ; _ 代表一个字符)

2.3  rlike 子句是 hive 中选择功能的一个扩展 ,其可以通过 java 的正则表达式这个更强大的语言来指定匹配条件

2.4  案例实操 :

1) 查找以 2 开头薪水的员工信息

hive (default)> select * from tb_emp where sal like '2%' 

2) 查找第二个数值为 2 的薪水的员工信息

hive (default)> select * from tb_emp where sal like '_2%'       --- _ 下划线代表占一个字符

3) 查找薪水中包含有 2 的员工信息

hive (default)> select * from tb_emp where sal rlike '[2]'    ---正则表达式

hive (default)> select * from tb_emp where sal like '%2%' 

3  逻辑运算符 (and / or / not)

hive 中不支持 ON 的不等连接

3.1 案例实操

1) 查询出薪水水平大于10000并且年龄大于30岁的员工信息

hive (default)> select * from where  sal >10000 and age>30 ;

2) 查询出薪水水平大于10000或者年龄大于30岁的员工信息

hive (default)> select * from where  sal >10000 or age>30 ;

3) 查询薪资水平除了15000 和20000以外的员工信息

 hive (default)> select * from where  sal not  in(15000, 20000) ;

四   分组
1  Group By 语句

1.1  group by 语句通常会和聚合函数一起使用 ,按照一个或者多个列队结果进行分组 ,然后对每个组执行聚合操作.

1.2  案例实操

1)  计算 emp 表每个部门的平均工资水平

hive (default)> select  emp.deptno, avg(emp.sal)  avg_sal  from  emp  group by emp.deptno;

2)  计算 emp 每个部门中每个岗位的最高薪水

hive (default)> select  emp.deptno,emp.job  max(emp.sal)  max_sal  from  emp  group by emp.deptno , emp.job;

2  Having 语句

2.1  having 与 where 的不同点

1) where 针对表中的列发挥作用 ,查询数据; having 针对查询结果中的列发挥作用,筛选数据 .

2) where 后面不能写分组函数 ,而 having 后面可以使用分组函数

3) having 只用于 group by 分组统计语句

2.2  案例实操

1) 求每个部门的平均薪水大于2000的部门

--------求每个部门的平均工资  group by

hive (default)> select deptno, avg(sal) from emp group by deptno;

--------求每个部门的平均薪水大于2000的部门

hive (default)> select deptno, avg(sal) avg_sal from emp group by deptno having avg_sal > 2000;

五   Join 语句
1  等值 join
1.1  hive 支持通常的 sql join 语句 ,但是只支持等值连接 ,不支持非等值连接

hive (default)> select * from tb_name1 join tb_name2 on tb_name1.deptno = tb_name2.deptno;

hive (default)> select * from tb_name1 join tb_name2 on tb_name1.deptno != tb_name2.deptno;

1.2  案例实操

根据员工和部门表中的部门编号相同 ,查询员工编号,员工名字和部门名字

hive (default)>select emp.empno,emp.ename,dept.dname from emp join dept on emp.deptno = dept.deptno;

2  表的别名
2.1  好处 : 使用别名可以简化查询 ; 使用别名前缀可以提高执行效率

2.2  案例实操

根据员工和部门表中的部门编号相同 ,查询员工编号,员工名字和部门名字

hive (default)>select e.empno,e.ename,d.dname from emp e join dept d on e.deptno = d.deptno;

3  左外连接
Join 操作符左边表中符合 where 子句的所有记录将会被返回(以左边表为主)

hive (default)> select e.empno, e.ename, d.deptno from emp e right join dept d on e.deptno= d.deptno;

4  右外连接
Join 操作符右边表中符合 where 子句的所有记录将会被返回(以右边表为主)

hive (default)> select e.empno, e.ename, d.deptno from emp e left join dept d on e.deptno= d.deptno;

5  多表连接
注意：连接 n个表，至少需要n-1个连接条件。例如：连接三个表，至少需要两个连接条件。

1) 大多数情况下，Hive会对每对JOIN连接对象启动一个MapReduce任务。本例中会首先启动一个MapReduce job对表e和表d进行连接操作，然后会再启动一个MapReduce job将第一个MapReduce job的输出和表l;进行连接操作。

2) 为什么不是表d和表l先进行连接操作呢？这是因为Hive总是按照从左到右的顺序执行的。

5.1  创建表

create table if not exists tb_location(
loc int,
loc_name string
)
row format delimited fields terminated by '\t';
5.2  加载数据

hive (default)> load data local inpath '/root/location.txt' into table default.tb_location;

 5.3  多表连接查询

hive (default)>SELECT 
e.ename, 
d.deptno, 
lo.loc_name
FROM   
emp e    ----别名
JOIN   
dept d
ON     d.deptno = e.deptno 
JOIN   
location lo
ON     d.loc = lo.loc;
 6  笛卡尔积(所有表中的所有行互相连接)-------不推荐/不建议/不要使用!!!---因为产生的数据量太大了,占用太大资源,会导致查询效率低下
案例实操

hive (default)> select empno, dname from tb_emp, tb_dept;

六   排序
1  全局排序(order by ,全局排序,一个Reduce)
1.1  使用 order by 子句排序

order by time asc         升序(默认的) ,asc (ascend)是可以省略的

order by time desc       降序 ,(descend) 不可以省略

1.2  order by 子句在 select 语句的结尾

1.3  案例实操

1)  查询员工信息按工资升序排列

hive (default)> select * from tb_emp order by sal;

2)  查询员工信息按工资降序排列

hive (default)> select * from tb_emp order by sal desc;

2  按照别名排序
按照员工薪水的2倍排序

hive (default)> select ename,sal*2  twosal from tb_emp order by twosal;

3  多个列排序
按照部门和工资升序排序

hive (default)> select ename,deptno,sal   from tb_emp order by deptno,sal;

4  每个MapReduce内部排序（Sort By）  combiner组件-----区内排序--重要!!!
sort by : 每个 reduce 内部进行排序 ,对全局结果集来说不是排序

4.1  设置 reduce 个数 : set mapreduce.job.reduce = 3

4.2  查看设置 reduce 个数 : set mapreduce.job.reduces;

4.3  根据部门编号降序查看员工信息 : select * from emp sort by empno desc; 

4.4  将查询结果导入到本地文件中(按照部门编号降序排列) :  overwrite(重写 ,覆盖的意思)

insert overwrite local directory '/root/hive' select * from emp sort by deptno desc ;

5  分区排序（Distribute By 分区字段）---重要!!!
5.1  Distribute By : 类似 MR 中 partition ,进行分区,结合 sort by 使用

5.2   注意 : hive 要求 distribute by 语句要写在 sort by 语句之前

5.3  对于 distribute by 进行测试, 一定要分配多reduce进行处理 ,否则无法看到distribute by 的效果

5.4  案例实操 : 

按照部门编号分区 ,再按照员工编号降序排序

hive (default)> set mapreduce.job.reduces=3;

hive (default)> insert overwrite local directory '/root/data/distribute-result' select * from emp distribute by deptno sort by empno desc;

原文链接：[https://blog.csdn.net/cch19930303/article/details/108609035](https://blog.csdn.net/cch19930303/article/details/108609035)
