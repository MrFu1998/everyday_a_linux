## mv命令

`mv`命令的`move`的缩写，可以用来移动文件或将文件改名（`move(rename) files`），是`Linux`系统下常用的命令，经常用来备份文件或目录

### 1.命令格式：

`mv [选项] 源文件或目录 目标文件或目录 

### 2.命令功能：

视`mv`命令中第二个参数类型的不同（是目标文件还是目标目录），`mv`命令将文件重命名或将其移至一个新的目录中，当第二个参数类型也是文件是，`mv`命令完成文件重命名。此时，源文件只能有一个（也可以是源目录名），它将所给的源文件或目录重命名为给定的目标文件名，当第二个参数是已存在的目录名称时，源文件或目录参数可以有多个，`mv`命令将各个参数指定的源文件均移至目标目录中，在跨文件系统移动文件时，`mv`先拷贝，再将原有文件删除，而链至该文件的链接也将丢失

### 3.命令参数：

> `-b` ,` like --backup`，若需覆盖文件，则覆盖前先行备份。
>
>` -f`,` --force` 强制的意思，如果文件已经存在。覆盖前不提示
>
>`-i`,` --interactive `     若目标文件 (destination) 已经存在时，就会询问是否覆盖
>
>`-n`,` --no-clobber`      不要覆盖现有文件
>
>  `-S`,` --suffix=SUFFIX`     覆盖通常的备用后缀
>
> ` -t`, `--target-directory=DIRECTORY  move all SOURCE arguments into DIRECTORY` 即指定`mv`的目标目录，该选项适用于移动多个源文件到一个目录的情况，此时目标目录在前，源文件在后。
>
>`-T`,`--no-target-directory `   将`DEST`视为正常文件
>
> ` -u`, `--update`       仅当`SOURCE`文件较新时才移动
>
>` -v`, `--verbose`     解释正在做什么
>
>  `-Z`, `--context`     设置目的地的`SELinux`安全上下文，文件到默认类型



### 4.常用实例

#### 例一：文件改名

命令：`mv log1.log log11.txt`

输出：

```shell
root@ubuntu:/home/test/test# ls
app  log1.log  log2.log  log3.log  log.log
root@ubuntu:/home/test/test# mv log1.log log11.txt
root@ubuntu:/home/test/test# ls
app  log11.txt  log2.log  log3.log  log.log
root@ubuntu:/home/test/test# 
```

说明：将文件`log1.log`重命名为`log11.txt`

#### 例二：移动文件

命令：`mv log2.log /home/test/test2`

输出：

```shell
root@ubuntu:/home/test# ls
test  test1  test2  test3
root@ubuntu:/home/test# cd test
root@ubuntu:/home/test/test# ls
app  log11.txt  log2.log  log3.log  log.log
root@ubuntu:/home/test/test# mv log2.log /home/test/test2
root@ubuntu:/home/test/test# ls
app  log11.txt  log3.log  log.log
root@ubuntu:/home/test/test# cd ../test2/
root@ubuntu:/home/test/test2# ls
log2.log
root@ubuntu:/home/test/test2# 
```

说明：将` log2.log`文件移至目录`test2`中

#### 例三：将文件`log11.txt log3.log`移动至目录`app`中

命令：

```shell
mv log11.txt log3.log app
mv -t /home/test/test3/ log11.txt log3.log
```

输出：

```shell
root@ubuntu:/home/test/test2# cd ../test
root@ubuntu:/home/test/test# ls
app  log11.txt  log3.log  log.log
root@ubuntu:/home/test/test# mv log11.txt log3.log app
root@ubuntu:/home/test/test# ls
app  log.log
root@ubuntu:/home/test/test# cd app
root@ubuntu:/home/test/test/app# ls
app.py  log11.txt  log3.log  templates
root@ubuntu:/home/test/test/app# mv -t /home/test/test3/ log11.txt log3.log root@ubuntu:/home/test/test/app# cd /home/test/test3
root@ubuntu:/home/test/test3# ls
log11.txt  log3.log
root@ubuntu:/home/test/test3# 
```

说明：第一个命令的将`log11.txt log3.log`两个文件移动至`app`目录中，第二个命令是将两个文件移动至`/home/test/test3`目录中

#### 例四：将文件`file1`改名`file2`，如果`file2`已经存在，则询问是否覆盖

命令:` mv -i txt1.txt  txt2.txt `

输出：

```shell
root@ubuntu:/home/test/test3# ls
log11.txt  log3.log  txt1.txt  txt2.txt
root@ubuntu:/home/test/test3# cat txt1.txt 
qwe123
root@ubuntu:/home/test/test3# cat txt2.txt 
123qwe
root@ubuntu:/home/test/test3# mv -i txt1.txt  txt2.txt 
mv: overwrite 'txt2.txt'? y
root@ubuntu:/home/test/test3# cat txt2.txt 
qwe123
root@ubuntu:/home/test/test3# ls
log11.txt  log3.log  txt2.txt
```

#### 例五：

命令：`mv -f txt1.txt  txt2.txt `

输出：

```shell
root@ubuntu:/home/test/test2# ls
log2.log
root@ubuntu:/home/test/test2# touch txt1.txt txt2.txt
root@ubuntu:/home/test/test2# vim txt1.txt 
root@ubuntu:/home/test/test2# vim txt2.txt 
root@ubuntu:/home/test/test2# cat txt1.txt 
char123
root@ubuntu:/home/test/test2# cat txt2.txt 
wtt or yjq 
root@ubuntu:/home/test/test2# mv -f txt1.txt  txt2.txt 
root@ubuntu:/home/test/test2# ls
log2.log  txt2.txt
root@ubuntu:/home/test/test2# cat txt2.txt 
char123
root@ubuntu:/home/test/test2# 
```

说明：`txt1.txt`覆盖了`txt2.txt`的内容，`-f`是一个危险的选择，使用的时候一定要保持头脑清晰，一般情况下最后不用加上它

#### 例六：目录的移动

命令：`mv dir1 dir2`

说明：如果`dir2`不存在，那么`dir1`将改名为`dir2`，存在则移入`dir2`中

`dir2`存在时：

```shell
root@ubuntu:/home/test/test2# cd ..
root@ubuntu:/home/test# ls
test  test1  test2  test3
root@ubuntu:/home/test# mv test1 test2
root@ubuntu:/home/test# ls
test  test2  test3
root@ubuntu:/home/test# cd test2/
root@ubuntu:/home/test/test2# ls
log2.log  test1  txt2.txt
root@ubuntu:/home/test/test2# 
```

`dir2`不存在时：

```shell
root@ubuntu:/home/test/test2# cd ..
root@ubuntu:/home/test# ls
test  test2  test3
root@ubuntu:/home/test# mv test3 test4
root@ubuntu:/home/test# ls
test  test2  test4
root@ubuntu:/home/test# 
```

#### 例七：移动当前目录下的所有文件到上一级目录

命令：`mv * ../`

输出：

```shell
root@ubuntu:/home/test# cd test
root@ubuntu:/home/test/test# ls
app  log.log
root@ubuntu:/home/test/test# mv *../
mv: missing destination file operand after '*../'
Try 'mv --help' for more information.
root@ubuntu:/home/test/test# mv  * ../
root@ubuntu:/home/test/test# ls
root@ubuntu:/home/test/test# cd ..
root@ubuntu:/home/test# ls
app  log.log  test  test2  test4
root@ubuntu:/home/test# 

```

**注意** `*`和 `..`之间要有空格隔开

#### 例八：把当前目录的一个子目录里的文件移动到另一个子目录里

命令：` mv test2/*.log test4`  

说明：`*.log`这个是可以换成你所要移动的文件

```shell
root@ubuntu:/home/test# cd test2
root@ubuntu:/home/test/test2# ls
log2.log  test1  txt2.txt
root@ubuntu:/home/test/test2# cd ..
root@ubuntu:/home/test# mv test2/*.log test4
root@ubuntu:/home/test# ls
app  log.log  test  test2  test4
root@ubuntu:/home/test# cd test2
root@ubuntu:/home/test/test2# ls
test1  txt2.txt
root@ubuntu:/home/test/test2# cd ../test4
root@ubuntu:/home/test/test4# ls
log11.txt  log2.log  log3.log  txt2.txt
root@ubuntu:/home/test/test4# 
```

#### 例九：文件被覆盖前做简单备份，前面加参数`-b`

命令：`mv log2.log -b log3.log`

输出：

```shell
root@ubuntu:/home/test/test4# ls
log11.txt  log2.log  log3.log  txt2.txt
root@ubuntu:/home/test/test4# mv log2.log -b log3.log 
root@ubuntu:/home/test/test4# ls
log11.txt  log3.log  log3.log~  txt2.txt
```

说明：

`-b` 不接受参数，`mv`会去读取环境变量`VERSION_CONTROL`来作为备份策略。

`–backup`该选项指定如果目标文件存在时的动作，共有四种备份策略：

* `CONTROL=none`或`off` : 不备份。

* `CONTROL=numbered`或`t`：数字编号的备份

* `CONTROL=existing`或`nil`：如果存在以数字编号的备份，则继续编号备份`m+1…n`：

  执行`mv`操作前已存在以数字编号的文件`log3.log.~1~`，那么再次执行将产生`log2.log~2~`，以次类推。如果之前没有以数字编号的文件，则使用下面讲到的简单备份。

* `CONTROL=simple`或`never`：使用简单备份：在被覆盖前进行了简单备份，简单备份只能有一份，再次被覆盖时，简单备份也会被覆盖。

  ​

