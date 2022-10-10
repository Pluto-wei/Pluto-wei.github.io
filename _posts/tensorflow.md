---
title: Linux下tensorflow的安装
abbrlink: 16031
date: 2020-08-10 21:06:27
tags:
categories:
about:
---

www呜呜呜真的被气到了，装了好几天终于hello了

![](https://s1.ax1x.com/2020/08/10/aqNitg.png)

<!-- more -->

---

## 安装

* Ubuntu18.04 + python3.7 + anaconda3

用国外的源下是真的不行！这是离成功最近的一次👇

![](https://s1.ax1x.com/2020/08/10/aqixL6.png)

已被杀死？？这是什么毛病，都下到最后了？？

我以为从这个源看到了希望

于是又尝试了一下午，不仅慢的一批，而且下到一半就一串红。。绝了呜呜呜（主要是不想学习，，虽然马上就考试了）

---

一开始用清华源下也报错，搞了好久都没解决，所以才回去用国外的源的，后来被我点死机了以后重启了一次，在网上找了一个清华源的代码试了一下，竟然不报错了！！！那真是秒下好啊！！！（没有对比就没有伤害）

果然，遇事不决就重启，早点重启就好了（我虚拟机老是不关，每次都是暂停，估计是运行时间太长了）

```
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple/ --upgrade tensorflow-cpu
```

第一次上面的代码里没加cpu，结果下的gpu版本，还要下载cuda那些？太麻烦了吧。于是又下了一个cpu版本的。

---

## 测试

迫不及待的试一下 

* 👇（我每次都是这样启动的）

```
anaconda-navigator
jupyter
spyder
```

```
import tensorflow as tf
```

说来也奇怪，之前没有装成功的时候，这行代码竟然不报错，但是tensorflow里的函数一个也用不了

~~~
import tensorflow as tf
hello = tf.constant('hello,tensorf')
sess = tf.Session()
print(sess.run(hello))
~~~

* 测试代码如上，但是还是报错，sess那里用不了

![](https://s1.ax1x.com/2020/08/10/aqEdk8.png
)

* 可能是版本问题？

~~~
import tensorflow as tf
tf.compat.v1.disable_eager_execution()
hello = tf.constant('hello,tensorflow')
sess= tf.compat.v1.Session()
print(sess.run(hello))
~~~

![](https://s1.ax1x.com/2020/08/10/aqEUTf.png)

* 至于为什么输出这个比别人多一个b和引号我也不清楚，为什么sess报错我也不理解

![](https://s1.ax1x.com/2020/08/10/aqVQH0.png)

* 查看版本（我不管这就是装好了）

![](https://s1.ax1x.com/2020/08/10/aqAWzd.png)

---

## 报错

* sess报错

>tensorflow2.0版本中的确没有Session这个属性，如果安装的是tensorflow2.0版本又想利用Session属性，可以将tf.Session()更改为：
>
>~~~
>tf.compat.v1.Session()
>~~~
>
>这个方法可以解决此类问题，不仅仅适用于Session属性。
>
>但是又会报另一个错因为2.0和1.0版本不兼容
>
>于是在开始部分加：
>
>~~~
>tf.compat.v1.disable_eager_execution()
>~~~
>
>tensorflow的官网对disable_eager_execution()方法是这样解释的：
>
>~~~
>This function can only be called before any Graphs, Ops, or Tensors have been created. <br>It can be used at the beginning of the program for complex migration projects from TensorFlow 1.x to 2.x.
>~~~
>
>此函数只能在创建任何图、运算或张量之前调用。它可以用于从TensorFlow 1.x到2.x的复杂迁移项目的程序开头。
>
>还有一个更简单的方法：
>
>~~~
>import tensorflow.compat.v1 as tf
>tf.compat.v1.disable_eager_execution()
>~~~

参考：https://www.cnblogs.com/123456www/p/12584427.html

* 啊这，真的可以！！！快乐了

![](https://s1.ax1x.com/2020/08/10/aqZYIf.png)

![](https://s1.ax1x.com/2020/08/10/aqeHns.png)

* 可是为什么多一个b呢，看着好不顺眼

> 这里的输出结果是一个字节字符串。要删除字符串引号和“b”（表示字节，byte）只保留单引号内的内容，可以使用 decode() 方法。

~~~
print(sess.run(hello).decode())
~~~

![](https://s1.ax1x.com/2020/08/10/aqNitg.png)

* 而且print方法好像也跟以前的版本不一样？也报错了，要加括号

~~~
print result
print (result)
~~~

* 网上教程还挺多的：

  https://www.w3cschool.cn/tensorflow_python/

  http://c.biancheng.net/view/1880.html

* 还是先看懂基本原理，吴恩达的深度学习看了

---

* 啊啊啊快乐了，明天开始复习！！！下次一定！！
* 再不开始复习就没了：微积分、大物、离散、模电、大化、六级、近代史
* 还有arduino和机器学习！！！

* 开学还要重装系统，又得配一遍环境装一遍系统，好麻烦呀

![](https://s1.ax1x.com/2020/08/10/aqNfUS.jpg)

* 听说有两个比较有用的工具：chocolatey、Docker，希望能简单一点

---

好想玩糖豆人  xmsl  想去上海呜呜呜

![](https://s1.ax1x.com/2020/08/10/aqUKKI.png)