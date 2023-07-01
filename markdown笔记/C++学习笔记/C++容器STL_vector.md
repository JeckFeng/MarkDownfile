# <mark>Vector 概述</mark>

1.vector是动态数组，从堆中申请空间；
2.随着元素的增加，vector的内部机制会自动扩充空间以容纳新的元素，然后将旧空间的数据搬到新空间，再释放原来的旧空间；
3.未雨绸缪，vector空间满了之后，会自动扩充原来大小的两倍空间，而不是一个；
4.单端array，只能在一段操作；

5.vector是模板而非类型，由vector生成的类型必须包含vector中的元素类型

# <mark>Vector 的方法概览</mark>

1.v.begin()
获取容器的起始迭代器(指向第0个元素)
2.v.end()
获取容器的结束迭代器(指向最后一个元素的下一个位置)
3.v.front()
vector的头元素
4.v.back()
vector的尾元素
5.rbegin()
6.rend()
7.insert()
8.push_back()

# <mark> Vector 的数据结构</mark>

1.Vector使用线性空间
2.Vector以两个迭代器Myfirst 和Mylast 分别指向配置得来的连续空间中已经被使用的范围，并以迭代器Myend指向整个线性空间的末端；
3.一个Vector的容量永远大于或等于其大小，当等于其大小时，说明Vector达到满载状态，当继续有新的元素加入时，则vector需要寻找一块新的，更大的内存空间，把旧空间中的数据搬到新的内存空间，并释放原来的旧空间。

# <mark> Vector常用API操作</mark>

## Vector的构造函数

第一种构造函数：

```C++
vector<T> v; //默认构造函数，vector是模板而非类型，由vector生成的类型必须包含vector中的元素类型
```

第二种构造函数：

```C++
vector(v.begin(),v.end());//将v[begin(),end()]区间中的元素拷贝给本身
```

第三种构造函数：

```C++
vector(n,elm); //构造函数将n个elm拷贝给本身
```

第四种构造函数：

```C++
vector(const vector &vec);//拷贝构造函数 //注意！两个vector的类型必须相同
```

example:

```C++
void test3(){
    vector<int> v1;  //默认构造函数
    vector<int> v2(5,100); //枚举类型的构造函数
    vector<int> v3(v2.begin(),v2.end()); //区间构造函数
    vector<int> v4(v3);//拷贝构造函数

    PrintVectorInt(v1);//PrintVectorInt是一个打印vector元素的函数
    PrintVectorInt(v2);
    PrintVectorInt(v3);
    PrintVectorInt(v4);
}
```

## 初始化vector

初始化vector即使用花括号括起来的0个或多个初始元素值被赋给vector对象：  

```C++
vector<char>  v5{a,b,c...};//v5包含了初始值个数的元素，每个元素被赋予相应的初始值
vector<char>  v5={a,b,c...};//等价于 v5{a,b,c...};


vector<string> article1 = ("a","an","the")；//错误 不能放置于圆括号内
```

**vector能容纳大部分类型的对象作为参数，但是因为引用不是对象，所以不存在包含引用的vector。**

## 构造迭代器

要访问顺序容器和关联容器中的元素，需要通过“迭代器（iterator）”进行。迭代器是一个变量，相当于容器和操纵容器的算法之间的中介。迭代器可以指向容器中的某个元素，通过迭代器就可以读写它指向的元素。从这一点上看，迭代器和指针类似。

构造迭代器的格式为：

```
容器类型<数据类型>::iterator 迭代器名称;
```

example:

```C++
vector<int>::iterator it;
```

## vector的遍历方式

首先需要定义一个迭代器指向vector的起始迭代器：

```C++
vector<int>::iterator it;//此时只是定义，但没有进行初始化
it = v.begin();
```

当然也可以在定义迭代器的时候就进行初始化：

```C++
vector<int>::iterator it = v.begin();
```

注意迭代器tierator也需要一个内存地址来存储它，迭代器虽然和指针很像，但它不是指针！

最后通过for循环和迭代器it来遍历vector：

```C++
vector<int> v;
v.push_back(1);
v.push_back(2);
v.push_back(3);
vector<int>::iterator it = v.begin();
    // ++iter 令iter指向容器中的下一个元素
    // --iter 令iter指向容器的上一个元素
for(;it!=v.end();it++){
   cout<<"it 所指向的数值 "<<*it<<" "<<endl;
   cout<<"it 所指向的数值的地址 "<<&(*it)<<" "<<endl;
   cout<<"存储迭代器it的地址 "<<&it<<" "<<endl;
  // 注意cout<<it<<endl;会报错
}
```

 上面这段代码的输出结果为：

![](E:\资料数据\markdown笔记\marktext图片保存位置\2023-06-29-11-21-34-image.png)

## vector的未雨绸缪机制

下面的代码片段用来测试vector是如何开辟空间的

```C++
void test(){
  vector<int> v2;
  vector<int>::iterator it;// 迭代器it一开始不指向任何东西
  int i=0;
  int count=0;
  for (i<=1000;i++){
    v2.push_back(i);
    if (it!=v2.begin()){
      count++;
      cout<<"第"<<count<<"次开辟新的空间"<<endl;
      cout<<"容量为"<<v2.capacity()<<endl;
      it = v2.begin(); // 每开辟一次新的空间，都让迭代器it指向新空间的开始迭代器
    }
  }
}
```

运行结果为：

![](E:\资料数据\markdown笔记\marktext图片保存位置\2023-06-29-11-10-59-image.png)

从运行结果可知，vector每次开辟的空间都是旧容量的两倍。

### vector事先预留一定的空间的方法

```C++
vector<int> v1;
v1.reserve(1000);//事先预留了1000个容量
```

# <mark>Vector 常用的赋值操作</mark>

## 函数原型：

```C++
vector &operator=(const vector &v); // 重载等号操作符
```

```C++
assign(v.begin,v.end);//将[begin,end)区间中的数据拷贝赋值给本身
```

```C++
assing(n,elm);//将n个elm拷贝赋值给本身
```

Example：

```C++
void test4(){
    // 定义v，并对其进行初始化
    vector<int> v={1,2,3,4,5};
    // 重载等号运算符的赋值操作
    vector<int> v2 = v;
    vector<int> v3;
    // 调用方法assign区间的赋值操作
    v3.assign(v2.begin(),v2.end());
    vector<int> v4;
    // 调用方法assign枚举的赋值操作
    v4.assign(4,100);
}
```

# <mark>Vector 的容量和大小</mark>

## 函数原型：

```C++
empty();//判断容器是否为空
```

```C++
capacity();//容器的容量
```

```C++
size();//返回容器中的元素个数
```

```C++
resize(int num);// 重新指定容器的长度为num，若容器变长，则以默认值填充新位置；
如果容器变短，则末尾超出容器长度的元素将被删除
```

```C++
resize(int num, eles);//resize()的重载函数，num表示重新指定的容器长度，
eles表示填充值
```

Example:

调用empty(), capacity(),size() 函数

```C++
if (v.empty()){
        cout<<"v is empty"<<endl;
    }
else{
        cout<<"v's capacity is "<<v.capacity()<<endl;
        cout<<"v's size is "<<v.size()<<endl;
    }
```

Example：

调用resize()函数，重新指定vector的容量

```C++
vector<int> v;
int i =0;
for (;i<=3;i++){
    v.push_back(i);
}
```

1.若reszie()之后，容器的容量变得比原来长，则填充默认值

```C++
v.resize(5);
```

输出结果为：

![](E:\资料数据\markdown笔记\marktext图片保存位置\2023-06-29-14-06-26-image.png)

当resize()之后的容量超过原来的容量，则以默认值0进行填充；

当然也可以使用resize(int num, eles)的重载函数来指定一个具体的数进行填充；

```C++
v.resize(5,-1)
```

![](E:\资料数据\markdown笔记\marktext图片保存位置\2023-06-29-14-09-19-image.png)

注意！** resize(int num,eles)中可以指定使用一个字符或字符串进行填充，但是输出结果则是该字符的ASCII码！**   

```C++
v.resize(5,'b');
```

输出结果为：

![](E:\资料数据\markdown笔记\marktext图片保存位置\2023-06-29-14-16-52-image.png)

```C++
v.resize(5,'abc');
```

输出结果为：

![](E:\资料数据\markdown笔记\marktext图片保存位置\2023-06-29-14-17-28-image.png)

# <mark>Vector的插入和删除</mark>

## 函数原型

```C++
push_back();//尾部插入一个元素
```

```C++
pop_back();//删除最后一个元素
```

```C++
insert(const_iterator pos ,el);//迭代器指向的位置pos插入元素els
```

```C++
erase(const_iterator pos);//删除迭代器指向的元素
```

```C++
erase(const_iterator start,const_iteartor end);
//删除迭代器从start到end之间的元素
```

```C++
clear();//删除容器中所有元素
```

Example：

调用push_bakc(), pop_bcak(), insert()

```C++
void test6(){
    vector<int> v;
    v={1,6,3,4,7};
    PrintVectorInt(v);
    v.push_back(10);
    v.push_back(11);
    PrintVectorInt(v);
    v.pop_back();//尾部删除
    PrintVectorInt(v);
    for(vector<int>::iterator it=v.begin();it!=v.end();it++){
        if (*it ==4){
            v.insert(it,-1); //当it所指向的元素为4时，在it处插入-1
            break;
        }
    }
    PrintVectorInt(v);
}
```

输出结果为：

![](E:\资料数据\markdown笔记\marktext图片保存位置\2023-06-29-15-03-33-image.png)

Example:

调用erase(const_iterator pos)和erase(const_iterator start,const_iteartor end)函数

```C++
void test6(){
    vector<int> v;
    v={1,6,3,4,7};
    PrintVectorInt(v);
    v.push_back(10);
    v.push_back(11);
    PrintVectorInt(v);
    v.pop_back();
    PrintVectorInt(v);
    for(vector<int>::iterator it=v.begin();it!=v.end();it++){
        if (*it ==4){
            v.erase(it); //删除迭代器it位置处的元素
        }
    }
    PrintVectorInt(v);
}
```

输出结果为：

![](E:\资料数据\markdown笔记\marktext图片保存位置\2023-06-29-15-06-25-image.png)

```C++
void test6(){
    vector<int> v;
    v={1,6,3,4,7};
    PrintVectorInt(v);
    v.push_back(10);
    v.push_back(11);
    PrintVectorInt(v);
    v.pop_back();
    PrintVectorInt(v);
    for(vector<int>::iterator it=v.begin();it!=v.end();it++){
        if (*it ==4){
            v.erase(it,it+2);//左开右闭区间
        }
    }
    PrintVectorInt(v);
}
```

输出结果为：

![](E:\资料数据\markdown笔记\marktext图片保存位置\2023-06-29-15-13-10-image.png)

# <mark>Vector 数据存取</mark>

## 函数原型

```C++
at(int idx);//返回索引idx所指的数据
```

```C++
operator[];//返回索引idx所指的数据
```

```C++
front();//返回容器中第一个数据元素
```

```C++
back();//返回容器中最后一个数据元素
```

Example:

```C++
void test7(){
    vector<int> v;
    for (int i=0;i<=9;i++){
        v.push_back(i);
    }
    cout<<endl;
    cout<<"v的容量为： "<<v.size()<<endl;

    cout<<"第一种索引方式"<<endl;
    for (int i=0;i<v.size();i++){
        cout<<v.at(i)<<" ";
    }
    cout<<endl;

    cout<<"第二种索引方式"<<endl;
    for (int i=0;i<v.size();i++){
        cout<<v[i]<<" ";
    }
    cout<<endl;
    cout<<"v 的第一个元素为： "<<v.front()<<endl;
    cout<<"v 的最后一个元素为： "<<v.back()<<endl;
}
```

输出结果为：

![](E:\资料数据\markdown笔记\marktext图片保存位置\2023-06-29-15-44-29-image.png)

# <mark>Vector swap()函数 </mark>

## 巧用swap()收缩内存空间

假设一开始，给`vector<int> v;`预留了1000个存储空间，但在实际操作的时候发现，v只存储了4个数据，从而导致了996个内存空间被浪费。此时，我们可以使用swap()函数将v的容量压缩到4个存储空间。

Example:

```C++
void test() {
    vector<int> v;
    v.reserve(1000);
    for (int i = 0; i < 4; i++) {
        v.push_back(i);
    }
    cout << "vector 的大小为： " << v.size() << endl;
    cout << "vector 的容量为： " << v.capacity() <<endl; 

    // 构建一个匿名对象,并把v传入匿名对象，调用匿名对象的拷贝构造函数
    vector<int>(v).swap(v);
    // 注意！ 拷贝构造只会把实际数据拷贝给 匿名对象
    cout << "swap之后！" << endl;
    cout << "vector 的大小为： " << v.size() << endl;
    cout << "vector 的容量为： " << v.capacity() << endl;
```

输出结果为：

![](E:\资料数据\markdown笔记\marktext图片保存位置\2023-06-30-11-45-18-image.png)

# <mark> 二维Vector</mark>

需求，现在有`vector<int> v1;`，`vector<int> v2;`，`vector<int> v3;` 。现在需要一个容器把v1，v2，v3都存储起来。

## 二维vector的定义格式：

```C++
vector< vector<type> > v;
```

Example：

```C++
void test1() {
    vector<int> v1(5, 1);
    vector<int> v2(5, 2);
    vector<int> v3(5, 4);
    vector<vector<int>> v;
    v.push_back(v1);
    v.push_back(v2);
    v.push_back(v3);
}
```

## 二维vector的**遍历**方式！！

对于二维的vector，采用两层for循环的遍历方式。每层for循环，都需要定义有一个迭代器。

注意！`*it`代表了vector内的元素值。

```C++
void test1() {
    vector<int> v1(5, 1);
    vector<int> v2(5, 2);
    vector<int> v3(5, 4);
    vector<vector<int>> v;
    v.push_back(v1);
    v.push_back(v2);
    v.push_back(v3);
    // 定义 外层 for循环的迭代器it
    vector<vector<int>>::iterator it = v.begin(); 
    for (; it != v.end(); it++) {
        //  定义 内层for循环的迭代器mit
        vector<int>::iterator mit = (*it).begin();
        for (; mit != (*it).end(); mit++) {
            //  输出内层for循环的迭代器所指向的元素的值
            cout << *mit << "  ";
        }
        cout << endl;
    }
}
```

输出结果 为：

![](E:\资料数据\markdown笔记\marktext图片保存位置\2023-06-30-12-48-19-image.png)

# <mark>使用sort()函数对vector进行排序</mark>

首先需要导入头文件`#include<algorithm>`  ,然后调用`sort(begin,end)`函数进行排序。

Example：

```C++
void test2() {
    vector<int>v = { 2,6,1,9,3,5 };
    PrintVector(v);
    cout << "排序之前的vector" << endl;
    sort(v.begin(), v.end());
    cout << "排序之后的vector" << endl;
    PrintVector(v);
}
```

输出结果为：

![](E:\资料数据\markdown笔记\marktext图片保存位置\2023-06-30-12-55-51-image.png)

# <mark>vector存储自己构造的数据类型！</mark>

首先定义一个Person类如下：

```C++
class Person{
private:
    //为了让PrintVectorPerson函数能够访问类中的私有成员，让其变为友好成员
    friend void PrintVectorPerson(vector<Person> &v);
    int  student_num;
    string name;
    float gard;
public:
    Person() {};//默认构造函数
    Person(int student_num, const string& name, float gard) //有参数的构造函数
        : student_num(student_num), name(name), gard(gard)
    {
        this->student_num = student_num;
        this->name = name;
        this->gard = gard;
    }
};
```

```

```

然后定义一个 vector保存类Person的实例化对象：

```C++
void test3() {
    vector<Person> v;
    v.push_back(Person(100, "abc", 30));
    v.push_back(Person(109, "bcd", 20));
    v.push_back(Person(103, "cde", 89));
    v.push_back(Person(112, "mark", 48));
    PrintVectorPerson(v);
}
```

```

```

定义一个能够打印输出`vector<Person>`的函数。

```C++
void PrintVectorPerson(vector<Person> &v) {
    vector<Person>::iterator it = v.begin();
    for (; it != v.end(); it++) {
        //(*it)代表Person类的实例化对象，因此可以使用 . 运算符来访问成员数据
        cout << "name is " << (*it).name << " " << "studentNum is " << (*it).student_num << " " << "grad is " 
            << (*it).gard << " " << endl;
    }
}
```

输出结果为：

![](E:\资料数据\markdown笔记\marktext图片保存位置\2023-06-30-13-30-29-image.png)

# 使用sort()函数对自定义类型的vector进行排序

使用sort()函数对自定义类型的vector进行排序时，需要指定排序的关键字，不然系统不知道怎么比较我们自定义的类型。

## 定义比较Person类的函数：

```C++
bool comparePerson(Person& obj1, Person& obj2) {
    // 小于是升序，大于是降序
    //排序关键 字为Person类中的私有成员student_num
    return obj1.student_num < obj2.student_num;
}
```

比较函数的类型一般为布尔类型，传入的参数至少需要两个，传入的参数 就是需要比较的对象。

然后，把比较函数comparePerson()当作参数传入sort()中 ：

```C++
sort(v.begin(), v.end(),comparePerson);
```

comparePerson()函数的作用就是为sort()函数指明比较两个自定义对象的**排序关键字** ！

输出结果为(排序关键 字为Person类中的私有 成员student_num) ：

![](E:\资料数据\markdown笔记\marktext图片保存位置\2023-06-30-13-45-16-image.png)

# <mark>使用Vector的注意事项</mark>

1. 如果你要表示的向量长度较长（需要为向量内部保存很多数），容易导致内存泄漏，而且效率会很低；

2. 如果你要表示的向量长度较长（需要为向量内部保存很多数），容易导致内存泄漏，而且效率会很低；

```C++
double Distance(vector<int>&a,vector<int>&b)
```

其中的“&”绝对不能少！！
