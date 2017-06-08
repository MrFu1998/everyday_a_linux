## touch 命令

`linux`的`touch`命令不常用，一般在使用`make`的时候可能会用到，用来修改文件的时间戳。或者新一个不存在的文件。

### 1.命令格式：

`touch [选项]..  文件.. 

### 2.命令参数：

>  ` -a`,`--time=atime`,`--time=access`,`--time=use` 只更改存取时间
>
> `  -c`,` --no-create  `不建立任何文档   
>
> `-d`, `--date=STRING      `使用指定的日期时间，而非现在的时间
>
>  `-f` 此参数将忽略不予处理，仅复制解决`BSD`版本`touch`指令的兼容性问题                    
>
>   `-h`, `--no-dereference`   影响每个符号链接，而不是任何引用
>
> `  -m`,`--time=mtime`,`--time=modify`只更改变动时间
>
>   `-r`, `--reference=FILE` 吧指定文档或目录的日期时间，统统设成和参考文档或目录的日期时间相同 
>
>  ` -t` 使用指定的日期时间，而非现在的时间
>
> 以下这两个参数几乎所有的命令都有，以后就不写了
>
>  `–help` 显示此帮助信息并离开
>
> `–version` 显示版本信息并离开

### 3.命令功能：

`touch`命令参数可更改文档或目录的日期时间，包括存取时间和更改时间

#### 4.常用实例：

#### 例一：用`touch`创建不存在的文件

命令 ： `touch log1.log log2.log log3.log`

输出：

```shell
root@ubuntu:/home/test/test# touch log1.log log2.log log3.log
root@ubuntu:/home/test/test# ls
log1.log  log2.log  log3.log
root@ubuntu:/home/test/test# 
```

如果`log4.log`不存在，则不创建文件

```shell
root@ubuntu:/home/test/test# touch -c  log4.log
root@ubuntu:/home/test/test# ls
log1.log  log2.log  log3.log
root@ubuntu:/home/test/test# touch -c  log2.log
root@ubuntu:/home/test/test# ls
log1.log  log2.log  log3.log
```

### 例二：更新`log.log`的时间和`log1.log`时间戳相同

命令:`touch -r log.log log1.log`

输出：

```shell
root@ubuntu:/home/test/test# touch log.log
root@ubuntu:/home/test/test# ll
total 8
drwxr-xr-x 2 root root 4096 Jun  4 03:34 ./
drwxr-xr-x 4 test test 4096 Jun  4 02:49 ../
-rw-r--r-- 1 root root    0 Jun  4 02:50 log1.log
-rw-r--r-- 1 root root    0 Jun  4 02:52 log2.log
-rw-r--r-- 1 root root    0 Jun  4 02:50 log3.log
-rw-r--r-- 1 root root    0 Jun  4 03:34 log.log
root@ubuntu:/home/test/test# touch -r log.log log1.log
root@ubuntu:/home/test/test#
total 8
drwxr-xr-x 2 root root 4096 Jun  4 03:34 ./
drwxr-xr-x 4 test test 4096 Jun  4 02:49 ../
-rw-r--r-- 1 root root    0 Jun  4 03:34 log1.log
-rw-r--r-- 1 root root    0 Jun  4 02:52 log2.log
-rw-r--r-- 1 root root    0 Jun  4 02:50 log3.log
-rw-r--r-- 1 root root    0 Jun  4 03:34 log.log
root@ubuntu:/home/test/test# 
```

### 例三：设定文件的时间戳

命令:`touch -t 201611142234.50 log.log`

输出：

```shell
root@ubuntu:/home/test/test# ll
total 8
drwxr-xr-x 2 root root 4096 Jun  4 03:34 ./
drwxr-xr-x 4 test test 4096 Jun  4 02:49 ../
-rw-r--r-- 1 root root    0 Jun  4 03:34 log1.log
-rw-r--r-- 1 root root    0 Jun  4 02:52 log2.log
-rw-r--r-- 1 root root    0 Jun  4 02:50 log3.log
-rw-r--r-- 1 root root    0 Jun  4 03:34 log.log
root@ubuntu:/home/test/test# touch -t 201611142234.50 log.log
root@ubuntu:/home/test/test# ll
total 8
drwxr-xr-x 2 root root 4096 Jun  4 03:34 ./
drwxr-xr-x 4 test test 4096 Jun  4 02:49 ../
-rw-r--r-- 1 root root    0 Jun  4 03:34 log1.log
-rw-r--r-- 1 root root    0 Jun  4 02:52 log2.log
-rw-r--r-- 1 root root    0 Jun  4 02:50 log3.log
-rw-r--r-- 1 root root    0 Nov 14  2016 log.log
root@ubuntu:/home/test/test# 
```

**说明：**

`-t  time` 使用指定的时间值 `time` 作为指定文件相应时间戳记的新值．此处的 `time`规定为如下形式的十进制数:      

`[[CC]YY]MMDDhhmm[.SS]`     

  这里，`CC`为年数中的前两位，即”世纪数”；`YY`为年数的后两位，即某世纪中的年数．如果不给出`CC`的值，则`touch`   将把年数`CCYY`限定在`1969--2068`之内．`MM`为月数，`DD`为天将把年数`CCYY`限定在`1969--2068`之内．`MM`为月数，`DD`为天数，`hh` 为小时数(几点)，`mm`为分钟数，`SS`为秒数．此处秒的设定范围是`0--61`，这样可以处理闰秒．这些数字组成的时间是环境变量`TZ`指定的时区中的一个时 间．由于系统的限制，早于1970年1月1日的时间是错误的。