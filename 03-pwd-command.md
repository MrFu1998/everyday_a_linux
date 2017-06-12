

## pwd命令

`Linux`中会用`pwd`命令来查看*当前工作目录*的完整路径，简单来说，每当你在终端操作时，都会有一个当前工作目录，在不太确定当前位置时，可以使用`pwd`来判断当前目录在文件系统内的确切位置

#### 1.命令格式：

`pwd [选项]`

#### 2.命令功能：

查看_当前工作目录_的完整路径

#### 3.常用参数：

一般情况下不带任何参数

如果目录的链接时：

格式：`pwd -P`显示出实际路径，而非使用链接（`link`）路径

#### 4.常用实例：

##### 实例一：用`pwd`命令查看默认工作目录的完整路径

命令：`pwd`

输出：

```shell
char@ubuntu:~$ pwd
/home/char
char@ubuntu:~$ 
```

#### 实例二：使用`pwd`命令查看指定文件夹

命令：`pwd`

输出：

```shell
root@ubuntu:~# cd /opt/test
root@ubuntu:/opt/test# pwd
/opt/test
root@ubuntu:/opt/test# 
```



#### 实例三：目录连接链接时，`pwd -P`显示出实际路径，而非使用链接（`link`）路径；`pwd`显示的是连接路径

命令：`pwd -P`

我试过这个命令，感觉无效：

```shell
root@ubuntu:/# cd etc/nginx/conf.d/
root@ubuntu:/etc/nginx/conf.d# pwd
/etc/nginx/conf.d
root@ubuntu:/etc/nginx/conf.d# pwd -P
/etc/nginx/conf.d
```

以下是原作者的输出：

```shell
[root@localhost soft]# cd /etc/init.d
[root@localhost init.d]# pwd
/etc/init.d
[root@localhost init.d]# pwd -P
/etc/rc.d/init.d
[root@localhost init.d]#
```

#### 实例四：`/bin/pwd`

命令：`/bin/pwd [选项]`

选项：

>-L 目录连接链接时，输出连接路径

>-P 输出物理路径

输出：

以下为我的输出

```shell
root@ubuntu:/etc/nginx/conf.d# /bin/pwd
/etc/nginx/conf.d
root@ubuntu:/etc/nginx/conf.d# /bin/pwd --help
Usage: /bin/pwd [OPTION]...
Print the full filename of the current working directory.

  -L, --logical   use PWD from environment, even if it contains symlinks
  -P, --physical  avoid all symlinks
      --help     display this help and exit
      --version  output version information and exit

If no option is specified, -P is assumed.

NOTE: your shell may have its own version of pwd, which usually supersedes
the version described here.  Please refer to your shell's documentation
for details about the options it supports.

GNU coreutils online help: <http://www.gnu.org/software/coreutils/>
Full documentation at: <http://www.gnu.org/software/coreutils/pwd>
or available locally via: info '(coreutils) pwd invocation'
root@ubuntu:/etc/nginx/conf.d# /bin/pwd -L
/etc/nginx/conf.d
root@ubuntu:/etc/nginx/conf.d# /bin/pwd -P
/etc/nginx/conf.d
root@ubuntu:/etc/nginx/conf.d# 
```

作者的输出为：

```shell
[root@localhost init.d]# /bin/pwd
/etc/rc.d/init.d
[root@localhost init.d]# /bin/pwd --help
[root@localhost init.d]# /bin/pwd -P
/etc/rc.d/init.d
[root@localhost init.d]# /bin/pwd -L
/etc/init.d
[root@localhost init.d]#
```

#### 实例五：当前目录被删除了，但是`pwd`命令仍让显示当前目录

输出：

```shell
root@ubuntu:/etc/nginx/conf.d# cd /opt/test
root@ubuntu:/opt/test# pwd
/opt/test
root@ubuntu:/opt/test# rm -f  test
root@ubuntu:/opt/test# pwd
/opt/test
root@ubuntu:/opt/test# cd ..
root@ubuntu:/opt# ls
char_flask  test
root@ubuntu:/opt# cd test
root@ubuntu:/opt/test# rm ../test -rf
root@ubuntu:/opt/test# pwd
/opt/test
root@ubuntu:/opt/test# cd ..
root@ubuntu:/opt# ls
char_flask

```

