---
title: 算法入门！
tags: [C语言,算法]
abbrlink: 65294
date: 2020-02-12 13:03:48
categories: 算法笔记
---

算法终于入门了！！
快乐！！！
从2月6号算起来刚好一个星期
这里是《算法笔记》3,4 章
<!-- more -->
2333还行吧，最近看剧《想见你》有点上头
还有10天就要开学了呜呜呜，学的东西好少😢淦！

下面👇进入正题



# 入门篇1--入门模拟

* 简单模拟
* 查找元素
* 图形输出
* 日期处理
* 进制转换
* 字符串处理

💡 以下是一些做题过程中的笔记
```c++
int step = 0;//计数器
int count = 0;//计数，num好奇怪
int ans = 0;
int temp;//临时存放
const int maxn = 100010;//?? 210??
int a[100]={0};//这是全部为0，但{1}=1,0,0,0,
int row,col;//行，列
int rank,score;//排名，分数
char id[15];//当int不够用的时候
bool flag = true;//标志
```

* 日期有点意思，

* 关于进制
```c
//不能直接读入读出二进制数
%d 十进制
%o 八进制
%x %X 十六进制 小写大写形式
%u 无符号十进制
```

```c++
#include <cstdio>
#include <cstring>
//可以直接用bool
```

```c
唔，scanf到底什么时候返回0什么时候返回EOF啊？？
反正黑框输入的时候必须ctrl+z手动结束
```

# 入门篇2--算法初步

💡 笔记中有些代码示例没有写明哪些是主函数里的，哪些不是，需自行区分

## 排序

### 排序

* 冒泡排序

* 选择排序

* 插入排序

  （插入用于排列多个结构体的时候就需要交换两个结构体变量，而不能直接交换他们的排名，因为实际位置不变的话，就无法寻找排名的上一位然后去比较，所以还是用sort函数吧）

  （而且插入排序的顺序记录好像就是数组下标，不能出现并列的情况）

### 排序题与sort函数的应用

* 对于涉及到排序的题目，建议直接使用c++中的sort函数，将精力放在题目逻辑本身

```c++
//sort函数的使用（详情见c++标准模板库STL）
#include <algorithm>
using namespace std;
sort (首元素地址,尾元素地址的下一个地址,比较函数(非必填));
```

* 排序题型常用的解题步骤
1. 相关结构体的定义
2. cmp函数的编写 
3. 排名的实现

💡 要判断两个字符串是否相等，不能直接==，要用strcmp，返回正数，0，负数
💡（有些东西不自己做还真不知道）

```c++
//cmp函数的编写
bool cmp(student a,student b){
    if(a.score != b.score) return a.score > b.score;
    else return strcmp(a.name,b.name)<0;//string.h
}
```
```c++
//把排名记录下来
stu[0].r=1;
for(int i=1;i<n;i++){
    if(stu[i].score == stu[i-1].score){
        stu[i].r = stu[i-1].r;
    }else {
        stu[i].r = i+1;
    }
}
```
```c
//要输出排名的时候，不在结构体里定义可以让代码变得简洁
int rank = 1;
for(int i=0;i<num;i++){
    if(i>0&&stu[i].score!=stu[i-1].score){
        rank=i+1;
    }//就可以printf了，否则rank就跟上一个一样
}
```

## 散列

* 散列(hash)是常用的算法思想之一
* 将元素通过一个函数转换为整数，使得该整数可以尽量唯一地代表这个元素，这个转换函数称为散列函数H
### 整数 key
```c++
//hashTable数组，记录正整数是否出现过
bool hashTable[maxn] = {false};
for(int i=0;i<n;i++){
    scanf("%d",&x);
    hashTable[x]=true; //x出现过
}//或者用int型记录次数
```

* key 元素转换后变成整数 H ( key )

```c
H(key)=key;//直接定址法中的恒等变换
H(key)=a*key+b;//直接定址法中的线性变换
H(key)=key%mod;//除留余数法，转换很大的数，mod取成表长TSize
```

* 有时会出现冲突的情况，可以直接用标准库模板库中的map

### 字符串 hash 初步

* 将字符串转化为唯一的整数
* 二十六进制，五十二进制转换为十进制，len不能太长

```c++
int hashFunc(char s[],int len){   //转换函数
    int id = 0;
    for (int i=0;i<len;i++){
        //id = id*26+(s[i]-'A');//26->10
        if(s[i]>='A'&&s[i]<='Z'){
            id =id*52+s[i]-'A';
        }else if(s[i]>='a'&&s[i]<='z'){
            id = id*52+(s[i]-'a')+26;
        }//52->10
    }
}
int hashTable[26*26*26+10]={0};//3位大写字母+日常加10
int main (){
    for(int i=0;i<n;i++){
        scanf("%s",s[i]);
        int id = hashFunc(s[i],3);
        hashTable[id]++;
    }
    for(int i=0;i<m;i++){
        scanf("%s",temp);
        int id = hashFunc(temp,3);
        printf("%d\n",hashTable[id]);
    }
}
```

## 递归

### 分治

* 分而治之，分解、解决、合并，是一种算法思想，可以用递归的手段实现
* 分治法分解出的子问题应当是相互独立没有交叉的
* 子问题个数为1称为减治，子问题个数大于1称为分治

### 递归

* 反复调用自身函数，把问题范围缩小，直到可以直接得到边界

```c++
//求Fibonacci数列第n项
int F(int n){
    if(n==0||n==1) return 1; //递归边界
    else return F(n-1)+F(n-2); //递归式   
}
```

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
* 暴力法--枚举所有情况判断是否合法
* 回溯法--在到达递归边界前的某层，由于不需要再往前递归，直接返回上一层

```c++
//n皇后问题，对每种可能的情况暴力法
bool flag = true;
for(int i=1;i<=n;i++){
    for(int j=i+1;j<=n;j++){
        if(abs(i-j)==abs(P[i]-P[j])){
            flag=false;
            break;
        }
    }
}if(flag) num++;
```

```c++
//回溯法就是把该判断每加一个数就执行一次，实时检验
//还是自己写的好理解👇
#include <cstdio>
#include <math.h>

int P[10];
int n;//n是总数
int m,x;//m是要填的数，x是填到的位置
int hash[10]={false};
int count=0;//符合条件的个数

void gP(int x){
    if(x==n+1){
        count ++;      
        return;//该函数结束，不是break哦
    }
    for(int m=1;m<=n;m++){ 
    //记住是把m填到x位上，对应就是(m,x)坐标
        if(hash[m]==false){
            bool flag = true;
            for(int i=1;i<=x-1;i++){
                if(abs(i-x)==abs(P[i]-m)){
                    flag=false;
                    break;
                }
            }if (flag){
                P[x]=m;
                hash[m]=true;
                gP(x+1);
                hash[m]=false;
            }
//else m就不能填在x位，那么进行下一个循环m+1，看是否可以
        }
    }
}
```

## 贪心

* 贪心法是求解一类最优化问题的方法
* 考虑当前状态下的局部最优，来使全局最优
* 证明一般采用反证法和数学归纳法
* 有简单贪心问题和区间贪心，即区间不相交问题和区间选点问题
* 💡注意这个不能左端点从小到大，只能**右端点从小到大**，**左端点从大到小**！！不需要代码额外减去更大包含别人了的区间，会自己很好排除掉

```c++
#include <cstdio>
#include <algorithm>
using namespace std;
const int maxn =110;
struct Inteval{         //interval是区间
    int x,y;//开区间左右端点
}I[maxn];

bool cmp(Inteval a,Inteval b){
    if(a.y=b.y) return a.x>b.x;
    else return a.y<b.y;
}

int main(){
    int n;
    while(scanf("%d",&n),n!=0){
        for(int i=0;i<n;i++){
            scanf("%d%d",&I[i].x,&I[i].y);
        }
    }sort(I,(I+n),cmp);
    int step=1,Y=I[0].y;//计数,记到的位置，右边的坐标
    for(int i=1;i<n;i++){
        if(I[i].x>Y){
            Y=I[i].y;
            step ++;
        }
    }printf("%d",step);
    return 0;   
}
```

## 二分

### 二分查找

* O ( $logn$ )

```c++
#include <stdio.h>
//A[]为严格递增序列，left为二分下界，right为二分上界，x为欲查询的数，二分区间为闭区间，传入的初值为[0,n-1]
int binarySearch(int A[],int left,int right,int x){
    int mid;
    while(left <= right){
        mid = (left + right)/2;
        if(A[mid]==x) return mid;
        if(A[mid]>x) right=mid-1;
        else left=mid+1;
    }return -1;//查找失败，返回-1
}
//二分上届如果超过int数据类型的一半，查询元素靠后的时候right+left就有可能溢出，一般使用👇代替
mid=left+(right-left)/2;
```
* “寻找有序序列第一个满足某条件的元素的位置”问题的固定模板

```c++
int solve(int left,int right){
    int mid;
    while(left<right){
        mid=(left+right)/2;
        if(条件成立){
            right=mid;
        }else{
            left=mid+1;
        }
    }
}
```

### 二分法拓展

* 求近似值，方程的近似根

```c++
const double eps = 1e-5;
double f(double x){
    return ...;
}
double solve(double L,double R){
    double left = L,right = R;
    while(right-left > eps){
        mid = (rigth+left)/2;
        if(f(mid)>0){  //递增
            right = mid;
        }else{
            left = mid;
        }
    }return mid;
}
```

* 关于书上留的一个思考题，👇是别人的一些解答

  <https://blog.csdn.net/a845717607/article/details/79079862>

  <https://blog.csdn.net/liuerin/article/details/98961797>

![](https://upload-images.jianshu.io/upload_images/20644861-7f4fc03acde6231a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 最后一排表达式应该是等号，下面是关于圆心在外部的理解，也就是说，有外接圆存在的组合只有一种可能，R没有别的可能性，变大变小都不可能构成多边形（想想也知道R变小除最大边以外都不变的话，最大边必须要变小）

![](https://img-blog.csdn.net/20180130102605806?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvYTg0NTcxNzYwNw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

* 最后用二分法求解即可

### 快速幂

* 要求$a^b$%m，循环部分为ans = ans * a % m，注意**每一次都要%m**，**a=a%m**，但是可能还是很大，当b<$10^{18}$时，复杂度太高
* m要是等于1直接就是0了
* 二分指数b，将时间复杂度变为logn，递归写法👇

```c++
typedef long long LL;
LL binaryPow(LL a,LL b,LL m){
    if(b==0) return 0;
    if(b%2==1) return a*binaryPow(a,b-1,m)%m;
    else{
        LL mul = binary(a,b/2,m);
        return mul*mul%m; 
        //要是两个binary(a,b/2,m)相乘，复杂度又变成b了
    }
}//(b%2==1)等价于(b&1) 位与操作
```

* 迭代写法👇（二进制，$a^b$可以写成$a^{2^k}$,...,$a^8$,$a^4$,$a^2$,$a^1中若干项的乘积）

```c++
LL binaryPow(LL a,LL b,LL m){
    LL ans = 1;
    while(b>0){
        if(b&1) ans = ans*a%m;
        a=a*a%m;
        b >>= 1; //将b的二进制右移一位，即b=b/2
    }return ans;
}
```

## two pointers

### two pointers and 序列合并

* 利用有序序列的枚举特性降低复杂度--编程计较
* 最原始就是指的下面第一个问题，广义就是利用问题本身与序列的特性，使用下标 i,j 对序列进行扫描

```c
//在递增序列中找和为定值的两个数
while(i<j){
    if(a[i]+a[j]==m){
        printf("%d %d\n",a[i],a[j]);
        i++;j--;
    }else if(a[i]+a[j]<m){
		i++;        
    }else j--;
}
```

```c
//序列合并问题,将递增序列A B合并到C里
int merge(int A[],int B[],int C[],int n,int m){
    int i=0,j=0,index=0;
    while(i<n&&j<m){
        if(A[i]<=B[j]){
            C[index++]=A[i++];//这里就不要啰嗦了好不好
        }else{
            C[index++]=B[j++];
        }
    }
    while(i<n) C[index++]=A[i++];
    while(j<m) C[index++]=B[i++];
    return index;//为什么要返回序列的长度？？
}
```

### 归并排序

* 是一种基于归并思想的一种排序方法
* 最基本的2-路归并排序

![归并排序](https://upload-images.jianshu.io/upload_images/20644861-40a623c5577ca22b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 递归实现

```c
const int maxn = 100;
void mergeSort(int A[],int left,int right){
    if(left<right){
        int mid = (left+right)/2;
        mergeSort(A,left,mid);
        mergeSort(A,mid+1,right);
        //注意1和2的时候mid是1，这两个都是left=right
        //也就是排序(1,1)和(2,2)
        merge(A,left,mid,mid+1,right);
        //和two pointers类似
    }
}
```

* 非递归实现

```c
void mergeSort(int A[]){
    for(int step=2;step/2<=n;step*2){
        for(int i=1;i<=n;i+=step){
            int mid =i+step/2-1;
            if(mid +1<=n){//如果右子区间存在
                merge(A,i,mid,mid+1,min(i+step-1,n));
                //注意这里的min去更小的一个
            }
        }//每循环排列step个，但step可能>n,例如step16，n12
    }
}//可以说这种方法要考虑很多了
```

### 快速排序

* quickSort 函数

* Partition 函数，👇，返回相遇的下标，即原先最左边的函数

* randPartition函数，在上面的函数基础上增加了随机数

* 选取**最左边的元素**，排成：比他小的在左边，比他大的在右边的顺序

  对他左边和右边通过递归采取同样的操作

* 当序列中的元素排列随机是效率较高，元素接近时会达到最坏时间复杂度（因为主元没有将区间划分成两个长度接近的区间）

* **随机主元**可以保证任意数据的**期望**时间复杂度是nlogn

```c
//产生随机数据
#include<stdio.h>
#include<stdlib.h>
#include<time.h>
int main(){
    srand((unsigned)time(NULL));
    //在main函数的开头加，生成随机数的种子
    for(int i=0;i<10;i++){
        printf("%d",rand());//使用随机数
    }return 0;
}
```

```c
//rand()范围[0,RAND_MAX]这是stdlib里的一个常数
//给定范围[a,b]
rand()%(b-a+1)+a;
//更大范围的随机数b-a>max
(int)((double)rand()/32767*(b-a+1)+a);
```

## 其他高效技巧和算法

### 打表

* 将所有可能用到的结果事先计算出来，用的时候直接查表获得
* 适用于：需要大量查询某数据；没有想到好的算法超时；从大量数据中找规律

### 活用递推

* 过程中可能存在的递推关系
* 例如某值可以通过左右两侧的结果得到

### 随机选择算法

* 从无序数组中找到第K大的数
* 与随机快速排序算法类似

```c
//从A[left,right]中返回第K大的数
int randSelect[int A[],int left,int right,int K]{
    if(left==right) return A[left];
    int p=randPartition[A,left,right];
    //划分后主元的位置p。该函数详情见快速排序👆
    //注意该函数对数组的修改就是对原数组的修改
    int M = p-left+1;//A[p]是原A序列中的第M大
    
    if(K==M) return A[p];
    if(K<M) return randSelect[A,left,p-1,K];
    else return randSelect[A,p+1,right,K-M];
}
```

* 完整的代码见4.7.3

  



**OVER !**