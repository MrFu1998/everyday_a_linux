## cp命令

`cp`命令用来复制文件或目录，是`Linux`系统中最常用的命令之一。一般情况下，`shell`会设置一个别名。在命令行下复制文件时，如果目标文件已经存在，就会询问是否覆盖，不管你是你是否使用`-i`参数，但是如果是在shell脚本中执行`cp`时，没有`-i`参数时不会询问是否覆盖，这说明命令行和`shell`脚本的执行方式有些不同

### 1.命令格式

```shell
 cp [选项]... [-T] 源 目的
 或： cp [选项]... 源... 目录
 或： cp [选项]... -t 目录 源...
```

### 2.命令功能

   将源文件复制至目标文件，或将多个源文件复制至目标目录。

### 3.命令参数

>`-a`,` --archive`   等于 `-dR --preserve=all`
>
> 	`--attributes-only`        不要复制文件数据，只是属性
>​	`--backup[=CONTROL]`       为每个已存在的目标文件创建备份
>
>`-b`    类似`--backup` 但不接受参数
>
>  ` --copy-contents`     在递归处理是复制特殊文件内容
>
>`-d`  等于`--no-dereference --preserve=links`
>
>`-f`, `--force `   如果目标文件无法打开则将其移除并重试(当 -n 选项  存在时则不需再选此项)
>
>`-i`,` --interactive`        覆盖前询问(使前面的` -n` 选项失效)
>
>`-H`    跟随源文件中的命令行符号链接
>
>`-l`, `--link`   链接文件而不复制
>
>`-L`, `--dereference`   总是跟随符号链接
>
>`-n`,` --no-clobber`   不要覆盖已存在的文件(使前面的 -i 选项失效)
>
>`-P`,` --no-dereference`   不跟随源文件中的符号链接
>
>`-p `   等于`--preserve=`模式,所有权,时间戳
>
> `--preserve[=ATTR_LIST]` 属性列表   保持指定的属性(默认：模式,所有权,时间戳)，如果可能保持附加属性：环境、链接、xattr 等
>
>`-R`,` -r`,` --recursive ` 复制目录及目录内的所有项目

### 4.常用实例

##### 例一：复制单一文件到目标目录，文件在目标文件中不存在

命令：` cp log.log test2`

输出：

```shell
test@ubuntu:~/test2$ ls
test1  txt2.txt
test@ubuntu:~/test2$ cd ..
test@ubuntu:~$ ls
app  log.log  test  test2  test4
test@ubuntu:~$ cp log.log test2
cp: cannot create regular file 'test2/log.log': Permission denied
test@ubuntu:~$ su root
Password: 
root@ubuntu:/home/test# ls
app  log.log  test  test2  test4
root@ubuntu:/home/test# cp log.log test2
root@ubuntu:/home/test# ls
app  log.log  test  test2  test4
root@ubuntu:/home/test# cd test2
root@ubuntu:/home/test/test2# ls
log.log  test1  txt2.txt
root@ubuntu:/home/test/test2# 

```

**说明**：在没有带-a参数时，两个文件的时间是不一样的。在带了-a参数时，两个文件的时间是一致的。  

#### 例二：目标文件存在时，会询问是否覆盖

命令：

本人输出：

```shell
root@ubuntu:/home/test/test4# ls
log11.txt  log3.log  log3.log~  log.log  txt2.txt
root@ubuntu:/home/test/test4# cd ..
root@ubuntu:/home/test# ls
app  log.log  test  test2  test4
root@ubuntu:/home/test# cp log.log test4
```

**本人说明** ：表示我的直接就覆盖了，没询问，作者的是直接就覆盖了

作者输出：

```shell
[root@localhost test]# cp log.log test5
cp：是否覆盖“test5/log.log”? n
[root@localhost test]# cp -a log.log test5
cp：是否覆盖“test5/log.log”? y
[root@localhost test]# cd test5/
[root@localhost test5]# ll
-rw-r--r-- 1 root root 0 10-28 14:46 log5-1.log
-rw-r--r-- 1 root root 0 10-28 14:46 log5-2.log
-rw-r--r-- 1 root root 0 10-28 14:46 log5-3.log
-rw-r--r-- 1 root root 0 10-28 14:48 log.log
```

**作者说明** ：目标文件存在时，会询问是否覆盖。这是因为cp是cp -i的别名。目标文件存在时，即使加了-f标志，也还会询问是否覆盖。

#### 例三：复制整个目录

命令：`cp -a test2 test4`

输出：

目标目录存在时

```shell
root@ubuntu:/home/test# ls
app  log.log  test  test2  test4
root@ubuntu:/home/test# cp -a test2 test4
root@ubuntu:/home/test# la
app            .bashrc  .mysql_history             test
.bash_history  .cache   .profile                   test2
.bash_logout   log.log  .sudo_as_admin_successful  test4
root@ubuntu:/home/test# ls
app  log.log  test  test2  test4
root@ubuntu:/home/test# tree test4/
test4/
├── log11.txt
├── log3.log
├── log3.log~
├── log.log
├── test2
│   ├── log.log
│   ├── test1
│   └── txt2.txt
└── txt2.txt

2 directories, 7 files

```

目标目录不存在时：

```shell
root@ubuntu:/home/test# ls 
app  log.log  test  test2  test4
root@ubuntu:/home/test# cp -a test2 test3
root@ubuntu:/home/test# ls
app  log.log  test  test2  test3  test4

```

**说明**：注意目标目录存在与否结果是不一样的。目标目录存在时，整个源目录被复制到目标目录里面。若不存在，则复制一个

#### 例四：复制`log.log`建立一个连结档 `log_link.log`

命令：`cp -s log.log log_link.log`

输出：

```shell
root@ubuntu:/home/test# ls
app  log.log  test  test2  test3  test4
root@ubuntu:/home/test# cp -s log.log log_link.log
root@ubuntu:/home/test# ll
total 52
drwxr-xr-x 8 test test 4096 Jun  8 23:08 ./
drwxr-xr-x 3 root root 4096 Apr  3 14:48 ../
drwxr-xr-x 4 root root 4096 Jun  5 21:18 app/
-rw------- 1 test test  315 Jun  4 05:39 .bash_history
-rw-r--r-- 1 test test  220 Apr  3 14:48 .bash_logout
-rw-r--r-- 1 test test 3771 Apr  3 14:48 .bashrc
drwx------ 2 test test 4096 Apr  3 14:52 .cache/
lrwxrwxrwx 1 root root    7 Jun  8 23:08 log_link.log -> log.log
-rw-r--r-- 1 root root    0 Nov 14  2016 log.log
-rw------- 1 test test  198 Apr  7 05:47 .mysql_history
-rw-r--r-- 1 test test  655 Apr  3 14:48 .profile
-rw-r--r-- 1 test test    0 Apr  3 14:52 .sudo_as_admin_successful
drwxr-xr-x 2 root root 4096 Jun  5 22:12 test/
drwxr-xr-x 3 root root 4096 Jun  8 22:51 test2/
drwxr-xr-x 3 root root 4096 Jun  8 22:51 test3/
drwxr-xr-x 3 root root 4096 Jun  8 23:01 test4/
root@ubuntu:/home/test# 
```

**说明**：那个 `log_link.log` 是由` -s` 的参数造成的，建立的是一个『快捷方式』，所以您会看到在文件的最右边，会显示这个文件是『连结』到哪里去