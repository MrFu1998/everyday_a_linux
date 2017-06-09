##  rmdir命令

`rmdir`命令是`linux`中的常用命令。`yrm -r dir`等同于`rmdir`，该命令的功能是删除空目录，一个目录被删除之前必须是空的，删除某目录时必须具有对父目录的写权限

### 1.命令格式：

`rmdir [选项] 目录`

### 2.命令功能：

该命令从一个目录中删除一个或多个子目录项，删除某目录时也必须具有对父目录的写权限

### 3.命令参数

> `-p`,` --parents`递归删除目录`dirname`，当子目录删除后其父目录为空时，也一同被删除
>
> `-v`, `--verbose ` 显示指令执行过程

### 4.常用实例：

#### 例一：`rmdir`不能删除非空目录

命令： `rmdir doc`

输出：

```shell
root@ubuntu:/home/test/test# mkdir -vp app/{static/{css,js,images},templates,app.py}mkdir: created directory 'app'
mkdir: created directory 'app/static'
mkdir: created directory 'app/static/css'
mkdir: created directory 'app/static/js'
mkdir: created directory 'app/static/images'
mkdir: created directory 'app/templates'
mkdir: created directory 'app/app.py'
root@ubuntu:/home/test/test# tree app
app
├── app.py
├── static
│   ├── css
│   ├── images
│   └── js
└── templates

6 directories, 0 files
root@ubuntu:/home/test/test# cd app
root@ubuntu:/home/test/test/app# 
root@ubuntu:/home/test/test/app# ls
app.py  static  templates
root@ubuntu:/home/test/test/app# rmdir static
rmdir: failed to remove 'static': Directory not empty 
root@ubuntu:/home/test/test/app# cd static
root@ubuntu:/home/test/test/app/static# 
root@ubuntu:/home/test/test/app/static# ls
css  images  js
root@ubuntu:/home/test/test/app/static# 
root@ubuntu:/home/test/test/app/static# rmdir css
root@ubuntu:/home/test/test/app/static# rmdir js
root@ubuntu:/home/test/test/app/static# cd ..
root@ubuntu:/home/test/test/app# tree
.
├── app.py
├── static
│   └── images
└── templates

4 directories, 0 files
root@ubuntu:/home/test/test/app# 
```

说明：`rmdir `目录名 命令不能直接删除非空目录

#### 例二：`rmdir -p`当子目录被删除后使它也成为空目录的话，则顺便一并删除

命令：`rmdir -p static`

输出

```shell
root@ubuntu:/home/test/test/app# tree
.
├── app.py
├── static
│   └── images
└── templates

4 directories, 0 files
root@ubuntu:/home/test/test/app# rmdir -p static
rmdir: failed to remove 'static': Directory not empty
root@ubuntu:/home/test/test/app# tree
.
├── app.py
├── static
│   └── images
└── templates

4 directories, 0 files
root@ubuntu:/home/test/test/app# rmdir -p static/images
root@ubuntu:/home/test/test/app# tree
.
├── app.py
└── templates

2 directories, 0 files
root@ubuntu:/home/test/test/app# 
```

   