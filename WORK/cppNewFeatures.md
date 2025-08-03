## Often

* long long
* list initialization
  + int num{1}; 
  + `vector<int> vec{1,2,3};`
* nullptr
* alias declaration
  + using AA = BB; 
* auto
* range for
* emplace/emplace_front/emplace_back
* to_string/stoi/stod
* lambda expression
* unordered_map/unordered_set
* shared_ptr/unique_ptr/weak_ptr
* =delete
* explicit
* override
* final
* enum class
* Forward Declarations for Enumerations

## Normal

* constexpr & constexpr function
* decltype
* in-class initializer
  + https://blog.csdn.net/m0_57168310/article/details/126746229
* cbegin/cend
* iterator begin/end (get begin&end for array)
* sizeof XXXCls::member
* initializer_list
* `int (*func(int i))[10];` equals `auto func(int i)->int(*)[10];`
* = default
* delegating constructor
* constexpr constructor
* array/forward_list
* std::swap
* shrink_to_fit
* bind
* std::move
* rvalue reference
* tuple
* bitset

## Rare

* move constructor/move-assignment operator
* move iterator
* reference qualifier &/&&
* `function<T>`
* inherited constructor(using Base:: Base)
* extern template
* Reference Collapsing
* std::forward
* variadic template
* sizeof...
* regex
* default_random_engine
* hexfloat/defaultfloat
* noexcept
* inline namespace
* enum XXX:type
* mem_fn

## weak_ptr

在C++中， `weak_ptr` 是一种智能指针类型，定义在 `std` 命名空间中，属于 C++11 标准库的一部分。它通常与 `std::shared_ptr` 一起使用，解决了对象间循环引用的问题。

### 1. `weak_ptr` 的基本概念

`weak_ptr` 是一种不控制对象生命周期的智能指针，它不会增加对象的引用计数。它的主要作用是为避免循环引用（circular reference）而设计的。当两个对象互相持有 `shared_ptr` 时，就会出现循环引用，导致对象无法被释放，造成内存泄漏。使用 `weak_ptr` 可以打破这种循环引用。

### 2. 主要特点

* **不拥有对象：** `weak_ptr` 并不会影响所指向对象的生命周期，也就是说，`weak_ptr` 不会增加 `shared_ptr` 的引用计数。
* **检测对象存活：** 通过 `weak_ptr`，你可以检查对象是否仍然有效（即它是否已被 `shared_ptr` 销毁）。这可以通过 `expired()` 方法或将 `weak_ptr` 转换为 `shared_ptr` 来实现。
* **防止循环引用：** 在某些复杂的对象关系中，使用 `weak_ptr` 可以防止 `shared_ptr` 之间的循环引用。

### 3. 主要操作

#### 创建 `weak_ptr`

`weak_ptr` 通常是通过一个现有的 `shared_ptr` 来构造的。例如：

```cpp
#include <iostream>
#include <memory>

int main() {
    std::shared_ptr<int> sp = std::make_shared<int>(42);
    std::weak_ptr<int> wp = sp;  // wp 是指向 sp 的弱引用

    return 0;
}
```

#### 检查对象是否仍然存在

`weak_ptr` 提供了 `expired()` 方法来检查所引用的对象是否已被销毁：

```cpp
if (wp.expired()) {
    std::cout << "对象已被销毁" << std::endl;
} else {
    std::cout << "对象仍然存在" << std::endl;
}
```

#### 锁定 `weak_ptr`

可以通过 `lock()` 方法将 `weak_ptr` 转换为 `shared_ptr` ，并访问对象。如果对象已经被销毁， `lock()` 会返回一个空的 `shared_ptr` ：

```cpp
std::shared_ptr<int> sp2 = wp.lock();
if (sp2) {
    std::cout << "对象值: " << *sp2 << std::endl;
} else {
    std::cout << "对象已被销毁" << std::endl;
}
```

#### 循环引用问题示例

假设有两个类 `A` 和 `B` ，它们相互持有对方的指针，且都使用 `shared_ptr` 。这样会造成循环引用，导致内存泄漏：

```cpp
#include <iostream>
#include <memory>

struct B;  // 前向声明

struct A {
    std::shared_ptr<B> ptrB;
    ~A() { std::cout << "A 被销毁" << std::endl; }
};

struct B {
    std::shared_ptr<A> ptrA;
    ~B() { std::cout << "B 被销毁" << std::endl; }
};

int main() {
    std::shared_ptr<A> a = std::make_shared<A>();
    std::shared_ptr<B> b = std::make_shared<B>();
    a->ptrB = b;
    b->ptrA = a;  // 循环引用

    return 0;  // A 和 B 都不会被销毁，导致内存泄漏
}
```

解决这个问题，可以将 `ptrA` 或 `ptrB` 改为 `weak_ptr` ，从而打破循环引用：

```cpp
struct B {
    std::weak_ptr<A> ptrA;  // 使用 weak_ptr 解决循环引用
    ~B() { std::cout << "B 被销毁" << std::endl; }
};
```

### 4. `weak_ptr` 的应用场景

* **防止循环引用：** 这是 `weak_ptr` 最典型的使用场景。当两个或多个对象需要互相引用时，使用 `weak_ptr` 可以打破循环，防止内存泄漏。
* **缓存系统：** 在某些缓存系统中，`weak_ptr` 可以用来避免缓存对象占用不必要的资源。缓存中的对象如果不再被外部持有，就可以自动释放。
* **观察者模式（Observer Pattern）：** 在实现观察者模式时，观察者通常使用 `weak_ptr` 观察被观察对象，防止因为观察者持有 `shared_ptr` 导致被观察对象无法销毁。

### 5. 总结

`std::weak_ptr` 是 C++ 中解决对象间循环引用的关键工具，它可以与 `std::shared_ptr` 结合使用，在不增加引用计数的前提下提供对对象的非拥有式访问。通过 `weak_ptr` ，程序员可以安全地检查对象的存活状态，防止内存泄漏。

## 右值引用

在C++中，右值引用（rvalue reference）是C++11引入的重要特性，它主要用于**移动语义**和**完美转发**，从而提高程序的效率，特别是在涉及大对象的情况下。

### 1. **左值与右值的概念**

* **左值（lvalue）**：表示可以取地址的对象，比如变量、数组元素等，生命周期通常较长。
* **右值（rvalue）**：表示临时对象，通常是表达式的结果，生命周期短，例如字面量和临时变量。

### 2. **右值引用的语法**

右值引用通过 `&&` 符号声明。例如：

```cpp
int &&rval_ref = 10;
```

`rval_ref` 是一个右值引用，它可以绑定到右值 `10` 上。

### 3. **右值引用的作用**

#### 3.1 **移动语义（Move Semantics）**
移动语义允许将资源（如内存、文件句柄等）从一个对象移动到另一个对象，而不进行深拷贝，从而提升性能，特别是在处理大数据对象时。

**示例：**

```cpp
#include <vector>
#include <iostream>

class MyClass {
public:
    std::vector<int> data;

    // 构造函数
    MyClass(size_t size) : data(size) {
        std::cout << "Constructed" << std::endl;
    }

    // 移动构造函数
    MyClass(MyClass&& other) noexcept : data(std::move(other.data)) {
        std::cout << "Moved" << std::endl;
    }

    // 复制构造函数
    MyClass(const MyClass& other) : data(other.data) {
        std::cout << "Copied" << std::endl;
    }
};

int main() {
    MyClass obj1(1000);  // 构造
    MyClass obj2 = std::move(obj1);  // 移动
    return 0;
}
```

在这个示例中， `std::move(obj1)` 将 `obj1` 转化为右值，从而调用移动构造函数，这样 `obj1` 的资源就被移动到 `obj2` ，避免了深拷贝。

#### 3.2 **避免不必要的拷贝**

右值引用的另一个主要用途是避免不必要的拷贝，尤其是在函数返回临时对象时，可以通过右值引用直接将临时对象的资源移动到目标对象，而不是进行拷贝。

**示例：**

```cpp
std::vector<int> createVector() {
    std::vector<int> temp(1000);
    return temp;  // 返回临时对象
}

int main() {
    std::vector<int> vec = createVector();  // 使用移动语义
}
```

在C++11之前，返回值会触发拷贝构造函数，而现在通过右值引用，编译器可以将返回值优化为移动操作，避免性能损失。

#### 3.3 **完美转发（Perfect Forwarding）**

右值引用还可以用于模板中的**完美转发**，即可以精确地将左值或右值参数传递给其他函数，避免不必要的拷贝或移动操作。

**示例：**

```cpp
template<typename T>
void wrapper(T&& arg) {
    func(std::forward<T>(arg));  // 根据T的类型选择左值或右值传递
}
```

`std::forward` 根据参数类型选择性地将左值保持为左值，将右值保持为右值，实现完美转发。

### 4. **总结**

右值引用在C++中有以下几个主要作用：
1. **移动语义**：将资源从一个对象移动到另一个对象，避免不必要的拷贝，显著提升效率。
2. **避免不必要的拷贝**：通过移动临时对象的资源，优化函数返回值等操作。
3. **完美转发**：在模板编程中准确保留参数的类型特性，避免多余的拷贝或移动。

右值引用的引入使得C++在处理大对象或复杂数据结构时，能够提供更高效的性能和资源管理。

## 右值引用与转发引用

在C++中，**右值引用**（rvalue reference）和**转发引用**（forwarding reference，也称为万能引用，universal reference）是两个重要的特性，它们虽然都使用了 `&&` 符号，但在语义和使用场景上有所不同。下面我们分别介绍它们的概念和作用，并分析它们的区别。

### 1. **右值引用（Rvalue Reference）**

#### 1.1 定义
右值引用是C++11引入的一种引用类型，用于绑定到**右值**（即临时对象，如字面量或表达式结果）。右值引用通过 `&&` 符号声明，主要用于**移动语义**，从而避免深拷贝。

#### 1.2 用法

右值引用常用于实现**移动构造函数**和**移动赋值操作符**，通过移动语义来优化性能。

```cpp
int &&rval_ref = 10; // rval_ref 是一个右值引用，可以绑定到右值 10
```

#### 1.3 移动语义

移动语义允许从一个对象“移动”资源到另一个对象，而不进行深拷贝。右值引用的主要作用是在移动构造和移动赋值中提升性能，尤其是当涉及大量资源（如内存、文件句柄等）时。

示例：

```cpp
class MyClass {
public:
    std::vector<int> data;

    // 移动构造函数
    MyClass(MyClass&& other) noexcept : data(std::move(other.data)) {
        // 移动构造，将 other 的 data 移动到当前对象
    }
};
```

在上述示例中， `MyClass` 的移动构造函数使用右值引用来避免不必要的深拷贝。

#### 1.4 注意点

* 右值引用只能绑定右值，不能绑定左值。
* 右值引用与`std::move`搭配使用时，可以将左值强制转化为右值，方便资源的移动。

---

### 2. **转发引用（Forwarding Reference）**

#### 2.1 定义
转发引用是一种特殊形式的引用，它出现在**模板函数**中，表示可以接受**任意类型的参数**（左值或右值）。转发引用也是通过 `&&` 符号表示的，但它的行为取决于传入的参数类型。

#### 2.2 用法

转发引用的典型场景是**完美转发**，即能够精确地将传递给模板函数的参数类型（左值或右值）传递给其他函数，而不会丢失参数的左值或右值属性。

```cpp
template <typename T>
void func(T&& arg) {
    // arg 是一个转发引用，可以是左值或右值
}
```

这里的 `T&&` 是转发引用，它能够根据传入参数的类型自动调整为左值引用或右值引用。

#### 2.3 完美转发

完美转发通过 `std::forward` 实现，它确保在模板函数中，左值仍然作为左值，右值保持为右值，避免不必要的拷贝或移动操作。

```cpp
template <typename T>
void wrapper(T&& arg) {
    func(std::forward<T>(arg)); // 精确转发 arg，保持其左值或右值属性
}
```

#### 2.4 注意点

* 转发引用只有在**模板**上下文中才会是万能引用。
* 转发引用通过模板参数推导，能够推导出参数的具体类型（左值或右值）。

---

### 3. **右值引用与转发引用的区别**

虽然右值引用和转发引用在语法上都使用 `&&` ，但它们的语义和用法有显著的不同：

| **特性**         | **右值引用**                       | **转发引用**                                      |
|------------------|------------------------------------|---------------------------------------------------|
| **使用场景**     | 主要用于移动语义                  | 主要用于完美转发                                  |
| **绑定对象**     | 只能绑定右值                       | 可以绑定左值或右值                                |
| **类型推导**     | 没有模板上下文时只能绑定右值       | 依赖模板参数推导，可以是左值引用或右值引用        |
| **语法**         | `Type&&` | `T&&` （模板参数）                                 |
| **常用配合**     | `std::move` | `std::forward` |

---

### 4. **示例对比**

#### 4.1 右值引用示例

```cpp
void process(MyClass&& obj) {
    // obj 是一个右值引用，只能接受右值
}

int main() {
    MyClass a;
    process(std::move(a));  // 通过 std::move 强制将 a 转化为右值
}
```

#### 4.2 转发引用示例

```cpp
template <typename T>
void process(T&& obj) {
    // obj 是一个转发引用，可以是左值或右值
    func(std::forward<T>(obj));  // 精确转发 obj
}

int main() {
    MyClass a;
    process(a);           // 传递左值，T 被推导为 MyClass&
    process(MyClass{});   // 传递右值，T 被推导为 MyClass&&
}
```

---

### 5. **总结**

* **右值引用**主要用于实现移动语义，通过绑定右值和使用`std::move`，可以避免深拷贝，提升程序性能。
* **转发引用**用于模板编程中的完美转发，它能够根据传入参数的类型决定是左值引用还是右值引用，从而避免不必要的拷贝或移动。

两者在C++现代编程中都非常重要，各自针对不同的场景提高了代码的效率和灵活性。

## 引用折叠

C++中的**引用折叠**（Reference Collapsing）是C++11引入的一项语言机制，主要用于处理当多层引用（特别是右值引用和左值引用）组合在一起时，最终引用的类型如何确定。引用折叠的出现主要是为了支持完美转发（Perfect Forwarding）和泛型编程。

### 引用折叠的动机

在C++11中，右值引用（ `T&&` ）的引入使得我们可以区分左值和右值，尤其是在模板编程中提供了强大的支持。比如，结合 `std::forward` 和 `std::move` ，可以实现完美转发，允许函数在不改变参数值类别的情况下将其转发出去。

但是，在模板中使用引用时，特别是当传递引用到引用的场景时，C++标准需要有一套规则来确定最终的引用类型。因此就有了**引用折叠规则**。

### 引用折叠规则

当多层引用组合在一起时，比如 `T& &` 、 `T& &&` 、 `T&& &` 和 `T&& &&` ，C++标准规定了引用折叠的规则，用于决定最终的引用类型。引用折叠遵循以下规则：

1. **左值引用和左值引用**折叠成**左值引用**。
   - `T& &` → `T&`

2. **左值引用和右值引用**折叠成**左值引用**。
   - `T& &&` → `T&`

3. **右值引用和左值引用**折叠成**左值引用**。
   - `T&& &` → `T&`

4. **右值引用和右值引用**折叠成**右值引用**。
   - `T&& &&` → `T&&`

换句话说，只要有左值引用参与折叠，最终的类型就会变成左值引用。如果只有右值引用折叠，则结果是右值引用。

### 举例说明

假设有以下代码：

```cpp
template <typename T>
void foo(T&& arg) {
    // 函数实现
}
```

此时，当我们传递不同类型的参数给 `foo` 函数时，会发生引用折叠：

1. 如果`T`是一个左值引用类型，例如`int&`，那么`T&&`会变成`int& &&`，根据引用折叠规则，这会折叠成`int&`，即**左值引用**。
2. 如果`T`是一个右值引用类型，例如`int`，那么`T&&`会变成`int&&`，这依然是**右值引用**。

这也是为什么模板函数 `foo` 可以既接收左值也可以接收右值的原因之一。

### 完美转发中的应用

引用折叠在完美转发中扮演了非常重要的角色。例如，结合 `std::forward` ，可以根据传入的值类别（左值或右值）选择性地转发参数：

```cpp
template <typename T>
void wrapper(T&& arg) {
    foo(std::forward<T>(arg));
}
```

在 `std::forward` 中， `T` 的类型决定了如何转发 `arg` ：

* 如果`T`是左值引用类型（如`int&`），则`std::forward<T>(arg)`会将`arg`作为左值引用传递。
* 如果`T`是右值引用类型（如`int&&`），则`std::forward<T>(arg)`会将`arg`作为右值引用传递。

这依赖于引用折叠机制来确保传递的引用类型正确无误。

### 总结

C++中的引用折叠机制是模板编程和完美转发的核心部分。其主要规则是，当引用与引用结合时，如果其中任何一方是左值引用，那么最终的结果是左值引用；如果两者都是右值引用，则最终结果是右值引用。这一机制确保了模板中引用类型的正确推导和处理。

## int&&

在C++中， `int&&` 表示右值引用（rvalue reference）。然而，具体的行为取决于上下文以及如何使用这些引用。

### 上下文和赋值行为

考虑以下代码：

```cpp
int b = 5;
int&& a = std::move(b);
```

在这个例子中， `a` 是一个右值引用。通过 `std::move(b)` ，我们将 `b` 转换为一个右值，因此 `a` 被初始化为对 `b` 的右值引用。此时， `a` 是一个右值引用，它绑定到 `b` 所存储的值。

### 左值和右值的区别

在C++中，左值（lvalue）和右值（rvalue）有不同的含义：

* **左值**：在内存中有一个确定的地址，可以取地址操作符（&）。
* **右值**：一般是一个临时值，不存储在任何确定的内存地址中，通常是表达式的结果，无法取地址。

即使 `a` 是一个右值引用，但 `a` 本身是一个有名称的变量，因此它作为表达式的时候是一个左值。为了区分这种情况，我们用以下例子说明：

```cpp
int b = 5;
int&& a = std::move(b);

// a 是右值引用，但 a 本身是左值
```

在这个例子中，尽管 `a` 是一个右值引用类型，但是 `a` 本身是一个左值，因为它是一个具名变量。我们可以通过以下代码进一步展示这种情况：

```cpp
void foo(int& x) {
    std::cout << "左值引用" << std::endl;
}

void foo(int&& x) {
    std::cout << "右值引用" << std::endl;
}

int main() {
    int b = 5;
    int&& a = std::move(b);
    
    foo(a);       // 输出 "左值引用"
    foo(std::move(a)); // 输出 "右值引用"
    
    return 0;
}
```

在 `foo(a)` 调用中， `a` 是一个具名变量，因此是左值，调用了左值引用版本的 `foo` 。而在 `foo(std::move(a))` 调用中， `std::move(a)` 将 `a` 转换为右值，调用了右值引用版本的 `foo` 。

### 总结

综上所述， `int&& a = b;` （假设 `b` 是一个右值表达式）中 `a` 是一个右值引用。尽管如此， `a` 作为一个具名变量，在表达式中仍然表现为一个左值。这个区分在模板编程和函数重载时非常重要。

## std::move

`std::move` 是 C++ 标准库中的一个函数模板，定义在 `<utility>` 头文件中。它的作用是**将对象显式地转换为右值引用**，从而允许对象的资源在转移操作中被“移动”而不是复制。

### 1. **为什么需要 `std::move` ？**

在C++中，对象的拷贝通常是昂贵的，因为拷贝操作需要分配新的内存并复制对象的内容。如果对象非常大（例如容器类），拷贝操作的成本会非常高。因此，C++11 引入了**移动语义**，允许我们在某些情况下通过**移动**对象的资源，而不是拷贝对象，以提高程序性能。

移动操作的核心是：**“资源的转移而不是复制”**。换句话说，移动对象的资源（如堆内存、文件句柄等）后，源对象将进入一个合法但未定义状态，通常这个状态不会持有原始资源。 `std::move` 就是实现这种移动操作的关键。

### 2. ** `std::move` 的作用**

`std::move` 的主要作用是将对象显式地转换为右值引用。右值引用允许我们调用**移动构造函数**或**移动赋值运算符**，以转移对象内部的资源。

**示例代码：**

```cpp
#include <iostream>
#include <utility>
#include <string>

int main() {
    std::string str = "Hello, World!";
    std::string str2 = std::move(str);  // 使用 std::move 移动 str 的资源到 str2

    std::cout << "str: " << str << std::endl;   // str 处于“已移动”状态，通常为空
    std::cout << "str2: " << str2 << std::endl; // str2 拥有原本属于 str 的资源

    return 0;
}
```

输出结果可能是：

```
str: 
str2: Hello, World!
```

在这段代码中， `std::move(str)` 将 `str` 显式地转换为右值引用，允许编译器调用 `std::string` 的**移动构造函数**。这将转移 `str` 的内部资源（如堆上的内存）给 `str2` ，而不是进行昂贵的内存复制操作。之后， `str` 处于一种合法但不可预知的状态，通常会变成空字符串。

### 3. ** `std::move` 不会移动对象本身**

需要注意的是，** `std::move` 并不会真的移动对象的资源**，它只是一个**类型转换工具**，将左值转换为右值引用。真正的移动操作是由对象的**移动构造函数**或**移动赋值运算符**来完成的。

`std::move` 的核心定义如下：

```cpp
template <typename T>
typename std::remove_reference<T>::type&& move(T&& t) {
    return static_cast<typename std::remove_reference<T>::type&&>(t);
}
```

这意味着它只是把对象的类型从左值引用转成右值引用。

### 4. **使用 `std::move` 的场景**

#### - **在函数返回值时使用 `std::move` ：**

在返回局部对象时，使用 `std::move` 可以避免不必要的拷贝。

```cpp
std::string createString() {
    std::string s = "Hello";
    return std::move(s);  // 使用 std::move 可以调用移动构造函数
}
```

#### - **在容器中移动对象：**

当需要将一个对象插入到容器中时，使用 `std::move` 可以避免容器对对象进行复制。

```cpp
std::vector<std::string> vec;
std::string s = "Hello";
vec.push_back(std::move(s));  // 避免拷贝操作，s 被移动到容器中
```

#### - **避免不必要的拷贝：**

在需要将对象转移到另一个作用域、容器或其他场景时，可以使用 `std::move` 避免拷贝，从而提高效率。

### 5. **常见误解和注意事项**

* **移动后对象的状态**：移动操作后的对象仍然是有效的，但其状态未定义（依赖于实现），通常会变为空或默认状态。使用移动后的对象时要特别小心，确保在移动后不再使用它的资源。
* **`std::move` 不会真正移动对象**：`std::move` 只是类型转换工具，它不会执行移动，移动操作是由对象的移动构造函数和移动赋值运算符执行的。
* **不要过度使用 `std::move`**：对于临时对象或即将销毁的对象，编译器会自动推导出移动语义，不需要显式调用 `std::move`。过度使用 `std::move` 可能会导致代码可读性下降。

### 6. **总结**

`std::move` 是一个简单而强大的工具，它允许程序员显式地将对象转换为右值引用，以启用移动语义，避免不必要的复制操作，提高程序性能。然而，它本身不会移动对象，实际的移动操作是通过对象的移动构造函数和移动赋值运算符完成的。

## 移动构造和移动赋值

在C++中，**移动构造函数**和**移动赋值运算符**是C++11引入的一种用于提升性能的机制，主要是为了支持**移动语义**（Move Semantics），以避免不必要的深拷贝，特别是在处理临时对象或大数据结构时。

### 1. 移动构造函数

**移动构造函数**是当对象被创建时，通过"移动"另一个对象的资源而不是拷贝它们来初始化新对象。这对于那些持有动态分配资源（如堆内存、文件句柄等）的对象尤为重要，因为可以通过移动资源而不是复制资源来避免昂贵的深拷贝操作。

#### 移动构造函数的签名：

```cpp
ClassName(ClassName&& other);
```

#### 解释：

* `ClassName&&` 表示一个右值引用（rvalue reference）。右值引用只能绑定到临时对象（右值）上，这些对象通常是那些将被销毁的对象，因此其资源可以被安全地"窃取"。
* `other` 是一个右值引用，它指向将被移动的对象。

#### 例子：

```cpp
#include <iostream>
#include <utility> // for std::move

class MyClass {
public:
    int* data;

    // 构造函数
    MyClass(int size) {
        data = new int[size];
        std::cout << "Constructor called" << std::endl;
    }

    // 移动构造函数
    MyClass(MyClass&& other) noexcept {
        data = other.data;    // 窃取资源
        other.data = nullptr; // 避免原对象持有指向相同资源的指针
        std::cout << "Move Constructor called" << std::endl;
    }

    // 析构函数
    ~MyClass() {
        if (data) {
            delete[] data;
            std::cout << "Destructor called, releasing memory" << std::endl;
        }
    }
};

int main() {
    MyClass obj1(10);             // 调用普通构造函数
    MyClass obj2 = std::move(obj1); // 调用移动构造函数
    return 0;
}
```

#### 输出：

```
Constructor called
Move Constructor called
Destructor called, releasing memory
```

在这个例子中，通过移动构造函数， `obj2` "窃取"了 `obj1` 的数据指针，而 `obj1` 的指针被置为 `nullptr` ，避免了双重释放的错误。

### 2. 移动赋值运算符

**移动赋值运算符**允许你在对象已经存在的情况下，通过移动另一个对象的资源来赋值当前对象。

#### 移动赋值运算符的签名：

```cpp
ClassName& operator=(ClassName&& other);
```

#### 解释：

* `ClassName&&` 仍然表示右值引用。
* `operator=` 是赋值运算符的重载，它用于在已有对象上进行资源的移动操作。

#### 例子：

```cpp
class MyClass {
public:
    int* data;

    // 构造函数
    MyClass(int size) {
        data = new int[size];
        std::cout << "Constructor called" << std::endl;
    }

    // 移动赋值运算符
    MyClass& operator=(MyClass&& other) noexcept {
        if (this != &other) {      // 防止自我赋值
            delete[] data;         // 释放当前对象的资源
            data = other.data;     // 窃取资源
            other.data = nullptr;  // 避免原对象持有指向相同资源的指针
            std::cout << "Move Assignment called" << std::endl;
        }
        return *this;
    }

    // 析构函数
    ~MyClass() {
        if (data) {
            delete[] data;
            std::cout << "Destructor called, releasing memory" << std::endl;
        }
    }
};

int main() {
    MyClass obj1(10);             // 调用普通构造函数
    MyClass obj2(20);             // 调用普通构造函数
    obj2 = std::move(obj1);       // 调用移动赋值运算符
    return 0;
}
```

#### 输出：

```
Constructor called
Constructor called
Move Assignment called
Destructor called, releasing memory
```

在这个例子中， `obj2` 通过移动赋值运算符窃取了 `obj1` 的数据，释放了它原本持有的资源。

### 3. `std::move` 的作用

在上面的例子中，你会注意到我们使用了 `std::move` 。 `std::move` 并不真正移动对象，它只是将一个左值转换为右值引用，从而能够触发移动语义。例如， `std::move(obj1)` 将 `obj1` 转为一个右值引用，之后可以调用移动构造或移动赋值。

### 4. 为什么需要移动语义？

在处理包含动态内存或资源的类时，如果没有移动语义，每次对象复制都需要进行深拷贝，这会带来性能开销。移动语义允许我们通过"窃取"资源而不是复制它们来大幅减少这种开销。

### 5. 总结

* **移动构造函数**：在创建新对象时，从另一个对象中移动资源。
* **移动赋值运算符**：在给现有对象赋值时，移动另一个对象的资源。
* **`std::move`**：用于显式地将对象转换为右值引用，触发移动语义。

这两者都是为了避免不必要的深拷贝，从而提升程序的性能，尤其是在处理临时对象或大型资源时。

## C++内联命名空间

在C++中，**内联命名空间**（Inline Namespace）是C++11引入的特性，主要用于版本控制和ABI（应用程序二进制接口）兼容性管理。它允许将命名空间内的成员“透明”地暴露给父命名空间，使得使用父命名空间时可以直接访问内联命名空间的内容，而无需显式指定。

---

### **核心特性**

1. **透明访问**  
   内联命名空间的成员会被视为父命名空间的成员，可以直接通过父命名空间访问，无需嵌套限定。

2. **版本控制**  
   常用于代码的版本管理。例如，将最新版本设为内联命名空间，旧版本保留为非内联。用户默认使用最新版本，但仍可显式访问旧版本。

3. **ABI兼容性**  
   在库开发中，通过内联命名空间避免因版本更新导致的链接错误。新旧版本的符号会被不同命名空间修饰，但默认使用内联版本。

---

### **语法示例**

```cpp
namespace Parent {
    inline namespace v1 { // v1 是内联命名空间
        void foo() { std::cout << "v1::foo\n"; }
    }
    namespace v2 {        // v2 是非内联命名空间
        void foo() { std::cout << "v2::foo\n"; }
    }
}

int main() {
    Parent::foo();    // 默认调用内联的 v1::foo
    Parent::v2::foo(); // 显式调用 v2::foo
    Parent::v1::foo(); // 显式调用 v1::foo（也可行）
}
```

---

### **典型应用场景**

1. **库的版本管理**  
   

```cpp
   namespace MyLib {
       inline namespace v2 { // 默认使用 v2
           class Widget { /*...*/ };
       }
       namespace v1 { // 保留旧版
           class Widget { /*...*/ };
       }
   }
   // 用户代码默认使用 MyLib::Widget（即 v2）
   ```

2. **ABI兼容性保障**  
   通过内联命名空间确保新旧版本的符号不同（避免链接冲突），同时提供默认的访问方式。

3. **简化模板特化**  
   内联命名空间允许在父命名空间中直接特化模板，而无需嵌套限定。

---

### **注意事项**

* **隐式使用风险**：内联命名空间的成员可能与父命名空间的其他成员发生名称冲突。
* **显式仍有效**：即使内联，仍可通过完整路径（如 `Parent::v1::foo`）访问。
* **扩展性**：支持嵌套内联（如 `inline namespace v1 { inline namespace sub { ... } }`）。

---

### **与普通命名空间的区别**

| **行为**               | **内联命名空间**       | **普通命名空间**       |
|------------------------|-----------------------|-----------------------|
| 成员是否自动暴露到父空间 | 是                    | 否                    |
| 是否需要显式指定路径     | 可选                  | 必须                  |
| 主要用途               | 版本控制、ABI兼容性   | 常规作用域隔离        |

---

通过内联命名空间，C++开发者可以更灵活地管理代码版本，同时保持接口的简洁性和兼容性。
