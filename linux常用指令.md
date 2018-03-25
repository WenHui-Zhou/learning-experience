linux 日常使用中用到指令
===============

> cd ~/pip

~/ 指的是home的目录

> vi filename

vi指令用于打开文件，如果文件不存在的话就是创建

> vi version.txt
> i    #在vi的环境下输入i指插入模式，开始修改文件
> ： #输入冒号指行末指令，通常用于保存文件等
> wq #在行末指令下输入wq指保存并退出
> q!   #退出不保存

创建文件夹：

> mkdir name
> touch filename  #创建空文件

pip的一些格式
--------

> pip install packetname  #下载包
> pip install -U packetname #更新包
> pip install -i https://pypi.tuna.tsinghua.edu.cn/simple -U name #暂时换源