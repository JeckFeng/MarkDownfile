# <mark>Deque 概述</mark>

deque容器为一个给定类型的元素进行线性处理，像向量一样，它能够快速地随机访问任一个元素，并且能够高效地插入和删除容器的尾部元素。但它又与vector不同，deque支持高效插入和删除容器的头部元素，因此也叫做**双端队列**。双端队列不论在尾部或头部插入元素，都十分迅速。而在中间插入元素则会比较费时，因为必须移动中间其他的元素。它不像vector一样把所有对象保存在一个连续的内存块，而是**多个连续的内存块**。并且在一个映射结构中保存对这些块以及顺序的跟踪。**deque不像vector那样拥有空间保留(reserve)功能。** 

![](E:\资料数据\markdown笔记\marktext图片保存位置\2023-06-30-16-43-28-image.png)

# <mark>Deque容器实现原理</mark>

Deque容器是逻辑上的连续空间。deque是由一段一段的定量的连续空间构成。一旦有必要在deque前端或者尾端增加新的空间，便配置一段连续定量的空间，串接在deque的头端或者尾端。deque是分段连续内存空间。

![](E:\资料数据\markdown笔记\marktext图片保存位置\2023-06-30-16-51-57-image.png)

# <mark> Deque的构造函数</mark>

```C++
deque();//创建一个空deque

deque(int nSize);//创建一个deque,元素个数为nSize

deque(int nSize,const T& t);//创建一个deque,元素个数为nSize,且值均为t

deque(const deque &);//复制构造函数
```

# <mark>Deque的常见API操作</mark>

## deque的大小操作

```C++
deque.size();//返回容器中元素的个数

deque.empty();//判断容器是否为空

deque.resize(num);//重新指定容器的长度为num,若容器变长，则以默认值填充新位置。如果容器变短，则末尾超出容器长度的元素被删除。

deque.resize(num, elem); //重新指定容器的长度为num,若容器变长，则以elem值填充新位置,如果容器变短，则末尾超出容器长度的元素被删除。
```

## deque 双端插入和删除操作

```C++
push_back(elem);//在容器尾部添加一个数据

push_front(elem);//在容器头部插入一个数据

pop_back();//删除容器最后一个数据

pop_front();//删除容器第一个数据
```

## deque 的数据存取

```c++
front();//返回第一个数据。

back();//返回最后一个数据
```

## deque 的插入操作

```C++```
insert(pos,elem);//在pos位置插入一个elem元素的拷贝，返回新数据的位置。

insert(pos,n,elem);//在pos位置插入n个elem数据，无返回值。

insert(pos,beg,end);//在pos位置插入[beg,end)区间的数据，无返回值。

```
## deque的删除操作

```C++
clear();//移除容器的所有数据

erase(beg,end);//删除[beg,end)区间的数据，返回下一个数据的位置。

erase(pos);//删除pos位置的数据，返回下一个数据的位置。
```

## deque的遍历操作

```C++
void printDeque(const deque<int> &d){//遍历容器
    for (deque<int>::const_iterator it = d.begin(); it != d.end(); it++) {
        cout<< *it <<" ";
    }
    cout<<endl;
}
```

## 使用sort()函数对deque进行排序

```C++
/* 回调函数 */
bool compare(int v1 ,int v2){
    return v1 > v2;//从大到小

}
void test(){
    deque<int> d;
    d.push_back(3);
    d.push_back(4);
    d.push_back(1);
    d.push_back(7);
    d.push_back(2);

    sort(d.begin(), d.end(), compare);
    printDeque(d);
}
```
