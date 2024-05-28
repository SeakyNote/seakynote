## delete后要不要set null

https://blog.csdn.net/goof/article/details/8212156 我认为悬挂指针不应该被使用

------

c++中在析构函数中内存释放后是否要将指针置为空？

https://stackoverflow.com/questions/3060006/is-it-worth-setting-pointers-to-null-in-a-destructor

有争议

------

C++ Primer关于此问题：在指针即将要离开其作用域之前释放掉它所关联的内存;如果我们需要保留指针，可以在delete后将nullptr赋予指针。

## C++宏 #的使用

#构串操作符: 将#右边内容转化为字符串

##合并操作符: ##左右直接拼接

## C++中的dynamic_cast和dynamic_pointer_cast

https://blog.csdn.net/jiayizhenzhenyijia/article/details/98209529

## 人为制造一个异常

std::string().at(1);

## c++万能头文件

#include<bits/stdc++.h>

## 初始化列表顺序问题

剑指offer

101 C47

CCG  C47

## 类的成员是否都要初始化

https://stackoverflow.com/questions/33124542/should-constructor-initialize-all-the-data-members-of-the-class

(Simple) Every constructor should initialize every member variable (either explicitly, via a delegating ctor call or via default construction)

(Simple) Default arguments to constructors suggest an in-class initializer might be more appropriate.

## C++mutable

https://blog.csdn.net/weixin_51684362/article/details/131364670

## 在删除之前是否有任何理由检查 NULL 指针？

https://stackoverflow.com/questions/615355/is-there-any-reason-to-check-for-a-null-pointer-before-deleting

## auto

https://herbsutter.com/2013/08/12/gotw-94-solution-aaa-style-almost-always-auto/

## heap corruption detected after normal block

可能是头文件不同步造成的

## `c.erase( remove( c.begin(), c.end() ,value ) );`

这行代码看起来像是C++中用于从容器中删除特定值的代码。让我解释一下：

```cpp
c.erase( std::remove(c.begin(), c.end(), value), c.end() );
```

这行代码的作用是从容器 `c` 中删除所有等于 `value` 的元素。这是通过结合使用 `std::remove` 和 `erase` 函数来实现的。

`std::remove` 函数实际上并不会真正删除元素，它会将所有等于 `value` 的元素移动到容器的末尾，并返回一个指向新的逻辑结尾之后的位置的迭代器。然后，`erase` 函数会使用这个迭代器，将从这个位置开始的所有元素都从容器中删除。

因此，这行代码的效果是将容器中所有等于 `value` 的元素移动到末尾，然后将它们从容器中删除，最终容器中不再包含任何等于 `value` 的元素。

## `vector<int>().swap( c );`

这行代码的作用是将名为c的vector对象清空并释放其内存，这样可以有效地回收vector占用的内存空间。通常情况下，使用`clear()`函数可以清空vector对象，但是它不会释放vector占用的内存，因此在处理大型vector时，`clear()`可能会导致内存占用过高。

相比之下，`vector<int>().swap(c)`的方式更加高效，因为它会创建一个临时的匿名vector对象，然后通过swap操作将其和c交换，这会导致c的内部数组指针指向了临时对象的数组，而临时对象则接管了c原来的数组指针。随后，临时对象会被销毁，从而释放了原来c所占用的内存。这样一来，c就变成一个空的vector，而且不再占用任何内存。

总的来说，`vector<int>().swap(c)`的作用是清空vector对象并释放其内存，这在需要释放大量内存时是一个高效的方法。

## `vector<int>( c ).swap( c );`

这段代码的作用是将一个名为 c 的 vector 对象清空。通常情况下，我们可以使用 clear() 方法来清空 vector 对象，但是有时候使用 swap() 方法可以更高效地完成这个任务。

让我们来解释一下这段代码的具体作用：

1. `vector<int>(c)`：创建了一个临时的 vector 对象，其内容是 c 的副本。这个副本会继承 c 的容量和分配器，但是不会继承 c 的元素。

2. `.swap(c)`：通过调用 swap() 方法，临时创建的 vector 对象与原始的 c 对象进行了交换。由于交换后临时创建的对象会被销毁，而原始的 c 对象现在包含了一个空的 vector，因此原始的 c 对象就被清空了。

总的来说，这段代码的作用就是清空 vector 对象 c，但是相比于直接调用 clear() 方法，它使用了 swap() 来更高效地完成清空操作。

## c++类的成员函数中声明`operator char*() const;`是什么意思？

在C++中，`operator char*() const;` 是一个类成员函数的声明，它声明了一个类型转换运算符（Type Conversion Operator）。这个运算符允许将一个类的对象转换为 `char*` 类型或者指向 `char` 类型的指针。

具体地说，`operator char*() const;` 声明了一个将类对象转换为 `char*` 类型的运算符，这个运算符是一个 const 成员函数。这意味着当你使用类对象进行 `char*` 类型的转换时，编译器会调用这个成员函数来执行转换操作。

以下是一个简单的示例，说明了如何使用这个类型转换运算符：

```cpp
#include <iostream>

class MyClass {
public:
    operator char*() const {
        return "Hello, World!";
    }
};

int main() {
    MyClass obj;
    const char* str = obj;  // 调用 operator char*() const;
    std::cout << str << std::endl;  // 输出 "Hello, World!"
    return 0;
}
```

在这个示例中，`operator char*() const` 被用来将 `MyClass` 的对象转换为 `char*` 类型，使得我们可以直接将 `MyClass` 对象赋值给 `char*` 类型的变量。

需要注意的是，类型转换运算符应该被谨慎使用，因为它可能会导致意外的类型转换，可能会使代码更难以理解。

## erase迭代器失效问题

根据标准，erase会造成当前位置和之后的迭代器失效，所以这是未定义的行为。
不管能不能运行，还是不要玩雷。

## string转wstring

```c++
std::string narrowStr = "Hello, World!";
std::wstring wideStr(narrowStr.begin(), narrowStr.end());
```

```c++
std::string narrowStr = "Hello, World!";
std::wstring wideStr;
std::copy(narrowStr.begin(), narrowStr.end(), std::back_inserter(wideStr));
```

## 找到vector中的最大值

max_element

删除该元素	erase(it)

## 最小堆

priority_queue<int, vector<int>, greater<int>>

push

top返回最小值

pop弹出最小值

## `vector<int>`搜索某项

```c++
auto it = std::find(numbers.begin(), numbers.end(), searchItem);

while (it != numbers.end()) {
    std::cout << "Item found at index: " << std::distance(numbers.begin(), it) << std::endl;
    it = std::find(std::next(it), numbers.end(), searchItem);
}
```

```c++
while (it != numbers.end()) {
    // 计算迭代器的位置（索引）
    int index = std::distance(numbers.begin(), it);
    std::cout << "Item found at index: " << index << std::endl;

    // 继续搜索下一个匹配项
    it = std::find(std::next(it), numbers.end(), searchItem);
}
```

## vector截取原始向量一段

`std::vector<int> subVector(originalVector.begin() + startIndex, originalVector.begin() + endIndex + 1);`

## 标准库函数对象

例子，降序排列

`sort(svec.begin(), svec.end(), greater<string>());`

## 按值传递还是引用传递

当 sizeof(ObjectType) > 2 * sizeof(void*) 时要求引用传递，否则要求值传递

https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rf-conventional

## bitset用法

初始化bitset `bitset<32> curbs(num);`

bitset遍历 `for (int i = 0; i < curbs.size(); ++i)`

检查某位是否为1 `if (curbs.test(i))`

修改某位为1 `b[i] = true;`

bitset转数字 `retVal = b.to_ulong();`

##  位运算

二进制第i位是否为1 `if ((num >> i) & 1)`

将二进制第i位设置为1 `ans |= 1 << i;` 位左移运算符 << 的优先级比位或运算符 | 更高

## 输出运行时间

```
#define OutputTime														\
	qDebug()<<"//---------------calc time------------------------\n"	\
			<<__func__<<" "<<__LINE__<<" "								\
            <<QTime::currentTime().toString("hh:mm:ss.zzz")    
```

## string操作

统计string中字符1出现的次数 `int cnt = count(s.begin(), s.end(), '1');`

由n个重复字符构造 `string s4(10, 'c'); // s4 is cccccccccc`

## 直接获得vector首尾元素

v.front()

v.back()

## c++头文件中的宏定义应该放在前置声明之前还是之后？

在C++头文件中，通常建议将宏定义放在前置声明之前。这是因为宏定义可能会影响到后续的代码，包括前置声明。通过将宏定义放在前置声明之前，可以确保在进行前置声明时，宏已经被正确定义，从而避免潜在的错误或不一致性。

例如，一个典型的C++头文件可能包括以下内容的顺序：

1. 头文件保护宏（例如 `#ifndef`、`#define`、`#endif`）
2. 其他头文件的引用（例如 `#include <iostream>`）
3. 宏定义（例如 `#define MAX_SIZE 100`）
4. 类或函数的前置声明（例如 `class MyClass;`）
5. 类或函数的实际定义

这种顺序可以确保在进行前置声明时，宏已经被正确定义，从而提高代码的可读性和可维护性。

## 枚举可以不初始化吗

与int一样，必须初始化

https://stackoverflow.com/questions/6842799/enum-variable-default-value

## 预处理变量大小写

Preprocessor variables, including names of header guards, must be unique throughout the program. Typically we ensure uniqueness by basing the guard’s name on the name of a class in the header. To avoid name clashes with other entities in our programs, preprocessor variables usually are written in all uppercase.

## c++中为什么push_back({1,2})可以，emplace_back({1,2})会报错?

https://www.zhihu.com/question/438004429