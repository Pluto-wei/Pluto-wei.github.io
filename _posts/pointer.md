---
title: 关于指针的初始化问题
tags: 碎碎念
abbrlink: 15588
date: 2020-02-08 14:07:36
categories: 瞎想
---



不要给任何没有初始化的指针赋值！
不要给任何没有初始化的指针赋值！
不要给任何没有初始化的指针赋值！
重要的事情说亿遍！！！！
<!-- more -->
老是忘掉！！！

💡应该在给 *p赋值前要给 *p分配一个空间

💡scanf读入字符串一定要事先为它申请足够的空间

* 字符串

```c
#include <stdlib.h>
char *str = (char*)malloc(20*sizeof(char));
```

* 结构体指针

```c
#include<stdio.h>
int main(){
    struct studentInfo{
        int id;
        char name[20];
        char gender;
        studentInfo* next;
    }*p;
    scanf("%d %c", &p->id, &p->gender);
    printf("%d %c", p->id, p->gender);
    return 0;
}//这样是无法输出的，因为对结构体指针没有进行初始化操作
```

```c
#include<stdio.h>
int main(){
    struct studentInfo{
        int id;
        char name[20];
        char gender;
        studentInfo* next;
    }stu, *p;
    p = &stu;
    scanf("%d %c", &p->id, &p->gender);
    printf("%d %c", p->id, p->gender);
    return 0;
}//这样才可以！
```

```c
//结构体数组指针也是一样
struct student{
	int id;
    char name;
}stu[100],*p;
p = stu;
scanf("%d %s",&(p+i)->id,(p+i)->name);
printf("%d %s",(p+i)->id,(p+i)->name);
```

* 而那个结构体的构造函数，是用于给结构体赋值方便的一个函数，那个初始化跟这个初始化不一样

💡 其实不过就是你在给指针指向的地方赋值的时候，总得知道他指向哪里吧