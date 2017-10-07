## cat命令

`cat`命令的用途是连接文件或标准输入并打印。这个命令常用来显示文件内容，或者将几个文件连接起来显示，或者从标准输入读取内容并显示，它常与重定向符号配合使用。 

### 1.命令格式

`cat [选项] [文件]...`

### 2.命令功能

**cat主要有三大功能** ：

1. 一次显示整个文件:`cat  filename`
2. 从键盘创建一个文件:`cat > filename` 只能创建新文件,不能编辑已有文件.
3. 将几个文件合并为一个文件:`cat file1 file2 > file`

### 3.命令参数

>`-A`, `--show-all`           等价于 -vET
>
>`-b`,` --number-nonblank`    对非空输出行编号
>
>`-e`                       等价于 `-vE`
>
>`-E`,` --show-ends`          在每行结束处显示 $
>
>`-n`, `--number `    对输出的所有行编号,由1开始对所有输出的行数编号
>
>`-s`,` --squeeze-blank`  有连续两行以上的空白行，就代换为一行的空白行 
>
>`-t`  与 `-vT` 等价
>
>`-T`,` --show-tabs `         将跳格字符显示为 ^I
>
>`-u`  (被忽略)
>
>`-v`,` --show-nonprinting`   使用` ^` 和` M- `引用，除了 `LFD` 和` TAB` 之外

###3.常用实例

#### 例一：把`txt2.txt`的文件内容加上行号后输入`txt1.txt`这个文件里

命令：` cat txt2.txt `

输出：

```shell
root@ubuntu:/home/test/test3# touch txt1.txt
root@ubuntu:/home/test/test3# ls
log.log  test1  txt1.txt  txt2.txt
root@ubuntu:/home/test/test3# vim txt1.txt 
root@ubuntu:/home/test/test3# cat txt1.txt 
qweqweqwe
qweqweqwe
qweqweqwe
qweqweqwe
qweqweqwe
qweqweqwe
root@ubuntu:/home/test/test3# cat txt2.txt 
char123
root@ubuntu:/home/test/test3# cat -n txt2.txt txt1.txt 
         1	char123
     2	
     3	
     4	
     5	
     6	
     7	qweqweqwe
     8	qweqweqwe
     9	qweqweqwe
    10	qweqweqwe
    11	qweqweqwe
    12	qweqweqwe
root@ubuntu:/home/test/test3#
```

**说明** 这样还会把空白行算进去

#### 例二：把`log.log`和`log1.log`的文件内容加上行号（空白行不加）之后的内容附加到`log.log`里

**命令** ：`cat -b log.log`

输出：

```shell
root@ubuntu:/home/test/test3# ls
log1.log  log.log  test1  txt1.txt  txt2.txt
root@ubuntu:/home/test/test3# cat -b log.log log1.log 
     1	123412
     2	wqewqe









     3	qweqwe
     4	qwe


root@ubuntu:/home/test/test3#  
```

### 例三：把`log.log`的文件内容加上行号后出入到`log1.log`这个文件里

输出：

```shell
root@ubuntu:/home/test/test3# cat log.log
123412
wqewqe
root@ubuntu:/home/test/test3# cat log1.log
qweqweqwe
qweqwe123
root@ubuntu:/home/test/test3# cat -n log1.log > log.log 
root@ubuntu:/home/test/test3# cat -n log.log 
     1	     1	qweqweqwe
     2	     2	qweqwe123
root@ubuntu:/home/test/test3# cat -n log1.log 
     1	qweqweqwe
     2	qweqwe123
root@ubuntu:/home/test/test3# 
```

#### 使用`here doc`来生成文件

输出：

```shell
root@ubuntu:/home/test/test3# ls
log1.log  log.log  test1  txt1.txt  txt2.txt
root@ubuntu:/home/test/test3# cat >txt1.txt <<EOF
> Hello World
> Python
> Linux
> PWD=$(pwd)
> EOF
root@ubuntu:/home/test/test3# cat txt1.txt 
Hello World
Python
Linux
PWD=/home/test/test3
root@ubuntu:/home/test/test3# ls -l txt1.txt 
-rw-r--r-- 1 root root 46 Jun  9 04:04 txt1.txt
root@ubuntu:/home/test/test3# 
```

说明：注意粗体部分，here doc可以进行字符串替换。

备注：

​	`tac` (反向列示)

命令：`tac txt1.txt `

输出

```shell
root@ubuntu:/home/test/test3# tac txt1.txt 
PWD=/home/test/test3
Linux
Python
Hello World
root@ubuntu:/home/test/test3# 
```

说明：`tac` 是将` cat` 反写过来，所以他的功能就跟 `cat` 相反，` cat` 是由第一行到最后一行连续显示在萤幕上，而 `tac`  则是由最后一行到第一行反向在萤幕上显示出来！