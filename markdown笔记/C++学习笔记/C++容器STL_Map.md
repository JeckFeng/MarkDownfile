# <mark> **map概述**</mark>

我们可以使用map存储这类一对一的数据：

第一个可以称为关键字(key)，每个关键字只能在map中出现一次；  
第二个可能称为该关键字的值(value)；

另外需要注意的是，使用 map 容器存储的各个键-值对，**键的值既不能重复也不能被修改**。换句话说，map 容器中存储的各个键值对不仅键的值独一无二，键的类型也会用 **const** 修饰，这意味着只要键值对被存储到 map 容器中，其键的值将不能再做任何修改。



# map 构造函数

1. 默认构造函数

```C++
map<T1,T2> map TT;
```

```

```

2. 拷贝构造函数

```C++
map(const map &mp);
```

```

```

# map的赋值操作

```C++
map &operator=(const map &mp);//重载等号操作符
```

```C++
swap(mp);//交换两个集合容器
```

# map的大小操作

```C++
size();//返回容器中元素的数目
```

```C++
empty();//判断容器是否为空
```

# map插入元素操作

```C++
map.insert(...);//往容器插入元素，返回pair<iterator,bool>
map<int,Student> mp;//Student 是自定义的类
//第一种插入方式
mp.insert(pair<int,string>(3,Student(1392, "dfsop", 90.1));
//第二种插入方式，通过pair的方式插入
mp.insert(make_pair(1392, Student(1392, "dfsop", 90.1)));
//第三种方式 通过value_type的方式插入
mp.insert(map<int, Student>::value_type(1294, Student(1294, "vnmks", 94.1)));
//第四种方式，通过数组的方式插入（不推荐）
mp[4392] = Student(4392, "sdfk", 49.1);

```

# map删除操作

```C++
clear();//删除所有元素
erase(pos);//删除pos迭代器所指的元素，返回下一个元素的迭代器
erase(begin , end);//删除区间[begin,end]的所有元素，返回下一个元素的迭代器
erase(keyElem);//根据字典的键值来删除，删除key为keyElem的对组
```

# map 查找操作

```C++
find(key);//查找键key是否存在，若存在，返回该键的元素的迭代器；若不存在，返回map.end()
count(keyElem);//返回容器中key为keyElem的对组个数，对map来说，要么是0，要么是1！因为键值不能重复。
lower_bound(keyElem);//返回第一个key>=keyElem元素的迭代器/
upper_bound(keyElem);//返回第一个key>keyElem元素的迭代器

```

```

```
