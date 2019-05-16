### Add mysql to service
```
ps -ef | grep mysql
cp -a mysql.server /etc/rc.d/init.d/mysql
service mysql start
service mysql restart
service mysql stop

cd /usr/local/mysql/bin/
./mysql -uroot -p
exit

ln -s /usr/local/mysql/bin/* /bin

cd /etc
lr -lrt | grep my.cnf

mysql -u<username> -p<password>
```

### Create database
```
create database <database name>
show databases;
show tables;
select database(); //show current database name
use <database>;

create database if not exists <database>;

create database <database> default character set gbk;

show create database <database>; //use default character set in /etc/my.cnf

show variables like 'character%';
```

### create table

```
create table <tablename> (
  <fieldname> <type> <constrain> comment <comment>,
  <fieldname> <type> <constrain> comment <comment>
)

desc <tablename>;

show create table <tablename>; //create table sql
show create table <tablename>\G //show with format

create table <tablename> as select * from <tablename2> where 1=2; //copy table structure. table content will be copied too without where

create table <tablename> like <tablename2>
```

### table maintain
```
rename table <old name> to <new name>;

alter table add <column> <type> comment <comment>;

alter table add <column> <type> comment <comment> first;
alter table add <column> <type> comment <comment> after <column>;

alter table <tablename> modify <column> <new type>;

alter table <tablename> change <old column name> <new column name> <type>;

alter table <tablename> dope <column name>;

alter table <tablename> character set <character set>;

drop table <tablename>;
drop table if exists <tablename>;
```

### DML
```
insert into <tablename> (<fieldname>) values (<value>);
insert into <tablename> values (<all values>);

insert into <tablename1> select * from <tablename2>;
insert into <tablename1> (<columnname1>, <columnname2>) select <columnname1>, <columnname2> from <tablename2>;

create table <tablename1> as select <columnname1>, <columnname2> from <tablename2>;

insert into <tablename> (<columnname>) values (<value1>), (<value2>), (<value3>);

update <tablename> set <coloumnname>=<value>, <columnname2>=<value2> where <columnname>=<value>;

delete from <tablename> where <columnname>=<value>;
delete from table <tablename>; //auto-increment will continue. 数据可以回退，不会释放空间，不会删除定义(auto increment)

truncate <tablename>; //auto-increment will be reset. 删除后不可恢复。会把表占用的空间恢复到最初。

drop table <tablename>; //删除整张表，释放所有空间。

删除速度
drop > truncate > delete

查看当前 mysql 使用的字符集
show variables like 'character%';

解决乱码问题
临时方法：
外部显示  set names gbk;
永久方法：
/etc/my.cnf
default-character-set=utf8
service mysql restart

库字符集：
[mysqld]
character_set_server=utf8

alter database <databasename> default charactere set gbk;
```

### where
```
not equal != <>
like 'xxxx%'
between 1000 and 3000
select * from <tablename> where <columnname> in ('', '','');
select distinct(<columnname>) from <tablename>;

count(<columnname>) or count(*)
select count(*) from <tablename>;

sum(<columnname>)
select sum(<columnname>) from <tablename>;
max()
select * from <tablename> where <columnname> = seclect max(<columnname>) from <tablename>; //find the max record.
avg()
min()

select concat(<columnname1>, <columname2>) from <tablename>; //concat multile string
```

### group
```
查询每个部门有多少员工
select deptnumber, count(*) from employee group by deptnumber; 
select deptnumber, job, count(*) from employee group by deptnumber, job; //显示几个列，group by 也要加几个列
```

### having
```
select job, count(*) from employee group by job having job='文员'; //对结果筛选
select deptnubmer, job, count(*) as '总数' from employee group by deptnumber, job having coung(*)>2; //对 count(*)筛选 

```

### order by
```
order by asc //default
order by desc
```

### limit
```
limit n, m //n 代表起始行数，默认为0，m 代表取出条数
```

### exists
```
select * from <tablename> t1 where exists(select 1 from <tablename2> where <condition>); // exists 中查询有结果则为 True
查询公司有员工的部门的详细信息
select * from dept d where exists (select 1 from employee e where d.deptnumber=e.deptnumber);
select * from dept d where not exists (select 1 from employee e where d.deptnumber=e.deptnumber); //没有员工的部门
```

### left join right join (外连接）
```
left join <tablename> on <condition> /left outer <tablename> join on <condition> //以左表为基准，左表内容都会显示，右表无内容则显示 NULL
right join <tablename> on <condition> /right outer <tablename> join on <condition>

select d.dname, d.addr, e.* from dept d left join employee e on d.detpnumber = e.deptnumber
```

### inner join
```
inner join <tablename> on <condition> //获取两个表中字段相匹配的内容
```

### union
```
把多个查询结果拼成一张表。字段数必须一致。去重。
select * from employee e where e.job=<value1> union select * from employee e where e.job=<value2>; 
union all //不去重
```
