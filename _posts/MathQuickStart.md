---
title: 数学入门
tags: C语言
categories: 算法笔记
abbrlink: 3549
date: 2020-02-15 11:12:29
about:
---

唔，这里是算法笔记第五章-数学问题💓
大概是两天半吧，内容挺少的。后面还划水了一部分😜
至此入门的三章算是看完咯！
<!-- more -->

迟到的情人节快乐哟🤗![](https://upload-images.jianshu.io/upload_images/20644861-5844382797ca18ab.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


# 入门篇3--数学问题

## 简单数学

- 只要掌握简单的数理逻辑

## 最大公约数与最小公倍数

- 一般用gcd(a,b)表示a,b的最大公约数
- 一般用欧几里得算法（辗转相除法）

```c
int gcd(int a,int b){
    if(b==0) return a;
    else return gcd(b,a%b);
    //简洁：return !b?a:gcd(b,a%b);
}
```

- 一般用lcm(a,b)来表示最小公倍数
- 最大公约数d，最小公约数a/d*b

## 分数的四则运算

### 分数的表示和化简

- 假分数，只有分子和分母
- 注意分母不能为0啦

```c
struct Fraction{ //分数
    int up,down; //分子分母
}
```

- down为非负数
- 若分数为0，则up=0，down=1
- 分子分母没有除了1以外的公约数

```c
//分数的化简
Fraction reduction(Fraction result){
    if(result.dowm<0){
        result.up=-result.up;
        result.down=-result.down;
    }
    if(result.up==0) {
        result.down=1;
    }else {
        int d=gcd(abs(result.up),result.down);
        result.up/=d;
        result.down/=d;
    }
    return result;
}
```

### 分数的四则运算

- 加减乘除

```c
Fraction add(Fraction f1,Fraction f2){
	Fraction result;
    result.up=f1.up*f2.down+f2.up*f1.down;//分数和的分子
    result.down=f1.down*f2,down;//分数和的分母
    return reduction(result);//化简    
}
Fraction minu(Fraction f1,Fraction f2);
Fraction multi(Fraction f1,Fraction f2);
Fraction divide(Fraction f1,Fraction f2);   
```

### 分数的输出

```c
void showResult(Fraction r){    //输出分数r
    r=reduction(r);
    if(r.down==1) printf("%lld",r.up);  //整数
    else if(abs(r.up)>r.down) {   //假分数
        printf("%d %d/%d",\
               r.up/r.down,abs(r.up)%r.down,r.down); 
    }else printf("%d/%d",r.up,r.down);   //真分数
    
}
```

- 💡分数的乘法和除法过程中可能使分子或分母超过int，一般用long long

## 素数

### 素数的判断

```c
bool isPrime(int n){
    if(n<=1) return false; //特判
    int sqr=(int)sqrt(1.0*n); //根号n, math.h
    for(int i=2;i<sqr;i++){ //用i*i<n容易溢出
        if(n%i==0) return false;
    }return true;
}
```

### 素数表

- 筛法，通过bool实现

```c
int prime[maxn];
bool isPrime[maxn]={0};
int findPrime(int n){
    int j=0;
    for(int i =2;i<maxn;i++){
        if(!isPrime[i]){
            prime[j++]=i;  //第j个素数是i
            for(int k=i+i;k<maxn;k+=i){
                isPrime[k]=1; //标识i的倍数
            }
        }if(j==n) break;
    }return 0;
```

## 质因子分解

- 定义结构体factor，用来存放质因子及其个数

```c
struct factor{
    int x,cnt; //x为质因子，cnt为其个数    
}fac[10];
```

- fac[ ]数组存放n的所有质因子，int范围只需要fac[10]就够了

## 大整数运算

### 大整数存储

- 没有考虑负数

```c
struct bign{  //bignumber
    int d[1000];
    int len;
    bign(){
        memset(d,0,sizeof(d));  //初始化
        len = 0;
    }
}
```

- 输入字符串时，先用字符串读入，再把字符串另存为bign结构体
- char数组读入时，整数的高位存储在低位，所以倒着赋给d[ ]数组

```c
bign change(char str[]){//把整数转化为bign
    bign a;
    a.len = strlen(str);
    for(int i=0;i<a.len;i++){
        a.d[i]=str[a.len-i-1]-'0';//逆着赋值
    }
    return a;
}
```

- 比较大小

```c
int compare(bign a,bign b){
    if(a.len>b.len) return 1; //a大
    else if(a.len<b.len) return -1; //a小
    else{
        for(int i=a.len-1;i--){
            if(a.d[i]>b.d[i]) return 1;
            else if(a.d[i]<b.d[i]) return -1;
        }return 0; //相等
    }
}
```

### 高精度四则运算

- 存在负号另外处理

```c
bign add(bign a,bign b){  //两正数相加
    bign c;
    int carry=0; //进位
    for(int i=0;i<a.len||i<b.len;i++){
        int temp =a.d[i]+a.d[i]+carry;
        c.d[c.len++]=temp%10;  //注意这里是c.len
        carry=temp/10;
    }
    if(carry!=0){
        c.d[c.len++]=carry;
    }
    return c;
}
```

```c
bign sub(bign a,bign b){  //大数减小数，否则交换
    bign c;
    for(int i=0;i<a.len||i<b.len;i++){
        if(a.d[i]<b.d[i]){
            a.d[i+1]--;
            a.d[i]+=10;
        }c.d[c.len++]=a.d[i]-b.d[i];
    }
    while(c.d[c.len-1]==0&&c.len!=1){
        c.len--;//保证结果至少有一位数
    }
}
```

```c
bign multi(bign a,int b){ //高精度乘低精度
    bign c;
    int carry;
    for(int i=0;i<len.a;i++){
        int temp=a.d[i]*b+carry;
        c.d[c.len++]= temp%10;
        carry=temp/10;
    }
    while(carry!=0){
        c.d[c.len++]=carry%10;
        carry/=10;
    }
    return c;
}
```

```c
bign devide(bign a,int b,int& r){ //使r值可以传出，初值为0
    bign c;
    c.len=a.len;
    for(int i=a.len-1;i>=0;i--){
        r=r*10+a.d[i];
        c.d[i]=r/b;
        r=r%b;
    }while(c.d[c.len]==0&&c.len!=1){
        c.len--;
    }return c;
}
```

## 拓展欧几里得算法

- 👇都是整数解
- 求解 ax+by=gcd(a,b)
- 求解ax+by=c，c是gcd的倍数才有解
- 同余式ax≡c(mod m)的求解
- 逆元的求解
- 计算(b/a)%m

唔，这个看书吧

迷迷糊糊

## 组合数

- n的阶乘的质因子p的个数
- 组合数的计算

好麻烦啊，，看书吧，后面跳过了几种方法，没看完。逐渐失去兴趣

**over**

