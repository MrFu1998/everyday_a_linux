## rm命令

[上个`mkdir`创建文件和目录的命令](4-mkdir-command.md)，这次这个是删除文件和目录的命令`rm`，`rm`是常用的命令，改命令的功能为删除一个目录的一个或多个文件或目录。它也可以将某个目录及其下的所有文件及子目录都删除，对于链接文件，只是删除了链接。原有文件均保持不变

`rm`是一个十分危险的命令，因为`linux`和`window`不一样`linux`中没有回收站，所以使用的时候要格外小心，尤其是新手。你可以试试在`/（根目录）`执行`rm * -rf `,哈哈，整个系统都会直接崩溃`GG`,所以我们在执行`rm`之前最好先使用`pwd`命令来确认下目前处于那个目录，到底要删除什么东西，操作时保持高度注意力

### 1.命令格式：

`rm [选项] 文件`

### 2.命令功能：

删除一个目录中的一个或多个文件或目录。如果没有使用`-r`选项，则`rm`不会删除目录。如果使用`rm`来删除文件，通常仍可以将该文件恢复原状

### 3.命令参数：

> `-f`,` --force` 忽略不存在的文件，从不给出提示           
>
> `-i` ,`  --interactive`进行交互式删除
>
> ` -r`,` -R`,` --recursive` 指示将参数列出的全部目录和子目录均递归地删除
>   `-d`, `--dir` 删除空目录       
> `  -v`, `--verbose ` 详细显示进行的步骤     
>
> ` --help`     显示此帮助信息并退出
> `  --version ` 输出版本信息并退出

### 4.命令实例：

#### 例一：删除文件`file`，系统会先询问是否删除

命令：`rm 文件名`

输出：我在`root` 用户下执行`rm`删除文件时没有提示，直接就删除了，切换到普通用户时提示权限不足

```shell
root@ubuntu:/opt/test/test3# touch log.log
root@ubuntu:/opt/test/test3# ll

total 8
drwxr-xr-x 2 root root 4096 Jun  3 02:55 ./
drwxr-xr-x 7 root root 4096 Jun  3 01:34 ../
-rw-r--r-- 1 root root    0 Jun  3 02:55 log.log
root@ubuntu:/opt/test/test3# 
root@ubuntu:/opt/test/test3# su char
bash: alias: ls: not found
bash: alias: =: not found
bash: alias: ls -color: not found
char@ubuntu:/opt/test/test3$ ll
total 8
drwxr-xr-x 2 root root 4096 Jun  3 02:55 ./
drwxr-xr-x 7 root root 4096 Jun  3 01:34 ../
-rw-r--r-- 1 root root    0 Jun  3 02:55 log.log
char@ubuntu:/opt/test/test3$ rm log.log
rm: remove write-protected regular empty file 'log.log'? y
rm: cannot remove 'log.log': Permission denied
char@ubuntu:/opt/test/test3$ 
```

这是作者输出：

```shell
[root@localhost test1]# ll
 
总计 4
 
-rw-r--r-- 1 root root 56 10-26 14:31 log.log
 
root@localhost test1]# rm log.log 
 
rm：是否删除 一般文件 “log.log”? y
 
root@localhost test1]# ll
 
总计 0[root@localhost test1]#
```

作者说明：输入`rm log.log`命令后。系统会询问是否删除，输入`y`后删除文件，不想删除则输入`n`

#### 例二：强行删除`file`，系统不再提示

命令：`rm -f log.log`

输出:

```shell
root@ubuntu:/opt/test/test3# ll
total 8
drwxr-xr-x 2 root root 4096 Jun  3 02:55 ./
drwxr-xr-x 7 root root 4096 Jun  3 01:34 ../
-rw-r--r-- 1 root root    0 Jun  3 02:55 log.log
root@ubuntu:/opt/test/test3# rm -f log.log
root@ubuntu:/opt/test/test3# ls
root@ubuntu:/opt/test/test3# 
```

#### 例三：删除任何`.log`文件；删除前逐一询问确认

命令：`rm -i *.log`

```shell
root@ubuntu:/opt/test/test3# touch test.log test1.log test2.log
root@ubuntu:/opt/test/test3# ll
total 8
drwxr-xr-x 2 root root 4096 Jun  3 03:04 ./
drwxr-xr-x 7 root root 4096 Jun  3 01:34 ../
-rw-r--r-- 1 root root    0 Jun  3 03:04 test1.log
-rw-r--r-- 1 root root    0 Jun  3 03:04 test2.log
-rw-r--r-- 1 root root    0 Jun  3 03:04 test.log
root@ubuntu:/opt/test/test3# rm -i *.log
rm: remove regular empty file 'test1.log'? y
rm: remove regular empty file 'test2.log'? y
rm: remove regular empty file 'test.log'? y
root@ubuntu:/opt/test/test3# ll
total 8
drwxr-xr-x 2 root root 4096 Jun  3 03:05 ./
drwxr-xr-x 7 root root 4096 Jun  3 01:34 ../
root@ubuntu:/opt/test/test3# 
```

#### 例四：将`test1`子目录及子目录中所有档案全部删除

命令：`rm -r test1`

输出：

```shell
root@ubuntu:/opt/test# ll
total 28
drwxr-xr-x 7 root root 4096 Jun  3 01:34 ./
drwxr-xr-x 4 root root 4096 Jun  3 01:15 ../
drwxr-xr-x 3 root root 4096 Jun  3 01:17 test1/
drwSrwSrw- 2 root root 4096 Jun  3 01:24 test2/
drwxr-xr-x 2 root root 4096 Jun  3 03:05 test3/
drwxr-xr-x 3 root root 4096 Jun  3 01:28 test4/
drwxr-xr-x 9 root root 4096 Jun  3 01:34 test5/
root@ubuntu:/opt/test# rm -r test1
root@ubuntu:/opt/test# ll
total 24
drwxr-xr-x 6 root root 4096 Jun  3 03:08 ./
drwxr-xr-x 4 root root 4096 Jun  3 01:15 ../
drwSrwSrw- 2 root root 4096 Jun  3 01:24 test2/
drwxr-xr-x 2 root root 4096 Jun  3 03:05 test3/
drwxr-xr-x 3 root root 4096 Jun  3 01:28 test4/
drwxr-xr-x 9 root root 4096 Jun  3 01:34 test5/
root@ubuntu:/opt/test# 
```

按照**作者**的说法，会有提示的，作者输出如下：

```shell
[root@localhost test]# ll
 
总计 24drwxr-xr-x 7 root root 4096 10-25 18:07 scf
 
drwxr-xr-x 2 root root 4096 10-26 14:51 test1
 
drwxr-xr-x 3 root root 4096 10-25 17:44 test2
 
drwxrwxrwx 2 root root 4096 10-25 17:46 test3
 
drwxr-xr-x 2 root root 4096 10-25 17:56 test4
 
drwxr-xr-x 3 root root 4096 10-25 17:56 test5
 
[root@localhost test]# rm -r test1
 
rm：是否进入目录 “test1”? y
 
rm：是否删除 一般文件 “test1/log3.log”? y
 
rm：是否删除 目录 “test1”? y
 
[root@localhost test]# ll
 
总计 20drwxr-xr-x 7 root root 4096 10-25 18:07 scf
 
drwxr-xr-x 3 root root 4096 10-25 17:44 test2
 
drwxrwxrwx 2 root root 4096 10-25 17:46 test3
 
drwxr-xr-x 2 root root 4096 10-25 17:56 test4
 
drwxr-xr-x 3 root root 4096 10-25 17:56 test5
 
[root@localhost test]#
```

#### 例五：`rm -rf test2`命令会将`test2`子目录及其子目录的所以文件全部删除，并且不用一一确认

命令:`rm -rf test2`

输出：

```shell
root@ubuntu:/opt/test# ls
test2  test3  test4  test5
root@ubuntu:/opt/test# rm -rf test2
root@ubuntu:/opt/test# ls
test3  test4  test5
```

#### 例六：删除以`-f`开头的文件

命令：`rm -- -f`

输出：

```shell
root@ubuntu:/opt/test# rm -- -f
root@ubuntu:/opt/test# touch -- -f
root@ubuntu:/opt/test# ls -- -f
-f
root@ubuntu:/opt/test# rm -- -f
root@ubuntu:/opt/test# 
```

#### 例七：自定义回收站功能

命令：`myrm(){ D=/tmp/$(date +%Y%m%d%H%M%S); mkdir -p $D;  mv "$@" $D && echo "moved to $D ok"; }`

```shell
root@ubuntu:/opt/test# myrm(){ D=/tmp/$(date +%Y%m%d%H%M%S); mkdir -p $D;  mv "$@" $D && echo "moved to $D ok"; }
root@ubuntu:/opt/test# alias rm='myrm'
root@ubuntu:/opt/test# touch 1.log 2.log 3.log
root@ubuntu:/opt/test# ls
1.log  2.log  3.log  test3  test4  test5

```



作者输出：

```shell
[root@localhost test]# myrm(){ D=/tmp/$(date +%Y%m%d%H%M%S); mkdir -p $D;  mv "$@" $D && echo "moved to $D ok"; }
 
[root@localhost test]# alias rm='myrm'
 
[root@localhost test]# touch 1.log 2.log 3.log
 
[root@localhost test]# ll
 
总计 16
 
-rw-r--r-- 1 root root    0 10-26 15:08 1.log
 
-rw-r--r-- 1 root root    0 10-26 15:08 2.log
 
-rw-r--r-- 1 root root    0 10-26 15:08 3.log
 
drwxr-xr-x 7 root root 4096 10-25 18:07 scf
 
drwxrwxrwx 2 root root 4096 10-25 17:46 test3
 
drwxr-xr-x 2 root root 4096 10-25 17:56 test4
 
drwxr-xr-x 3 root root 4096 10-25 17:56 test5
 
[root@localhost test]# rm [123].log
 
moved to /tmp/20121026150901 ok
 
[root@localhost test]# ll
 
总计 16drwxr-xr-x 7 root root 4096 10-25 18:07 scf
 
drwxrwxrwx 2 root root 4096 10-25 17:46 test3
 
drwxr-xr-x 2 root root 4096 10-25 17:56 test4
 
drwxr-xr-x 3 root root 4096 10-25 17:56 test5
 
[root@localhost test]# ls /tmp/20121026150901/
 
1.log  2.log  3.log
 
[root@localhost test]#
```



说明：

上面的操作过程模拟了回收站的效果，即删除文件的时候只是把文件放到一个临时目录中，这样在需要的时候还可以恢复过来。





参考资料:[传送门](http://codingstandards.iteye.com/blog/983531)