## 三板斧试试强度

- 对迭代器的理解
```cpp
	std::map<std::string, std::string>::iterator it;
	for (it = dataMap.begin(); it != dataMap.end(); it++)
	{
		if (it->second == "")
			break;
	}
	if (it == dataMap.end())
	{
		combo->addItem("");
	}
```
- 类初始化列表顺序问题

```cpp
class A
{
private:
    int n1;
    int n2;
public:
    A() : n2(0), n1(n2 + 2)
    {
    }
    void print()
    {
        cout << "n1: " << n1 << endl;
        cout << "n2: " << n2 << endl;
    }
};

int main()
{
    A a;
    a.print();
    return 0;
}
```

- 类成员可见性和可访问性

```cpp
int n = 0;
class Parent
{
public:
    Parent() : n(1) {}
private:
    int n;
};

class Child : public Parent
{
public:
    Child() {}
    void Func()
    {
        cout << n << endl;
    }
};

int main()
{
    Child c;
    c.Func();
    return 0;
}
```

- 随机算法题

## 近半年工作内容

其中感兴趣的项目

- 背景
- 自己做的工作
  - 单独或带队做的话
    - 总体框架设计
    - 核心算法
    - 团队合作
- 项目中碰到的最大问题，如何解决
- 学到什么/收获
- 什么时候会和其他团队成员起冲突（开发、测试、设计、项目经理）
  - 如何解决

## C++

智能指针有使用过吗?什么时候使用智能指针？标准库各智能指针的使用场景和区别？

讲一讲C++中的堆区和栈区

- C++内存分布管理这块
- 各存放什么类型的数据
- 内存是如何释放的
- 内存释放顺序
- 容量大小

虚函数的作用/多态是什么？举个之前项目中的例子

C++的四种cast讲一下，区别和使用场景

struct/class区别

介绍下标准库容器中end成员函数返回迭代器的含义及其常见用法

各顺序容器的特点和使用场景——vector/list/arrary

为什么引用不像指针一样区分顶层const和底层const

## Qt

qt的使用版本

cmake/qmake

- cmake这块了不了解
  - cmake怎么区分debug/release
  - 编译优化级别
- 二者的区别

控件提升了不了解。举几个之前项目中具体的例子

信号槽连接直连式、队列式、自动式的区别

tablewidget和tableview的区别和使用场景

qframe和qwidget的区别和使用场景

qpushbutton和qtoolbutton的区别和使用场景

qtimer和qElapsedTime的区别和使用场景

qt多线程有没有做过，讲一下怎么做的。当时是什么场景

processEvents（处理事件）方法的作用

qss样式表有没有用过，讲一下你的使用场景

## Git

git有没有使用过

能讲下什么场景用merge什么场景用rebase吗？

revert/reset区别

怎么操作git的，用哪些工具

讲一下工作流

## 算法/程序题

数据结构和算法这块有没有学习和了解过

讲一下快速排序的原理

**要输出前n个自然数中的质数的话，应该采取怎样的算法逻辑**

- 回答筛法的话，问怎么求自然数中前n个质数

求斐波那契数列第n项

**爬楼梯**问题，一个人可以爬楼梯，一次可以爬一级也可以爬两级，总共有n级台阶，他有多少种爬法？

有向图拓扑排序

一个数的整数次方

单源最短路径，边权为正

给定一个长字符串，返回这个字符串中出现不止一次，长度为5的子字符串，可以任意顺序返回答案。

## 设计模式

各种单例模式的使用场景

- 饿汉式——加载时创建
- 懒汉式——调用时创建
- 双重检查锁定

工厂方法模式和抽象工厂模式
