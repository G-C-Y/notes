实现方式
1.SQL模板
```java
SELECT
	t1.重复列,
	t1.时间列,
	t1.其余列 
FROM
	表 t1
	INNER JOIN ( SELECT t2.重复列, max( t2.时间列 ) AS 时间列 FROM 表 t2 GROUP BY t2.重复列 ) AS t3
	ON t1.重复列 = t3.重复列 AND t1.时间列 = t3.时间列
	GROUP BY t1.重复列
```
思想：
1）先把该表进行 group by 分组，并查询出每组最大的时间列，得到一个子表。
2）再将原本的表和子表通过重复列和时间列关联起来；
这样查询出来的数据，都是以原表数据为准的，得到了时间最大的记录的所有字段信息。
3）但是如果最近的时间不止一条记录，那么就会出现重复，所以在外层还需要对原表进行group by去重。

2.SQL实现
1）mysql 5.7.5 以下版本sql实现：

-- mysql 5.7.5 以下版本
```java
SELECT
	t1.USER_ID,
	t1.last_updated_date,
	t1.ID,
	t1.problems 
FROM
	t_iov_help_feedback t1
	INNER JOIN ( SELECT t2.USER_ID, max( t2.last_updated_date ) AS last_updated_date FROM t_iov_help_feedback t2 GROUP BY t2.USER_ID ) AS t3 
	ON t1.USER_ID = t3.USER_ID AND t1.last_updated_date = t3.last_updated_date
	GROUP BY t1.USER_ID;
```
2）mysql 5.7.5 及以上版本 sql实现：

-- mysql 5.7.5 及以上版本
```java
SELECT
	t1.USER_ID,
	ANY_VALUE(t1.last_updated_date) as last_updated_date,
	ANY_VALUE(t1.ID) as ID,
	ANY_VALUE(t1.problems) as problems
FROM
	t_iov_help_feedback t1
	INNER JOIN ( SELECT t2.USER_ID, max( t2.last_updated_date ) AS last_updated_date FROM t_iov_help_feedback t2 GROUP BY t2.USER_ID ) AS t3 
	ON t1.USER_ID = t3.USER_ID AND t1.last_updated_date = t3.last_updated_date
	GROUP BY t1.USER_ID;
```
为什么高版本和低版本的sql语句不一样？

这是因为mysql 版本高于5.7.5时，默认设置的 sql_mode 模式是：only_full_group_by。如果没有去除这个默认模式，又使用上述低版本的group by语句，会报以下错误：

mysql高版本，对报错字段（非group by字段）加了ANY_VALUE(）函数可以规避这个问题。
tips：ANY_VALUE()会选择被分到同一组的数据里第一条数据的指定列值作为返回数据。

原文链接：[https://blog.csdn.net/u012660464/article/details/113972869](https://blog.csdn.net/u012660464/article/details/113972869)
