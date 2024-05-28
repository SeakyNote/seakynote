## c++中，到底什么是对象？

 C++ programmers tend to refer to variables as “variables” or “objects” interchangeably.

Most generally, an object is a region of memory that can contain data and has a type.

Some use the term object only to refer to variables or values of class types.

Others distinguish between named and unnamed objects, using the term variable to refer to named objects.

object: A region of memory that has a type. A variable is an object that has a name. 

## c++创建对象的三种方式 

https://www.bilibili.com/read/cv10416320/

## 函数传参：指针vs引用

https://stackoverflow.com/questions/114180/pointer-vs-reference

Use pointers if you want to do pointer arithmetic with them (e.g. incrementing the pointer address to step through an array) or if you ever have to pass a NULL-pointer.

Use references otherwise.

## 枚举只对第一个赋值

后面依次累加

## enum/enum class

在C++中，`enum` 和 `enum class` 都用于定义枚举类型，但它们有一些重要的区别。

1. `enum`:
   - 在传统的 `enum` 中，枚举值是在同一个命名空间下的，因此存在命名冲突的风险。
   - `enum` 中的枚举值可以直接被隐式转换为整数，并且在同一作用域内的枚举类型之间可以进行隐式转换。

示例：
```cpp
enum Color {
    RED,
    GREEN,
    BLUE
};
```

2. `enum class`:
   - `enum class` 是在C++11中引入的，它引入了新的作用域规则，枚举值在枚举类型的作用域内，因此不会造成命名冲突。
   - `enum class` 中的枚举值不会被隐式转换为整数，需要显式转换为整数类型。
   - `enum class` 提供了更强的类型安全性，并且不会污染命名空间。

示例：
```cpp
enum class Color {
    RED,
    GREEN,
    BLUE
};
```

总结来说，使用 `enum class` 更加安全，因为它提供了更严格的作用域规则和类型安全性，而传统的 `enum` 则在使用时需要更加小心以避免命名冲突和意外的隐式转换。

## 基类构造函数调用虚函数问题

https://blog.csdn.net/tax10240809163com/article/details/122691584

## C++中为什么写派生类头文件时对基类不能前置声明而必须包含头文件？

在C++中，派生类的头文件需要包含基类的头文件，而不能只使用前置声明来引用基类。这是因为派生类需要知道基类的具体定义，以便正确地继承基类的成员变量和成员函数。

当你在派生类中包含基类的头文件时，编译器可以确保基类的定义是可用的，并且可以正确地分析派生类与基类之间的关系。这样可以确保派生类能够正确地访问基类的成员，以及正确地重载或覆盖基类的成员函数。

如果只使用前置声明而不包含基类的头文件，编译器在处理派生类时将无法确定基类的具体结构，这样就会导致编译错误或者在链接时出现问题。

因此，为了确保派生类能够正确地继承基类的成员和行为，必须在派生类的头文件中包含基类的头文件。

## 简要谈谈C++继承中派生类的 构造 拷贝 赋值 析构的调用问题

https://blog.csdn.net/m0_46606290/article/details/123994641

## C++避坑：基类函数有无virtual关键字，差别巨大

https://blog.csdn.net/qq_23418043/article/details/126316239

## protected（保护）访问权限

https://blog.csdn.net/weixin_46060711/article/details/123932852

## C++多态

https://www.runoob.com/cplusplus/cpp-polymorphism.html

https://blog.csdn.net/zhang_si_hang/article/details/126173598

## c++中重载，重写，覆盖

https://www.cnblogs.com/tianzeng/p/9775672.html

https://blog.csdn.net/JachinYang/article/details/117442902

### Overload（重载）

函数重载（Function Overloading）是指在一个类中定义多个同名函数，但它们的参数列表不同。编译器根据函数的参数列表来唯一标识每个函数，并根据调用时的实参来选择调用哪个函数。函数重载通常用于解决类似但参数不同的问题，提高代码的复用性。

可以定义两个同名的add函数，一个是两个整数相加，另一个是两个浮点数相加

### Override（覆盖）

函数覆盖（Function Overriding）是指在派生类中定义与基类中同名同参数的虚函数，以覆盖（替代）基类的虚函数。派生类的虚函数调用时会优先调用自己重写的虚函数，而基类的虚函数会被忽略。

函数覆盖通常用于实现多态性（Polymorphism），让不同的派生类对象调用同一个虚函数，却产生不同的行为。需要注意的是，只有虚函数才能被覆盖，而且派生类重写基类虚函数的参数列表和返回类型必须相同。

例如，可以定义一个Shape基类，包含纯虚函数calcArea，来计算形状的面积；然后在Circle和Rectangle派生类中分别实现自己的calcArea函数，覆盖Shape基类的虚函数

------

同一个类的同名函数不同参数列表：重载
基类和派生类中的函数，基类函数是虚函数，派生类函数与基类函数名称与参数列表完全相同：覆盖
派生类函数与基类函数名称与参数列表完全相同，但是基类函数不是虚函数：隐藏
派生类函数与基类函数名称相同但是参数列表不同，无论基类函数是不是virtual：隐藏。

## c++ 中*&的应用

https://blog.csdn.net/weixin_45650172/article/details/105080470

## const_cast

https://www.cnblogs.com/xiangtingshen/p/10851245.html

## c++中dynamic_cast和static_cast在转换指针后是否应判断下是否为空再使用？

在C++中，使用`dynamic_cast`和`static_cast`进行指针转换后，通常需要根据具体情况来判断是否为空再使用。这取决于转换的类型和转换后的使用方式。

1. `dynamic_cast`：
   - 当使用`dynamic_cast`进行指针转换时，如果转换失败（即指针指向的对象类型不匹配），`dynamic_cast`将返回一个空指针（nullptr）。
   - 因此，在使用`dynamic_cast`进行指针转换后，应该始终检查返回的指针是否为空，以确保转换成功，然后再使用转换后的指针。

   ```cpp
   Base* basePtr = new Derived;
   Derived* derivedPtr = dynamic_cast<Derived*>(basePtr);
   if (derivedPtr) {
       // 转换成功，可以安全地使用 derivedPtr
   } else {
       // 转换失败，derivedPtr 为空，不能安全地使用
   }
   ```

2. `static_cast`：
   - 使用`static_cast`进行指针转换时，编译器不会进行运行时类型检查，因此无法保证转换的安全性。如果进行了不安全的类型转换，程序可能会出现未定义的行为。
   - 由于`static_cast`不提供运行时类型检查，转换后的指针不会为空。因此，在使用`static_cast`进行指针转换后，不需要检查返回的指针是否为空。

   ```cpp
   Base* basePtr = new Base;
   Derived* derivedPtr = static_cast<Derived*>(basePtr);
   // 不需要检查 derivedPtr 是否为空
   // 但是需要确保转换的安全性
   ```

总之，在使用`dynamic_cast`进行指针转换后，需要检查返回的指针是否为空，以确保转换的安全性。而在使用`static_cast`进行指针转换后，不需要检查返回的指针是否为空，但需要确保转换的安全性。

## 派生类转化为基类可以直接转吗？还是要通过static_cast?

在C++中，派生类转化为基类可以直接进行，因为派生类对象中包含了基类对象的部分。这种转换被称为向上转换（upcasting），它是隐式的，不需要使用任何显式的类型转换操作符。因此，你可以直接将派生类的对象指针或引用赋值给基类的指针或引用。

举个例子：

```cpp
class Base {
    // ...
};

class Derived : public Base {
    // ...
};

int main() {
    Derived derivedObj;
    Base& baseRef = derivedObj; // 向上转换，无需显式转换
    Base* basePtr = &derivedObj; // 向上转换，无需显式转换
    return 0;
}
```

然而，如果你想在编码时显式地表明你正在进行向上转换，你可以使用`static_cast`，但这不是必需的。

```cpp
Derived derivedObj;
Base& baseRef = static_cast<Base&>(derivedObj); // 显式使用 static_cast 进行向上转换
Base* basePtr = static_cast<Base*>(&derivedObj); // 显式使用 static_cast 进行向上转换
```

需要注意的是，向上转换是安全的，因为派生类对象包含了基类对象的部分。但是，向下转换（从基类指针或引用到派生类指针或引用）是不安全的，因为基类对象可能不包含派生类对象的所有部分。在这种情况下，你应该使用`dynamic_cast`，它会在运行时检查转换的合法性。

## c++中将空指针dynamic_cast会有问题吗？

在C++中，使用`dynamic_cast`对空指针进行类型转换是安全的。`dynamic_cast`会在运行时检查指针所指向的对象的实际类型，并进行相应的转换。如果指针是空指针，`dynamic_cast`会返回空指针，而不会引发任何异常或错误。

例如：

```cpp
#include <iostream>

class Base {
public:
    virtual void foo() {
        std::cout << "Base::foo()" << std::endl;
    }
};

class Derived : public Base {
public:
    void bar() {
        std::cout << "Derived::bar()" << std::endl;
    }
};

int main() {
    Base* basePtr = nullptr;
    Derived* derivedPtr = dynamic_cast<Derived*>(basePtr);
    if (derivedPtr == nullptr) {
        std::cout << "dynamic_cast returned nullptr for a null pointer" << std::endl;
    }
    return 0;
}
```

在上面的示例中，`dynamic_cast`会安全地将空指针`basePtr`转换为`Derived*`类型的指钝`derivedPtr`，并且`derivedPtr`会被设置为`nullptr`。

因此，对于空指针使用`dynamic_cast`是安全的，不会导致任何问题。

## switch语句中必须有default选项吗？

switch语句中不是必须有default选项的。switch语句首先会找满足条件的case值做为执行后面的程序入口，若所有的case都不满足，则找default入口，若未找到则退出整个语句；default只是一个备用入口，有没有都无所谓。

## NULL/nullptr

在C++中，nullptr 是 C++11 标准引入的空指针常量，它是一种特定类型的字面值，可以隐式转换为任意指针类型，而 NULL 则通常被定义为整数 0。nullptr 相比 NULL 有以下几个优势：

1. 类型安全：nullptr 是一种特定的类型，可以隐式转换为任意指针类型，因此在类型安全性上优于 NULL。这意味着在使用 nullptr 时，编译器可以帮助检测指针类型不匹配的错误。

2. 易读性：nullptr 明确表示空指针，而 NULL 可能被定义为整数 0，可能会引起歧义。nullptr 的使用可以使代码更加清晰易懂。

下面是一个简单的例子，说明了 nullptr 相对于 NULL 的优势：

```cpp
#include <iostream>

void foo(char* ptr) {
    std::cout << "Function taking char* pointer\n";
}

void foo(int value) {
    std::cout << "Function taking int value\n";
}

int main() {
    foo(NULL); // 可能会引起歧义，因为NULL可能被定义为整数0
    foo(nullptr); // 明确表示空指针常量，不会引起歧义

    return 0;
}
```

在上面的例子中，如果使用 NULL 调用 foo 函数，可能会引起歧义，因为 NULL 可能被定义为整数 0，导致调用了不希望调用的函数。而使用 nullptr 则能够明确表示空指针，避免了这种歧义。

## 断言assert()函数的使用

https://blog.csdn.net/sanqima/article/details/40832875

## iostream vs stdio

https://www.cnblogs.com/Solstice/archive/2011/07/17/2108715.html

## malloc vs new

https://stackoverflow.com/questions/184537/in-what-cases-do-i-use-malloc-and-or-new

## 异常还是错误码

https://stackoverflow.com/questions/253314/conventions-for-exceptions-or-error-codes

## c++栈区、堆区

https://blog.csdn.net/jinking01/article/details/88675935

## 短路规则

https://blog.csdn.net/m0_57781693/article/details/129776811

## 模板类与前置声明

在C++中，vector是标准库中的一个模板类，它需要在使用之前进行实例化，而实例化需要知道模板类的定义。因此，如果你想在代码中使用vector，就需要包含<vector>头文件以便编译器能够找到vector模板类的定义。

C++中的模板类在使用时需要进行实例化，而实例化需要知道模板类的定义，包括其成员函数和成员变量。如果你尝试对一个模板类进行前置声明而不包含相应的头文件，编译器将无法确定模板类的具体定义，因此会导致编译错误。

因此，为了能够正确地使用vector，你必须包含<vector>头文件，以便编译器能够找到并使用vector模板类的定义。

## c++中类的成员变量应设为public还是提供方法去读写？

在 C++ 中，类的成员变量应该根据封装的原则进行设计。封装是面向对象编程中的重要概念，它可以帮助控制对类的成员变量的访问和修改。

一般来说，最好将类的成员变量设为私有（private），并提供公共的方法（成员函数）来读取（get）和设置（set）这些成员变量的值。这种方式可以提供更好的封装性，以及更好的控制和安全性。

例如，对于一个名为 `Person` 的类，可以这样设计：

```cpp
class Person {
private:
    std::string name;
    int age;

public:
    // 公共方法用于读取成员变量的值
    std::string getName() const {
        return name;
    }

    int getAge() const {
        return age;
    }

    // 公共方法用于设置成员变量的值
    void setName(const std::string& newName) {
        name = newName;
    }

    void setAge(int newAge) {
        age = newAge;
    }
};
```

这样设计的好处是，可以控制对成员变量的访问，同时在必要的时候可以添加一些逻辑来确保成员变量的合法性。

当然，并不是所有成员变量都需要通过公共方法进行读写，有些情况下，成员变量可以直接设为公共的（public），这通常用于一些非敏感的数据结构或者为了方便访问而设计的数据成员。

## 介绍下C++中的友元类

在C++中，友元类是一种特殊的类关系，允许一个类的成员函数或整个类访问另一个类的私有或受保护成员。通过将一个类声明为另一个类的友元，可以在友元类中访问该类的私有成员，从而实现更灵活的数据封装和访问控制。

要声明一个类为另一个类的友元，可以在类的定义中使用 `friend` 关键字。例如：

```cpp
class B; // 前向声明类B

class A {
public:
    friend class B; // 声明B为A的友元类
private:
    int privateData;
};
```

在上面的例子中，类A声明了类B为友元类，这意味着类B的成员函数可以访问类A的私有成员。

下面是一个更完整的示例，演示了如何使用友元类：

```cpp
class B; // 前向声明类B

class A {
public:
    A(int data) : privateData(data) {}

    friend class B; // 声明B为A的友元类

private:
    int privateData;
};

class B {
public:
    void accessA(A& a) {
        // 友元类B可以访问类A的私有成员privateData
        std::cout << "B accessing A's private data: " << a.privateData << std::endl;
    }
};

int main() {
    A objA(5);
    B objB;
    objB.accessA(objA); // B通过友元关系访问A的私有成员
    return 0;
}
```

在上面的示例中，类B被声明为类A的友元类，因此类B的成员函数`accessA`可以访问类A的私有成员`privateData`。

需要注意的是，友元关系是单向的，即如果类A声明类B为友元类，那么只有类B可以访问类A的私有成员，反之不成立。友元关系打破了类的封装性，因此应该谨慎使用，以避免破坏类的封装和数据隐藏原则。

## c++版本

![](cppConcepts.assets/cpp-v.png)

`__cplusplus` 是一个预定义的宏，用于在 C++ 程序中表示编译器所遵循的 C++ 标准的版本号。这个宏的值是一个整数，代表编译器所遵循的 C++ 标准的年份。通过检查 `__cplusplus` 的值，可以在代码中进行条件编译，以确保代码在不同版本的 C++ 标准下能够正确编译和执行。

例如，C++98 标准中，`__cplusplus` 的值为 199711；C++11 中，值为 201103；C++14 中，值为 201402；C++17 中，值为 201703；C++20 中，值为 202002。

这个宏通常用于在代码中进行条件编译，以便根据不同的 C++ 标准版本采取不同的行为或使用不同的语言特性，从而确保代码的兼容性和可移植性。

## c++中的vector应该怎么翻译成中文？

在C++中，"vector" 通常被翻译为 "向量" 或 "动态数组"。这两个翻译都是比较常见的，具体选择取决于上下文和你的偏好。一般而言，"向量"更接近其数学含义，而"动态数组"更直观地描述了其在编程中的作用。因此，你可以根据具体情境选择适合的翻译。