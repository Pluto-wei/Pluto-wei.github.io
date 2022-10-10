---
title: C++标准模板库STL介绍
tags: C++
categories: 算法笔记
abbrlink: 36477
date: 2020-02-16 23:58:50
about:
---



大概是两天看完的，这一部分主要还是以后需要查阅，只是知道了大概的用法吧。想学数据结构了，应该接下来就是了！淦！！

<!-- more -->

《想见你》大结局啦，哭死了，这部剧挺好的，撒花❀
详情见下一篇文章qaq😢

# C++标准模板库（STL）介绍

💡写在前面：

- 除了vector和string外的STL容器都不支持*(it+i)的访问方式，只能it=name.begin( )+i    it++;    *it  

## vector的常见用法

- 向量，可变长数组

```c++
#include<vector>
using namespace std;
```

- 定义

```c
vector<typename> name; //typename可以是任意类型int，double,char
```

```c
vector<int> name;
vector<node> name; //node是结构体类型
vector<vector<int> > name;  //>>之间要加空格，否则视为移位操作
vector<typename> Arrayname[arrySize];//一维可伸长，上面的是二维
```

- 元素访问（下标访问和迭代器iterator访问）

  迭代器类似指针,通过*it访问vector里元素

```c
vector<typename> vi;
vi[index];//下标访问

for(int i=i;i<=5;i++){
    vi.push_back(i);
}
for(vector<int>::iterator it=vi.begin();i!=vi.end();i++){
    printf("%d",*it);
}
for(int i=0;i<vi.size();i++){
    printf("%d",v[i]);
}


vector<typename>::iterator it = vi.begin();//取首地址vi[0]
vi.push_back(i);//在末尾赋值
vi.end();//取尾地址的下一个地址
printf("%d",*(it+i));//输出vi[i];
```

- 常用函数

  用的时候都是name.👇

```c
push_back(x);//在vector后面添加元素x
pop_back();//删除vector尾元素
size();//返回vector中元素的个数
clear();//清空所有元素
insert(it,x);//vi.insert(vi.begin()+2,-1)在vi[2]处插入-1
erase();//vi.erase(vi.begin()+3)删除vi[3]
        //vi.erase(vi.begin()+1,vi.begin()+4);删除vi[1]-vi[3]
```

- 用途：储存数据like数组，用邻接表储存图

## set的常见用法详解

- 集合，内部自动有序且不含重复元素的容器

```c++
#include <set>
using namespace std;
```

- 定义（其实和前面的一样）

```c++
set<typename> name;
set<int> name;
set<double> name;
set<char> name;
set<node> name;
set<typename> Arrayname[arraySize];
```

- 访问，只能用迭代器iterator访问，且只能枚举

```c++
set<typename>::iterator it;
```

```c
set<int> st;
st.insert(3);
st.insert(5);
st.insert(2);
st.insert(3);
for(set<int>::iterator it=st.begin();i!=st.end();it++){
    printf("%d",*it);
}
输出为2 3 5（自动递增，删除重复元素）

```

- 函数 st.👇

```c++
insert(x);//将x插入set容器，自动增序，去重
find(value);//返回set中对应值为value的迭代器，it=find(2)
erase();erase(it);erase(value);erase(first,last);//迭代器
//st.erase(st.find(200));  st.erase(400);
//st.erase(it,st.end)
size();//元素个数
clear();//清空

```

- 用途：自动去重并升序

  unordered_set可以只去重不排序

  multiset可以处理不唯一的情况

## string的常见用法详解

```c++
#include<string>
using namespace std;

```

- 定义

```c
string str;
string str="abcd";

```

- 访问

```c++
str[i];
cin>>str;
count<<str;//读入读出整个字符串只能用cin count，除非转换👇
printf("%s\n",str.c_str());//用c_str()将string型str变成字符数组

```

```c++
string::iterator it;
for(string::iterator it=str.begin();it!=str.end();it++){
    printf("%c",*it);
}

```

- 常见函数

```c
str3=str1+str2;//将str1和str2拼接，赋值给str3
str1+=str2;//将str2直接拼接到str1上

```

```c
if(str1<str2) ...
== != < <= > >=  比较规则是字典序

```

```c
length()/size()
printf("%d %d",str.length(),str.size());

```

```c
insert()
insert(pos,string);//在pos号位置插入sring
insert(it,it2,it3);//在it处插入[it2,it3)
str.insert(3,str2);
str.insert(str.begin()+3,str2.begin(),str2.end());

```

```c++
erase(it);
erase(first,last);
erase(pos,length);//需要删除的起始位置+删除个数
str.erase(str.begin()+4);
str.erase(str.begin()+2,str.end()-1);

```

```c
clear();
str.clear();

```

```c
substr(pos,len);//返回从pos号位开始，长度为len的字串
cout<<str.substr(14,4)<<endl;

```

```c
string::npos==-1/4294967295;作为函数失配时的返回值

```

```c
find();
str.find(str2);//str2是子串时返回第一次出现的位置，否则返回👆
str.find(str2,pos);//从str的第pos号为开始匹配，返回值与上相同

```

```c
replace(pos,len,str2);//把str从pos号位长度为len的字串替换为str2
replace(it1,it2,str2);//str[it1,it2)替换为str2

```

- 将数转化成科学计数法并比较的题A1060（看书(x)）

## map的常用用法详解

- 映射，可以建立任何基本类型之间的映射

```c++
#include<map>
using namespace std;

```

- 定义

```c
map<typename1,typename2> mp;//键，值
map<string,int> mp;//如果时字符串到整型只能是string，不能是char

```

- 访问

  会按键从小到大自动排序（内部红黑树实现同set）

```c
map<string,int> mp;
mp['m']=20;
mp['c']=30;
mp['a']=40;
printf("%d",mp['c']);
mp<typename1,typename2>::iterator it;//迭代器
for(map<char,int>::iterator it=mp.begin();it!=mp.end();it++){
    printf("%c %d\n",it->first,it->second);
}
it->first是当前映射的键，it->second是当前映射的值

```

- 函数 mp.👇

```c++
find(key);//返回键为key的映射的迭代器 it=mp.find('b');
erase(); mp.erase(it); mp.erase(key); mp.erase(first,last);
size();//映射的对数
clear();

```

- 用途：需要建立字符与整数之间的映射，判断大整数或者其他类型数据是否存在，字符串和字符串的映射

- 一般一一对应，mutimap一个键可以对应多个值

  unordered_map以散列代替map内部红黑树实现，不按key排序，更快

## queue的常见用法详解

- 队列，先进先出的容器

```c++
#include<queue>
using namespace std;

```

- 定义

```c++
queue <typename> name;

```

- 元素访问

```c
queue<int> q;
q.push(i);//push(i)将i压入队尾
printf("%d %d\n",q.front(),q.back());
//只能通过front()来访问队首元素，back()访问对尾元素

```

- 函数 q.👇

```c
push(x);//x进入队列
front();back();//分别获得对首元素和队尾元素
pop();//令队首元素出列
empty();//检测队列是否为空，返回true则空，false则非空
size();//返回queue内元素的个数

```

- 用途：需要实现广度优先搜素

- 💡使用front和pop函数前必须用empty函数判断队列是否为空，否则可能出现错误

- deque，双端队列，首尾皆可插入

  priority_queue，优先队列，使用堆实现，默认将最大元素至置于对首

## priority_queue的常见用法详解

- 优先队列，队首元素为当前队列中优先级最高的（底层的数据结构堆heap会随时调整结构）

```c++
#inlcude<queue>
using namespace std;

```

- 定义

```c++
priority_queue<typename> name;

```

- 访问，没有front和back，只有top访问队首元素（堆顶元素）

```c++
priority_queue<int> q;
q.push(3);
q.push(4);
q.push(1);
printf("%d",q.top());

```

- 函数 q.👇

```c++
push(x);//令x入列
top();//获得队首元素
pop();//令首队元素出队
empty();//检测队列是否为空，true/false
size();//返回元素个数

```

- 元素优先级的设置
- 基本数据类型（int,double,char）, 默认数字大的优先级更高（字典序）

```c++
priority_queue<int> q;//和下面一个相同
priority_queue<int,vector<int>,less<int> > q;//数字大的优先级大
priority_queue<int,vector<int>,greater<int> > q;//数字小的
priority_queue<double,vector<double>,less<double> > q;
priority_queue<char,vector<char>,less<char> > q;

```

- 结构体

```c++
struct fruit{
    string name;
    int price;
};//现在希望水果价格高的优先级高，需要用到重载小于号<
struct fruit{
    string name;
    int price;
    friend bool operator < (fruit f1,fruit f2){  //>会出错
        return f1.price < f2.price;
    }//重载后小于号还是小于号
}
priority_queue<fruit> q;//内部就是价格高的优先级高
//将return中的<改成>即实现价格低的优先级高

//如果结构体内的数据较为庞大，出现字符串/数组，建议使用引用
friend bool operator < (const fruit &f1,const fruit &f2){
    return f1.price > f2.price;
}

```

- 也可以重载在结构体外面

```c++
struct cmp{
    bool operator()(fruit f1,fruit f2){
        return f1.price > f2.price;
    }//这里返回true的优先级低一些
/*  bool operator()(const fruit &f1,const fruit &f2){
        return f1.price > f2.price;
    }  */
}
prioity_queue<fruit,vector<fruit>,cmp> q;

```

- 常见用途：可以解决一些贪心问题，对Dijkstra算法进行优化
- 💡使用top前必须用empty判断队列是否为空

## stack的常见用法详解

- 栈，后进先出的容器

```c++
#include<stack>
using namespace std;
stack<typename> name;

```

- 访问，只能top

```c++
st.push(i);
printf("%d",st.top());

```

- 函数 st.👇

```c++
push(x);
top();//获得栈顶元素
pop();//弹出栈顶元素
empty();//检查是否为空，返回true/false
size();//返回元素个数

```

- 常见用途：实现一些递归，防止程序对栈内存的限制而导致程序出错

## pair的常见用法详解

- 两个元素绑在一起作为一个合成元素，可以看作内部有两个元素的结构体
- 且两个元素的类型可以指定

```c++
struct pair{
    typeName1 first;
    typeName2 second;
};

```

```c++
#include<utility>  //或者#include<map>,里面包含utility
using namespace std;

```

```c++
pair<typeName1,typeName2> name;
pair<string,int> p;
pair<string,int> p("haha",5);

```

- 元素访问，pair中只有两个元素，first和second

```c++
p.first = "haha";
p.second = 5;
cout<<p.first<<" "<<p.second<<endl;
p = make_pair("xixi",55);
cout<<p.first<<" "<<p.second<<endl;
p=pair<string,int>("heihei",555);
cout<<p.first<<" "<<p.second<<endl;

```

- 函数，比较操作数   ==      !=      <     <=     >    >=  

  先以first大小作为标准，再比较second

- 用途：代替二元结构体机器构造函数

  作为map的键值对进行插入

```c++
map<string,int> mp;
mp.insert(make_pair("heihei",5));
mp.insert(pair<string,int>("haha",10));

```

## algorithm头文件下的常用函数

```c++
#include<algorithm>
using namespace std;

```

### max,min,abs

```c++
max(x,y);max(x,max(y,z));//返回最大值
min(x,y);
abs(x);//x必须是整数，浮点型用math头文件下的fabs

```

### swap

```c++
swap(x,y);//用来交换x和y的值

```

### reverse

- 可以将数组指针在[it,it2)之间的元素或容器的迭代器在[it,it2)的元素进行反转

```c++
reverse(it,it2);

```

### next_permutation

- 给出一个序列在全排序中的下一个序列
- 已到达全排序最后一个则返回false

```c++
int a[10]={1,2,3};
do{
    printf("%d%d%d\n",a[0],a[1],a[2]);
}while(next_permutation(a,a+3));

```

### fill

- 可以把数组或容器中的某一段区间赋为某个相同的值
- 和memset不同，这里的赋值可以赋任意值

```c++
int a[5]={1,2,3,4,5};
fill(a,a+5,233);

```

### sort()

- sort函数的使用

```c++
#include <algorithm>
using namespace std;
sort (首元素地址,尾元素地址的下一个地址,比较函数(非必填));
//第二项-排序几个数就是首元素地址加几

```

- 第三个可选参数就是compare函数（cmp），用来实现排序规则

- 💡注意！！这个cmp是函数！返回bool类型，要放在main外面！！

- ①基本数据类型数组

  默认从小到大，想要从大到小:

```c++
bool cmp(int a,int b){
	return a >b; //当a>b时把a放到b前面
}
sort(a,a+4,cmp);

```

- ②结构体数组的排序

```c++
struct node{
	int x,y;
}ssd[10];
//按照x从大到小(一级排序)
bool cmp(node a,node b){
    return a.x>b.x; 
}
//x相等时按y排序(二级排序)
bool cmp(node a,node b){
    if(a.x != b.x) return a.x > b.x;
    else return a.x < a.y;
}
sort(ssd,ssd+3,cmp);//排序

```

- ③容器的排序

  只有vector，string，deque是可以用sort的

  像set，map这种容器都是用红黑树实现的，元素本身有序的

- vector

```c++
bool cmp(int a,int b){
    return a>b;
}
int main(){
    vector<int> vi;
    vi.push_back(3);
    vi.push_back(1);
    vi.push_back(2);
    sort(vi.begin(),vi.end(),cmp);
    for(int i=0;i<3;i++){
        printf("%d ",vi[i]);
    }
}

```

- string，默认字典序从小到大

```c++
//如果要字符串长度从小到大
bool cmp(string str1,string str2){
    return str1.length() < str2.lengh();
}

```

### lower_bound 和 upper_bound

- lower_bound(first,last,val)返回范围内第一个值**大于等于**val的元素的位置（指针/迭代器） 
- upper_bound(first,lasst,val)返回第一个值**大于**val元素的位置
- 如果找不到返回的是该元素应当在的位置

```c++
int a[10]={1,2,2,3,3,3,5,5,5,5};
printf("%d,%d\n",lower_bound(a,a+10,3)-a, /
       upper_bound(a,a+10,3)-a);

```

















k