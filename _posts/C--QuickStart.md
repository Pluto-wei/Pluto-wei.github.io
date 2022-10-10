---
title: C语言 快速入门！！
tags: C语言
abbrlink: 11944
date: 2020-02-05 12:25:10
categories: 算法笔记
---

233333
我终于快速入门了！！
<!-- more -->
2月2号开始看的《算法笔记》
今天终于把快速入门看完了==
4天嗷~

突然想放一张散散~生日快乐
![@7.png](https://upload-images.jianshu.io/upload_images/20644861-6f36adacb730b7a1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

下面进入正题~

# 基本数据类型

## 变量类型：

* 整型：short， int ，long long

  绝对值在**$10^9$**范围内（32位）都可以定义为int

  $10^{10}$-$10^{18}$就得用long long（64位）

  （若赋大于int最大($2^{31}-1$)的值，则需要在初值后面加LL，才能编译成功）

* 浮点型：float，double

  精度 float 6-7位，double15-16位

  记住：遇到浮点用double

* 字符型：

  标准ASCII范围是0-127，包含控制字符（转义字符\n\t\0）和可显示字符

  记住：**小写字母比大写字母ASCII码大32，**

  '字符'%c 	"字符串"%s

  ```c
  char c1 = 'z',c2 = 'j',c3 = 117;
  printf("%c%c%c",c1,c2,c3);
  //字符常量（单个字符）用单引号标注
  //输出为 zju
  ```

* 布尔值：

  c语言中要**stdbool.h**

  true（非零）false（零）

## 强制类型转换

（新类型名）变量名

```c
printf("%.f",(double)a/(double)b);
```

## 定义常量

* 符号常量-宏定义

  define是原封不动直接替换，记得加（）

  ```c
  #define 标识符 常量/任何语句或片段
  #define pi 3.14
  ```

* const常量

  ```c
  const 数据类型 变量名 = 常量；
  const double pi = 3.14；
  ```

## 运算符

* 算术运算符 

  / 取商，向下取整，舍去小数  %取余数

  i++先用再加，++i先加再用

* 关系运算符

  < > <= >= == !=

* 逻辑运算符

  &&与    ||或    ！非

* 条件运算符

  唯一的三目运算符

  ```c
  A ? B : C ; //A真则B，A假则C
  ```

* 位运算符

  ```c
  const int INF = (1 << 30)-1; //无穷大，上限，
  const int INF = 0x3fffffff;//避免两个数相加超过int最大值
  ```

  按二进制进行:  左移<<  右移>>  位于&  位或|  位异或^  位取反~

# 顺序结构

## 赋值表达式

* 注意 +=   -=   /=    *=   %=  的运用

## scanf和printf输入输出

```c
scanf("格式控制"，变量地址)；
scanf("%d",&n);  //int
scanf("%lld",&n); //long long
scanf("%f",&fl); //float
scanf("%lf",&db); //double
scanf("%c",&c);  //char
scanf("%s",str); //字符串char*，char str[]
```

* 除char数组整个输入 不加&，其他变量类型都要加&
* 除%c，scanf对其他格式符的输入（%d，%s）是以空白符为结束的
* %c是可以读入空格跟换行的

```c
printf("格式控制"，变量名称)；
printf("%d",n);  //int
printf("%lld",n); //long long
printf("%f",fl); //float
printf("%f",db); //double
printf("%c",c);  //char
printf("%s",str); //字符串char*，char str[]
```

* 唯一不同：double输出格式%f ，输入%lf

```c
printf("%%");
printf("\\");
printf("\t \n");
```

```c
printf("%md",a);//%md不足m位的int以m位进行右对齐输出，高位空格补齐
printf("%-md",a);//左对齐
printf("%0md",a); //高位补0而不是补空格
printf("%.mf",a); //保留m位小数
printf("%n.mf",a); //保留m位小数,宽度占n位
```

## getchar与putchar输入输出

* 输入输出单个字符，可以识别存储换行符\n

```c
char c1,c2;
c1 = getchar();
getchar();
c2 = getchar();
putchar(c1);
putchar(c2);
```

## typedef

* 给复杂的数据类型起别名

```c
typedef long long LL;
LL a = 123456789012345,b = 34567890123456;//直接使用LL
```

## 常用math函数

```c
#include <math.h>
```

```c
fabs(double x); //对double型变量取绝对值
floor(double x);//对double型变量向下取整，得到的值更小，无论正负
ceil(double x); //对double型变量向上取整
pow(double r,double p); //返回$r^p$
sqrt(double x);//返回算术平方根
log(double x);//取以e为底对数，任意底数要用换底公式
sin(double x),cos(double x),tan(double x);//参数要求弧度制
asin(double x),acos(double x),atan(double x);
round(double x);//四舍五入到个位，返回类型double
```

* 但是这些函数直接以%f输出会都很多零

  最好还是要控制位数%.0f   %.mf

  也可以 %d ，(int)db

* double x 只是说明这是一个double型变量，并不需要加上double

* pi精确定义为acos(-1.0)

# 选择结构

## if 语句

```c
if (条件A) {
    ...
} else if (条件B) {
    ...
} else {
    ...
}
```

* 技巧：if（n==0） 等价于if（!n），if（n!=0）等价于if（n）
* if语句的嵌套

## switch 语句

* 用于分支条件比较多的情况

```c
switch(表达式){
    case 常量表达式1:
        ...
        break;
    case 常量表达式2:
        ...
        break;
    case 常量表达式n:
        ...
        break; 
    default:
		...
}   //break结束当前switch，表达式等于常量表达式n就执行第n条
```

#  循环结构

## while 语句

```c
while(条件A){
    ...
}
```

## do while 语句

```c
do{
    ...
} while (条件A);
```

## for 语句

```c
for(表达式A;表达式B;表达式C){
    ...
} //先执行A，再判断B，每个循环后执行C
```

## break 和 continue 语句

* break直接退出以上三种循环，switch语句
* continue临时结束循环的当前轮回，进入下一轮回

# 数组

* 注意从a[0]开始

## 一维数组

```c
数据类型 数组名 [数组大小] = { , , };
数组名称[下标]; //访问
```

## 二维数组

```c
数据类型 数组名 [第一维大小][第二维大小] = { { , , },{ },      };
```

* 如果数组较大（$10^6$级别），需要将其定义在主函数之外
* 多维数组类似

## memset 函数

* 对数组中的每一个元素赋相同的值
* 需要头文件string.h
* 建议只赋0/-1，其他数字（会出错）使用fill函数
* 因为memset使用的是按字节赋值

```c
memset(数组名,值,sizeof(数组名));
```

## 字符数组



```c
char str[15] = "Good Story!"; //直接赋值仅限于初始化
char str[15] = {'G','o',...}; //记得长度要多一个存\0
```

## gets和puts 输入输出 

* **scanf 输入 printf 输出**（见上文）

* **getchar 输入 putchar 输出** （见上文）

  二维数组时 用 getchar ( ) 吸收掉每行末尾的换行符

* **gets 输入 puts 输出**

  gets 识别换行符\n作为输入结束，可以读入空格

  puts 输出后会紧跟一个换行

* puts 和 printf 通过识别 \0作为字符串的结尾

* 如果不是 scanf的%s 或gets输入（例如getchar），要在字符串末尾加\0

* 只有char型数组需要\0，int型数组不需要

## string.h 头文件

```c
strlen(字符数组);//得到第一个\0前的字符的个数
strcmp(字符数组1,字符数组2);//按字典序比较两个字符串大小
strcpy(字符数组1,字符数组2);//把字符数组2复制给字符数组1，包括\0
strcat(字符数组1,字符数组2);//把字符数组2接到字符数组1后面
```

* strcmp：

  从前往后比，a小于b，aaaa小于aab，

  字符数组1<字符数组2,则返回一个负整数；

  字符数组1==字符数组2,则返回0；

  字符数组1>字符数组2,则返回一个正整数；

## sscanf 与 sprintf

* 第一个s理解为string，均在stdio头文件下
* scanf 和 printf 只是把下面的str 换成screen

```c
sscanf(str,"%d",&n);//把字符数组str中的内容以%d的格式写入n
sprintf(str,"%d",n);//把n以%d的格式写到str字符数组中
```

```c
char str[100]="2048:3.14,hello";
sscanf (str,"%d:%lf,%s",&n,&db,&str2) ;//从左边读到右边

int n=32;
double db = 3.1415;
char str[100],str2[100]="good";
sprintf(str,"%d:%.2f,str",n,db,str2); //从右边读到左边
```

* sscanf 还支持 [正则表达式](https://www.runoob.com/regexp/regexp-tutorial.html)（匹配）

# 函数

```c
返回类型 函数名称(参数类型 参数){
    函数主体
}
```

* 注意全局变量和局部变量，形参和实参
* 以**数组作为函数参数**时，对数组元素的修改就是对原数组的修改（与普通的局部变量不同）
* 但不可以返回数组
* 函数的嵌套调用，例如max三个数可以用到max两个数
* 函数的递归调用，自己调用自己，例如算n的阶乘

# 指针

* ❗ 不要给任何没有初始化的指针的赋值！
* ❗ 应该在给*p赋值前要给*p分配一个空间

```c
int *p1,*p2;
double *p；
char *p;
```

```c
int a,b;
int *p = &a,*p2;
p2 = &b; //取地址
*p = 233; //取址
```

* int *是指针变量的类型，p才是变量名
* 因此地址&a是赋给p而不是*p
* 指针变量支持自增自减操作
* a=&a[0]
* a+i = &a[i+1]
* 两个int型指针相加减，等价于之间相差了几个int
* 指针变量作为函数参数，只有在获取地址的情况下才能真正修改变量

```c
//?? scanf能赋值给字符数组，不能赋值给指针的问题
//scanf读入字符串一定要事先为它申请足够的空间
#include <stdlib.h>
char *str = (char*)malloc(15*sizeof(char));
```



## 引用

* c++语法，产生变量的别名
* &加在，会对原变量进行修改
* 就是说x是对原来a取的一个别名，改变x就是改变a，当然这里的x用a也可以

```c
void change(int &x){
    ...
}
change(a);
```



# 结构体的使用

## 结构体的定义

```c
struct Name{
    //一些基本的数据结构或者自定义的数据类型
}
```

* 结构体能定义除了自己本身的任何数据类型
* 不能定义自身，但可以定义自身类型的指针变量

```c
struct node{
    node n; //不能定义node型变量
    node* next; //可以定义node*型指针变量
}
```

## 访问结构体内的元素

```c
struct studentInfo{
	int id;
    char name[20];
    studentInfo* next;
}stu,*p;
//访问变量：stu.id stu.name stu.next
//访问指针变量p中的元素：(*p).id  p->id p->name p->next

```

## 结构体的初始化

* 构造函数：用以初始化
* 结构体内有默认构造函数，函数名和结构体名相同
* 只要参数个数和类型不完全相同，就可以定义任意多个构造函数，适应不同场合
* 好处：在结构体元素交多时显得代码精炼，不需要临时变量就可以初始化一个结构体

```c
struct studentInfo{
    int id;
    chat gender;   
    //用以不初始化就定义结构体变量
    studentInfo(){}
    //只初始化gender
    studentInfo(char _gender){
        gender = _gender
    }
    //同时初始化id和gender
    studentInfo(int _id,char _gender){
        id = _id;
        gender = _gender;
    }//可以简化为
    studentInfo(int _id,char _gender):id(_id),gender(_gender){}
}stu[10];
//初始化的时候就可以直接使用构造函数
stu[i]=studentInfo(2019,0);//类似这样子
```

# 补充

## cin 与 cout

* 添加头文件 #include <iostream> 和 using namespace std;才能使用
* 不需要指定输入输出格式，不需要取地址符&

```c++
cin >> n; //输入一个整数n
cin >> db; //double型浮点数
cin >> c;//char型数组
cin >> n >> db >> c >> str; //同时读入多个变量
char str[100];
cin.getline(str,100); //读入一整行到char型数组str[]中
string str;
getline(cin,str); //string容器输入
```

```c++
cout << n << " "<< db << " " << c << str; //输出时不会加空格
cout << n << "haha" << "\n" << db << endl; //endl也会换行
```

```c
//控制double的型的精度
#include <iomanip>
cout << setiosflags(ios::fixed) << setprecision(2) << 1.2345
```

* 只有在十分必要的时才使用cin和cout，例如 string

## 浮点数的比较

* 浮点数在经过运算后可能会变成3.14000001，3.1399999，就不会判为==
* 引入极小数eps来对误差进行修正
* 成立返回true，想要使用不等于!Equ(a,b),可直接对浮点数进行比较
* 加括号防止宏定义可能带来的错误

```c
const double eps = 1e-8;
const double pi = acos(-1.0)
#define Equ(a,b) ((fabs((a)-(b)))<(eps)) //等于运算符==
#define More(a,b) (((a)-(b))>(eps)) //大于运算符>
#define Less(a,b) (((a)-(b))<(-eps)) //小于运算符<
#define MoreEqu(a,b) (((a)-(b))>(-eps)) //大于等于运算符>=
#define LessEqu(a,b) (((a)-(b))<(eps)) //小于等于运算符<=
```

* 类似的还有开根号,asin,acos，需要eps保证变量在定义域内的问题
* 0.00还会变成-0.00，则要与-0.00进行比较，若比对成功则加上eps来修正

## 复杂度

* **时间复杂度**O(n)，基本运算次数

  一般的OJ系统，一秒能承受的运算次数$10^7$ ~ $10^8$

* **空间复杂度**，消耗的数据空间

  空间一般够用，常常以空间换时间

* **编码复杂度**，定性的概念

# 黑盒测试

## 单点测试

判断每组数据是否正确

## 多点测试

一次性运行所有数据

* while... EOF型，默认读到文件末尾，EOF=-1状态

  无法读取时，scanf会返回-1（关于scanf的返回值，还需要多测试）

  手动触发EOF：<Ctrl+Z> ^z 再按回车就可结束

```c
while(scanf("%d",&n) != EOF){
    ...
}
```

* while...break型

```c
while(scanf("%d%d"),&a,&b != EOF){
    if(a==0 && b==0) break;
    ...
}
while(scanf("%d%d",&a，&b),a||b){ //简洁版，ab有一个不为0就循环
    ...
}
```

* while(T--)型，给出测试数据的组数

```c
//三种输出类型
1.正常输出
2.每组数据输出出后额外加一个空格
3.最后一组数据后面没有空行
while(T--){
	...
	if(T > 0) printf("\n");
}
```

* 注意每次循环都要重置变量和数组
* 重置数组一般使用memset函数或fill函数
