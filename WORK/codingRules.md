## 注释占比 15%左右

https://www.solidot.org/story?sid=65769

通过代码注释，可以看出代码作者的编码功底。新手写代码，要么不写注释，要么注释里尽写些废话，犹如画蛇添足；而优秀的程序猿写的注释言简意赅、恰到好处，有画龙点睛之妙。

## 标准制定

是否合理，还是制定者个人喜好，哪些地方需要制定规范

能否自动化/增加的工作量有多少？

主流项目是否制定了这个标准

## 代码检查

https://blog.csdn.net/qq_36631379/article/details/114533196

https://blog.csdn.net/qq_35333978/article/details/122347687

## google c++ 编程规范

https://zh-google-styleguide.readthedocs.io/en/latest/

https://google.github.io/styleguide/cppguide.html

## 更改 VS Code C++ 默认代码风格为 Google C++ Style

https://blog.csdn.net/sinat_34524528/article/details/85878592

## C++编程规范

https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#main

## 有的注释风格需要许多重复性劳动，应舍弃之，改用易于维护的注释风格。

## 直接把代码注释掉是讨厌的做法。别这么干！

《代码整洁之道》4.4.12

## c++在提交代码到git时，要保留注释掉的代码吗？

通常情况下，在提交代码到 Git 时，建议不要将注释掉的代码保留在提交中。Git 提交应该只包含当前正在使用的代码，而不是注释掉的或被废弃的代码。

如果注释掉的代码是针对特定情况的备份或调试目的，最好将其保存在本地，而不要将其提交到共享的代码库中。这可以通过本地的备份或分支来实现。Git 提交的目的是记录代码的改变历史，如果注释掉的代码不再需要，最好将其删除，保持提交的干净和可读性。

然而，有时注释掉的代码可能对于理解历史上的更改或者作为参考是有用的。在这种情况下，可以考虑使用版本控制系统的一些技巧，比如使用 git blame 或 git log 来查看代码历史，而不必保留注释掉的代码在提交中。

## 魔法字符串

https://www.cnblogs.com/perhaps/archive/2005/07/06/187464.html

## BS C++ style

https://www.stroustrup.com/bs_faq2.html

## 匈牙利记法

NL.5: Avoid encoding type information in names

https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#Rl-knr

## c++101编程规范

https://killwing.github.io/c++-coding-standards.md.html

## 函数默认传递指针用const修饰

 `[CG]Con.3`

## 魔数/魔法字符串

ES.45: Avoid “magic constants”; use symbolic constants

## 不要用C风格转换

ES.49: If you must use a cast, use a named cast

## 成员函数与纯函数

Cpp Core Guidelines 的 "F.8: Prefer pure functions" 指导原则的核心在于 强调函数的可预测性、可测试性和可维护性，并尽量避免副作用。

理解这个原则的关键在于理解什么是“纯函数”。

纯函数 (Pure Function) 的定义：

1.  确定性 (Deterministic): 对于相同的输入，总是产生相同的输出。
2.  无副作用 (No Side Effects): 函数的执行不会修改外部状态，也不会依赖于外部的可变状态。这意味着函数不会：
    -   修改全局变量或静态变量。
    -   修改传入的引用或指针指向的数据（除非是显式地通过参数返回的修改）。
    -   执行 I/O 操作（如打印到控制台、读写文件）。
    -   抛出未捕获的异常（在某些严格的定义下）。

为什么Cpp Core Guidelines 提倡纯函数？

*   可预测性: 你可以确信给定输入，函数的行为总是相同的，这使得理解和推理代码变得更容易。
*   可测试性: 纯函数非常容易测试。你只需要提供输入并检查输出，无需设置复杂的测试环境或模拟外部依赖。
*   可维护性: 当一个函数没有副作用时，你可以安全地移动它、并行化它，或者将其优化，而不用担心破坏其他部分的代码。
*   编译器优化: 编译器可以更容易地对纯函数进行各种优化，例如死代码消除、循环展开等。

---

对于类的成员函数，如果函数内需要使用成员变量，是否应把该成员变量作为函数的参数传入？

答案是：通常不建议将成员变量作为函数的参数传入，除非是为了实现更严格的“纯函数”定义，或者有特定的设计目的。

让我们深入分析一下：

成员函数与纯函数的权衡

类的成员函数，特别是那些需要访问或修改类状态（即成员变量）的函数，本质上很难完全符合纯函数的严格定义。

*   访问成员变量: 即使函数不修改成员变量，它也依赖于类实例的状态。`this` 指针隐式地指向了类对象，而类对象包含了成员变量。因此，从最严格的意义上来说，一个访问成员变量的函数（即使只是读取）也 不是一个纯函数，因为它依赖于类的内部状态，而这个状态可以随时改变（通过其他方法）。
*   修改成员变量: 如果成员函数修改了成员变量，那么它就 肯定不是纯函数，因为它有副作用（修改了类的状态）。

那么，"F.8: Prefer pure functions" 对成员函数意味着什么？

这个原则更多的是一种指导思想和目标，而不是一个绝对的禁令。对于成员函数，我们可以从两个层面来理解：

1.  尽可能模拟纯函数的特性:
    -   避免不必要的副作用: 如果一个成员函数可以只读取成员变量而不需要修改它们，那么它应该尽量避免修改其他成员变量或全局状态。
    -   明确的意图: 函数的名称应该清晰地表明它是否会修改类的状态。例如，使用 `get` 前缀通常表示只读取，而没有前缀或使用 `set` 前缀则可能表示修改。
    -   封装: 类的成员变量本身就是封装的一部分。访问这些成员变量是类内部的“业务”，而不需要将它们暴露给外部作为参数。

2.  将“纯”的概念应用到更细的粒度:
    -   辅助函数 (Helper Functions): 在一个非纯的成员函数内部，你可以定义一些 私有的辅助函数。如果这些辅助函数只接受参数并且不修改任何外部状态（包括类的成员变量），那么它们可以被视为纯函数。这有助于提高代码的可读性和可测试性，即便整个成员函数不是纯的。

关于将成员变量作为参数传入的讨论：

将成员变量作为参数传入一个成员函数，在大多数情况下，这是一种反模式 (anti-pattern)，因为它破坏了面向对象设计的核心思想：

*   破坏封装: 类的成员变量是类的内部实现细节，不应该被暴露给成员函数本身作为参数。成员函数应该能够自然地访问它所属对象的状态。
*   冗余: 如果一个函数属于一个类 `MyClass`，并且需要访问 `MyClass` 的成员变量 `m_value`，那么在函数定义中写成 `void MyClass::my_func(int m_value)` 是多余的，并且会混淆 `this->m_value` 和传入的 `m_value`。
*   增加复杂性: 每次调用都需要显式传递成员变量，使得代码更冗长。

什么时候可能会考虑（非常特殊的情况下）将成员变量作为参数传入？

虽然不推荐，但有极少数情况下，你可能需要考虑这种做法，通常是为了实现一个更严格的、与类实例状态解耦的计算逻辑：

*   将计算逻辑从对象中剥离: 假设你有一个复杂的计算，它 *偶然地* 使用了某个成员变量的值，但这个计算本身也可以独立于对象存在。你可以创建一个静态成员函数（没有 `this` 指针）或一个独立的非成员函数，并将需要的成员变量作为参数传入。

```cpp
class MyClass {
    int data;
public:
    int calculate_something() const {
        // 传统的成员函数方式
        return data * 2;
    }

    // 另一种思考方式：将计算逻辑剥离成一个独立的函数
    static int calculate_something_pure(int value) {
        // 这个函数是纯函数
        return value * 2;
    }

    int get_data() const { return data; }
};

// 在类的外部使用独立的纯函数
MyClass obj; 
int result = MyClass::calculate_something_pure(obj.get_data()); 
```

在这个例子中， `calculate_something_pure` 是一个纯函数，它接受一个 `int` 参数并返回一个 `int` 。我们仍然可以通过 `obj.get_data()` 来获取需要的值并传递给它。这并没有改变 `calculate_something` 的成员函数形式，但展示了将纯粹的计算逻辑独立出来的思想。

*   测试中的模拟 (Mocking): 在进行单元测试时，你可能需要模拟成员变量的行为。但通常这通过依赖注入或更高级的测试框架来实现，而不是直接在成员函数签名中修改。

总结:

Cpp Core Guidelines 的 "F.8: Prefer pure functions" 是一个重要的原则，它鼓励我们编写清晰、可预测和易于测试的代码。

*   对于普通的成员函数，它们通常需要访问或修改类的成员变量，因此 难以成为严格意义上的纯函数。
*   我们应该尽量让成员函数在不修改类状态的情况下，只读取成员变量，并避免不必要的副作用。
*   不应该将成员变量作为参数传入成员函数。这是违反封装原则的，并且冗余。成员函数天然地可以通过 `this` 指针访问其所属对象的成员变量。
*   可以将纯粹的计算逻辑从成员函数中剥离出来，作为静态成员函数或独立的非成员函数，并显式传递所需的参数。这样可以使这部分计算逻辑更符合纯函数的定义。

理解 "Prefer pure functions" 更多的是关于软件设计的哲学，即在可能的情况下，尽量追求无副作用和确定性，而不是要求所有成员函数都必须是纯的。对于成员函数，重点在于 管理和控制副作用，使其行为清晰可控。

## C.140: Do not provide different default arguments for a virtual function and an overrider

## F.9: Unused parameters should be unnamed

## 成员变量命名规范

派生类成员函数通过get方法获取基类私有成员变量，此时通过这个函数得到的变量不太好命名了
考虑暂加上基类的前缀

## "Con.1: By default, make objects immutable"局部变量返回的例外情况

A local variable that is returned by value and is cheaper to move than copy should not be declared const because it can force an unnecessary copy.
满足两个条件
* 作为值被返回
* 移动比拷贝开销更低

相关例子

```cpp
double positionFromPointTxt(const CAMGraphicsSimpleTextItem& pointTxt, CAMAnimationModel* model, double end_pos)
{
    const auto basePos = model->positionFromTime(pointTxt.xStartTime);
    const auto itemWidth = pointTxt.item->boundingRect().width();
    return end_pos - basePos < itemWidth ? basePos - itemWidth : basePos;
}
```

## 多层嵌套代码容易造成笔误，应对这种类型代码进行重构

## 对于以指针作为输入的函数，注意开头判断指针是否为空，现在可能没问题，以后维护加新东西就可能出问题了

```cpp
Group* GroupCollection::getGroupParent(const Group* groupOrPair) const
{
    // 新加的
    if (groupOrPair->get_parentIdentified())
    {
        return groupOrPair->get_parent().get();
    }

    // 遍历item获取父级，保证Group在未赋上_parent成员时也可获得父级
    for (const auto& item : *_items)
    {
        const auto& children = item->get_children();
        if (children && !children->empty() &&
            std::any_of(children->begin(), children->end(),
                        [groupOrPair](const auto& child) { return child.get() == groupOrPair; }))
        {
            return item.get();
        }
    }
    return nullptr;
}
```

## PPP3 Member functions and helper functions (8.7.5)

这是一段关于 C++ 程序设计（特别是面向对象设计）中“成员函数（Member functions）”与“辅助函数（Helper functions）”设计原则的经典论述。这段话极有可能出自 Bjarne Stroustrup（C++之父）的著作，如《C++程序设计原理与实践》。

以下是对该段落的详细中文解析，按照原逻辑结构分为几个核心观点：

### 1. 核心原则：接口最小化 (Minimal Interfaces)

原文要点：
*   设计类（Class）的接口时，应该追求“最小化但完整（minimal though complete）”。
*   黄金法则： 如果一个功能可以简单、优雅、高效地作为一个独立函数（freestanding function / nonmember function）来实现，那么它就不应该被写成类的成员函数。

解析：
这是一种防卫性编程思想。成员函数可以直接访问类的私有数据（representation），而独立函数（辅助函数）只能通过公共接口访问。将不必要的功能移出类，可以减少能够直接修改类内部数据的代码量。

### 2. 为什么要这样做？（两点理由）

#### A. 调试与安全性 (Debugging and Safety)

原文要点：
*   隔离 Bug： 如果一个独立函数（辅助函数）出了 Bug，它无法直接破坏类的内部私有数据，因为它没有权限访问。
*   缩小嫌疑范围： 调试就像警察抓嫌疑犯（"Round up the usual suspects"）。当对象的数据出错时，我们首先检查那些直接访问数据的函数。
*   对比： 检查 12 个函数比检查 50 个函数要轻松得多。

例子：
作者提到他在商业库中见过包含 `next_Sunday()` （下个周日）、 `next_workday()` （下个工作日）等 50 多个成员函数的 `Date` 类。这种设计是为了方便用户，但牺牲了代码的可理解性、实现难度和维护性。这类功能应该作为辅助函数放在类外面。

#### B. 应对内部实现的变更 (Changes in Representation)

原文要点：
*   如果将来我们需要修改类的内部数据结构（representation），只有那些直接访问数据的成员函数需要重写。
*   辅助函数因为是通过公共接口调用的，通常不需要修改。

例子：
假设 `Date` 类最初是用 `(year, month, day)` 三个变量存储日期的。后来开发者觉得用“自1900年1月1日以来的天数（一个整数）”存储更高效。
*   如果是成员函数： 所有的 `next_Sunday` 等几十个函数都需要重写，因为它们可能直接读取了旧的 `year/month/day` 变量。
*   如果是辅助函数： 只要 `Date` 类依然提供 `d.day()` 等公共接口，这些辅助函数完全不用改动。

### 3. 辅助函数的具体示例

作者列举了一些典型的辅助函数写法：
*   `next_Sunday(const Date& d)`：通过调用 `d.day()` 等公共接口计算，返回一个新的 `Date` 对象。
*   `operator==` 和 `operator!=`：用于比较两个日期是否相等。这是非常典型的非成员辅助函数。

### 4. 辅助函数的组织方式 (Namespaces)

原文要点：
*   “辅助函数”是一个逻辑上的设计概念，不是语法概念。
*   通常使用 命名空间 (namespace) 将类和它的辅助函数打包在一起。

代码示例解析：

```cpp
namespace Chrono {
    enum class Month { /* ... */ };
    class Date { /* ... */ }; // 核心类

    // 以下都是辅助函数，它们位于类之外，但与类在同一个命名空间下
    bool is_date(int y, Month m, int d); 
    Date next_Sunday(const Date& d);
    bool leapyear(int y);
    bool operator==(const Date& a, const Date& b);
    // ...
}
```

### 5. 特别提到的两个点

1.  关于 `==` 和 `!=`： 编译器不会像自动生成拷贝构造函数那样自动生成这两个运算符，因为并非所有类都需要比较相等性。它们通常作为辅助函数实现。
2.  关于 `is_date()`： 作者建议将“检查日期是否合法”的功能从 `Date::is_valid()`（成员函数）改为 `is_date()`（辅助函数）。
    -   理由： 验证逻辑（例如：2月30日不存在）通常与数据是如何存储的无关。无论内部怎么存，2月30日永远是非法的。这体现了逻辑与实现的解耦。

---

### 总结

这段话的核心教诲是：不要把所有功能都塞进类里（不要写“巨型类”）。

*   成员函数只负责最核心的、必须直接操作私有数据的任务。
*   辅助函数负责基于核心接口扩展出的便利功能。

这种做法能让代码更健壮（更少的数据破坏风险）、更容易调试（嫌疑范围小）、更容易维护（修改内部实现不影响外部逻辑）。

## "SF.6: Use using namespace directives for transition, for foundation libraries (such as std), or within a local scope (only)"中foundation libraries指什么？

在 C++ Core Guidelines 的这条规则（SF.6）中，“foundation libraries”（基础库）指的是在整个项目或特定模块中极其基础、核心且无处不在的库。这些库的使用频率非常高，以至于如果每次使用其中的功能都要加上命名空间前缀（例如 `std::` 或 `boost::` ），代码会变得极其冗长、难以阅读，从而分散对核心业务逻辑的注意力。

### 1. 如何理解 "Foundation Libraries"

在这里，"Foundation"（基础）有以下几个关键特征：

*   普适性 (Pervasiveness)： 几乎每一行代码或每一个文件都在使用它提供的基本类型（字符串、向量、智能指针等）。
*   默认认知 (Mental Default)： 开发人员已经默认这些类型是语言的一部分。例如，当你看到 `vector` 时，你脑子里想的就是标准库的 vector，而不是某个自定义的 `MyLib::vector`。
*   低冲突风险（相对而言）： 团队通常非常熟悉这个库的内容，因此会下意识地避免定义与其冲突的变量名。

核心逻辑是： 当显式限定命名空间（ `std::` ）带来的视觉干扰（Verbose and distracting）超过了命名冲突风险（Name clash）时，这个库就可以被视为 Foundation Library。

---

### 2. 除了 `std` 之外，还有哪些算作 Foundation Libraries？

除了 C++ 标准库 ( `std` )，是否算作“基础库”通常取决于你的项目依赖什么技术栈。以下是常见的例子：

#### A. Boost ( `using namespace boost;` )

*   背景： 在 C++11 之前，Boost 几乎是 C++ 的事实标准库。
*   场景： 如果你的项目深度依赖 Boost 的文件系统、网络或算法，且没有使用 C++17/20 的对应特性，Boost 就充当了基础库的角色。

#### B. 框架特定的命名空间

如果你在使用某个大型应用框架开发，该框架的核心命名空间往往被视为基础库：

*   Qt: 虽然 Qt 通常不使用命名空间隔离核心类（直接是`QString`,`QVector`），但在某些模块中可能存在。
*   OpenCV (`using namespace cv;`): 在计算机视觉项目中，几乎每行代码都在处理 `cv::Mat` 或 `cv::imread`。如果在 `.cpp` 文件中大量处理图像算法，`using namespace cv;` 是非常常见的做法。
*   Eigen (`using namespace Eigen;`): 在重度数学运算或图形学项目中，`Matrix4f`,  `Vector3d` 等类型使用极高频，一直写 `Eigen::` 会非常累赘。
*   DirectX / Microsoft WRL (`using namespace Microsoft::WRL;`): 在 Windows 这里的 COM 编程中。

#### C. 项目内部的基础模块 ( `using namespace MyProject::Core;` )

*   场景： 许多大型公司或项目会有自己的“Base”或“Core”库，里面定义了项目专用的基础类型（如自定义的日志系统、基础数据结构、错误码等）。
*   用法： 在上层业务逻辑代码中，为了方便使用这些基础设施，通常会展开这个核心命名空间。

#### D. 测试框架 ( `using namespace testing;` / `using namespace Catch;` )

*   场景： 在编写单元测试文件时（例如使用 Google Test）。
*   逻辑： 在测试文件中，`ASSERT_EQ`,`Test`,`InitGoogleTest` 等极其常用，加上命名空间前缀毫无意义且干扰阅读，因此 Google Test 命名空间在测试代码中被视为基础库。

### 总结与建议

规则 SF.6 的核心不是鼓励你随意使用 `using namespace` ，而是提供了一种务实的例外情况。

判定一个库是否为 "Foundation Library" 的标准是：
如果在你的 `.cpp` 文件（注意不是头文件）中，去掉这个命名空间前缀能显著提高代码的可读性，且团队成员都能清楚分辨出这些名字的来源，那么它就可以被当作基础库来处理。
