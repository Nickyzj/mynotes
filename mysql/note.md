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
  <fieldname> <type> <constrain> <comment>,
  <fieldname> <type> <constrain> <comment>
)

desc <tablename>;

show create table <tablename>; //create table sql
show create table <tablename>\G //show with format

create table <tablename> as select * from <tablename2> where 1=2; //copy table structure. table content will be copied too without where

create table <tablename> like <tablename2>




```



