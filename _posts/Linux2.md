---
title: Linux2
tags: Linux
abbrlink: 58108
date: 2020-06-27 23:52:43
categories:
about:
---



Vim，Shell，正则 ...

<!-- more -->

后面好多都不想看了，先跳了....明天开始肝别的。最近玩的时间太多了。。。

# 文本编辑器 Vim

* vim常用操作

```shell
vi 进入命令模式  插入模式  编辑模式
esc 从INSERT模式退出
插入命令  aio
定位  :  set nu  :n  $  0  G  g
删除  x  nx  dd  ndd
复制和剪切  yy-p  dd-p
替换和恢复  r/R  u
搜素和替换 /+关键词 n下一个 :指定范围/要替换的关键词和字符串/替换为/g
保存退出  :wq  ZZ  :q!  :wq!

:set ic 忽略大小写
%s 全文(搜素)
:w [new_filename] 另存为
```

![](https://s1.ax1x.com/2020/06/26/NruWYn.png)

![](https://s1.ax1x.com/2020/06/26/NrMugx.png)

# 软件包管理

## 软件包分类

* 源码包 （脚本安装包 .c文件）
* 二进制包（别名RPM包，系统默认包）（相当于.exe文件）（写有安装界面）

## rpm

* 命名 

  全名=包名-版本-发布次数.适合的Linux平台.适合的硬件平台.扩展名rpm

* RPM包依耐性：树形依赖，环形依赖，模块依赖

## sudo

```
sudo apt-get install <name> 
//安装某一命令
```

（6.9-9.3跳过）

# Shell基础

## shell概述

* 编程语言

* 分为Bourne（bash，sh）和C

```
vi /etc/shells可以看有哪些shell
```

## shell脚本的执行方式

```
echo "Hello world!!"
echo -e "a\tb\bc\t\n\a\x64"
echo -e "\e[1;31m abcd \e[0m"

-e 支持反斜线控制的字符转换
```

```
vi hello.sh
#!/bin/bash  注意是小写是小写
...
chmod 755 hello.sh
./hello.sh //直接运行,(不能直接文件名哦)
bash hello.sh //通过Bash调用执行脚本
(命令都是小写)
```

```
不能识别wins的文件:
dos2unix 
```

## Bash的基本功能

* 历史命令 history  [-c清空 -w保存入文件]

  !字串 重复执行最后一条以该字串开头的命令

* 命令补全 Tab	

* 命令别名 

  alias 别名='原命令'

  alias   //查询别名

* 别名永久生效  vi /root/.bashrc

* 常用快捷键

  Ctrl+C 终止

  Ctrl+L 清屏

  Ctrl+U 删除或剪切

  Ctrl+Y 粘贴

  Ctrl+R 搜素

  Ctrl+D 退出终端

* 输入输出重定向（命令行与文件）

  命令 &>>文件  追加，正确错误一个文件

  命令 >>[文件1]  2>>[文件2]

  命令 &>>/dev/null   //垃圾箱

  输出重定向 wc > 文件  // 统计行数，字节数，单词数

* 多命令顺序执行

  ;  &&  ||

  命令 && echo yes || echo no

* 管道符

  命令1 | 命令2   命令1的正确输出作为命令2的输入

  grep [选项] 搜索内容

* 通配符--匹配文件名

  ?  匹配一个任意字符	*  匹配0个或任意多个字符

  []  匹配中括号中任意一个字符

  [-] 匹配括号中任意一个字符 -代表范围  [a-z]

  [^] 不是括号内的一个字符  [ ^0-9]

  ```
  ls [^0-9]abc
  ls *abc
  ls *abc*
  ls ?abc
  ```

* 其他特殊符号

  #注释 

  ' ' 单引号 中没有特殊字符

  " " 双引号  $调用变量的值 `引用命令  \转义符  有特殊含义

  ` = $( ) 反引号 调用系统命令  

---

（10.4-10.6跳过）

Bash的变量 Bash的运算符 环境变量配置文件

# Shell编程

## 正则表达式

* 正则在文件中匹配，通配符匹配符合条件的文件名
* 正则包含匹配 通配符完全匹配
* ls，find，cp等不支持正则，只能使用shell自己的通配符
* grep，awk，sed等支持正则

```
* 前一个字符匹配0/n次
. 除了换行以外任意字符(相当于?)
^ 匹配行首 ^hello(以hello开头)
$ 匹配行尾
[] 匹配指定的任意一个字符，一个
[^] 以外的任意一个，一个
\ 转义符
\{n\} 表示其前面的字符恰好出现n次 [0-9]\{4\}  [1][3-8][0-9]\{9\}
\{n,\} 表示前面的字符出现不小于n次
\{n,m\} 表示前面的字符出现[n,m]次
```

```
grep -n 匹配一行 标号
grep "a*"  xx.txt  //全文(感觉没什么意义)
grep "s..d" xx.txt
grep "s.*d" xx.txt //.*就是任意，什么都可以，没有也可以
grep "^M" xx.txt
grep "n$" xx.txt
grep -n "^$" xx.txt
grep -n "[0-9]" xx.txt
grep -n "^[a-z]" xx.txt
grep -n "^[^a-zA-Z]" xx.txt
grep -n "\.$" xx.txt
grep -n ".$" xx.txt /非空白行
```

## 字符截取命令

```
cut [选项] 文件名 //提取指定列
-f列号  -d分隔符(按照指定分隔符分割列) (\t)

cut -f 2,4 student.txt
cut -d ":" -f 1,3 /etc/passwd
cat /etc/passwd | grep /bin/bash | grep -v root | cut -d ":" -f 1
```

```
printf '输出类型输出格式' 输出内容
printf '%s %s %s\n'  
```

```
awk命令
```

```
sed命令
```

## 字符处理命令

## 条件判断

## 流程控制

* if
* case
* for
* while