## mkdir命令

`Linux mkdir`命令是用来创建指定的名称的目录，要求创建目录的用户在当前目录中具有写权限，并且指定的目录名不能是当前目录中已有的目录

### 1.命令格式 :

`mkdir [选项] 目录`

###  2.命令功能

通过`mkdir`命令可以实现现在指定位置创建以`DirName（指定的文件名）`命名的文件夹或目录。要创建文件夹或目录的用户必须对所创建的文件夹的父文件夹具有写权限。并且，所创建的文件夹（目录）不能与其父目录（即父文件夹）中的文件名重名，即同一个目录下不能有同名的（区分大小写）

### 3.命令参数

>`-m `,` --model= 模式` ，设定权限<模式>（类似(`chmod`)），而不是`rwxrwxrwx `减`umask`  **不是很理解**
>
>`-p` ,` --parents` 可以是一个路径名称。此时若路径中的某些目录尚不存在，加上此选项后，系统将自动建立好那些尚不存在的目录，即一次可以创建多个目录
>
>`-v` ,` --verbose `每次创建新目录都显示信息 , **不过现在不需要加这个参数也会默认提示信息**
>
>`--help` 显示此帮助信息并退出
>
>`--version` 输出版本信息并退出

### 4.命令实例

#### 例一：创建一个空目录

命令：`mkdir test`

输出：

```shell
root@ubuntu:/opt# ls
char_flask
root@ubuntu:/opt# mkdir test
root@ubuntu:/opt# ls
char_flask  test
root@ubuntu:/opt# cd test
root@ubuntu:/opt/test# pwd
/opt/test
```

#### 例二：递归创建多个目录

命令：`mkdir -p test1/test11`

输出：

```shell
root@ubuntu:/opt/test# mkdir -p test1/test11
root@ubuntu:/opt/test# ls
test1
root@ubuntu:/opt/test# ll
total 12
drwxr-xr-x 3 root root 4096 Jun  3 01:17 ./
drwxr-xr-x 4 root root 4096 Jun  3 01:15 ../
drwxr-xr-x 3 root root 4096 Jun  3 01:17 test1/
root@ubuntu:/opt/test# cd test1
root@ubuntu:/opt/test/test1# ll
total 12
drwxr-xr-x 3 root root 4096 Jun  3 01:17 ./
drwxr-xr-x 3 root root 4096 Jun  3 01:17 ../
drwxr-xr-x 2 root root 4096 Jun  3 01:17 test11/
root@ubuntu:/opt/test/test1# 
```

#### 例三：创建权限为`6666`的目录 

命令：`mkdir -m 666 test2`

输出：

```shell
root@ubuntu:/opt/test# mkdir -m 6666 test2
root@ubuntu:/opt/test# ll
total 16
drwxr-xr-x 4 root root 4096 Jun  3 01:24 ./
drwxr-xr-x 4 root root 4096 Jun  3 01:15 ../
drwxr-xr-x 3 root root 4096 Jun  3 01:17 test1/
drwSrwSrw- 2 root root 4096 Jun  3 01:24 test2/
root@ubuntu:/opt/test# 
```

说明：`test2`的权限为`drwSrwSrw-`

#### 例四：创建新目录都提示信息

命令：`mkdir -v test3`

输出：

```shell
root@ubuntu:/opt/test# mkdir -v test3
mkdir: created directory 'test3'
root@ubuntu:/opt/test# mkdir -vp test4/test44
mkdir: created directory 'test4'
mkdir: created directory 'test4/test44'
root@ubuntu:/opt/test# 
```

#### 例五：一个命令创建项目的目录结构

参考：[http://www.ibm.com/developerworks/cn/aix/library/au-badunixhabits.html](http://www.ibm.com/developerworks/cn/aix/library/au-badunixhabits.html)

命令：`mkdir -vp test5/{decorator,forms,models,static/{css,js,images},templates,utils,views}`

```shell
root@ubuntu:/opt/test# mkdir -vp test5/{decorator,forms,models,static/{css,js,images},templates,utils,views}
mkdir: created directory 'test5'
mkdir: created directory 'test5/decorator'
mkdir: created directory 'test5/forms'
mkdir: created directory 'test5/models'
mkdir: created directory 'test5/static'
mkdir: created directory 'test5/static/css'
mkdir: created directory 'test5/static/js'
mkdir: created directory 'test5/static/images'
mkdir: created directory 'test5/templates'
mkdir: created directory 'test5/utils'
mkdir: created directory 'test5/views'
root@ubuntu:/opt/test# tree test5/
test5/
├── decorator
├── forms
├── models
├── static
│   ├── css
│   ├── images
│   └── js
├── templates
├── utils
└── views

10 directories, 0 files
root@ubuntu:/opt/test# 

```

