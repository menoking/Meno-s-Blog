# 【C++入门】半小时入门C++开发(深入理解new+List+范围for+可变参数)

> 原创 已于 2025-12-28 22:42:14 修改 · 粉丝可见 · 1.4k 阅读 · 23 · 5 · 本内容遵循CC 4.0 BY-SA版权协议 版权声明：本文为博主原创文章，遵循 CC 4.0 BY 版权协议，转载请附上原文出处链接和本声明。 GEO检测 · 编辑
> 文章链接：https://menoking.blog.csdn.net/article/details/143314496

**目录**

[TOC]





## 一.深入理解new

类似于C语言中的 `malloc` 、 `calloc` 和 `realloc关键字，在C++中动态分配内存一般使用new关键字，其返回值是一个指向内存块的地址。` 

### 使用格式

> **new:** 
> 
> - 类型指针  指针变量名  =  new  类型名;
> 
>   - Type*  variable = new Type;
> 
> - 类型指针  指针变量名  =  new  类型名(初始值);
> 
>   - Type*  variable = new Type();
> 
> - 类型指针  指针变量名  =  new  类型名[元素个数];
> 
>   - Type*  variable = new Type[];
> 
> **delete:** 
> 
> - delete 指针变量名;
> 
>   - delete  variable;//释放单个空间
> 
> - delete[] 指针变量名;
> 
>   - delete[]  variable;//连续释放多个空间
> 
> 

```cpp
//申请内存空间
int* p = new int;
//申请并初始化
int* p = new int(1);
//申请连续10个空间，由于一个指针为4字节，所以总共4*10=40
int* p = new int[10];
 
//释放单个空间
delete p;
//释放多个空间，常用于数组
delete[] arr;
```

new对于对象的空间申请和分配有很好的效果：

```cpp
class A{
public:
    A(int a = 10){};
    ~A(){};
};
 
//合法但不应使用，未调用构造函数初始化
A* a = new A;
//为对象申请空间，并初始化
A* a = new A();
//在类的构造函数中有默认参数时，可以连续申请多个空间
A* a = new A[10];
 
delete a;
```

即，new去申请对象会先申请对象的空间并调用对象的构造函数完成对象的初始化；delete会先去完成对象的资源清理，再将对象所占的空间释放掉。

## 二.List列表

List是C++的一个序列容器，底层结构是一个 **带头双向循环链表** ，使用列表来 **插** 入和删除元素的效率较高， **适用于频繁进行插入和删除操作** ；但 **不能直接通过位置(下标)来直接访问元素** 。想要访问list的某个元素，必须从list的一端（或已知位置）迭代到该元素。

### 定义一个列表

```cpp
list <typename> name;
```

### 迭代器

```cpp
list<string> a;
list<string>::iterator it;	// 迭代器
 
for(it=a.begin();it!=a.end();it++)
{
    string temp=*it;
    print(temp);
}
```

### 添加元素

```cpp
void push_front(const T& x);	// 头部添加
void push_back(const T& x);		// 尾部添加
insert(iterator, value);        //迭代器任意添加
```

### 删除元素

```cpp
void pop_front();		// 头部删除
void pop_back();		// 尾部删除
myList.remove(value);   //删除特定值元素
mylist.remove_if(func)  //删除满足特定条件的元素
mylist.erase(it);       //迭代器删除元素
```

### 排序

```cpp
myList.sort();//降序排列
```

### 反转序列

```cpp
myList.reverse();
```

## 三.范围for

C++11引入一新的语法 **范围-based for 循环** （range-basedfor loop），用于简化遍历容器或集合中的元素。

```cpp
//普通循环
for(表达式 1; 表达式 2; 表达式 3)
{
    // 循环体
}
 
// 范围for循环
for (int declaration : expression) 
{ 
    // 循环体
}
```

> 注意：
> 
> - **适用范围广泛** ：范围for循环可以用来遍历任何支持 `begin()` 和 `end()` 函数的容器，比如 `std::vector` 、 `std::array` 、 `std::list` 等标准容器。
> 
> 

## 四.可变参数

### std::initializer_list

std::initializer_list用于表示某种特定类型的值的数组，是一种模板类型。

```cpp
#include <initializer_list>
 
void func(std::initializer_list<int> list) 
{
    for (int a : list) 
    {
        std::cout << a << " ";
    }
    std::cout << std::endl;
}
```

特别注意：用initializer_list传递参数只能读，不能写！

### 可变参数模板（variadic template）

```cpp
template<class T, class... Args>
//template<typename T, typename... Args>
void func(const T &t, const Args&... test); 
```

> 
> 
> 1. 这里的"class"和"typename"表示 **“这里声明的 `T` 是一个类型参数”** ，并非是指类。
> 
> 2. `class T` 告诉编译器 `T` 是一个类型参数。
> 
> 3. `class... Args` 告诉编译器 `Args` 是一个 **类型参数包** ，它可以包含多个类型。
> 
> 

## 五.类静态成员

在C++中，当我们定义的类需要共享同一个属性或行为时，就可以使用到静态成员。我们使用 **static** 关键字来把类成员定义为静态的。当我们定义静态成员变量时，必须要在类外初始化这个静态成员变量的值；当我们定义静态成员函数时，无需类外初始化。

### 静态成员变量

> 
> 
> - **类外初始化（若不在类外初始化，创建第一个对象是自动初始化为0）**
> 
> - **被所有对象共享**
> 
> - **生命周期不依赖任何对象，为程序的生命周期**
> 
> 

```cpp
#include <iostream>
 
using namespace std;
 
class AAA
{
   public:
      static int B;
      // 构造函数定义
      AAA()
      {
      }
};
 
// 初始化类 Box 的静态成员
int AAA::B = 0;
 
int main(void)
{
   AAA a(); 
 
    cout << AAA::B<< endl;//访问静态变量
    cout << a.B<< endl;//同上
}
```

### 静态成员函数

> 
> 
> - **没有 this 指针**
> 
> - **即使在类对象不存在的情况下也能被调用**
> 
> - **只能直接访问静态成员变量，静态成员函数和类外其他函数**
> 
> 

```cpp
#include <iostream>
 
using namespace std;
 
class AAA
{
   public:
      static int B;
      // 构造函数定义
      AAA()
      {
      }
      static int getValue()
      {
         return B;
      }
};
 
// 初始化类 Box 的静态成员
int AAA::B = 0;
 
int main(void)
{
   AAA a(); 
 
    cout << AAA::getValue<< endl;//访问静态函数
}
```