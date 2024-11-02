## delete后要不要set null

https://blog.csdn.net/goof/article/details/8212156 我认为悬挂指针不应该被使用

------

c++中在析构函数中内存释放后是否要将指针置为空？

https://stackoverflow.com/questions/3060006/is-it-worth-setting-pointers-to-null-in-a-destructor

有争议

------

C++ Primer关于此问题：在指针即将要离开其作用域之前释放掉它所关联的内存;如果我们需要保留指针，可以在delete后将nullptr赋予指针。

## C++宏 `#`的使用

`#`构串操作符: 将#右边内容转化为字符串

##合并操作符: ##左右直接拼接

## C++中的dynamic_cast和dynamic_pointer_cast

https://blog.csdn.net/jiayizhenzhenyijia/article/details/98209529

## 人为制造一个异常

std::string().at(1);

## c++万能头文件

`#include<bits/stdc++.h>`

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

```cpp
std::string narrowStr = "Hello, World!";
std::wstring wideStr(narrowStr.begin(), narrowStr.end());
```

```cpp
std::string narrowStr = "Hello, World!";
std::wstring wideStr;
std::copy(narrowStr.begin(), narrowStr.end(), std::back_inserter(wideStr));
```

## 找到vector中的最大值

max_element

删除该元素	erase(it)

## 最小堆

`priority_queue<int, vector<int>, greater<int>>`

push

top返回最小值

pop弹出最小值

## `vector<int>`搜索某项

```cpp
auto it = std::find(numbers.begin(), numbers.end(), searchItem);

while (it != numbers.end()) {
    std::cout << "Item found at index: " << std::distance(numbers.begin(), it) << std::endl;
    it = std::find(std::next(it), numbers.end(), searchItem);
}
```

```cpp
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

## include guard vs pragma once

https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rs-guards

## 最好为所有依赖项显式包含标头，以便代码不会因头文件更改而出错

https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#sf10-avoid-dependencies-on-implicitly-included-names

https://zh-google-styleguide.readthedocs.io/en/latest/google-cpp-styleguide/headers.html#include-what-you-use

## 如何理解queue不能基于vector构造？
```
    vector<int> vec{1,2,3};
    queue<int, vector<int>> q3{vec};
    q3.pop();//加上这行编译就出问题了
    cout << q3.front() << " " << q3.back()<<endl;
```
实测gcc编译器可以基于vector构造queue，但调用pop函数时会报编译错误

## 智能指针作用域
与局部变量一致，离开作用域，指向的内存释放

## string::compare
- 类似C中的strcmp
- C++ primer 5e 9.5.4

## 模板类中的`operator->`
在C++模板类中，`T* operator->()` 是一个重载运算符，用于返回指向模板类型对象的指针。这个运算符通常在需要通过模板类的实例访问其内部对象的成员时使用。
### 详细解释

1. **定义和用途**：
    - `operator->` 运算符用于对象的指针成员访问。这意味着可以使用类似指针的语法来访问对象的成员。
    - 在模板类中，`T* operator->()` 重载通常用于包装类，这些类封装了一个指向对象的指针，以便于管理对象的生命周期或增加额外的功能。

2. **示例代码**：
    下面是一个简单的示例，展示了如何在模板类中定义和使用 `operator->`：

    ```cpp
    #include <iostream>
    #include <memory>

    // 一个简单的模板类，封装了指针
    template <typename T>
    class SmartPointer {
    private:
        T* ptr; // 原始指针

    public:
        // 构造函数
        explicit SmartPointer(T* p = nullptr) : ptr(p) {}

        // 析构函数
        ~SmartPointer() {
            delete ptr;
        }

        // 重载 -> 运算符
        T* operator->() {
            return ptr;
        }

        // 重载 * 运算符
        T& operator*() {
            return *ptr;
        }
    };

    // 一个简单的类，用于测试
    class Test {
    public:
        void show() {
            std::cout << "Test::show() called" << std::endl;
        }
    };

    int main() {
        SmartPointer<Test> sp(new Test());
        sp->show(); // 使用重载的 -> 运算符来调用 Test::show()
        return 0;
    }
    ```

3. **工作原理**：
    - 在上述示例中，`SmartPointer` 类封装了一个指向类型 `T` 的指针 `ptr`。
    - 当使用 `sp->show()` 时，`operator->` 被调用，返回 `ptr`，然后通过 `ptr` 调用 `show()` 方法。
    - 这种机制使得 `SmartPointer` 对象看起来像是指针，可以像使用普通指针那样使用它。

4. **实际应用**：
    - `operator->` 重载在智能指针（如 `std::shared_ptr` 和 `std::unique_ptr`）中广泛使用，使得智能指针可以像原始指针一样进行成员访问。
    - 它还可以用于其他封装类，提供一种安全、便捷的访问内部指针的方法。

通过重载 `operator->`，模板类可以增强指针的功能，提供更高层次的抽象，同时保持指针使用的简便性和直观性。

## LoadLibrary执行失败原因
加载动态库依赖的动态库或后续依赖的动态库不存在

## stdafx.h的特殊性
必须第一个#include

## string::data和string::c_str区别
在C++中，`std::string::data()` 和 `std::string::c_str()` 是两个用于获取字符串内部字符数组指针的成员函数。虽然它们看起来类似，但在细节上有一些区别。

### `std::string::data()`
- 返回指向字符串内容的指针。
- 在C++11之前，`data()`返回的指针不是以null终止符（`\0`）结尾的，从C++11开始，`data()`函数和`c_str()`函数的行为一致，返回的字符数组是以`\0`结尾的。
- 从C++17开始，返回的指针类型为 `char*`，可以修改字符串的内容（当然前提是你不是用`const`修饰的字符串对象来调用这个方法）。

### `std::string::c_str()`
- 返回指向以null终止符（`\0`）结尾的字符数组的指针。
- 保证返回的字符数组始终以`\0`结尾，这在需要与C风格字符串兼容时非常重要。
- 返回类型是 `const char*`，因此不能通过它来修改字符串的内容。

### 总结区别
1. **用途不同**：`c_str()`主要用于需要与C API交互的场景，保证返回的字符串是以`\0`终止的。而`data()`更通用，可以用于各种需要字符数组指针的场合。
2. **返回类型不同**：`c_str()`返回`const char*`，不能用于修改字符串内容；而在C++17及之后的版本中，`data()`返回`char*`（对于非`const`的`std::string`对象），允许修改字符串内容。
3. **是否以`\0`结尾**：`c_str()`保证以`\0`结尾；`data()`从C++11开始也是如此，但在此之前的版本中，`data()`返回的字符数组未必以`\0`结尾。

所以，在现代C++（C++11及之后）的编程中，`data()`和`c_str()`的行为几乎是一致的，只是`data()`允许更灵活的操作。

## C++获取已销毁布尔对象的引用会怎么样？
在C++中，获取已销毁布尔对象（或任何对象）的引用会导致**未定义行为（undefined behavior, UB）**。未定义行为意味着程序的行为是不可预测的，可能会表现为以下几种情况：

1. **程序崩溃**：程序可能会因为访问已销毁对象的内存位置而崩溃，这通常会导致段错误（segmentation fault）。

2. **不正确的值**：引用的对象可能会返回垃圾值，因为该内存位置可能已经被其他数据覆盖或重新分配。

3. **数据损坏**：访问已销毁对象可能会导致意外的内存修改，从而损坏数据或引发其他不可预见的问题。

4. **未观察到的行为**：在某些情况下，程序可能会继续运行，但以错误的方式运行。这些错误可能很难调试，因为它们可能不会立即显现。

具体来说，如果你有一个布尔对象`bool myBool`，然后你通过某种方式获取了这个对象的引用`bool& ref = myBool;`，接着销毁了这个对象（例如对象超出了作用域），如果你再使用这个引用`ref`，就会触发未定义行为。

例如：

```cpp
bool* createBool() {
    bool localBool = true;
    return &localBool;  // 返回局部变量的指针
}

int main() {
    bool* ptr = createBool();  // 获取已经销毁的布尔对象的指针
    bool ref = *ptr;  // 解引用这个指针
    std::cout << ref << std::endl;  // 打印的值是未定义的
    return 0;
}
```

在这个例子中，`localBool`在`createBool()`函数返回时已经被销毁。随后在`main()`函数中解引用这个已经销毁的对象将导致未定义行为。

为了避免这种问题，应该确保在访问对象时，它们仍然是有效的，特别是在使用指针和引用时，要格外小心。

## bool初始化问题
在 C++ 中，`bool` 类型的变量是否会被初始化取决于变量的声明位置和是否显式初始化。

1. **局部变量（在函数内部声明的变量）：**
   - 如果你在函数内部声明了一个 `bool` 变量，但没有对它进行显式初始化，那么它的值是未定义的。这意味着它可能持有任何值，无法预测。
   - 示例：
     ```cpp
     void foo() {
         bool myBool;  // 未定义行为，myBool 未初始化
         if (myBool) {
             // 这可能会做任何事情，因为 myBool 的值是未定义的
         }
     }
     ```

2. **全局变量或静态变量：**
   - 如果 `bool` 变量是在全局作用域（函数外部）或是 `static` 关键字修饰的，那么它将被自动初始化为 `false`。
   - 示例：
     ```cpp
     bool myBoolGlobal;  // 自动初始化为 false

     void foo() {
         static bool myBoolStatic;  // 自动初始化为 false
     }
     ```

总结来说：
- **局部变量**（函数内部声明的）：不会自动初始化，需要你显式地赋值。
- **全局变量**和**静态变量**：会自动初始化为 `false`。

## c++自定义构造必须声明默认构造函数吗？

在C++中，如果你定义了一个自定义构造函数，**编译器不会自动生成默认构造函数**。这意味着如果你的类需要一个默认构造函数（即无参数构造函数），你必须显式地声明它。

### 示例解释
```cpp
class MyClass {
public:
    MyClass(int x) { /*...*/ }  // 自定义构造函数
    // MyClass() {}             // 默认构造函数（需要显式声明）
};
```

在上面的代码中，`MyClass`有一个带参数的构造函数。如果你不显式声明一个默认构造函数`MyClass()`，那么你将不能创建没有参数的`MyClass`对象：

```cpp
MyClass obj; // 错误：没有默认构造函数
```

### 何时需要声明默认构造函数
你需要显式声明默认构造函数的情形包括：

1. **需要创建默认构造对象**：例如，容器类如`std::vector`在扩展容量时可能需要使用默认构造函数来初始化新分配的元素。
2. **多重继承**：在多重继承的情况下，基类的默认构造函数可能被隐式调用，除非你提供其他的构造函数。
3. **默认参数设置**：当你需要为某些成员变量设置默认值。

### 解决方法
你可以通过显式定义默认构造函数来解决这个问题：

```cpp
class MyClass {
public:
    MyClass() {}          // 显式声明默认构造函数
    MyClass(int x) { /*...*/ }
};
```

或使用默认的构造函数：

```cpp
class MyClass {
public:
    MyClass() = default;  // 使用编译器生成的默认构造函数
    MyClass(int x) { /*...*/ }
};
```

这样，`MyClass obj;`就可以正常工作了。

## C++默认构造函数可以不声明吗？
是的，C++的默认构造函数可以不声明。如果类中没有用户显式声明任何构造函数，编译器会自动为类生成一个默认构造函数。这个默认构造函数是无参的，执行对象成员的默认初始化。

不过，如果你在类中声明了其他的构造函数（比如带参数的构造函数），但没有声明默认构造函数，那么编译器就不会再自动生成默认构造函数。如果在这种情况下你还想要一个默认构造函数，那么就需要显式地声明它。

举个例子：

```cpp
class MyClass {
public:
    MyClass(int value) { /* 带参数的构造函数 */ }
    // 此时编译器不会为MyClass生成默认构造函数
};

// 如果你希望这个类有一个默认构造函数，你需要显式声明它
class MyClass {
public:
    MyClass() = default; // 声明默认构造函数
    MyClass(int value) { /* 带参数的构造函数 */ }
};
```

总结一下：
- 如果类中没有声明任何构造函数，编译器会自动生成一个默认构造函数。
- 如果类中已经声明了其他构造函数，但没有声明默认构造函数，编译器不会再生成默认构造函数，此时需要手动声明默认构造函数。

## C++写enum class中枚举值如何不写enum class类型？（C++20）
```
enum class Color {
    Red,
    Green,
    Blue
};

using enum Color;

int main() {
    Color color = Red;  // 直接使用枚举值
    return 0;
}
```

## avoid endl
`[CG] SL.io.50`

## 头文件全局作用域不允许使用using namespace
`[CG] SF.7`

## C++17花括号初始化逻辑变更?
`[CG] ES.23`

## 返回值优化 (RVO) 详解
### 返回值优化 (RVO) 详解

**返回值优化 (Return Value Optimization, RVO)** 是C++编译器的一种优化技术，旨在减少对象的拷贝和构造开销。在传统的函数返回值处理中，函数返回的对象可能需要先在函数内部构造一个临时对象，然后再将这个临时对象拷贝或移动到调用者的上下文中。这种过程可能会引入不必要的开销。RVO旨在消除这些不必要的拷贝构造和析构调用，从而提高程序的效率。

### RVO 的工作原理

当一个函数返回一个对象时，RVO允许编译器直接在调用者的栈空间上构造返回的对象，而不是在函数内部构造一个临时对象并将其拷贝或移动到调用者的栈上。

例如，考虑以下代码：

```cpp
#include <string>

std::string createString() {
    std::string temp = "Hello, RVO!";
    return temp;
}

int main() {
    std::string str = createString();
    return 0;
}
```

在传统的处理方式中，`createString`函数会在其内部创建一个临时`std::string`对象，然后返回这个对象。在返回时，可能需要调用`std::string`的拷贝构造函数将临时对象拷贝到调用者的`str`变量中。之后，临时对象被销毁，调用析构函数。

然而，有了RVO，编译器会直接在`str`所在的内存位置上构造返回的字符串对象，而不会创建和拷贝临时对象。这意味着以下步骤：

1. **在调用者的内存位置上**直接构造`temp`对象。
2. 省略了返回时的拷贝或移动操作。

### 编译器支持和强制RVO

大多数现代C++编译器都支持RVO，并且会在符合条件时自动应用这种优化。这些优化通常是隐式的，程序员不需要显式地请求RVO。

C++17引入了**强制RVO (Mandatory RVO)**，这意味着在某些情况下，编译器必须应用RVO。例如，当函数返回一个局部变量时，编译器不再需要检查是否可以进行RVO，而是必须执行。这减少了开发人员的负担，因为他们不必再考虑临时对象的拷贝开销。

### 移动语义与RVO的关系

在C++11引入移动语义后，编译器可以通过移动构造函数进一步优化返回值处理。如果RVO未能应用，编译器可以尝试使用移动构造函数代替拷贝构造函数，从而减少开销。

不过，如果RVO生效，那么移动语义并不会被触发，因为没有临时对象需要移动。RVO直接消除了临时对象的生成，从而使得移动语义也变得不必要。

### 总结

RVO是一种强大的编译器优化技术，极大地提升了函数返回值处理的效率。通过消除不必要的拷贝和移动，RVO减少了性能开销，并在现代C++中得到了广泛的支持和应用。C++17引入的强制RVO进一步提升了代码效率，使得开发者可以更加专注于代码逻辑，而不必担心返回值的性能问题。

## 测量push_back及emplace_back效率差别
```cpp
#include <iostream>
#include <vector>
#include <chrono>

class MyClass {
public:
    int x, y;
    MyClass(int a, int b) : x(a), y(b) {}
};

int main() {
    const int num_elements = 100'000'000;

    // 测试 push_back 的效率
    std::vector<MyClass> vec_push_back;
    auto start_push_back = std::chrono::high_resolution_clock::now();
    for (int i = 0; i < num_elements; ++i) {
        MyClass obj(i, i+1);
        vec_push_back.push_back(obj);
    }
    auto end_push_back = std::chrono::high_resolution_clock::now();
    auto duration_push_back = std::chrono::duration_cast<std::chrono::microseconds>(end_push_back - start_push_back).count();

    // 测试 emplace_back 的效率
    std::vector<MyClass> vec_emplace_back;
    auto start_emplace_back = std::chrono::high_resolution_clock::now();
    for (int i = 0; i < num_elements; ++i) {
        vec_emplace_back.emplace_back(i, i+1);
    }
    auto end_emplace_back = std::chrono::high_resolution_clock::now();
    auto duration_emplace_back = std::chrono::duration_cast<std::chrono::microseconds>(end_emplace_back - start_emplace_back).count();

    std::cout << "push_back duration: " << duration_push_back << " microseconds" << std::endl;
    std::cout << "emplace_back duration: " << duration_emplace_back << " microseconds" << std::endl;

    return 0;
}
```
emplace_back慢一些

相反例子:
```cpp
#include <iostream>
#include <vector>
#include <chrono>

// 定义一个更复杂的类，包含动态内存分配
class MyClass {
public:
    int* data;
    int size;
    
    // 构造函数
    MyClass(int s) : size(s) {
        data = new int[size];
        for (int i = 0; i < size; ++i) {
            data[i] = i;
        }
    }

    // 复制构造函数
    MyClass(const MyClass& other) : size(other.size) {
        data = new int[size];
        std::copy(other.data, other.data + size, data);
    }

    // 移动构造函数
    MyClass(MyClass&& other) noexcept : data(other.data), size(other.size) {
        other.data = nullptr;
        other.size = 0;
    }

    // 析构函数
    ~MyClass() {
        delete[] data;
    }
};

int main() {
    const int num_elements = 10'000;
    const int num_iterations = 10;

    long long total_duration_push_back = 0;
    long long total_duration_emplace_back = 0;

    for (int j = 0; j < num_iterations; ++j) {
        std::vector<MyClass> vec_push_back;
        vec_push_back.reserve(num_elements);  // 预先分配内存
        
        auto start_push_back = std::chrono::high_resolution_clock::now();
        for (int i = 0; i < num_elements; ++i) {
            MyClass obj(1000);  // 使用更复杂的对象
            vec_push_back.push_back(obj);
        }
        auto end_push_back = std::chrono::high_resolution_clock::now();
        total_duration_push_back += std::chrono::duration_cast<std::chrono::microseconds>(end_push_back - start_push_back).count();

        std::vector<MyClass> vec_emplace_back;
        vec_emplace_back.reserve(num_elements);  // 预先分配内存

        auto start_emplace_back = std::chrono::high_resolution_clock::now();
        for (int i = 0; i < num_elements; ++i) {
            vec_emplace_back.emplace_back(1000);  // 直接在容器中构造对象
        }
        auto end_emplace_back = std::chrono::high_resolution_clock::now();
        total_duration_emplace_back += std::chrono::duration_cast<std::chrono::microseconds>(end_emplace_back - start_emplace_back).count();
    }

    std::cout << "Average push_back duration: " << total_duration_push_back / num_iterations << " microseconds" << std::endl;
    std::cout << "Average emplace_back duration: " << total_duration_emplace_back / num_iterations << " microseconds" << std::endl;

    return 0;
}
```

## C++中`int a[]{1,2,3,4}`和`int a[4]{1,2,3,4}`有什么区别？
在C++中，`int a[]{1,2,3,4}` 和 `int a[4]{1,2,3,4}` 都是用于定义和初始化数组的语法，但是它们之间有一些细微的差异。

### 1. `int a[]{1,2,3,4};`
- **数组大小自动推断**：这里使用的是一个没有指定大小的数组初始化器，编译器会根据初始化列表中的元素数量来自动推断数组的大小。
- **数组大小**：在这个例子中，数组的大小将被推断为4，因为初始化列表中有4个元素。
- **示例**：
  ```cpp
  int a[]{1, 2, 3, 4};
  ```
  这相当于定义了一个大小为4的数组`a`，内容为`{1, 2, 3, 4}`。

### 2. `int a[4]{1,2,3,4};`
- **显式指定数组大小**：这里数组的大小是显式指定的，即`4`。
- **数组大小**：即使初始化列表的元素少于指定的大小，数组也会被初始化到指定的大小。多余的元素将被自动初始化为零。如果初始化列表中的元素多于指定的大小，则会导致编译错误。
- **示例**：
  ```cpp
  int a[4]{1, 2, 3, 4};
  ```
  这也定义了一个大小为4的数组`a`，内容为`{1, 2, 3, 4}`。

### 主要区别总结：
- `int a[]{1,2,3,4};`：数组大小是由初始化列表中的元素个数自动推断的。
- `int a[4]{1,2,3,4};`：数组大小是显式指定的，初始化列表中的元素不会影响数组的大小（除非元素多于数组大小，则会导致错误）。

在这两个例子中，由于初始化列表中的元素个数恰好为4，因此两者的效果是一样的，都是创建一个包含4个元素的数组`a`。不过在某些情况下，这两个语法会表现出不同的行为，尤其是在数组大小与初始化列表中的元素数量不一致时。

## 每个声明仅声明一个名称
`[CG]ES.10`

## 处理json中的字符串值
```cpp
#include <iostream>
#include <rapidjson/document.h>
#include <rapidjson/writer.h>
#include <rapidjson/stringbuffer.h>
#include <algorithm>

// 将字符串转换为大写
std::string to_upper(const std::string& str) {
    std::string result = str;
    std::transform(result.begin(), result.end(), result.begin(), ::toupper);
    return result;
}

// 递归处理 JSON 对象
void process_json(rapidjson::Value& value, rapidjson::Document::AllocatorType& allocator) {
    if (value.IsObject()) {
        // 如果是对象，递归处理每一个成员
        for (auto& member : value.GetObject()) {
            process_json(member.value, allocator);
        }
    } else if (value.IsArray()) {
        // 如果是数组，递归处理每一个元素
        for (auto& element : value.GetArray()) {
            process_json(element, allocator);
        }
    } else if (value.IsString()) {
        // 如果是字符串，转换为大写并更新 JSON 值
        std::string upper_str = to_upper(value.GetString());
        value.SetString(upper_str.c_str(), allocator);
    }
}

int main() {
    // 示例 JSON 字符串
    const char* json_str = R"({"name": "john", "age": "30", "city": "new york", "languages": ["english", "french"]})";

    // 解析 JSON 字符串
    rapidjson::Document document;
    if (document.Parse(json_str).HasParseError()) {
        std::cerr << "Error parsing JSON!" << std::endl;
        return 1;
    }

    // 处理 JSON 对象，将所有字符串类型的值转换为大写
    process_json(document, document.GetAllocator());

    // 将修改后的 JSON 输出为字符串
    rapidjson::StringBuffer buffer;
    rapidjson::Writer<rapidjson::StringBuffer> writer(buffer);
    document.Accept(writer);

    std::cout << buffer.GetString() << std::endl;

    return 0;
}
```
## lambda表达式递归调用
在C++中，**lambda表达式**是可以使用递归的，但需要一些特别的技巧。因为C++的lambda表达式默认是匿名的，无法直接通过名称进行自我调用，因此我们需要显式地传递lambda表达式本身作为参数，或者使用其他技巧。

### 方法1：通过参数传递自身

最常见的方式是将lambda表达式定义为接受自身作为参数的一个函数。以下是一个简单的例子，展示了如何使用递归的lambda来实现阶乘函数：

```cpp
#include <iostream>
#include <functional>

int main() {
    // 定义一个递归lambda表达式，用std::function保存它的类型
    std::function<int(int)> factorial = [&](int n) -> int {
        if (n <= 1)
            return 1;
        else
            return n * factorial(n - 1);
    };

    // 测试
    std::cout << "Factorial of 5: " << factorial(5) << std::endl;
    return 0;
}
```

在这个例子中，`factorial` 是一个 `std::function<int(int)>`，我们使用 `std::function` 的原因是它可以存储具有递归调用的lambda表达式。同时，lambda表达式通过捕获外部的 `factorial` 变量实现自我调用。

### 方法2：C++20中的`auto`递归

从C++20开始，可以直接用 `auto` 来推导递归lambda表达式的类型，而无需使用 `std::function`。这样代码可以更加简洁：

```cpp
#include <iostream>

int main() {
    // 递归lambda使用C++20的auto
    auto factorial = [](int n, auto&& self) -> int {
        if (n <= 1)
            return 1;
        else
            return n * self(n - 1, self); // 递归调用自己
    };

    // 调用时需要传递lambda本身
    std::cout << "Factorial of 5: " << factorial(5, factorial) << std::endl;
    return 0;
}
```

在这个C++20的版本中，我们使用了第二个参数 `self` 来显式传递lambda表达式本身，从而实现递归调用。

### 总结

- 在C++11到C++17中，你需要使用 `std::function` 来保存递归lambda表达式。
- 在C++20及之后，可以利用 `auto` 和通用lambda参数来直接实现递归。

## C++模板类T* operator->() const函数是什么意思？
在C++中，`T* operator->() const` 是一个重载的运算符函数，用于让用户自定义类在使用“箭头运算符”（`->`）时表现出特定行为。

### `operator->()`的作用
“箭头运算符”（`->`）通常用于访问指针指向的对象的成员，例如：

```cpp
ptr->member;
```

这里的`ptr`是一个指针，它通过`->`运算符解引用，来访问指向对象的成员。

如果一个类重载了`operator->()`，就可以控制当该类的对象使用`->`时的行为。具体来说，`operator->()`应该返回一个指针类型的对象，以允许对返回对象使用`->`访问成员。

### `T* operator->() const`函数解释
1. **`T*`**: 这是该函数的返回类型，意味着`operator->()`返回一个指向类型`T`的指针。
2. **`operator->()`**: 这是函数名称，表示重载箭头运算符。
3. **`const`**: 这是一个`const`成员函数，意味着该函数不能修改它所操作的对象的状态（即在`const`对象上也可以调用它）。

### 举个例子
考虑一个自定义智能指针类`SmartPointer`，它重载了`operator->()`来模拟原生指针的行为：

```cpp
template<typename T>
class SmartPointer {
private:
    T* ptr; // 内部指向对象的原生指针
public:
    SmartPointer(T* p = nullptr) : ptr(p) {}
    
    // 重载operator->, 返回内部的指针
    T* operator->() const {
        return ptr;
    }

    ~SmartPointer() {
        delete ptr;
    }
};

class Test {
public:
    void display() {
        std::cout << "Test::display()" << std::endl;
    }
};

int main() {
    SmartPointer<Test> sp(new Test());
    sp->display();  // 通过重载的operator->访问Test对象的成员
    return 0;
}
```

### 详细分析
1. `SmartPointer<Test> sp(new Test());` 创建了一个`SmartPointer`类的对象`sp`，它内部持有指向`Test`对象的指针。
2. 当使用`sp->display();`时，编译器会调用`sp`的`operator->()`，该函数返回指向`Test`对象的原生指针。
3. 随后，`->`会作用于返回的指针，进而调用`Test`对象的`display()`函数。

### 总结
`T* operator->() const`函数的主要作用是当类的对象使用“箭头运算符”时，自定义其行为。通常，这个运算符返回一个指针，让调用者能够通过该指针继续访问对象的成员。在智能指针类中，`operator->()`的重载是常见的，用来模拟原生指针的行为。

## chrono用法
```cpp
#include <chrono>
#include <iostream>

using std::cout;
using std::chrono::duration;
using std::chrono::duration_cast;
using std::chrono::milliseconds;
using std::chrono::steady_clock;

#define START_TIMER()                       \
    static auto duration = milliseconds(0); \
    const auto startTime { steady_clock::now() };

#define END_TIMER()                                               \
    const auto endTime { steady_clock::now() };                   \
    duration += duration_cast<milliseconds>(endTime - startTime); \
    cout << __func__ << " use " << duration.count() << " milliseconds\n";

int main()
{
    START_TIMER();

    // do something

    END_TIMER();
}
```
宏函数添加参数可考虑：
```cpp
#define START_TIMER(n)                         \
    static auto duration##n = milliseconds(0); \
    const auto  startTime##n{steady_clock::now()};

#define END_TIMER(n)                                                       \
    const auto endTime##n{steady_clock::now()};                            \
    duration##n += duration_cast<milliseconds>(endTime##n - startTime##n); \
    cout << "duration" << #n << " use " << duration##n.count() << " milliseconds\n";
```

## 默认情况下，把成员函数设为const
CG Con.2
## 默认情况下，将对象赋`const/constexpr[Con.1]`
两个例外
- 函数要返回的对象
- 值传递的参数

## 枚举值不要全大写
Enum.5

## C++什么时候使用命名空间下的函数，什么时候使用类中的静态成员函数？
在C++中，命名空间下的函数和类中的静态成员函数都有各自的适用场景和设计意图。下面详细解释两者在不同情况下的使用选择：

### 1. **命名空间下的函数**
命名空间（`namespace`）的主要目的是**避免命名冲突**。命名空间下的函数通常适用于那些与具体类无关的函数，或者说它们与某一具体对象的状态没有直接关联。

#### 适用场景：
- **工具函数/辅助函数**：如果函数的逻辑不依赖于某个类的成员变量或状态，命名空间是很好的选择。比如，数学库的常用函数（如`sin`、`cos`）就放在标准库的`std::`命名空间中。
- **全局功能**：如果函数在整个项目中是通用的，不依赖于特定对象的状态，使用命名空间可以更好地组织代码。例如，日志系统、文件操作、字符串处理等可以放在一个工具类的命名空间下。
- **模块化设计**：命名空间帮助将功能模块化，便于维护。你可以将不同模块的函数放在不同命名空间下，如`math::add()`、`string::concat()`等。

#### 使用示例：
```cpp
namespace MathUtils {
    int add(int a, int b) {
        return a + b;
    }
}
```

调用方式：
```cpp
int result = MathUtils::add(5, 3);
```

### 2. **类中的静态成员函数**
静态成员函数属于类，但不依赖于具体的实例。它们**可以访问类的静态成员变量**，但不能访问非静态成员变量（因为静态函数不依赖具体对象）。

#### 适用场景：
- **逻辑上属于类的功能**：如果函数逻辑与类紧密关联，但又不依赖于对象实例（比如需要操作静态数据成员或者是对类的某些行为进行封装），静态成员函数是不错的选择。
- **访问类的静态数据成员**：如果一个函数需要访问或修改类的静态成员变量，那么它应该作为类的静态成员函数。
- **工厂模式**：静态成员函数通常用于工厂模式中，用于创建类的对象。
- **单例模式**：单例模式中，静态成员函数通常用于控制类实例的唯一性。

#### 使用示例：
```cpp
class Calculator {
public:
    static int add(int a, int b) {
        return a + b;
    }
};
```

调用方式：
```cpp
int result = Calculator::add(5, 3);
```

### 3. **对比与选择**
- **与类是否相关**：如果函数与类没有强关联，放在命名空间中；如果函数逻辑与类有关联，特别是与类的静态数据或功能相关，那么应该放在类的静态成员函数中。
- **功能归属**：命名空间适用于模块级的划分，而静态成员函数更适用于类内部的功能封装。
- **代码可读性**：如果一个函数属于某类的核心逻辑，将其作为静态成员函数可以提高代码的可读性，使得逻辑清晰。而如果函数与类关系不大，放在命名空间中可以避免不必要的类耦合。

### 4. **命名空间下的函数和静态成员函数的常见误区**
- **不要滥用静态成员函数**：并非所有与类相关的功能都需要作为静态成员函数，如果函数实际上不依赖类的状态，考虑使用命名空间。
- **命名空间也可以包含类**：命名空间不仅可以包含函数，也可以包含类。可以将类和函数都归类到同一个命名空间中以实现模块化的代码组织。

### 5. **组合使用的场景**
有时可以组合使用命名空间和静态成员函数。例如，创建一个与某个功能模块相关的命名空间，其中包含多个类，而这些类的某些静态成员函数实现具体的功能。

### 总结
- **命名空间下的函数**：适用于与类无关的全局函数，通常用于工具类、辅助函数或模块化设计。
- **类的静态成员函数**：适用于与类逻辑相关、但不依赖于对象实例的函数，通常用于访问类的静态成员变量、工厂函数、单例模式等。

通过合理使用命名空间和静态成员函数，能够提高代码的组织性、可维护性和可读性。

## 不要给命名空间std加东西
SL.3

## C++中查找容器中是否有某个元素，一般用哪个容器？
在 C++ 中，查找容器中是否有某个元素的效率和方便性取决于容器的类型。不同的容器在查找操作上有不同的表现：

1. **`std::set` 和 `std::unordered_set`**:
   - 如果查找是常见操作，且对元素不需要顺序存储，推荐使用这些容器。
   - **`std::set`** 是基于平衡二叉树（通常是红黑树）实现的，查找的时间复杂度是 O(log n)。
   - **`std::unordered_set`** 是基于哈希表实现的，查找的时间复杂度是平均 O(1)（最坏情况下为 O(n)，取决于哈希冲突的处理）。

   **示例：**
   ```cpp
   #include <set>
   #include <unordered_set>

   std::set<int> s = {1, 2, 3, 4};
   if (s.find(3) != s.end()) {
       // 元素 3 存在
   }

   std::unordered_set<int> us = {1, 2, 3, 4};
   if (us.find(3) != us.end()) {
       // 元素 3 存在
   }
   ```

2. **`std::vector`**:
   - 如果容器是 `std::vector`，可以使用标准库算法 `std::find` 进行查找，时间复杂度为 O(n)。
   
   **示例：**
   ```cpp
   #include <vector>
   #include <algorithm>

   std::vector<int> v = {1, 2, 3, 4};
   if (std::find(v.begin(), v.end(), 3) != v.end()) {
       // 元素 3 存在
   }
   ```

3. **`std::map` 和 `std::unordered_map`**:
   - 这两个容器用于存储键值对。如果你需要查找某个键是否存在，使用 `std::map` 或 `std::unordered_map` 非常高效。
   - **`std::map`** 的查找时间复杂度是 O(log n)。
   - **`std::unordered_map`** 的查找时间复杂度是 O(1)（平均情况）。

   **示例：**
   ```cpp
   #include <map>
   #include <unordered_map>

   std::map<int, int> m = {{1, 10}, {2, 20}, {3, 30}};
   if (m.find(2) != m.end()) {
       // 键 2 存在
   }

   std::unordered_map<int, int> um = {{1, 10}, {2, 20}, {3, 30}};
   if (um.find(2) != um.end()) {
       // 键 2 存在
   }
   ```

### 总结：
- **快速查找**：如果需要快速查找某个元素，建议使用 **`std::unordered_set`** 或 **`std::unordered_map`**。
- **顺序敏感**：如果元素有顺序，或者不介意 O(n) 的查找开销，可以使用 **`std::vector`** 和 `std::find`。
- **有序数据结构**：如果需要有序存储并支持高效查找，使用 **`std::set`** 或 **`std::map`**。

## all_of/any_of/none_of
https://en.cppreference.com/w/cpp/algorithm/all_any_none_of

## 计时测试宏迭代
```cpp
#include <chrono>
#include <iostream>

using std::cout;
using namespace std::chrono;

#define START_TIMER(n) \
    INIT_TIMER(n)      \
    START_TIMER_NINIT(n);

#define END_TIMER(n)   \
    END_TIMER_NCOUT(n) \
    COUT_TIMER(n)

#define END_TIMER_NCOUT(n)                                                \
    const auto endTime##n { steady_clock::now() };                        \
    duration##n += duration_cast<nanoseconds>(endTime##n - startTime##n); \
    START_TIMER_NINIT(n##l);                                              \
    const auto endTime##n##l { steady_clock::now() };                     \
    duration##n -= duration_cast<nanoseconds>(endTime##n##l - startTime##n##l);

#define COUT_TIMER(n)                                                           \
    cout << __func__ << ' ' << #n << " use " << duration##n.count() / 1'000'000 \
         << " milliseconds\n";

#define INIT_TIMER(n) static auto duration##n = nanoseconds(0);

#define START_TIMER_NINIT(n) const auto startTime##n { steady_clock::now() };
```
非宏函数形式
```cpp
#include <chrono>
#include <iostream>

using std::cout;
using namespace std::chrono;

class Timer {
public:
    Timer()
        : duration(nanoseconds(0))
    {
    }

    // 开始计时
    void start()
    {
        startTime = steady_clock::now();
    }

    // 结束计时但不输出
    void end_no_output()
    {
        auto endTime = steady_clock::now();
        duration += duration_cast<nanoseconds>(endTime - startTime);

        // 二次计时修正
        auto startTime_l = steady_clock::now();
        auto endTime_l = steady_clock::now();
        duration -= duration_cast<nanoseconds>(endTime_l - startTime_l);
    }

    // 输出计时结果
    void output(const char* funcName, int timerNo) const
    {
        cout << funcName << ' ' << timerNo << " use " << duration.count() / 1'000'000 << " milliseconds\n";
    }

    // 结束计时并输出
    void end(const char* funcName, int timerNo)
    {
        end_no_output();
        output(funcName, timerNo);
    }

private:
    steady_clock::time_point startTime;
    nanoseconds duration;
};

// 用法示例
void example()
{
    Timer timer1;

    // 开始计时
    timer1.start();

    // 结束计时并输出结果
    timer1.end(__func__, 1);
}

int main()
{
    example();
    return 0;
}

```
