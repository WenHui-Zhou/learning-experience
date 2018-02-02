Linux
=====

introduce
---------

linux make its components available via file.

linux with the top node of the system being **root** or **/**

linux 是一个multi-tasking 的系统

linux 术语
-------

kernel：内核，指的是Linux操作系统的大脑，操纵着硬件以及软件。

distribution：发布，指的是一些程序的集合，这些集合与kernel一起组成了Linux-based 操作系统。

boot loader: 是一个启动操作系统的应用程序。

Service: 服务，作为一种后台程序执行。例如httpd,nfsd等

FileSystem: 用于保存以及组织文件。例如ext3,FAT,XFS等文件系统。

X window system：提供了一种标准的工具以及协议，用于建立图形用户界面。

desktop Environment：是在操作系统上的一个图形用户接口，例如GNOME,KDE等。

command line：是一个用于输入指令的接口。

shell：是command line的编译器，编译输入的指令，指导操作系统完成一些工作。

gdm：GNOME显示环境管理器，是一个后台的小程序

lightDM：跨桌面环境的显示管理器

系统开机
----

当系统开机后， Basic Input/Output System (BIOS) 对硬件，屏幕等等进行初始化，BIOS存放在ROM中，其他初始化工作由操作系统完成。同时完成开机自检（POST）

The boot process has multiple steps, starting with BIOS, which triggers the boot loader to start up the Linux kernel. From there, the initramfs filesystem is invoked, which triggers the init program to complete the startup process.

BIOS(init the devices such as keyboard)->boot loader(start up the linux kernel) -> inittramfs filesystem invoked -> init program(complete the startup)

文件系统
----

打开文件系统，默认在当前桌面文件夹，快捷键`ctrl+l` 获得当前位置

软件升级
--
Debian系统：dpkg是这些系统的底层包管理器;它可以安装、移除和构建包。与更高级别的包管理系统不同，它不会自动下载和安装包并满足它们的依赖关系。
Debian系列的系统使用更高级的工具：apt-based(Advanced Package Tool)来作为包管理器。例如：apt-get 等等。

系统开发软件
------

编译器：C++/C的编译器 gcc。

Debugger：gdb

Linux顶级目录
---------

    /              根目录
    ├── bin     存放用户二进制文件
    ├── boot    存放内核引导配置文件
    ├── dev     存放设备文件
    ├── etc     存放系统配置文件
    ├── home    用户主目录
    ├── lib     动态共享库
    ├── lost+found  文件系统恢复时的恢复文件
    ├── media   可卸载存储介质挂载点
    ├── mnt     文件系统临时挂载点
    ├── opt     附加的应用程序包
    ├── proc    系统内存的映射目录，提供内核与进程信息
    ├── root    root 用户主目录
    ├── sbin    存放系统二进制文件
    ├── srv     存放服务相关数据
    ├── sys     sys 虚拟文件系统挂载点
    ├── tmp     存放临时文件
    ├── usr     存放用户应用程序
    └── var     存放邮件、系统日志等变化文件

Command Line Operations
-----------------------

文件操作：

 - cat /home/zhou/Desktop/afiles   --  用于显示文件里头的内容
 - tac /home/zhou/Desktop/afiles   --  逆序显示文件
 - head /home/zhou/Desktop/afiles   --  用于显示文件头部一部分的文件
 -  tail /home/zhou/Desktop/afiles   --  用于显示文件尾部一部分的文件
 -  man /home/zhou/Desktop/afiles   --  用于显示文档
 -  pipe（|）：例如  A | B 作用是先执行A 然后将返回的值传给B执行
 - tail :默认实现后10行，tail -n 15 后15行
 - touch filename  ：新建文件
 - touch -t 03201600 myfile ：为myfile 设置时间为03201600（03,20，1600）
 - mkdir：用于创建文件夹，mkdir newdir
 - mv file newfile：给file取了一个新名字newfile
 - rm file：删除文件
 - rm -f file：强制删除文件
 - rm -rf file：强制删除目录
 - 使用rm -i 当你不知道要怎么删除一个文件的时候
 - pile( | ) :  command1 | command2 | command3 ，command2以command1的返回为输入，command3以command2的返回为输入
 - locate file ： 寻找file的位置 ，locate file | grep pp，寻找file位置，同时包含字符pp
 - 

> command是你说要执行的程序，它通常包含很多的选项，通常由一个或两个（-）开头，如 -p 或 --print。

 - **sudo** 操作：开头的命令，允许用户使用root的权限来运行程序。
 - 关闭GUI：sudo systemctl stop gdm
 - 快捷键：ctrl+alt+F4从GUI切换到virtual terminal，返回gui: ctrl+alt+F7
 - 连接远端机器：使用Secure Shell（SSH）: ssh username@remote-server.com
 - 关机：sudo shutdown -h   重启：sudo shutdown -r
 - 可执行文件一般存在于：/bin, /usr/bin, /sbin, /usr/sbin, or under /opt.
 - 在当前位置寻找文件：which afile 
 - 在更大的包空间中寻找文件： whereis afile
 - ls file? ： 用？ 来代替任意一个字符
 - ls *.out 输入所有out为后缀的文件，
 - ls ba[a-s].out 输出所有ba开头，一个字符在a-s之间的字符
 - find 未加参数则列出所有文件，find -name gcc gcc名字的所有文件，find -type d -name gcc 只找目录为gcc的文件

访问目录
----

当你第一次登入系统的时候，你的位置在home directory 。通过echo ￥HOME来输出home位置（echo将argument送出至标准输出（STDOUT））

 - pwd:显示当前的路径
 - cd: 如cd path。 进入path这个路径
 - cd .. 返回到上一级
 - cd -回到上一个目录的位置（- 减号）
 - 单独使用cd 或者cd ~ 意味返回到home directory
 - 绝对路径由 / 开头，相对路径从现在的位置出发的下一个位置
 - （.）表示当前路径。（..）表示上一级路径。（~）home directory
 - cd / ：回到根目录
 - ls：列出当前目录下的目录
 - ls -a :（list all）列出当前位置下的所有路径，文件，包括那些隐藏的文件
 - ls -li：列出文件名， 文件iNode等许多信息
 - tree：以tree的形式显示filesystem
 - echo "something" > afile： 覆盖的形式重新afile
 - echo "something" >> afile：追加afile一些内容

> 硬链接：ln file hard：（给file取一个hard的名字）一个文件有几个文件名就说这个文件的链接数为几。硬链接就是同一个文件有多个别名，公有一个iNode（同一个文件），改变任何一个别名的文件，都会改变文件。删除操作只会删除掉别名，由于iNode区域仍存在，不会影响其他别名的文件。
> 软链接（符号链接）：ln -s file soft：soft里头仅仅保存着原文件的路径

在linux中有三个标准文件流，standard input，名称为stdin，序号为0，默认为键盘。standard output，名称stdout，默认为terminal。standard error，名称为stderr。默认为terminal。我们可以为他们重定向。

 - 输入重定向：do_something_program < inputfile ：inputfile文件作为输入，到program中
 - 输出重定向：do_something_program > file : 输出到file中

安装软件
----

> linux提供了两个类型的包管理系统，一类是低级别的管理器如dpkg，用于解压缩单独的安装包，运行脚本，确保软件安装正确。另一类是高水平的工具，如apt-get等，用于与组包一起工作，从供应商下载软件包，并计算依赖关系。大多时候调用apt-get 就行了，它会调用底下的dpkg。

 - 查找包： sudo apt-cache search lynx
 - 安装包：sudo apt-get install lynx
 - 查看安装状态：sudo apt-cache policy lynx
 - 卸载包：sudo apt-get remove lynx
 - 得到安装目录：sudo dpkg -l
 - 更新包：sudo apt-get update

> 感觉apt-get更偏向去下载，卸载，apt-cache偏向去查询的作用。

问题修复
----

当键盘打不出来pipe（|） 的时候，命令行输入：setxkbmap us 即可。

linux帮助文档
---------

 - man page
 - GUN info
 - command help

**man pages：** 是linux的用户帮助手册，里头有配置文件，系统调用等信息。man 程序包含了这些信息。可以利用`man -f 指令` 来查看指令的作用，`man -k 指令` 来看涉及到该指令的地方。

GNU info System
---------------
man page 的替代品，提供更加方便的使用方式。info  topic

help方式
------

man --help 或man -h 列出man的参数说明

文件
--
diff [option] file1 file2  列出两个文件的不同

bash shell script
-----------------

bash指的是一套准则，用这套规则，我们来写scripts，可以一次性执行很多条语句。