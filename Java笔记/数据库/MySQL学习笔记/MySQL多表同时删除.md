MySQL可以在一个SQL语句中删除多张表的记录，也可以通过多个表之间的关联关系删除某个表的数据，在MySQL4.0版本之后MySQL支持多表删除。
假定目前有两张表goods和goods_price表，前者是保存商品的具体信息，后者是保存商品的价格，具体的表结构如下：
```sql
create table goods (

`id` int unsigned primary key auto_increment,

`goods_name` varchar(30) not null default ''

)engine innodb charset utf8;

create table goods_price (

`goods_id` int unsigned not null,

`price` decimal(8,2) not null default '0.00'

)engine innodb charset utf8;

insert into goods values (1,'商品1'),(2,'商品2'),(3,'商品3'),(4,'商品4'),(5,'商品5');

insert into goods_price values (1,'5.44'),(2,'3.22'),(3,'5.55'),(4,'0.00'),(5,'4.54');
```
### 在delete时使用逗号分割删除
这里我们不适用join连接操作进行删除，具体SQL如下：
```sql
delete g.*,p.* from goods as g,goods_price as p where g.id = p.goods_id and g.id = 1;
```
### 使用连表查询
#### 使用inner join删除
使用inner join在连接时指定表与表之间的关联关系进行删除，具体SQL如下：
```sql
DELETE g.*,p.* FROM goods as g INNER JOIN goods_price as p ON g.id=p.goods_id WHERE g.id = 2;
```
使用连接删除的时候不必删除所有表数据，上面的SQL语句会同时删除goods和goods_price两张表中的数据，但是可以指定DELETE g.*从而只删除goods表中的记录，而不删除goods_price表中的记录[DELETE g.* FROM goods as g INNER JOIN goods_price as p ON g.id=p.goods_id WHERE g.id = 3;]，但是在这里明显是不合适的，但是我们可以这样做。
### 使用left join删除
left join的使用方法如上，具体的SQL如下：
```sql
DELETE g.*,p.* FROM goods as g LEFT JOIN goods_price as p ON g.id=p.goods_id WHERE g.price = '0.00';
```
### 使用外键约束
给表新增约束外键并使用级联(cascade)方式对表与表之间关系进行约束。具体的SQL如下:
```sql
alter table goods_price
add constraint FK_goods_id foreign key(goods_id)
references goods(id) on delete cascade on update cascade;
```
修改完后我们后期删除主表数据，关联表数据也会被删除。
```sql
delete from goods where id=5;
```
### [MYSQL删除三张表的联合信息](https://www.cnblogs.com/hjd21/p/12944346.html)
如要删除三张表的联合信息，使用MYSQL的左连接方法：LEFT JOIN ON
例如，删除三张表中张三的所有数据：
```sql
delete student,sc,stu 
    from student left join sc on student.sno = sc.sno 
                left join stu on sc.sno = stu.sno
                where student.sname = '张三';
```
