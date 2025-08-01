# P: Philosophy

### P.1: 在代码中直接表达你的想法

编译器是不会去读注释（或设计文档）的，许多程序员也（固执地）不去读它们。 而代码中所表达的东西是带有明确的语义的，并且（原则上）是可以由编译器和其他工具进行检验的。

### P.2: 用 ISO 标准 C++ 来编码

使用最新版的 C++ 编译器（目前支持 C++20 或 C++17），并打开禁用语言扩展的选项。

### P.3: 表达你的设计意图

一些代码如果不（比如通过命名或者代码注释）说明其设计意图的话，是不可能搞清楚代码是否达成其预定目标的。

### P.4: 理想情况下，程序应当是静态类型安全的

* `union` - 使用 `variant`（C++17 提供）
* 强制转换 - 尽可能减少其使用；使用模板有助于这点
* 数组退化 - 使用 `span`
* 范围错误 - 使用 `span`
* 窄化转换 - 尽可能减少其使用

### P.5: 编译期检查优先于运行时检查

为了代码清晰性和性能。 对于编译期识别的错误是不需要编写错误处理的。

### P.6: 应当使无法在编译期进行的检查能够在运行时实施

把难于检测的错误遗留在程序中，总会带来程序崩溃或得到错误的运行结果。

### P.7: 尽早识别运行时错误

避免“神秘的”程序崩溃。 避免能够产生（也许无法识别的）错误结果的程序错误。

### P.8: 不要泄漏任何资源

即使是缓慢的资源增长，随着时间推移，也会耗尽这些资源的可用性。 这对于长时间运行的程序来说尤其重要，而且是负责任的编程行为的基础方面。

### P.9: 不要浪费时间或空间

你用的语言是 C++。

### P.10: 不可变数据优先于可变数据

对常量进行推理要比变量简单得多。 不可变的事物是不可能被意外改变的。 不可变性有时候也带来更好地进行优化的机会。 在常量上不会出现数据竞争。

### P.11: 把杂乱的构造封装起来，而别让其散布到代码中

杂乱的代码更有可能隐藏有 Bug 而且难于编写。 而好的接口使用起来更容易和安全。 杂乱的，底层的代码会混杂出更多这样的代码。

### P.12: 适当采用支持工具

许多事情机器都比人做得更好。 对于重复劳动，计算机既不会累也不会厌烦。 相对于重复性的例行任务，我们通常可以做一些更有意义的事情。

### P.13: 适当采用支持程序库

使用设计良好，文档全面，并且有良好支持的程序库可以节省时间和工作量； 如果你的大部分工时都必须耗费在实现上的话， 程序库的质量和文档很可能要比你能做到的要好得多。 程序库的成本（时间，工作量和资金等等）可以由大量的用户所分担。 一个被广泛应用的程序库，远比一个独立的应用程序更加能够保持为最新状态，并被移植到新的系统之上。 对于被广泛应用的程序库的相关知识，也可以节省其他或未来的项目中的时间。 因此，如果你的应用领域中存在合适的程序库的话，请使用它。

# I: Interfaces

### I.1: 使接口明确

* 函数不能基于声明于命名空间作用域的变量来作出影响控制流的决定。
* 函数不能对声明于命名空间作用域的变量进行写入操作。

### I.2: 避免非  `const`  全局变量

非  `const`  全局变量能够隐藏依赖关系，并使这些依赖项可能出现无法预测的变动。

### I.3: 避免使用单例

单例基本上就是经过伪装的更复杂的全局对象。

### I.4: 使接口严格和强类型化

* 报告将 `void*` 用作参数或返回类型的情况
* 报告使用了多个 `bool` 参数的情况
* 查找使用了过多基础类型的参数的函数。

### I.5: 说明前条件（如果有）

在参数上蕴含着使它们在被调用方中能够恰当使用的约束关系。

### I.7: 说明后条件

以检测到对返回结果的误解，还可能发现实现中存在错误。

### I.9: 当接口是模板时，用概念来文档化其参数

更严谨地说明接口，并使其在（不远的）将来可以在编译时进行检查。

### I.10: 使用异常来表明无法实施所要求的任务

不应该让错误可以被忽略，因为这将导致系统或者一次运算进入未定义的（或者预料之外的）状态。 这是错误的一个主要来源。
我们并不认为“性能”是一种不使用异常的合理理由。
* 通常，显式的错误检查和处理会消耗掉和异常处理一样多的时间和空间。
* 通常，使用异常的更清晰的代码会带来更好的性能（简化了对程序执行路径的追踪和其优化）。
* 一条对性能关键代码的好规则是，把检查从代码的关键部分中移出去。
* 长期来看，更规整的代码会得到更好的优化。
* 在做出性能相关的声明前一定要小心地进行测量。

### I.11: 决不以原始指针（ `T*` ）或引用（ `T&` ）来传递所有权

如果对调用者和被调用方哪一个拥有对象有疑问，那就会造成泄漏或者发生提早的析构。

### I.13: 不要只用一个指针来传递数组

(pointer, size) 式的接口是易于出错的。同样，（指向数组的）普通指针还必须依赖某种约定以使被调用方来确定其大小。

### I.22: 避免全局对象之间进行复杂的初始化

复杂的初始化可能导致未定义的执行顺序。

### I.23: 保持较少的函数参数数量

大量参数会带来更大的出现混乱的机会。大量传递参数与其他替代方案相比也通常是代价比较大的。
两个最常见的使得函数具有过多参数的原因是：
1. _缺乏抽象_ 缺少一种抽象，使得一个组合值被以 一组独立的元素的方式进行传递，而不是以一个单独的保证了不变式的对象来传递。 这不仅使其参数列表变长，而且会导致错误， 因为各个成分值无法再被某种获得保证的不变式进行保护。  
2. _违反了“函数单一职责”原则_ 这个函数试图完成多项任务，它可能应当被重构。
多少参数算很多？请使用少于四个参数。 有些函数确实最好表现为四个独立的参数，但这样的函数并不多。

### I.24: 避免可以由同一组实参以不同顺序调用造成不同含义的相邻形参

相同类型的相邻参数很容易被不小心互换掉。

### I.25: 优先以空抽象类作为类层次的接口

空的（没有非静态成员数据）抽象类要比带有状态的基类更倾向于保持稳定。

### I.26: 当想要跨编译器的 ABI 时，使用一个 C 风格的语言子集

不同的编译器会实现不同的类的二进制布局，异常处理，函数名字，以及其他的实现细节。

### I.27: 对于稳定的程序库 ABI，考虑使用 Pimpl 手法

由于私有数据成员参与类的内存布局，而私有成员函数参与重载决议， 对这些实现细节的改动都要求使用了这类的所有用户全部重新编译。而持有指向实现的指针（Pimpl）的 非多态的接口类，则可以将类的用户从其实现的改变隔离开来，其代价是一层间接。

```cpp
//header
class widget {
    class impl;
    std::unique_ptr<impl> pimpl;
public:
    void draw(); // public API that will be forwarded to the implementation
    widget(int); // defined in the implementation file
    ~widget();   // defined in the implementation file, where impl is a complete type
    widget(widget&&) noexcept; // defined in the implementation file
    widget(const widget&) = delete;
    widget& operator=(widget&&) noexcept; // defined in the implementation file
    widget& operator=(const widget&) = delete;
};
```

```cpp
//source
class widget::impl {
    int n; // private data
public:
    void draw(const widget& w) { /* ... */ }
    impl(int n) : n(n) {}
};
void widget::draw() { pimpl->draw(*this); }
widget::widget(int n) : pimpl{std::make_unique<impl>(n)} {}
widget::widget(widget&&) noexcept = default;
widget::~widget() = default;
widget& widget::operator=(widget&&) noexcept = default;
```

### I.30: 将有违规则的部分封装

维持代码简单且安全。 有时候因为逻辑的或者性能的原因，需要使用难看的，不安全的或者易错的技术。 此时，将它们局部化，而不是使其“感染”接口，可以避免更多的程序员团队必须当心其 细节和微妙之处。 如果可能的话，实现复杂度不能通过接口渗透到用户代码之中。
