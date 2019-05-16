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

```
