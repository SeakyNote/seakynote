## 简单地作自我介绍

## 之前工作情况

* 现在找机会/离职原因
  + 老板太苛刻？
  + 同事太难相处？
  + 加班太多？
  + 工资太低？
* 之前工作的工作强度

## C++基本功评分

### 1. STL迭代器

```cpp
// context
auto refreshCombo = [&](QComboBox* combo, std::map<std::string, std::string> dataMap,
                        std::string value) {
    // do something

    std::map<std::string, std::string>::iterator it;
    for (it = dataMap.begin(); it != dataMap.end(); it++) {
        if (it->second == "")
            break;
    }
    if (it == dataMap.end()) {
        combo->addItem("");
    }

    // do something
};
// context
```

### 2.const/auto/pointer

```cpp
struct TestCls {
    int mem = 0;
};

TestCls* getTestClsObjFromSomewhere()
{
    // 从其它地方获取的指针，此处new仅作测试示意
    return new TestCls;
}

int main()
{
    // 说明以下变量定义不使用auto的等价写法
    auto testFuncRes1 = getTestClsObjFromSomewhere();
    const auto testFuncRes2 = getTestClsObjFromSomewhere();
    const auto* testFuncRes3 = getTestClsObjFromSomewhere();
    const auto* const testFuncRes4 = getTestClsObjFromSomewhere();

    // 以下哪些语句是合法的，哪些语句是非法的？
    testFuncRes1->mem = 2;
    testFuncRes2->mem = 2;
    testFuncRes3->mem = 2;
    testFuncRes4->mem = 2;
    testFuncRes1 = nullptr;
    testFuncRes2 = nullptr;
    testFuncRes3 = nullptr;
    testFuncRes4 = nullptr;
}
```

### 3. 成员变量初始化顺序

```cpp
#include <iostream>
using namespace std;

class A {
private:
    int n1;
    int n2;

public:
    A()
        : n2(0)
        , n1(n2 + 2)
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
}
```

### 4. 可见性与可访问性

```cpp
#include <iostream>
using namespace std;

int n = 0;
class Parent {
public:
    Parent()
        : n(1)
    {
    }

private:
    int n;
};

class Child : public Parent {
public:
    Child() { }
    void Func()
    {
        cout << n << endl;
    }
};

int main()
{
    Child c;
    c.Func();
}
```

### 5. 函数传参

```cpp
class CAMJsonBase {
    // context
protected:
    // ToWriteEvery作用是将输入不同类型val值存入writer中
    template <typename T>
    static void ToWriteEvery(Writer<StringBuffer>& writer, T& val)
    {
        if (std::is_base_of<CAMJsonBase, T>::value) {
            CAMJsonBase* p = (CAMJsonBase*)(&val);
            if (p == nullptr)
                throw "对象序列化失败：引用值为NULL";

            p->ToWrite(writer);
        } else {
            throw "类型序列化失败";
        }
    }

    static void ToWriteEvery(Writer<StringBuffer>& writer, int32_t& val)
    {
        writer.Int(val);
    }
    static void ToWriteEvery(Writer<StringBuffer>& writer, int64_t& val)
    {
        writer.Int64(val);
    }
    static void ToWriteEvery(Writer<StringBuffer>& writer, uint32_t& val)
    {
        writer.Uint(val);
    }
    static void ToWriteEvery(Writer<StringBuffer>& writer, uint64_t& val)
    {
        writer.Uint64(val);
    }
    static void ToWriteEvery(Writer<StringBuffer>& writer, float& val)
    {
        writer.String(ToString(val).data());
    }
    static void ToWriteEvery(Writer<StringBuffer>& writer, double& val)
    {
        writer.String(ToString(val).data());
    }
    static void ToWriteEvery(Writer<StringBuffer>& writer, bool& val)
    {
        writer.Bool(val);
    }
    static void ToWriteEvery(Writer<StringBuffer>& writer, std::string& val)
    {
        writer.String(val.data());
    }
    static void ToWriteEvery(Writer<StringBuffer>& writer, char* val)
    {
        writer.String(val, static_cast<unsigned int>(strlen(val)));
    }
    // context
};
```

## 开放性问题

### 1. 代码优化/重构

```cpp
void CAMRobotHomeJointsDlg::showEnableHomeJointsLevel(std::shared_ptr<CAMPlan::Robot> robot)
{
    QString defaultLevel = "默认";
    QString usingLevel = "(生效中)";
    if (_robotLevel)
    {
        ui->tabWidget->setTabText(0, robot->get_name().c_str() + usingLevel);
        ui->tabWidget->setTabText(1, robot->get_model().c_str());
        ui->tabWidget->setTabText(2, robot->get_vendor().c_str());
        ui->tabWidget->setTabText(3, defaultLevel);
        return;
    }
    if (_noRobotLevel == 2)
    {
        ui->tabWidget->setTabText(0, robot->get_name().c_str());
        ui->tabWidget->setTabText(1, robot->get_model().c_str() + usingLevel);
        ui->tabWidget->setTabText(2, robot->get_vendor().c_str());
        ui->tabWidget->setTabText(3, defaultLevel);
        return;
    }
    else if (_noRobotLevel == 1)
    {
        ui->tabWidget->setTabText(0, robot->get_name().c_str());
        ui->tabWidget->setTabText(1, robot->get_model().c_str());
        ui->tabWidget->setTabText(2, robot->get_vendor().c_str() + usingLevel);
        ui->tabWidget->setTabText(3, defaultLevel);
        return;
    }
    else
    {
        ui->tabWidget->setTabText(0, robot->get_name().c_str());
        ui->tabWidget->setTabText(1, robot->get_model().c_str());
        ui->tabWidget->setTabText(2, robot->get_vendor().c_str());
        ui->tabWidget->setTabText(3, defaultLevel + usingLevel);
        return;
    }
}
```

### 2. 代码比较

```cpp
void CAMWeldlineCreateDlg::connectAutoCalcSigalSlots() const
{
    const std::unordered_map<QPushButton*, CAMWeldlineAutoCalc::AutoCalcType> buttonToAutoCalcType {
        { ui->pushButtonAutoCalcThickness1, CAMWeldlineAutoCalc::AutoCalcType::Thickness1 },
        { ui->pushButtonAutoCalcThickness2, CAMWeldlineAutoCalc::AutoCalcType::Thickness2 },
        { ui->pushButtonAutoCalcConnectionAngle, CAMWeldlineAutoCalc::AutoCalcType::ConnectionAngle },
        { ui->pushButtonAutoCalcNormal1, CAMWeldlineAutoCalc::AutoCalcType::Normal1 },
        { ui->pushButtonAutoCalcNormal2, CAMWeldlineAutoCalc::AutoCalcType::Normal2 }
    };

    for (const auto [pushButton, autoCalcType] : buttonToAutoCalcType) {
        connect(pushButton, &QPushButton::clicked, this,
            [this, autoCalcType] { autoCalcCertainType(autoCalcType); });
    }

    const std::vector<std::pair<decltype(&CAMSegmentWeldingPropertiesDlg::autoCalcThickness1),
        CAMWeldlineAutoCalc::AutoCalcType>>
        funcToAutoCalcType { { &CAMSegmentWeldingPropertiesDlg::autoCalcThickness1,
                                 CAMWeldlineAutoCalc::AutoCalcType::Thickness1 },
            { &CAMSegmentWeldingPropertiesDlg::autoCalcThickness2,
                CAMWeldlineAutoCalc::AutoCalcType::Thickness2 },
            { &CAMSegmentWeldingPropertiesDlg::autoCalcConnectionAngle,
                CAMWeldlineAutoCalc::AutoCalcType::ConnectionAngle },
            { &CAMSegmentWeldingPropertiesDlg::autoCalcNormal1,
                CAMWeldlineAutoCalc::AutoCalcType::Normal1 },
            { &CAMSegmentWeldingPropertiesDlg::autoCalcNormal2,
                CAMWeldlineAutoCalc::AutoCalcType::Normal2 } };

    for (const auto [func, autoCalcType] : funcToAutoCalcType) {
        connect(segmentWeldingPropsDlg, func, this,
            [this, autoCalcType] { autoCalcCertainTypeForContourPt(autoCalcType); });
    }
}
```

```cpp
void CAMWeldlineCreateDlg::connectAutoCalcSigalSlots() const
{
    auto connectAutoCalc = [this](auto pushButton, auto autoCalcType) {
        connect(pushButton, &QPushButton::clicked, this,
            [this, autoCalcType] { autoCalcCertainType(autoCalcType); });
    };

    connectAutoCalc(ui->pushButtonAutoCalcThickness1,
        CAMWeldlineAutoCalc::AutoCalcType::Thickness1);
    connectAutoCalc(ui->pushButtonAutoCalcThickness2,
        CAMWeldlineAutoCalc::AutoCalcType::Thickness2);
    connectAutoCalc(ui->pushButtonAutoCalcConnectionAngle,
        CAMWeldlineAutoCalc::AutoCalcType::ConnectionAngle);
    connectAutoCalc(ui->pushButtonAutoCalcNormal1, CAMWeldlineAutoCalc::AutoCalcType::Normal1);
    connectAutoCalc(ui->pushButtonAutoCalcNormal2, CAMWeldlineAutoCalc::AutoCalcType::Normal2);

    auto connectAutoCalcForContourPt = [this](auto signal, auto autoCalcType) {
        connect(segmentWeldingPropsDlg, signal, this,
            [this, autoCalcType] { autoCalcCertainTypeForContourPt(autoCalcType); });
    };

    connectAutoCalcForContourPt(&CAMSegmentWeldingPropertiesDlg::autoCalcThickness1,
        CAMWeldlineAutoCalc::AutoCalcType::Thickness1);
    connectAutoCalcForContourPt(&CAMSegmentWeldingPropertiesDlg::autoCalcThickness2,
        CAMWeldlineAutoCalc::AutoCalcType::Thickness2);
    connectAutoCalcForContourPt(&CAMSegmentWeldingPropertiesDlg::autoCalcConnectionAngle,
        CAMWeldlineAutoCalc::AutoCalcType::ConnectionAngle);
    connectAutoCalcForContourPt(&CAMSegmentWeldingPropertiesDlg::autoCalcNormal1,
        CAMWeldlineAutoCalc::AutoCalcType::Normal1);
    connectAutoCalcForContourPt(&CAMSegmentWeldingPropertiesDlg::autoCalcNormal2,
        CAMWeldlineAutoCalc::AutoCalcType::Normal2);
}
```

## 自我评估/学习能力/成长潜力

* 评价一下自己编程水平/C++编程基本功
* 最近有没有看C++、编程、软件工程方面的书籍、资料、文章
  + 印象最深的章节，具体讲讲
  + 有哪些地方讲得/写得有问题？
* 有没有写博客或个人网站或做开源项目
* 有没有读过什么大佬的网站或者博客
  + 印象深刻的技术文章
  + 要输出前n个自然数中的质数的话，应该采取怎样的算法逻辑
    - 回答筛法的话，问怎么求自然数中前n个质数

## Qt

* C++/qt的使用版本
* 项目构建使用的是cmake/qmake；二者区别
* 界面是基于qml的还是传统widget的；二者区别
* qpushbutton和qtoolbutton的区别和使用场景
* qss样式表有没有用过，讲一下你的使用场景
* 控件提升了不了解（Designer中选中控件右键"提升为..."按钮）举几个之前项目中具体的例子

## Git

* git有没有使用过
* 怎么操作git的，用哪些工具
* 能讲下什么场景用merge什么场景用rebase吗？
* revert/reset区别

## 近半年工作内容

其中感兴趣的项目
* 背景
* 自己做的工作
  + 单独或带队做的话
    - 总体框架设计
    - 核心算法
    - 团队合作
* 项目中碰到的最大问题，如何解决
* 学到什么/收获
* 什么时候会和其他团队成员起冲突（开发、测试、设计、项目经理）
  + 如何解决

## 行业经验

对三维CAD设计/仿真软件是否有概念及使用经验

## 个人意愿

* 想找一份什么样的工作，理想中的工作环境是怎样的？
* 短期/长期的发展目标，技术上的/职业上的
* 后续希望从事哪方面的软件开发，例如界面/网络/数据库/算法/架构/业务逻辑等，为什么？

## 业余爱好
