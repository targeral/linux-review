# linux 复习

## 3. shell and shell command

### shell 基本功能

* 命令解释执行
* 文件名替换
* I/O重定向
* 通信管道建立
* 系统环境设置
* shell 编程

*关于shell的命令集，默认情况下，当用户从键盘输入一个命令时，shell首先检查它是否带有路径，若有则按路径搜索他，找到后执行；若不是，再检查是否是一个外部命令或应用程序。*

*shell的另一个重要特性是他自身就是一个解释型的程序设计语言*

### 字符与保留字

#### 1. 字符

1. 白空格：空格和Tab称为白空格。用于命令行中命令名，参数及选项的分隔。在特殊时候，白空格中也包含回车字符。
2. 通配符：“*”（代表从他所在位置开始的任何字符串），“?”（代表他所在位置上的任何单个字符），“[]”（代表一个指定范围的字符）。
3. 注释符与注释：“#"开头的行是注释行
4. 转义字符：“\b” 退格键、"\f" 换页、"\n" 换行、"\t" tab键、"\\" \、"\e" Esc。

#### 2.特殊键

1. Ctrl + D ：结束当前程序输入或结束当前程序或从系统中注销
2. Ctrl + C ：终止当前程序的执行
3. Ctrl + Alt + Del ：默认动作为重启系统

#### 3. 保留字



### 文件命名及文件类型

#### 1.文件与文件名

它由字母，数字，下画线和圆点组成的字符串构成。

#### 2. 文件类型

linux系统中有三种基本的文件类型：普通文件，目录文件和设备文件。

1. 普通文件：(1) 文本文件 (2) 二进制文件
2. 目录文件：**注意：目录文件的大小只能增加，尽管可以目录中删除文件和子目录，但不能使目录变小。使目录变小的方法是删除后重建。**
3. 设备文件：设备文件与普通文件和目录文件不同，他除了在目录文件和文件说明信息表中占据相应的位置之外，**并不占有实际的物理存储空间**。通常情况下，设备文件存放在系统的设备目录/dev下。

​        常见的设备文件有一下几种：

1. 块设备文件
2. 字符设备文件
3. 管道设备文件：(1) 无名管道 (2) 命名管道
4. 符号链接文件：又叫软链接
5. 套接字文件



### 目录结构与路径

#### 1. 目录与目录结构

* /：系统的根目录
* /dev：系统的设备目录，其中存放着几乎所有的设备文件
* /mnt：外部设备的挂装点，用于挂载设备文件。
* /boot：linux的启动目录。
* /tmp、/usr/tmp：临时目录。
* /bin、/usr/bin：用户级的命令与工具目录。
* /lib、/usr/lib：库文件存放目录，其中有表态库和动态库。
* /usr/src：linux源代码目录，编译内核时使用。



### shell命令解释及执行	

#### 1. 分隔符

白空格

#### 2. 选项和参数

选项是由符号"-"引导的字符或字符串。

#### 3. 命令行编译特性

1. 命令和文件名扩展：tab补全。
2. 命令行编辑
3. 历史记录



### 环境变量与变量

#### 1. 环境变量

环境变量可以用命令`env` 或 `set`来查询。

#### 2. 变量

引用变量时需要使用 `$` 作为变量名的前导字符。

变量的定义方法：

```bash
var_name=var_value
```

变量的定义和使用示例：

```bash
# x=123
# y='I am a student'
# echo $x $y $HOME
# z="$x $y"
```



### 标准流与输入/输出重定向

#### 1. 标准流

当执行一个命令时，shell通常会自动为其打开三个标准流（文件）：标准输入流，标准输出流和标准错误流。



| 标准流  | 文件号  | 描述符    | 使用设备 |
| :--- | ---- | ------ | ---- |
| 标准输入 | 0    | stdin  | 键盘   |
| 标准输出 | 1    | stdout | 屏幕   |
| 标准错误 | 2    | stderr | 屏幕   |



#### 2. I/O重定向

I/O重定向是指通过文件的形式实现标准I/O流。I/O重定向可以通过以下符号实现。

1. `<` ：标准输入重定向
2. `>` ：覆盖方式标准输出重定向。若文件不存在，则创建；否则覆盖。
3. `>>` ：追加方式标准输出重定向。若文件不存在，则创建；否则在其尾部追加。
4. `&>` 或 `>&` ：标准输出和标准错误同时重定向（不能用于追加方式）。

### 管道

#### 1. 管道

实现管道机制的符号是"|",其方法为：

`命令1 | 命令2 |....| 命令n`

例如：

```sh
#ls -l /dev | wc -l
#cat sample.txt | grep "High" | wc -l
```

#### 2. 三通

有时，对某文件进行处理时，既要在屏幕上看见输出，又要同时保存一个副本，这时可以使用管道与tee命令配合来实现三通。

tee命令的功能是读取标准输入的数据，并将内容输出到指定文件，其用法为：

```sh
tee [-ai][files]
```



### 引号机制、命令替换与参数替换

#### 1. 引号机制

在shell中有三种引号： 单引号，双引号，返单引号，前两者用于变量定义，后者用于命令替换。

*所谓命令替换是指返单引号内的内容将作为命令首先被执行，然后再将命令执行的结果替换返单引号以及其括住位置的信息。*

**双引号具有变量替换和命令替换。**

#### 2. 参数替换



### shell命令的执行

#### 1. 标准流与程序I/O

#### 2. 命令的返回值

一般情况下，返回值为0表示成功，非0表示失败。



### shell 种类



## 3.2 linux系统的基本命令

### 目录操作基本命令

#### 1.列目录内容(`ls`)

```
ls [options] [files]

options:
        -a
        -A
        -b
        -i
        -l
        -F
        -r
        -R 递归列出目录及子目录
        -t
        -U
```

#### 2. 建立目录(`mkdir`)

```
mkdir [-p] [-m MODE] dirs

-p: 如果要创建的目录存在也不报错，必要时可一同创建父目录
-m: 按照权限MODE创建子目录
```

#### 3. 删除目录

```
rmdir [-p] dirs

-p: 使用-p参数，rmdir在删除一个目录时，若其子目录也是空的，则一并删除。
例如：

# rmdir temp #删除子目录temp，若非空则报错
# rmdir -p a/b/c #删除目录时一同删除其空子目录
# #注意，若a只有子目录b，b只有子目录c，则以上命令等同于：
# rmdir a/b/c;rmdir a/b;rm a
```

#### 4. 改变工作目录(`cd`)

```
cd [dir]

# cd /tmp #切换到目录/tmp
# cd ~ #切换到刚离开的目录
# cd .. #切换到上级目录
# cd #切换到家目录
```

#### 5. 显示当前目录(`pwd`)

```
pwd [-P] [-L]

-P,-L分别用于显示当前目录的物理和逻辑位置，默认为后者。
```



### 文件操作基本命令

#### 1. 显示文件的内容或合并文件(`cat`)

```
cat [options] [files]

options: 
	    -E: 在行末显示$符号
	    -n: 为所有行添加行号
	    -v: 显示所有内容
	    -s: 当有一个或多个空行时只显示一个
	    
示例:
	#cat tst1.txt tst2.txt > tst.txt #将tst1.txt和tst2.txt的内容合并为tst.txt
```

#### 2. 分屏显示文件内容(`more`)

```
more [-dflpcsu] -lines[+linenum | +/pattern] files
```

#### 3. 使用less命令浏览文件

**比more更强大**

#### 4. 修改文件存取时间或创建空文件(`touch`)

touch命令的功能有两个：一个是建立空文件，二是更新文件的存取时间。

```
touch [-acm] [-r ref_file] [-t [[CC]YYMMDDhhmm[.ss]] files
touch [-acm] [-t MMDD[yy]] files
```

#### 5. 文件或目录的删除(`rm unlink`)

```
rm [options] files

options:
        -i: 交互方式。删除前逐一询问确定，回答时，y/yes表示确定，其他为放弃。
        -f: 强制删除，删除时不进行提示。
        -r/-R: 递归方式。
```

```
unlink 用于删除单个文件，但不能删除目录
```
#### 6. 文件移动或更名(`mv`)

```
mv [options] source dest     将源文件移动到目的文件，可用于文件移动或更名
mv [options] source directory   将一批文件移动到某个目录下。
```

#### 7. 文件和目录复制(`cp`)

用于复制文件或目录，**不能复制设备文件，但可复制设备文件的内容以构造映像**

```
cp [options] source dest
cp [options] source... directory

options: 
   		-d 复制时复制符号链接
   		-p 复制源文件时，保留源文件的属性信息
   		-l 不复制，只创建硬链接
   		-s，不复制，之创建符号链接
   		-R,-r 递归复制。
```

#### 8. 显示文件的开头或结尾部分(`head/tail`)

```
head [-num | -n num] [files]
tail [-num | -n num] [files]
```

#### 9. 文件的格式输出(`pr`)

```
pr [options] files
```

#### 10. 以指定格式或进制显示文件内容(`od`)

默认为八进制。

```
od [options] files
od --traditional [files] [[+]offset [[+]label]]
```

#### 11. 显示文件或文件系统状态信息(`stat`)

```
stat [options] files
```

### 文本文件编辑与操作基本命令

#### 1. 文本编辑命令(`vi`)

#### 2. 字符串过滤命令(`grep`)

`grep` 命令的功能是字符串搜索与过滤。用于字符串过滤的命令有三个：`grep` 、`egrep` 、`fgrep` 。

`grep` 使用标准正则表达式，`egrep` 使用扩展正则表达式，`fgrep` 则使用固定的字符串表达式。

```
grep [options] pattern [files]
grep [options] [-e pattern | -f patternfile] [files]
```

#### 3. 文件排序命令(`sort`)

#### 4. 处理文件中的重复行命令(`uniq`)

`uniq` 命令的功能是处理文件中的重复行。该命令首先比较相邻的行，然后处理其后重复的行，在文件中不相邻的重复行将不会处理。**若想发现某文件中的所有重复行，可先用`sort` 命令排序。**

```
uniq [options] [infile [outfile]]
```

#### 5. 文件内容信息统计(`wc`)

`wc` 命令的功能是对输入文件的信息进行统计。统计信息包括行数，单词数和总字节数等。

```sh
wc [-c] [-m] [-w] [-l] [-L] files

-c/-m 字节/字符数统计
-w 统计单词数
-l 统计行数
-L 统计最长行的字节数
```

### 进程管理基本命令

#### 1. 进程树及进程状态查询(`pstree`)

显示系统内进程间的关系——进程树。

```
pstree -n 按pid排序，而非默认进程名称排序
pstree -p 显示pid
pstree -u 显示用户名称
```

#### 2. 终止进程执行(`kill`)

### 时间管理命令

#### 1. 时期与时间管理命令(`date`)

#### 2. 日历显示命令(`cal`)

```
cal [-smjy13] [[month] year]
```

### 文件或目录比较命令

#### 1. 比较两个文件的命令(`cmp`)

```
cmp [-l] [-s] file1 file2 [skip1 [skip2 ]]

-l 显示所有不同的位置和差异
-s 只返回退出码。0：文件相同；1：文件不同；>1：错误
skip1,skip2 分别表示file1 file2 开始的偏移位置
```

**说明：通常使用`cmp` 命令比较非文本文件，使用`diff` 比较文本文件**

#### 2. 比较文件的差异(`diff`)

```
diff [options] file1 file2
```

#### 3. 逐行比较两个已经排序的文件(`comm`)

#### 4. 显示或剪取文件行的指定部分(`cut`)

#### 5. 连接文件的行(`paste`)

```
paste -d Sep   指定在并行合并时使用Sep作为输出分隔符，默认为Tab。
```

#### 6. 连接两个文件的行(`join`)

#### 7. 文本文件排版(`fmt`)

#### 8. 文本文件包装(`fold`)

### 其他操作命令

#### 1. 清屏命令(`clear`)

#### 2. 字符串或变量输出命令(`echo`)

#### 3. 变量输入命令(`read`)

`read` 命令从标准输入上读入一行，并将它读到的内容*按照分隔符分隔的字符串传递给相应变量。* 若值得个数多余变量个数，多余的部分赋给最后一个变量；若值的个数少于变量个数，则后面多余的变量被置空。如果没有指定变量名，则默认为REPLY作为变量名。

```
read [-d delim] [-n num] [-p prompt] [-r] [-s] [-t time] var1 var2 ...

-d delim 指定新的分隔符
-n num 当read读到num个字符后返回
-p prompt 设置提示信息
-s 安静方式。键盘输入屏幕不回显，可用于密码输入
-t timeout 设置超时时间为timeout。当等待时间超过timeout秒后返回
```

#### 4. 显示环境变量命令(`env`)

#### 5. 环境变量的定义(`export`)

#### 6. 定位可执行程序及相关信息(`which` 、`whereis` 、`whatis` 、`apropos`)

`find` 命令可用于各种文件的查找与搜索，但linux为用户提供了`which` 、`whereis` 、`whatis` 、`apropos` 命令专门用于对命令及其相关信息进行搜索。

#### 7. 为可执行程序定义别名(`alias`)

```
#alias #显示所有已经定义的别名
#alias ll rm #显示ll 和 rm 的别名定义
#alias li='ls -l -i' #定义别名li，其功能为ls -l -i
```



## 4. 用户、组和密码管理

### Unix系统的用户和组

#### 1. 用户与uid

用户uid是系统辨识用户的唯一标志，而用户名则是用户的外部表示。**用户信息存放在文件`/etc/passwd` 中。用户标志uid可用命令`id`来查询**

#### 2. 用户组

系统在创建用户时，为每个用户安排了一个归属组(group)。系统中的每个组都有一个组名(group name)和一个组标志(gid)。

一个组是具有某种联系或关系的用户集合。一个组可以包含多个用户，一个用户可以参与不同的组。

**组信息存放在文件`etc/group` 中，组标志`gid` 也可以用命令`id` 来查询。**

### 与用户和组管理相关的文件

与用户和组管理相关的文件有

* `/etc/passwd` （系统用户数据库文件，包括系统内所有已经注册用户的信息，是一个文本文件） 

* `/etc/shadow` （影子密码文件） 

* `/etc/group` （组定义文件）

* `/etc/login.defs` （定义了与用户创建和密码管理相关的参数）

* `/etc/default/useradd` （创建用户的默认属性参考值）

   等等，用于对用户设置和用户登录进行控制。

### 用户管理命令

#### 1. 用户创建(`useradd`)

#### 2. 用户删除(`userdel`)

#### 3. 用户修改(`usermod`)

### 组管理命令

#### 1. 组创建(`groupadd`)

```
groupadd [-g gid [-o]] [-r][-f] group

-f,--force 当指定组已经存在时，不报告错误而直接成功返回
-g gid 指定新创建组gid，gid应满足条件: GID_MIN <= gid <= GID_MAX
```

#### 2. 组删除(`groupdel`)

#### 3. 组修改(`groupmod`)

### 密码管理

#### 1. 密码管理命令(`password`)

### 与用户身份和位置相关的其他命令

#### 1. 显示已登录用户的信息(`who`)

#### 2. 显示与用户和组相关的身份信息(`id`)

```
id [options] [username]
```

#### 3. 显示使用者的用户名(`whoami`)

#### 4. 确定用户所使用的终端设备(`tty`)

#### 5. 不退出系统而将自己切换成其他用户(`su`)

```
su [options] [-] [newuser [args]]
```

若不指定用户名，则默认为root。

#### 6. 向系统中已登录的所有用户发消息(`wall`)

```
wall [message]
```

`wall` 命令可以将其命令行参数的内容作为信息发送。当不带参数时，`wall`命令将使用标准输入，用户在输入完毕时应按^D结束

## 5. Unix/Linux文件系统及管理

### 文件系统权限及管理

#### 1. 两种用户

一类是超级用户或根用户root，另一类为普通用户或称为一般用户。

#### 2. 三种权限

* 读权限(r)
* 写权限(w)
* 执行权限(x)

#### 3. 三类人

* 主用户(u)
* 同组用户(g)
* 其他人(o)

#### 4. 权限控制

```
-rwxr-xr-x
```

输出的第一列为文件的类型和权限，其中的第一个字符为文件类型。"b"表示文件为块设备文件；"c"表示文件为字符设备文件；"d"表示文件为目录文件；"l"表示文件是一个指向`/dev/scd0` 的符号链接；"-"表示文件是一个普通文件。

### 权限管理命令

#### 1. 设置文件创建掩码(`umask`)

#### 2. 改变文件的权限(`chmod`) 

`chmod` 功能为改变文件或目录的访问权限。

```
chmod [options] <a|u|g|o> <+|-|=> <str_perm>,...file

chmod [options] num_perm file...
```

#### 3. 改变文件的所有者(`chown`) 

本质上改变用户的`uid`。只有超级用户有权使用`chown`

```
chown [options] owner[:group] file...
chonw [options] :group file...
```

如果用户组被指定，则文件的所属组也将被改变。

#### 4. 改变文件的组(`chgrp`)

```
chgrp [options] new_group file...
```

### 文件系统管理

#### 1. Unix/Linux支持的文件系统

`msdos` 、`umsdos` 、`vfat` 、`ntfs` 文件系统

#### 2. 文件系统的创建

`fdisk` ：在硬盘上创建分区

`mkfs` ：创建文件系统

#### 3. 文件系统的使用

* `mount` 文件系统安装
* `umount` 文件系统卸载

## 6. 进程与任务或作业管理

### 程序和进程的概念

#### 1. 程序、进程、作业和任务

**程序** 是一个存储在存储介质上的文件，它是数据文件，但又不同于一般数据文件，不仅具有可执行的属性，而且具有执行的内容。

**进程** 是一个程序的动态执行过程。

**作业** 或 **任务** 是用户需要计算机完成某项任务时要求计算机所做工作的集合，一个作业可能需要几个程序联合完成。

#### 2. 三类进程

* 前台进程：是指用户直接控制的用于完成某个任务的进程。
* 后台进程：是指在系统后台运行的进程。
* 守护进程：也叫服务器或精灵进程，它是后台进程的一种，该类进程永久不停地运行着，以等待其他进程提出服务请求，从而为它们提供服务。
* 批处理进程：是用户按照某种意图将一批作业和任务通过编程的方法提交给系统，让系统在某个适合的时间来调度和执行的进程。

### 进程管理与调度命令

