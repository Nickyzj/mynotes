https://www.youtube.com/playlist?list=PLUDwpEzHYYLvFc8ic8eAsN7aFki9YlvRL



## Linux commands

### cat

* create new file

```shell
cat >testing.txt
#content
ctrl-d
```

* display content of file

```shell
cat <testing.txt
```

* concatenating more than one file

```shell
cat testing.txt bigdata.txt
```

* appending data to the existing file

```shell
cat >>testing.txt
```

* copying many files in to one single file

```shell
cat testing.txt bigdata.txt >hadooptesting.txt
```

### mv

* renaming file, directory
* move files

### rm

* delete file

```shell
???
rm -i file.txt # -i will not confirm, rm directly
```

* delete directory

```shell
rm -r directory # -r directory contains file
```

### ls

```shell
ls -l # dolumnar format
ls -a # hidden files
ls -R # display directories along with sub directories
```

### wild card 

```shell
? single
* multiple
[] range of values
ls [a-z]
```

### head

display first lines of file

```shell
head -n3 smple.txt # first three line
```

### tail

display last lines

```shell
tail -n3 sample.txt # last three line
```

### ps

```shell
ps <id> # display id
```

### who

all user connected

### whoami

current user

### grep

```shell
grep "welcome" sample.txt
-i ignore case
-n line number
-c counts number
-v verbose display lines does not match (other lines)
```

### sort

arrange number/text in ascending/descending order

```shell
sort >sample.txt
sort -r >sample.txt # descending
```

### chmod

* owners
* groups
* others
* read - r 4
* write - w 2
* execute - e 1

```shell
chmod u-w g-w o-r sample.txt
```

### Run MapReduce jar file

```shell
hadoop jar wordcount.jar WordCount /wordcountinput/wordcount.txt /wordcountoutput
```

![](https://github.com/Nickyzj/mynotes/blob/master/screenshots/Screen%20Shot%202019-06-27%20at%209.32.58%20PM.png?raw=true)

