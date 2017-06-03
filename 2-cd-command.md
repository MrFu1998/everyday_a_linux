## cd 命令

`Linux  cd`命令可以说是Linux中最基本的命令语句，其它的命令要进行操作，都是建立在使用`cd`命令上的，所以，学习`Linux`常用命令，首先就要学好`cd`命令的使用方法技巧

### 1.命令格式：

`cd  [目录名]`

### 2.命令功能

切换当前目录至`dirName`

### 3.常用范例

#### 3.1 例一：进入系统根目录

命令：`cd /`

输出 : 

```shell
char@ubuntu:~$ cd /
char@ubuntu:/$ 
```

进入系统根目录后通过`ls`命令可以查看

```shell
char@ubuntu:/$ ls
bin   dev  home        lib    lost+found  mnt  proc  run   srv  tmp  var
boot  etc  initrd.img  lib64  media       opt  root  sbin  sys  usr  vmlinuz
char@ubuntu:/$ 
```

命令 :`cd ..` 或者 `cd ..//` 

示范：

```shell
root@ubuntu:/opt/test# pwd
/opt/test
root@ubuntu:/opt/test# cd ..//
root@ubuntu:/opt# cd ..
root@ubuntu:/# pwd
/

```

说明 ：进入某个目录后可以使用`cd ..`一直退，就可以达到根目录

命令 : `cd ../..`或者`cd ../..//`	

示范：

```shell
root@ubuntu:/opt/test# pwd
/opt/test
root@ubuntu:/opt/test# cd ../..
root@ubuntu:/# pwd
/
```

```shell
root@ubuntu:/opt/test# pwd
/opt/test
root@ubuntu:/opt/test# cd ../..//
root@ubuntu:/# pwd
/
```

说明：使用``cd ../..`或者`cd ../..//`	`可以进入当前目录的父目录的父目录

####  例二：使用`cd`命令进入当前用户的主目录

命令1 ： `cd`

示范：

```shell
root@ubuntu:/home/char# pwd
/home/char
root@ubuntu:/home/char# cd
root@ubuntu:~# pwd
/root

```

命令2 ： `cd ~`

输出：

```shell
root@ubuntu:/home/char# pwd
/home/char
root@ubuntu:/home/char# cd ~
root@ubuntu:~# pwd
/root
```

#### 例三：跳转到指定目录

命令： `cd /home/char`

输出:

```shell
root@ubuntu:~# cd /home/char
root@ubuntu:/home/char# pwd
/home/char
root@ubuntu:/home/char# ls
project  py2-env  py3-env  test
root@ubuntu:/home/char# cd test
root@ubuntu:/home/char/test# ls
etc  green.py  heavy.py  zero.md
root@ubuntu:/home/char/test# pwd
/home/char/test
```

说明：跳转到指定目录，从根目录开始，目录名称前加 / ,当前目录内的子目录直接写名称即可

#### 例四：返回进入此目录之前所在的目录

命令：`cd -`

输出 ： 

```shell
root@ubuntu:/home/char/test# pwd
/home/char/test
root@ubuntu:/home/char/test# cd -
/home/char
root@ubuntu:/home/char# pwd
/home/char
root@ubuntu:/home/char# cd -
/home/char/test

```

#### 例五：把上个命令的参数作为`cd`参数使用

命令 ： `cd !$`

输出：

```shell
root@ubuntu:/home/char/test# cd !$
cd -
/home/char
root@ubuntu:/home/char# 

```

