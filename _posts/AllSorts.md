---
title: 关于全排序的一些理解
tags: 碎碎念
abbrlink: 34333
date: 2020-02-09 22:29:04
categories: 瞎想
---

这个递归真的想了好久
就是觉得别扭，想bb几句🤐
![](https://upload-images.jianshu.io/upload_images/20644861-98104d5e39d449c2.gif?imageMogr2/auto-orient/strip)
<!-- more -->


# 来理解一下全排序(递归)

```c++
//输出1~n的全排列
#include <cstdio>
const int maxn =11;
int n,P[maxn],hashTable[maxn]={false};
void generateP(int index){
    if(index == n+1){ //递归边界
        for(int i=1;i<=n;i++){
            printf("%d",P[i]);
        }printf("\n");
        return;
    }
    for(int x=1;x<=n;x++){
        if(hashTable[x]==false){
            P[index]=x;
          	hashTable[x]=true;
            generateP(index+1); //递归在这里！！！
            hashTable[x]=false;
        }
    }
}
generateP(1);//从1开始的全排序
```

- 要写从1~3的全排序：

- 一共三位

  第一位从1开始循环，每一轮回就是引用一次剩下2个数的全排列

- 每用一个数，就用hashTable标记该数已经使用，然后开始下一位的全排列，并在排列完并输出以后，恢复这个数没有使用的状态，并且这个数没到最大值的话，这一位上的这个数就要加一了，否则就会退出。（该前面的数恢复了）

- n个数排完后会执行generateP(n+1)，就会输出这n个数，然后返回继续后面的步骤，继续排列

------

- 比如generateP(2)，就是从第二位开始的全排列，不会给前面赋值，第一位每个数都会调用一次generateP(2)，当然前面用过的数会不再使用
- 直到最后一个数的全排序，就等于剩下的那个数

------

- 但是递归边界又不能写只剩最后一个数，

```c
#include <cstdio>

int n,m,P[100];//n是总数，m是当前填的数，x是位数
bool hT[100]={false};
void g (int x){
    if(x==n){  
        for(int i=1;i<=n;i++){
            if(hT[x]==false){
                P[x]=i;
            }
        }
        for(int i=1;i<=n;i++){
            printf("%d",P[i]);
        }printf("\n");
        return;
    }for(int m=1;m<n;m++){
        if(hT[m]==false){
            P[x]=m;
            hT[m]=true;
            g(x+1);
            hT[m]=false;
        }
    }
}

```

- 为什么这样是不行的，因为g(n)运行完后跳到上一位变成false，m+1以后到了n没有循环了
- 也就是倒数第二位不会变成最大的数，就以为自己的全排列已经结束了
- 也就是最大的数永远不会出现在前面
- 所以递归边界不能写n，必须是n+1

```c
int main (){
    n=4;
    g(1);
}
输出：
1234
1324
2134
2314
3124
3214
n=3 时输出：
123
213
```

![](https://upload-images.jianshu.io/upload_images/20644861-c18c9fe808091d6c.gif?imageMogr2/auto-orient/strip)