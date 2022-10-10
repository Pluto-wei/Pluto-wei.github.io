---
title: Linux 常用命令操作
tags: Linux
abbrlink: 34706
date: 2020-06-26 00:41:58
categories:
about:
---



一点点Linux的命令，待续...

<!-- more -->

6.22-6.25

https://www.bilibili.com/video/BV1mW411i7Qf

## 基础知识

### Linux系统的文件结构

```bash
/bin        二进制文件，系统常规命令,最经常使用的命令
/boot       系统启动分区，系统启动时读取的文件，包括一连接文件以及镜像文件
/dev        设备文件，Linux的外部设备
/etc        所有的系统管理所需要的配置文件和子目录
/home       普通用户的家目录
/lib        存放着系统最基本的动态连接共享库，其作用类似于Windows里的DLL文件。几乎所有的应用程序都需要用到这些共享库。
/lost+found 这个目录一般情况下是空的，当系统非法关机后，这里就存放了一些文件。
/media      linux 系统会自动识别一些设备，例如U盘、光驱等等，当识别后，linux会把识别的设备挂载到这个目录下

/lib64      64位库

/mnt        系统提供这个目录是让用户临时挂载其他的文件系统，我们可以将光驱挂载在/mnt/上，然后进入该目录就可以查看光驱里的内容了。
/opt        第三方软件安装位置，比如你安装一个ORACLE数据库则就可以放到这个目录下。默认是空的

/proc       进程信息及硬件信息,虚拟的目录,是系统内存的映射,可直接访问这个目录来获取系统信息。
/root       临时设备的默认挂载点，系统管理员的主目录
/sbin       系统管理命令，这里存放的是系统管理员使用的管理程序
/srv        存放一些服务启动之后需要提取的数据
/var        数据,某些大文件的溢出区，比方说各种服务的日志文件
/sys        内核相关信息
/tmp        临时文件
/usr        用户相关设定，类似program files
```

```
/usr 最庞大的目录，要用到的应用程序和文件几乎都在这个目录。其中包含：
/usr/x11r6 存放x window的目录
/usr/bin 众多的应用程序
/usr/sbin 超级用户的一些管理程序
/usr/doc linux文档
/usr/include linux下开发和编译应用程序所需要的头文件
/usr/lib 常用的动态链接库和软件包的配置文件
/usr/man 帮助文档
/usr/src 源代码，linux内核的源代码就放在/usr/src/linux里
/usr/local/bin 本地增加的命令
/usr/local/lib 本地增加的库
```

### Linux系统命令行的含义

```
示例：root@app00:~# 
root    //用户名，root为超级用户
@       //分隔符
app00   //主机名称
~       //当前所在目录，默认用户目录为~，会随着目录切换而变化
#       //表示当前用户是超级用户，普通用户为$
```

### 命令的组成

```
示例：命令 参数名 参数值
```

## 目录操作

```
cd //change directory 切换目录
cd [目录]

/根目录  .该文件夹  ..上一级目录  ~home目录  -上次访问的目录
xx(文件夹名) 本目录下的文件夹
/xxx/xx/x 输入完整的路径，直接切换到目标目录，输入过程中可以使用tab键快速补全(从根目录开始)
```

```
ls [-aldi] [文件或目录] //查看目录

a所有文件 l详细信息显示 d目录属性 i:id
u所有者 g所属组 o其他人
r读 w写 x执行
```

```
mkdir //make directories 创建新目录
mkdir -p [目录名] [目录名] //-p 递归创建（否则只有一层）
```

```
pwd  //print working directory 查看当前目录
```

```
rmdir //remove empty directory 删除空目录
rmdir [目录名]
```

```
cp  //copy 复制文件或目录（目录加-r,可以是非空文件夹）
cp -r -p [源文件或目录] [目标目录]

r复制目录 p保留文件属性
```

```
mv  //move 剪切文件、改名（可以是非空文件夹）修改目录
mv [原文件或目录] [目标目录]
```

```
rm //remove 删除文件（目录-r）
rm -rf [文件或目录]

r删除目录 f强制执行
```

## 文件操作

```
touch //新增文件
touch [文件名]
```

```
cat //显示文件内容
cat [文件名]
-n标记行号 
tac //反向列示，不支持-n
```

```
more //分页显示文件内容
more [文件名]
(空格)/f:翻页  (Enter):换行  q或Q:退出
----------- -------------------------------------------------
less //分页显示文件内容
less [文件名]
可向上翻页：page up,↑
查找 /关键词 n下一个
```

```
head //显示前几行
head [-n 20] [文件名] //指定行数
tail [-n 20 -f] [文件名] 
-f 动态显示文件末尾内容
```

```
ln  //link 生成链接文件
ln [-s] [原文件] [目标文件]
-s 生成软链接，否则生成硬链接
//软链接类似快捷方式，硬链接类似拷贝cp-p并可同步更新，id相同，不针对目录
```

## 权限管理命令

```
chmod //change the permissions mode of a file改变文件或目录权限
chmod [{ugoa}{+-=}{rwx}] [文件或目录]
chmod [777] [文件名或目录]
r-4 w-2 x-1
rwxrw-r-- 764
-R 递归修改
只有所有者u和管理员root可以更改权限

file:r:cat/more/head/tail/less
	 w:vim
	 x:script command
directory:r:ls
		  w:touch/mkdir/rmdir/rm
		  x:cd
```

```
chown //change file ownership 改变文件或目录的所有者
useradd xx
chown [用户] [文件或目录]
只有管理员root可以操作
chgrp //change file froup ownership 改变所属组
groupadd xx
chgrp [用户组] [文件或目录]
```

```
umask [-S] //显示设置文件的缺省(default)权限
mkdir的文件具有 rwxr-xr-x(目录)
touch的文件在mkdir的基础上去掉x rw-r--r--(文件)

-S以rwx的形式显示新建文件的缺省权限，否则直接显示数字
umask 0022  0:特殊权限 022----w--w- 逻辑异或:rwxr-xr-x(目录)

umask 077 //更改权限成 rwx------(目录)
```

## 文件搜索命令

* find locate which whereis grep

```
find //文件搜索
find [搜索范围] [匹配条件]

find [目录/] -name [文件名]  //精准搜索
-iname 不区分大小写
*内容* //文件名包含内容，匹配任意字符
内容*  //以内容开头
内容???//内容后有3个字符，?单个字符

find / -size +204800  //大于100MB的文件
+n大于 -n小于 n等于
1数据块 512字节 0.5k

find /home -user [user]
find /home -group [grp]

find /home -cmin -5
-amin 访问时间 access
-cmin 文件属性 change
-mmin 文案进内容 modify
-5 5min之内
+5 超过5minn

find / -type {fdl} //文件类型 f文件d目录l软链接文件
find / -inum 23333 //i节点 文件名很奇怪的时候“”

find / -size +163840 -a -size -204800
-a 同时满足and 
-o 二者之一or
find / -name [] -exec [操作ls -l] {} \;
-exec/-ok 命令 {} \; 对搜素结果执行操作  
```

```
locate //速度快，在文件资料库中查找文件
updatedb //更新文件资料库(root权限)(对tmp临时文件无效)
locate -i xx 不区分大小写
```

```
which //搜素命令所在目录及别名信息
which [cp/ls]
whereis //搜索命令所在目录以及帮助文档路径
```

```
grep //文件内容中搜素
grep -iv [指定字串] [文件]
-i 不区分大小写
-v 排除指定字串

grep -v ^# /etc/inittab //排除以#开头的行
```

## 帮助命令

```
man //manual 获得帮助信息
man [命令或配置文件]
命令: NAME 作用 /选项
配置文件: NAME 存放信息文件格式，直接写文件名，不需要写绝对路径
1 命令的帮助 5 配置文件的帮助 (同名的时候)  例:man 5 passwd

whatis 命令 apropos 配置文件(简短介绍信息)
xx --help  选项信息
info 与man类似
date 查看时间
man date 更改系统时间
help [命令] //获得shell内置命令的帮助信息(找不到路径) 例:help umask
```

## 用户管理命令

```
useradd 用户名 //添加新用户
passwd 用户名 //password设置用户密码，root任何人，passwd改自己密码
who //查看登录用户名，登录终端，tty本地终端，pts远程终端，登录时间，IP地址
w //比who还能获得当前系统时间，连续运行时间uptime，几个用户登录，负载均衡指数
```

## 压缩解压命令

```
.gz
gzip //压缩文件，不能压缩目录，tar且不保留原文件
gunzip //GNU unzip 解压gz的压缩文件

tar //打包目录。.tar 再gip压缩成 .tar.gz
tar -zcf 压缩后文件名 目录
tar -zxvf 解压 压缩包
c打包 v显示详细信息 f指定文件名 z打包同时压缩/解压缩 x解包 

zip压缩文件或目录
zip -r 压缩后文件名 文件或目录
r压缩目录
unzip 解压缩

bzip2 -k 文件// 文件格式 .bz2
k是否保留压缩包
tar -cjf xx.tar.bz2 xx
bunzip2 -k 压缩文件
tar -xjf xx.tar.bz2
```

* ![](https://s1.ax1x.com/2020/06/25/NDuLUs.png)

## 网络命令

```
write
```

## 关机重启命令

``` 
shutdown [选项-h] [时间20:30/now] 
-c 取消前一个关机命令
-h 关机
-r 重启
其他关机命令 halt，poweroff，init 0
其他重启命令 reboot，init 6
系统运行级别 init 0123456 帮助文档 help inittab
查询当前的运行级别 runlevel
改变运行级别 init n
退出登录命令 logout
```

先切换到超级用户 su root
