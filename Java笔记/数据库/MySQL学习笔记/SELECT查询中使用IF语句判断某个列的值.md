## 问题描述
比如，在MySQL数据库中，有如下的MySQL查询语句：
SELECT id,amount FROM report; 
现在需要根据列amount的值来判断，并转换出对应的查询结果。比如，如果report.type='P'，那么amount的值就是本身，如果report.type='N'，那么amount的值则为-amount，在MySQL数据库中，应该如何实现以上的需要呢？
MySQL数据库中，是否有IF ... ELSE...的判断呢？
## 方案一
在MySQL数据库中，可以使用IF控制函数来处理上述的问题，如下：
```java
SELECT id,         
	   IF(type = 'P', amount, amount * -1) as amount 
FROM report 
```
这条语句写得更健壮些的话，我们还可以使用IFNULL函数来检查判断的字段值是否为null，如下：
```java
SELECT id,         
	   IF(type = 'P', IFNULL(amount,0), IFNULL(amount,0) * -1) as amount 
FROM report 
IFNULL(amount,0)表示：当amount字段的值不空null时，返回其本身，否则返回 0
```
## 方案二
使用case语句，如下：
```java
select id,     
       case report.type         
       		when 'P' then amount         
      		 when 'N' then -amount     
       end as amount 
from     
`report` 
```
## 方案三
在case语句中使用IN(...)，如下：
```java
SELECT CompanyName,
	   CASE WHEN Country IN ('USA', 'Canada') THEN 'North America'          
       		WHEN Country = 'Brazil' THEN 'South America'         
       		ELSE 'Europe' END AS Continent 
FROM Suppliers 
ORDER BY CompanyName; 
```
## 方案四
case语句的另一种写法，如下：
```java
select
	id,   
	case      
        when report_type = 'P'
        then amount
        when report_type = 'N'
        then -amount      
        else null    
    end 
from table 
```
## 方案五
使用UNION，而不使用IF控制函数或者case语句，如下：
```java
SELECT 
	id, amount 
FROM report 
WHERE type='P' 
    
UNION

SELECT id, (amount * -1) AS amount 
FROM report WHERE type = 'N' 

ORDER BY id;
```
