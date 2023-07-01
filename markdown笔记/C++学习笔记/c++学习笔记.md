## cout 关于输出十进制，十六进制，八进制

1. cout << oct <<number1<<endl; //输出number1为八进制
2. cout << hex << number2<<endl;  //输出为十六进制
3. cout默认输出十进制

## cin 关于输入十进制，十六进制，八进制

1. cin >>hex>> array[i] ;    //为数组array输入十六进制的元素
2. cin >>oct>> array[i] ;     // 为数组输入八进制的元素

## C++中关于字符串的操作   

1. 导入头文件 #include <string>

2. 整型转换为字符串：to_string()函数

   - ​		示例：
     ​                  

     ```c++
     #include <iostream>
     #include <string>
      
     using namespace std;
      
     int main()
     {
         int a = 100;
         string strTest;
      
         strTest = to_string(a) + " is a string."; //to_string函数将变量a转换为了字符串类型
      
         cout << "a is: " << a << endl;
         cout << "pszTest is: " << strTest << endl;
      
         return 0;
     }
     
     ```

     

     }

3. 字符串索引：string str; str[];

4. 返回字符串长度：str.size()

## C++的强制类型转换（int）,(int &), (int *)

1. （int）:(int)x 强制类型转换，是将浮点数x为参数构造整数（即float转换为int）
2. (int &):(int &)y 则是告诉编译器将y看成int对待
3. (int *):强制转换成整型指针

## C++返回字符串长度函数：

```c++
#include <iostream>
using namespace std;
#include <string>
int main()
{
string str="asdcsfgvfb";
cout << strlen(str); //输出字符串str的长度
return 0;
}
```



## C++返回数组的长度写法：

```c++
#include <iostream>
using namespace std;
int main()
{
int array={1,2,3,4,5}
cout << sizeof(array)/sizeof(array[0]);
return 0;
}
```

## C++让系统生成一个随机数字：

```c++
#include <iostream>
#include <time.h>  //注意需要导入time头文件
using namespace std;
//让系统生成一个随机数0-100
	srand((unsigned)time(NULL));
	int start = 0; //起始数字
	int end = 100;  //最大数字
	int dis = end - start;
	int randint = rand() % dis + start;
```

## C++内联函数

1. 内联函数的作用：为了解决频繁地调用函数，导致程序开销增大，降低系统运行效率的问题。
2. 内联函数的定义：需要在函数开头添加inlin进行修饰

```c++
inline <返回类型> <函数名称> (参数列表)
{
	<函数体>
}
```

   3.内联函数的使用规则：不应该出现复杂控制结构或循环语句，如，while，for，switch

   4.实例：

```c++
#include <iostream>
# include <iomanip>
using namespace std;
/*
定义一个比较大小的内联函数，程序中有一个10行3列的数组，利用函数求出每行
的最大值，并将每行的最大值相加



*/

inline int max(int a, int b,int c)
{
	int max = 0;
	max =  a > b ? a : b;
	return max > c ? max : c;
}

int main()
{
	int data[10][3] = {
	{2,4,59},  //1
	{4,8,456},  //2 
	{78,55,489},  //3
	{45,16,87},  //4
	{48,231,545},  //5
	{15,984,32},  //6
	{1,484,23},   //7
	{546,324,78},    //8
	{787,5,2},    //9
	{12,0,9}    //10
	};


	//打印出数组data

	for (int i = 0; i < 10; i++)
	{
		for (int j = 0; j < 3; j++)
		{
			cout << setiosflags(ios::left);
			cout << data[i][j] << "\t";
			
		}
		cout << endl;

	}

	cout << endl;


	int sum = 0;
	for (int i = 0; i < 10; i++)
	{
		cout << "第" << i << "行的最大值为" << max(data[i][0], data[i][1], data[i][2]) << endl;
		sum = max(data[i][0], data[i][1], data[i][2]) + sum;  //累加操作

	}


	//输出最大值之和
	cout << "最大值之和为：	" << sum << endl;
	system("pause");
}
```



## C++重载函数

1. 重载函数的作用：重载函数共享同一个函数名称，但是它们的实现是不同的，重载的目的在于多个函数共用一个函数名。

2. 举例：实现一个加法函数的重载

   ```c++
   int add (int ,int );   //两个int类型做加法
   double add (double ,double);  //两个double类型做加法
   short add(short ,short );   //两个short类型做加法
   ```

   

3. 多个函数重载至少要在函数的参数类型，参数个数，参数顺序上要有所不同。

4. ds 

## C++指针操作

1. 在32位的操作系统下，一个指针所占的内存大小 为4个字节（不管什么数据类型）。在64位的操作系统下，一个指针所占的内存大小位8个字节（不管什么数据类型）。

   ```c++
   int a = 10;
   short b = 1;
   int* p = &a;
   short* p = NULL;
   //用sizeof(int *)查看指针所占用的内存空间
   cout<<"整型指针所占内存大小为：	" << sizeof(int *) << endl;  //sizeof(int *) 等价于 sizeof(p)
   cout << "整型指针所占内存大小为：	" << sizeof(p) << endl;
   cout << "短整型指针所占内存大小为：	" << sizeof(short *) << endl;  //sizeof(short * )等价于sizeof(p1)
   cout << "短整型指针所占内存大小为：	" << sizeof(p1) << endl;
   	 
   ```

2. 运用指针求char型的字符串长度（即求出字符串有几个字符），代码：

   ```c++
   #include <iostream>
   using namespace std;
   void main(void)
   {
       char ch[] = "hello world";
       char* p1 = ch;  ///定义指向字符串的指针    
       //打印出字符串的首地址
       cout<<"字符串的首地址为：	"<<(int) &ch<<endl;
       cout << "字符串ch中每个元素所占的内存空间为：sizeof(ch[0])=" << sizeof(ch[0]) << endl;
       while(*p1 != '\0')
       {
           p1++;
           cout <<"指针自增之后指向的地址为：	" << (int)pl << endl;       
       }
        
      cout<<"字符串的长度为：	"<< abs( (int)p1 - (int)ch ) / sizeof(ch[0])<<endl;
       
       system("pause");
       
   }
   ```

   ![](C:\Users\fxl\AppData\Roaming\Typora\typora-user-images\image-20210309161039423.png)

3. 地址+1和指针+1是不一样的。

## C++ 使用new动态分配内存

1. 利用new操作可以实现变量的动态内存分配，其基本格式如下：

   ```c++
   <变量类型>*   <变量指针名>  = new   变量类型名   ;
   ```
   实现变量的动态分配内存示例：

   ```c++
   // 为一个double类型的变量申请内存空间
   #include <iostream>
   using namespace std;
   void main ()
   {
       double* pDoub = new double;
       
       *pDoub = 10.0;  //pDoub 所指内存空间值为10.0
       double* pDoub1 = new double(10.0) ;   //声明的时候进行初始化
   }
   
   ```


2. 为数组动态分配内存空间，基本格式为：

   ```c++
   <数组类型名>*  <指针变量名> = new  <数组类型名>[数组大小]；
   
   ```

   实现数组的动态分配内存示例：
   
   ```c++
   #include <iostream>
   using namespace std;
   //为一个数组动态分配内存空间
   void main()
   {
   	int* pInt = new int [10];
   
   }
   ```
   
3. delete释放动态申请的空间，释放变量或数组的基本格式如下：

   ```c++
   delete 指针名；
   delete []指针名；
   ```

   ```c++
   #include <iostream>
   using namespace std;
   void main()
   {
   	int* p = new int(10);  //初始化指针p并赋值为10
       double *pd = new double[10]; //初始化一个大小为10 ，数据类型为double的数组
       delete p;     //释放p指针指向的内存块
       delete []pd;  //释放pd内存块
       p = 0；   //将p指向空地址
       pd = 0； //将pd指向空地址
   
   }
   ```

   

4. 实现数组动态创建和对应内存回收的例子：

   ```c++
   #include<iostream>
   using namespace std;
   void main(void)
   {
   	double * pd = new double[6];  //声明一个动态数组pd
   	for (int i = 0; i < 6; i++)
   	{
   		*(pd + i) = i;
   
   	}
   	cout << "pd的内存地址为：	" << &pd  <<  "  pd的值为：	"<< pd <<endl;
   
   	for (int i = 0; i < 6; i++)
   	{
   		cout << *(pd + i) << "   " << endl;  //输出pd所指内存空间的值
   		//cout << pd[i] << "   " << endl;
   	}
   
   	cout << endl;
   	delete[]pd;
   	cout << "pd的内存地址为：	" << &pd << "  pd的值为：	" << pd << endl;  //输出pd地址和pd值
   	pd = 0;
   	cout << "pd的内存地址为：	" << &pd << "  pd的值为：	" << pd << endl;   //输出pd地址和pd值
   }
   ```

   在上面这个例子中，pd的内存地址的意思为：**pd指针保存在内存中的地址**；pd的值的意思为：**pd指针所指向内存空间的首地址**。当delete运算符释放pd所指向的内存空间后，打印pd所占内存地址和pd的值与之前的所在地址和值都没有发生改变。**说明delete指针本身不会删除指针，pd还会指向别的内存空间。**

5. 指针的强制类型转换，可以按照下面的格式

   ```c++
   <新的数据类型>*  <指针名> = (新的指针类型*) <指针表达式>
   ```

   举例如下：

   ```c++
   #include<iostream>
   using namespace std;
   
   void main()
   {
   
   	double d = 10.0;
   	double *pd = &d;
   	int *pi = (int *)&d;
   	char *pc = (char *)&d;
   	short *ps = (short *)&d;
   }
   
   ```

   





