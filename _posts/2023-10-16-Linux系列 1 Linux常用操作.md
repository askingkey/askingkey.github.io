---
title: 【Linux】Linux常用操作
date: 2023-10-16 16:52:00 +0800
categories: [2023 Learning]
pin: true
mermaid: true
math: true
comments: true
---


## 案例：Linux下的课堂笔记

小Z喜欢用电脑记录课堂笔记，为了方便存储，并且在不同电脑上都能看到自己的笔记，她决定将新学期的笔记有条理地记录、存储到Linux服务器上。在构建自己的笔记框架的同时，她也想熟悉一下Linux系统的各类常用的命令。

### 0 查看命令的参数与说明

**磨刀不误砍柴工。**在开始学习之前，小Z想知道，如果遇到了问题，该从哪里获得帮助。除了去问Google，Chatgpt之外，她的老师推荐利用**Linux指令自带的一些参数**进行更加“地道”、全面且精准的命令用法及说明。

```shell
# 查看command的用法
command --help
command -h

# 查看说明
man command
```

以cat为例，她在服务器上进行了查询：

```shell
$ cat --help
# 命令的基本用法
Usage: cat [OPTION]... [FILE]...
# 命令的解释
Concatenate FILE(s) to standard output.

# 参数介绍
With no FILE, or when FILE is -, read standard input.

  -A, --show-all           equivalent to -vET
  -b, --number-nonblank    number nonempty output lines, overrides -n
  -e                       equivalent to -vE
  -E, --show-ends          display $ at end of each line
  -n, --number             number all output lines
  -s, --squeeze-blank      suppress repeated empty output lines
  -t                       equivalent to -vT
  -T, --show-tabs          display TAB characters as ^I
  -u                       (ignored)
  -v, --show-nonprinting   use ^ and M- notation, except for LFD and TAB
      --help     display this help and exit
      --version  output version information and exit
# 举例
Examples:
  cat f - g  Output f's contents, then standard input, then g's contents.
  cat        Copy standard input to standard output.

# 完整帮助文档链接
GNU coreutils online help: <https://www.gnu.org/software/coreutils/>
Full documentation at: <https://www.gnu.org/software/coreutils/cat>
or available locally via: info '(coreutils) cat invocation'
```

她发现，指令自带的帮助信息确实更加简洁详细，再搭配前人整理的攻略，相信自己可以读懂Linux这本菜谱。


### 1 建立清晰的文件目录框架

#### 1.1 文件、目录的检视：pwd, ls, cd

终于进入到了实战环节，这学期，小Z所在的班级即将共用一个服务器账号，她输入了服务器账号和密码，进入了用户目录。她想要先使用`pwd`命令查看自己所在的路径。

```shell
(base) bioinfo23@node02:~$ pwd
/home/bioinfo23
```

接下来，小Z想看看自己目录下的文件结构是什么样的。通过查找Linux菜谱，她发现，`ls`命令有很多参数，他摘录了其中的几种参数，如下：

```shell
## ls [参数] [路径(默认为当前路近)]
## ls指令的参数
-a : 把全部的文件，包含隐藏文件（开头为.的文件）一起列出来
-l : 长数据串行出，包含文件的属性与权限等数据
-d : 仅列出目录本身，而不是列出目录内的文件数据
--full-time ：以完整时间模式（包含年、月、日、时、分）输出
```

在服务器上分别输入`ls -la`和`ls --full-time`，部分结果如下：

```shell
$ ls -la
total 2080136
drwxr-xr-x 36 bioinfo23 bioinfo23       4096 Oct 16 03:39  .
drwxr-xr-x 55 root      root            4096 Sep 25 09:27  ..
-rw-rw-r--  1 bioinfo23 bioinfo23          0 Oct 11 05:47 '!1.txt'
-rw-rw-r--  1 bioinfo23 bioinfo23          0 Oct 11 05:47 '1!.txt'

# 对比ls -la，ls --full-time可以列出更多的时间信息
$ ls --full-time
total 2080008
-rw-rw-r--  1 bioinfo23 bioinfo23   0 2023-10-11 05:47:42.099272103 +0000 '!1.txt'
-rw-rw-r--  1 bioinfo23 bioinfo23   0 2023-10-11 05:47:42.282272090 +0000 '1!.txt'
```

看来，班上的同学已经在用户目录下建立了很多文件和文件夹，小Z想使用`cd`命令进入目录下的test文件夹。

此外，她想起了之前学过的绝对路径与相对路径，并做了一些练习。

```shell
## cd [相对路径或绝对路径]
# 进入test文件夹
$ cd test

# 返回到自己的主文件夹（仅输入cd是一样的效果）
$ cd ~

# 去到当前目录的上层目录
$ cd ..

# 前往当前目录中的media文件夹 (.表示当前目录)
$ cd ./media

# 前往当前上一级目录中的sys文件夹  (..表示上层目录，sys和media是同级的)
$ cd ../sys
```



#### 1.2 建立文件与文件夹：touch, mkdir

在学会了在服务器的各个文件夹中自由穿梭后，小Z准备着手搭建自己的笔记目录。她这学期有Linux操作系统、Python数据结构、生物信息学导论三门专业课，需要在自己的目录下先建立三个文件夹。

``` shell
# 进入自己的目录
$ cd kyzhu
$ ls
diary  exercise  hello.ipynb  hello.md  output.png  scripts  software

# 在自己的下建立Notebook文件夹
$ mkdir kyzhu/Notebook

# 在Notebook下分别建立三门课程的文件夹
$ mkdir kyzhu/Notebook/Linux
$ mkdir kyzhu/Notebook/DataStructure
$ mkdir kyzhu/Notebook/BioinfoIntro

# 查看当前目录下的文件框架
$ ls -l
total 0
drwxrwxr-x 2 bioinfo23 bioinfo23 10 Oct 16 06:56 BioinfoIntro
drwxrwxr-x 2 bioinfo23 bioinfo23 10 Oct 16 06:55 DataStructure
drwxrwxr-x 2 bioinfo23 bioinfo23 10 Oct 16 06:55 Linux
```

接着，她使用`touch`命令建立了Linux操作系统第一堂课的笔记文件。

```shell
# 建立Linux第一堂课的笔记
bioinfo23@node02:~/kyzhu/Notebook/Linux$ touch Lesson1

# 检查是否建立成功
bioinfo23@node02:~/kyzhu/Notebook/Linux$ ls
Lesson1
```


#### 1.3 复制、删除、移动：cp, rm, mv

小Z想在笔记Lesson1的基础上改动一些内容，但是又想留一份Lesson1的备份，以免进行了不可逆的误操作，因此，她决定使用cp命令对Lesson1进行备份。在此之前，她查阅了一些cp的相关用法：

```shell
## cp的基本用法
# Copy SOURCE to DEST, or multiple SOURCE(s) to DIRECTORY.
用法: cp [OPTION] SOURCE(源文件或文件夹) DEST(目标文件)/DIRECTORY(目标文件夹)

## 常用参数
-r: copy directories recursively 复制目录时需要添加

## 举例
cp /bin/?sh . #复制/bin目录下的多个文件到当前目录
cp -r /etc/skel . #复制/etc/skel目录下的所有内容到当前目录
```
**提示：**

* 若A、B都是已存在的文件，当cp A B时，**B会被A覆盖！**且在bioinfo23服务器上，不会有额外的提示，这个操作很危险！
* 若B不存在，当cp A B时，则会创建一个文件B作为输出！

```shell
# 复制Lesson1为Lesson1_1
$ cp Notebook/Linux/Lesson1 Notebook/Linux/Lesson1_1
$ ls Notebook/Linux
Lesson1  Lesson1_1  Lesson2
```

在更改完Lesson1_1中的内容后，小Z想把原来的Lesson1文件删掉，这需要用到`rm`命令，其用法如下：

```shell
## rm的基本用法（很危险的命令，慎用！）
# Remove (unlink) the FILE(s).
用法: rm [OPTION] [FILE]

## 常用参数
-r: remove directories and their contents recursively 删除文件夹和其中的内容，向下递归，不管有多少级目录，一并删除（rm默认是只移除文件，需要加这个参数才能对文件夹进行操作）
-d: remove empty directories 删除空目录
-f: ignore nonexistent files and arguments, never prompt 强行删除，没有任何提示

## 举例
rm -r usr/ #删除usr目录及其内容，root用户有删除提示
rm -rf usr/ #强制删除usr目录及其内容，无删除提示
rm -d usr/ #删除usr目录，usr是一个空目录

# 删除Lesson1
$ rm Notebook/Linux/Lesson1
$ ls Notebook/Linux
Lesson1_1  Lesson2
```

小Z误将数据结构课的笔记Lesson2放到了Linux课程的目录下，需要把Lesson2移回DataStructure文件夹中，这需要用到`mv`命令，其用法如下：

```shell
## mv的基本用法
# Rename SOURCE to DEST, or move SOURCE(s) to DIRECTORY.
用法: mv [OPTION] SOURCE DEST/DIRECTORY

## 举例
mv FAQ bash-FAQ #将FAQ改名为bash-FAQ
mv [yz]* usr/ #将y或z开头的文件移动到usr目录下

# 把Lesson2移动到DataStructure文件夹中
$ mv kyzhu/Notebook/Linux/Lesson2 kyzhu/Notebook/DataStructure/
$ ls kyzhu/Notebook/DataStructure/
Lesson2
$ ls kyzhu/Notebook/Linux/
Lesson1_1
```



### 2 文件搜寻：which, whereis, find

在日常使用中，难免会出现找不到文件的情况，小Z未雨绸缪，参考了《鸟哥的Linux私房菜》，整理出了可能会用到的文件搜寻命令。

#### 2.1 可执行文件 (指令) 的路径搜寻：which

```shell
## which的基本用法
# which根据“PATH”这个环境变量所规范的路径，去搜寻“可执行文件”的文件名”，返回的是可执行文件或链接的路径名
# which 默认是找 PATH 内所规范的目录，一些bash内置的指令是找不到的
用法: which [filename](完整的文件名)

## 常用参数
-a: 打印每个参数的所有匹配路径名

## 举例
$ which which
/usr/bin/which
$ which -a which
/usr/bin/which
/bin/which
```

#### 2.2 文件文件名的搜寻：whereis, find

1. whereis

```shell
## whereis的基本用法
# 由一些特定的目录中寻找文件文件名，输出文件所在的路径
用法: which [filename](完整的文件名)

## 常用参数
-l: 可以列出 whereis 会去查询的几个主要目录而已
-b: 只找 binary 格式的文件
-m: 只找在说明文档 manual 路径下的文件
-s: 只找 source 来源文件
-u: 搜寻不在上述三个项目当中的其他特殊文件

## 举例
$ whereis passwd
passwd: /usr/bin/passwd /etc/passwd /usr/share/man/man1/passwd.1.gz /usr/share/man/man1/passwd.1ssl.gz /usr/share/man/man5/passwd.5.gz
$ whereis -m passwd
passwd: /usr/share/man/man1/passwd.1.gz /usr/share/man/man1/passwd.1ssl.gz /usr/share/man/man5/passwd.5.gz
```

2. find

```shell
## find的基本用法
# 输出文件所在的路径
用法: find [PATH] [option] [action]

## 常用参数
1. 与时间有关的参数
-mtime n: n 为数字，意义为在 n 天之前的“一天之内”被更动过内容的文件；
-mtime +n: 列出在 n 天之前(不含 n 天本身)被更动过内容的文件文件名；
-mtime -n: 列出在 n 天之内(含 n 天本身)被更动过内容的文件文件名;
-newer file: file 为一个存在的文件，列出比 file 还要新的文件文件名。

2. 与使用者或群组名称有关的参数
-uid n: n 为数字，UID是使用者的帐号ID
-gid n :n 为数字，GID是群组名称的ID

3. 与文件权限及名称有关的参数
-name filename: 搜寻文件名为filename的文件；
-size [+-]SIZE: 搜寻比SIZE还要大 (+)或小 (-) 的文件；
		SIZE 的规格有
			c: 代表 Byte
			k: 代表 1024Bytes
-type TYPE: 搜寻文件的类型为TYPE的文件。

## 举例：寻找文件名包含了passwd的文件（只列出了部分文件）
$ find / -name passwd
/snap/core20/1974/etc/pam.d/passwd
/snap/core20/1974/etc/passwd
/snap/core20/1974/usr/bin/passwd
/snap/core20/1974/usr/share/bash-completion/completions/passwd
/snap/core20/1974/usr/share/doc/passwd
```



### 3 笔记内容查询与统计

> 本节使用命令：`cat, tac, head, tail, more, less, wc`

在进行了一段时间的学习后，小Z的笔记也越记越多。她需要快速浏览每个笔记的内容，并且统计笔记中的字符（为了展示自己的工作量有多大哈哈），而这就需要用到Linux系统中文件内容查询与统计的相关命令。

#### 3.1 重定向与管道

> 参考文档：
>
> [Linux命令中的重定向和管道](https://murphypei.github.io/blog/2018/04/linux-redirect-pipe)；
>
> [linux shell管道命令(pipe)使用及与shell重定向区别](https://www.cnblogs.com/pengliangcheng/p/5211786.html)

在学习生物信息的过程中，难免会遇到很多数据预处理的工作。有时，使用仅仅一行的shell命令就可以进行文件排序、去重等操作，而重定向和管道两种方式就是“一行命令秒杀任务”的关键。在笔记内容查询与统计的部分中，小Z觉得有必要学习这两个小知识点。先用一句话概括一下，重定向和管道都可以实现“传递”。

##### 3.1.1 重定向

1. **输出重定向** 

```shell
## 格式一般如下
command [1-n] > file或者文件描述符或者设备
# [1-n]: 文件描述符
#	标准输入：standard input(0)
# 标准输出：standard output(1)
# 标准错误：standard error(2)

### 示例
## 不重定向输出（假设当前目录下只存在一个文件exists.txt）
ls exists.txt no-exists.txt
# 因为exists.txt文件存在，而no-exists.txt文件不存在，因此这个命令即具有成功执行的结果（标准输出），又具有出错的结果（标准错误）。由于这个命令没有进行重定向，因此标准输出和标准错误都将打印在屏幕上。

## 重定向输出
ls exists.txt no-exists.txt 1 > success.txt 2 > fail.txt
# 命令执行，屏幕上将不显示任何信息，但是多了两个文件，其中succcess.txt中是执行成功的结果，标准输出重定向的文件，内容为exists.txt，而fail.txt是执行出错的结果，标准错误重定向的结果，内容为ls: no-exists.txt: No such file or directory。

## 只重定向标准输出
ls exists.txt no-exists.txt  > result.txt
#其意义就是将命令执行成功的结果输出到result.txt中，因此屏幕上没有命令执行成功的结果，只有出错的结果。值得注意的是，标准输出的文件描述符1可以省略
```

* 注意

  shell遇到\`>\`操作符，会判断右边文件是否存在，**如果存在就先删除**，并且创建新文件；不存在直接创建。无论左边命令执行是否成功，右边文件都会存在。
  

2. **输入重定向**

```shell
## 格式一般如下
command [n] < file或文件描述符或者设备
# [n]: 文件描述符

## 示例
# 这条命令cat命令的输入重定向到input.txt文件，因此该文件的内容作为cat的输入。然后cat命令的输出重定向到output.txt，因此将内容输出到output.txt中。
cat > output.txt  < input.txt
```

##### 3.1.2 管道

1. **介绍**

管道的符号是`|`，它仅能处理经由前面一个指令传出的正确输出信息，也就是标准输出（standard output）的信息，对于标准错误（stdandard error）信息没有直接处理能力。然后，传递给下一个命令，作为其标准输入（standard input）。因此可以认为**管道其实是重定向的一种常用形式**。

1. **注意**

- 管道命令只处理前一个命令正确输出，不处理错误输出；
- 管道命令的右边命令，必须能够接收标准输入流命令才行。

3. **使用实例**

```shell
## 管道示例
#cat test.txt会将test.txt的内容作为标准输出，然后利用管道，将其作为grep -n 'test'命令的标准输入。
cat test.txt | grep -n 'test'

## xargs: 处理管道传输过来的stdin，将处理后的数据传递到正确的位置
# 从根目录开始查找所有扩展名为.log的文本文件，并找出包含"ERROR"的行
find / -type f -name "*.log" | xargs grep "ERROR"
```

##### 3.1.3 重定向和管道的区别

1. **管道**触发两个子进程，执行`|`两边的程序；而**重定向**是在一个进程内执行；

2. 管道两边都是shell命令；

3. 重定向符号的右边只能是Linux文件（普通文件，文件描述符，文件设备）；

4. **重定向符号的优先级大于管道**。

   

#### 3.2 直接检视文件内容：cat, tac

当笔记的内容不是很多的时候，小Z就可以使用`cat`和`tac`命令把文件中的内容直接打印到终端上。

```shell
## cat和tac的基本用法（很明显，tac就是把cat反过来的一个词）
# 输出文件所有内容（cat：正序；tac：逆序）
用法: cat [OPTION] [FILE]
	 	 tac [OPTION] [FILE]

## 常用参数
-A: 生信工作中很重要的一个参数，可以把文件中所有的内容以符号的形式展示，包括可以把TAB符输出成^I（避免TAB和空格混淆），并在每行结束的位置输出\$
（但是zsh中无法使用-A参数）
# 仅凭肉眼无法看出test文件中tab键和空格的区别，可以使用这个参数
```

#### 3.3 可翻页检视：more, less

`more`和`less`都是用来分页显示文本文件内容的命令，小Z想比较下这两者的不同之处。

```shell
## more和less的基本用法
# 这两个命令均是用来分页显示文本文件内容的命令
# more 只能向下翻页，less可以上下翻页，且可以通过输入/pattern方式查找匹配
用法: more [OPTION] [FILE]
		 less [OPTION] [FILE]

# more的用法
参数:  -n          定义屏幕大小为n行
      -s         合并显示连续空行
操作:  空格键       向下滚动一屏
      q或Ctrl+C   退出more
      回车键       滚动n行，默认1行

# less的用法 (Less is more!)
选项:  -s                  合并显示连续空行
操作:  空格键               向下滚动一页
      q或ZZ               退出less
      回车键               滚动一行
      [pagedown]          向下翻动一页
      [pageup]            向上翻动一页
      /字符串或?字符串      向下或上搜索字符串
      g                   转到第一行
      :n                  转到第n行
```

她使用这两个命令查看了Lesson3文件，感觉less集成了更多功能，且单独开辟了一个页面。

毕竟，less is more！


#### 3.4 数据撷取：head, tail

小Z觉得一次性把笔记全部展示出来会太过冗余，于是她决定使用`head`与`tail`命令查看笔记的部分内容。

```shell
## head和tail的基本用法
# 显示普通文件的前后若干行内容命令
用法: head -n [FLIE] (n为数字，意为显示的行数，空行也算一行！)
		 tail -n [FLIE] (n为数字，意为显示的行数)
```

此时，小Z又想到了一个问题，如何用`head`与`tail`查看第n行呢？虽然`less`也有这个功能，但是不能把第n行单独打印到屏幕上。而这时，就可以用到之前学习到的“管道”用法，将`head`与`tail`进行组合，就可以完成输出啦。

```shell
# 打印文件的第m行
head -m [FILE] | tail -1

# 示例
$ head -3 kyzhu/Notebook/Linux/Lesson3 | tail -1
In any traditional operating system, there are users and groups. They exist solely for access and permissions. When running a process, it will run as the owner of that process whether that is Jane or Bob. File access and ownership is also permission dependent. You wouldn\'t want Jane to see Bob\'s documents and vice versa.
```

当然，还有其他的命令，诸如`sed`，`awk`可以不用管道就实现这个功能，但那是后话啦。



#### 3.5 文件内容统计：wc

为了展示自己的工作量，小Z使用`wc`命令来对自己的笔记进行的内容统计，`wc`的用法如下：

```shell
## wc的基本用法
wc  [OPTION]  [FILE]

## 常用参数
默认输出：lines words bytes
-l: --lines	输出行数统计
-w: --words	显示单词计数
-c: --bytes	输出字节数统计（中文3字节，换行1字节）
-m: --chars	输出字符数统计（中文1字符，换行1字符）

## 示例
(base) bioinfo23@node02:~$ wc kyzhu/Notebook/Linux/Lesson3
   9  281 1617 kyzhu/Notebook/Linux/Lesson3
   # 9行 281个单词 1617个字节
```


### 4 文件链接操作：ln

#### 4.1 硬链接

```shell
#创建源文件file1的硬链接file2
ln file1 file2
```

* **特点**

  * 硬链接不是一个链接文件，其文件类型仍是`-`；

  * 硬链接不能跨文件系统；

  * 删除源文件或硬链接，不影响文件内容；

  * 只能建立对文件的链接。

小Z为了避免误删一些文件，决定建立一些硬链接来“保护”自己的笔记文件。

```shell
# 创建文件Lesson3的硬链接Lesson3_hl1
$ ln kyzhu/Notebook/Linux/Lesson3 kyzhu/Notebook/Linux/Lesson3_hl1
$ ls -l kyzhu/Notebook/Linux
total 12
-rw-rw-r-- 1 bioinfo23 bioinfo23    0 Oct 16 07:34 Lesson1_1
-rw-rw-r-- 2 bioinfo23 bioinfo23 1617 Oct 16 08:36 Lesson3
-rw-rw-r-- 2 bioinfo23 bioinfo23 1617 Oct 16 08:36 Lesson3_hl1
-rw-rw-r-- 1 bioinfo23 bioinfo23   47 Oct 16 08:38 test1
# 可以看到，Lesson3_hl1的字节数和Lesson3是一样的

# 删除原文件，硬链接仍可以访问
$ rm kyzhu/Notebook/Linux/Lesson3
$ head -3 kyzhu/Notebook/Linux/Lesson3_hl1
Linux Lesson 3
1. Users and Groups
In any traditional operating system, there are users and groups. They exist solely for access and permissions. When running a process, it will run as the owner of that process whether that is Jane or Bob. File access and ownership is also permission dependent. You wouldn't want Jane to see Bob's documents and vice versa.
```



#### 4.2 软链接

```shell
#创建源文件file1的软链接file2
ln -s file1 file2
```

* **特点**

  * 软链接是一个真正的链接文件，其文件类型是`l`；

  * 软链接可以跨文件系统，即可以跨磁盘分区；

  * 删除源文件，链接会失效。

小Z想在自己的主目录中建立自己笔记的软链接，方便访问。

软链接会有`->`的标识，且在终端中会以不同的颜色显示。

删除原文件，软链接失效，但软链接文件依然存在。



### 5 磁盘和目录容量查询：du, df

小Z很好奇自己笔记所占用的空间，她检索到了两类指令，可以进行磁盘和目录容量查询。

1. du

```shell
## du的基本用法（du: desk usage）
# 显示文件使用磁盘空间量，默认输出文件的行数
用法: du [OPTION] [FILE]

## 部分参数简介
-b: 单位为字节bytes

## 举例
du a.txt #显示a.txt占用磁盘的空间信息

## 查看文件Lesson2所占的磁盘空间
$ du Lesson2
4	Lesson2
$ du -b Lesson2
23	Lesson2
```

2. df

```shell
## df的基本用法
# 显示文件系统磁盘空间的使用情况
用法: df

## 举例
df #显示磁盘使用情况
df -h #用阅读性较好的方式显示磁盘使用情况
```


### 6 压缩与解压缩：tar

学弟学妹来问小Z要笔记，小Z决定使用`tar`命令把笔记打包给他们。

```shell
## tar的基本用法
# tar命令的主要功能其实是归档（即打包），可以选择不压缩
用法: tar [OPTION] [FILE]

## 参数介绍（可以分为三个部分）
# 压缩/解压缩选项（仅能同时存在一个）
-c: 压缩
-x: 解压
-t: 查看
# 压缩算法选项（仅能同时存在一个）
-z: 使用gzip算法，一般压缩后文件名为xxx.tar.gz
-Z: 使用compress算法，一般压缩后文件名为xxx.tar.Z
-j: 使用bzip2算法，一般压缩后文件名为xxx.tar.bz2
# 其他常用选项
-f filename: 归档文件名；在f后要立即接文件名！不能再接参数！
						错误：tar -zcfv tfile sfile
						正确：tar -zcvf tfile sfile
-v: 压缩、解压过程打印压缩文件信息
-C dirname: 在制定目录解压缩，否则在当前压缩包的目录

## 举例
tar –tf myusr.tar.gz  #查看myusr.tar.gz包中的内容 
tar -zcvf myusr.tar.gz mydoc #用gzip将mydoc目录打包后压缩成myusr.tar.gz
tar -zxvf myusr.tar.gz #解压
tar -zxvf myusr.tar.gz -C /home/CentOS/a #解压到指定目录/home/CentOS/a
```


希望学弟学妹们能理解小Z的辛苦之作！



### 附：在Power Shell中实现上述操作

我使用的是MacOS系统，并没有使用Windows下Power Shell的需求，但出于好奇，简单查阅了相关资料，总结成了一张表格，如下：

| 描述                        | Linux 命令 | PowerShell 等效命令  |
|:------------------------------------:|:-------------:|:---------------------------:|
| 获取当前目录                        | pwd           | Get-Location 或 pwd         |
| 列出目录内容                        | ls            | Get-ChildItem 或 ls        |
| 更改目录                            | cd            | Set-Location 或 cd         |
| 创建一个新的空文件                  | touch         | New-Item -Type File         |
| 创建目录                            | mkdir         | New-Item -Type Directory    |
| 复制文件或目录                      | cp            | Copy-Item 或 cp            |
| 删除文件或目录                      | rm            | Remove-Item 或 rm          |
| 移动或重命名文件或目录              | mv            | Move-Item 或 mv            |
| 查找命令的位置                      | which         | Get-Command                 |
| 获取命令路径                        | whereis       | Get-Command                 |
| 查找文件                            | find          | Get-ChildItem -Recurse      |
| 显示文件内容                        | cat           | Get-Content                 |
| 从尾到头显示文件内容                | tac           | Get-Content -Tail 1         |
| 分页显示文件内容                    | more          | more                        |
| PowerShell没有less的直接等效        | less          | 不直接等效，可以使用more    |
| 显示文件的前n行                     | head          | Get-Content -Head n         |
| 显示文件的最后n行                   | tail          | Get-Content -Tail n         |
| 统计词、行、字符                    | wc            | 使用组合命令进行操作        |
| 创建软链接                          | ln            | New-Item -ItemType SymbolicLink |
| 查看文件或目录大小                  | du            | Get-Item 或更复杂的脚本     |
| 查看磁盘使用情况                    | df            | Get-PSDrive                 |
| 压缩或解压缩文件                    | tar           | 依赖于外部程序，如7-Zip等   |

