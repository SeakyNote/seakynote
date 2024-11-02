## 理论

### qt对象父对象被析构子对象也会被析构吗？

在 Qt 中，当父对象被析构时，其子对象通常也会被析构。这是因为 Qt 使用了对象树的概念，其中父对象负责管理其下的子对象。当父对象被析构时，Qt 会自动递归析构其所有子对象。这确保了对象之间的正确管理和释放，有助于避免内存泄漏和其他资源管理问题。

https://zhuanlan.zhihu.com/p/476682300

### 为什么qt控件不使用智能指针？

https://stackoverflow.com/questions/34433435/why-dont-the-official-qt-examples-and-tutorials-use-smart-pointers

### 解决This application failed to start because no Qt platform plugin could be initialized问题

https://blog.csdn.net/weixin_44819948/article/details/115497784

### Qt多版本并存

启动程序时环境变量Path中，新的qt路径需要放到老的之前

### qt plugins目录下的dll在没有相关环境变量的情况下是如何被调用的？

在没有相关环境变量的情况下，Qt插件目录下的DLL文件通常是通过Qt框架的动态链接库加载机制被调用的。Qt框架提供了一种灵活的插件系统，允许将特定功能或者特定类型的资源（比如插件）作为独立的模块动态加载到应用程序中。这种机制使得应用程序可以在运行时根据需要加载或者卸载插件，从而实现灵活性和可扩展性。

在Qt中，插件通常是作为动态链接库（DLL）的形式存在的。当应用程序需要使用插件时，它可以使用Qt提供的相关类（比如QPluginLoader）来加载插件。在加载插件时，Qt会根据一定的约定（比如插件元数据）来确定插件的类型和功能，并将其加载到应用程序的内存空间中。加载插件后，应用程序可以通过插件提供的接口来调用其功能。

如果没有设置相关的环境变量，Qt通常会默认搜索一些标准的插件目录，比如应用程序所在的目录、Qt库所在的目录等。因此，即使没有设置环境变量，Qt仍然可以找到并加载位于Qt插件目录下的DLL文件。当然，如果DLL文件不在这些默认的目录下，那么应用程序可能会找不到插件而加载失败。在这种情况下，可以通过手动指定插件路径或者设置相应的环境变量来告诉Qt框架插件的位置。

## 控件

### QHBoxLayout

https://github.com/tomxuetoy/Qt_age/blob/master/main.cpp

```cpp
QHBoxLayout *layout = new QHBoxLayout;
layout->addWidget(spinBox);
layout->addWidget(slider);
window->setLayout(layout);
```

### 如何去除QTableWidget表格选中Item时的虚线框?

https://baijiahao.baidu.com/s?id=1695623686163136327&wfr=spider&for=pc

### tablewidget外边框颜色设定

`border: 1px solid rgb(255,0,0)`

### QTableWidget添加控件（自定义代理）

https://blog.csdn.net/ss_0507/article/details/127033981

### 用setValue()设置UI控件内的内容，如何避免valuechange()被触发

https://blog.csdn.net/weixin_49601095/article/details/118635908

### QHBoxLayout,QVBoxLayout的setStretch的作用

https://blog.csdn.net/gezhi_dove/article/details/105063695

### 子widget填充父widget
```cpp
// 创建一个父widget和子widget
QWidget* parentWidget = new QWidget();
QWidget* childWidget = new QWidget(parentWidget);

// 创建一个水平布局管理器，并将子widget添加到其中
QHBoxLayout* layout = new QHBoxLayout(parentWidget);
layout->addWidget(childWidget);

// 将布局管理器应用到父widget中
parentWidget->setLayout(layout);

// 设置子widget充满父widget
childWidget->setSizePolicy(QSizePolicy::Expanding, QSizePolicy::Expanding);
```

### QPushButton也可以check

加入QButtonGroup可以互斥

可以用qss修饰

### 获取QLabel的实际宽度

`width = label.fontMetrics().boundingRect(label.text()).width()`

### 对QComboBox设置text和Data

```cpp
ui->comboBox->addItem(tr("Chinese"),Tmk::Chinese);
ui->comboBox->addItem(tr("English"),Tmk::English);

int comboIndex = ui->comboBox->findData(parameter->SystemLanguage);
ui->comboBox->setCurrentIndex(comboIndex);

parameter->SystemLanguage = static_cast<Tmk::LanguageEnum>(ui->comboBox->currentData().toInt());
```

### QTablewidget只显示横分割线，不显示竖分割线

https://blog.csdn.net/qq_16383977/article/details/79191089

### QTextEdit如何设置为1行？

使用setMaximumBlockCount(1), setWordWrapMode(QTextOption::NoWrap)

### qwidget/qframe

QFrame和QWidget都是Qt框架中的基础控件类，用于构建GUI应用程序中的界面元素。它们可以作为容器来组织其他控件，例如按钮、标签、文本框等。但是，它们在某些方面有所不同，以下是两者主要的区别和场景使用：

QFrame：
QFrame是一个简单的矩形框架，其主要目的是提供腔体或分隔符（separator）的视觉效果，并且可以设置边框的样式、颜色和宽度等属性。它通常用于包含具有相似功能或特定类型的控件，例如工具栏、状态栏或菜单。此外，QFrame还支持简单的绘图操作，例如画线和画矩形等。

QWidget：
QWidget是Qt框架中最基本的窗口部件类，它提供了一个空白的窗口，并且可以包含子控件。QWidget具有更广泛的用途，它可以作为许多其他控件的基类，例如：QPushButton、QLabel、QLineEdit等，因此，这些控件都可以添加到QWidget中。另外，QWidget还支持鼠标和键盘事件处理、大小调整和窗口管理等功能。

综上所述，如果您需要创建一个简单的框架或分隔符，则使用QFrame；如果您需要创建一个复杂的界面并添加多个控件，则使用QWidget。但是，在实际开发中，通常情况下QWidget更为常用，因为它提供了更丰富的功能和灵活性来满足不同的需求。

### QTableWidget设置列宽行高大小的几种方式及其他常用属性设置 

https://www.cnblogs.com/david-china/p/16836652.html

### QT中常用文本控件区别（LineEdit、TextEdit 、PlainTextEdit ）

https://blog.csdn.net/GuiH168/article/details/127690629

### QMessageBox

https://blog.csdn.net/ccc369639963/article/details/122699085

yes or no用`QMessageBox::StandardButton result=QMessageBox::question(&widget, "Title","text");`

### Qt无边框窗口实现拖动

https://blog.csdn.net/qq_36709282/article/details/119960923

### QTableWidget关于item内存释放

https://blog.51cto.com/u_13999641/4915328

### Qt--自定义UI控件并集成到Qt Designer

https://blog.csdn.net/Mr_robot_strange/article/details/108469284

### Qt编写自定义控件及插件的使用

https://blog.csdn.net/u011555996/article/details/124459635?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-1-124459635-blog-118877328.pc_relevant_recovery_v2&spm=1001.2101.3001.4242.2&utm_relevant_index=4

注意LIBS+=的使用

### accept/reject自动析构

构造里加上`setAttribute(Qt::WA_DeleteOnClose)`

### QSlider change with double values（Qt滑动进度条显示小数）

https://blog.csdn.net/coldplayplay/article/details/78550083

## 中文

### 编码显示测试

|                | QString | QStringLiteral |
| :------------: | :-----: | :------------: |
|     UTF-8      |   OK    |      NOK       |
| UTF-8 with Bom |   NOK   |       OK       |

### Qt翻译——简洁步骤

https://blog.csdn.net/weibuu/article/details/108802258

注意翻译文件需要包含在qrc中

使用trans.load(":/cn.qm");

### 使用qt5_create_translation来创建ts国际化

https://www.cnblogs.com/Paoyao/p/15752116.html

### Qt中lupdate 和 lrealease 命令使用

https://blog.csdn.net/m0_37998692/article/details/112268934

### Qt Creator + CMake 管理工程翻译文件

https://blog.csdn.net/Tclser/article/details/125364058

### ts/qm清理问题

https://bugreports.qt.io/browse/QTBUG-41736

### QStringLiteral和QString::fromLocal8Bit的区别

`QStringLiteral` 和 `QString::fromLocal8Bit` 是用于处理字符串的两种不同方法，它们之间有一些重要的区别：

1. **编译时解析 vs 运行时解析**：
   - `QStringLiteral` 在编译时将字符串解析为 Unicode 字符串，并将其储存在只读内存中。这意味着字符串的解析工作在编译时完成，不会产生额外的运行时开销。
   - `QString::fromLocal8Bit` 则是在运行时执行字符编码的转换工作。它接受一个本地的 8 位字符编码，并将其转换为 `QString` 类型。因此，它的性能开销主要发生在运行时。

2. **适用场景**：
   - `QStringLiteral` 适用于编译时已知的字符串，特别是对于那些不需要进行字符编码转换的情况。它在需要提高性能的场景中很有用。
   - `QString::fromLocal8Bit` 更适用于运行时需要转换字符编码的场景，比如处理来自不同来源的数据或者读取本地文件时。它提供了字符编码转换的功能，因此可以处理各种字符编码的情况。

3. **性能开销**：
   - 由于 `QStringLiteral` 在编译时进行字符串解析并存储在只读内存中，因此在运行时没有额外的性能开销。
   - `QString::fromLocal8Bit` 则需要在运行时执行字符编码的转换工作，因此可能会有一定的性能开销，特别是当处理大量字符串或者频繁调用该方法时。

综上所述，`QStringLiteral` 适用于编译时已知且不需要字符编码转换的字符串，而 `QString::fromLocal8Bit` 更适用于需要在运行时进行字符编码转换的情况。

## 信号槽

### 槽函数未正确跑通，尝试用queue方式

### Qt5 connect新语法：Lambda表达式

https://blog.csdn.net/csm201314/article/details/77914281

### disconnect

调disconnect之前应connect

考虑优先用blocksignals

### qt转到槽功能

不用connect和信号函数

### 信号槽连接为什么没反应？

只有槽函数才能用SLOT()

## qss

### Qt Style Sheets Reference

https://doc.qt.io/qt-5/stylesheet-reference.html

### QSS

http://qtdebug.com/qtbook-qss/

### 伪类选择器

冒号与感叹号之间不得有空格

### 颜色

https://www.w3.org/TR/css-color-3/#svg-color

### qss格式化给:与!之间加空格问题

    "editor.formatOnSave": true,
    "[css]": {
        "editor.formatOnSave": false
    }

### 关于Qt中的qss样式表需要注意的坑

https://zhuanlan.zhihu.com/p/475026361

## 容器转换

### Qt之QString与wchar_t 互相转换

https://blog.csdn.net/qq_45662588/article/details/123799322

转中文存在问题

### qstring-double互转

toDouble/QString::number(d,'f',2)

## 文件

### 检查文件是否可读

_access未生效

QFileInfo::isReadable未生效

QFile::isReadable生效	也未生效，为中文路径时返回false

QFile::open(QIODevice::ReadOnly)生效

Qt之文件读取QFile、QFileDialog、QFileInfo

https://www.jianshu.com/p/f792258f6a43

### QFile::close()

在Qt中，QFile::close()是用来关闭文件的方法。如果不调用QFile::close()来关闭文件，可能会导致以下一些影响：

1. 文件资源泄漏：如果不关闭文件，操作系统将会继续将文件标记为打开状态，这可能导致文件句柄资源泄漏，尤其是在程序需要频繁打开和关闭文件时。

2. 数据不稳定：某些操作系统或文件系统可能会在未正确关闭文件的情况下缓冲写入数据。这可能导致在程序关闭前数据未完全写入磁盘，从而可能导致数据丢失或损坏。

3. 其他进程无法访问：在某些情况下，未关闭文件可能会导致其他进程无法访问该文件，因为它仍然被当前进程保持着打开状态。

因此，确保在文件操作完成后调用QFile::close()来关闭文件是一个良好的编程习惯，可以避免上述问题的发生。

## qt多线程

### Qt程序主线程执行大量计算 界面卡顿，有什么方法优化？

1.假的多线程，可以适时调用 QCoreApplication::processEvents()，这样各种状态条都能刷新，比如for里面 i %1000==0时刷一次。

2.真的双线程，用子线程做，主线程进度条。适时emit signal_process(v)，刷进度条

3.线程池，比如 QFuture Mapreduce，适合批量密集均衡计算（每个核心预计在差不多的时间完成）。流水线线程池，适合批量密集的非均衡计算，每个事务分为微粒，最多一次处理100个微粒就重新排队，避免阻塞他人。

4.控制刷新速率，子线程不断刷新一个曲线的数据缓存，主线程每秒只读30次。我们做过频谱仪，FFT缓存在后台均衡，主界面的刷新周期是固定的，就是30次。足够了。要刷新的东西是在另一个线程形成了最终产品才显示的。比如你65536点fft，但当前视窗就1024x768，则进行下归并。

真正显示的流量，只要满足肉眼看着花哨不卡顿就行了。

Qt的信号槽、Event、底层线程模型、Concurrent、Qt容器、智能指针、Lambda绑定这些合起来，几乎是无敌的存在，各种计算密集、吞吐密集、计算+吞吐密集、均匀峰值、猝发峰值、平均性能指导优化、峰值性能指导优化、最差性能指导优化，都能应对。

### QT中使用另外的线程运行定时器

https://blog.csdn.net/zgrjkflmkyc/article/details/41381327

### Cannot send events to objects owned by a different thread.

https://blog.csdn.net/sinat_34156619/article/details/84197079

### QtConcurrent和processEvents

https://blog.csdn.net/weixin_39390491/article/details/129752566

### QtConcurrent调用函数抛出异常

子线程可以正常结束

直接调future.result会崩

调用resultCount输出为0，正常输出为1

### QT线程的三种使用方法（1、重写run，2、moveToThread，3、QtConCurrent::run）

https://blog.csdn.net/qq_41768362/article/details/111717619

## 缩放

### 介绍下qt中pointSize和pixelSize的区别？

在Qt中，`pointSize`和`pixelSize`是用于字体大小的两个属性。它们之间的区别在于单位和用途：

1. **pointSize（磅值）**：`pointSize`属性表示字体大小的磅值（point），磅值是印刷行业常用的长度单位，等于1/72英寸。在Qt中，1磅等于1/72英寸，因此设置字体大小为10点意味着字母“M”的高度为10/72英寸。

2. **pixelSize（像素值）**：`pixelSize`属性表示字体大小的像素值。这是字体实际在屏幕上显示时的像素大小。不同的显示设备有不同的像素密度，因此在不同的屏幕上，相同的像素大小可能会看起来不同大小。

因此，`pointSize`是相对单位，而`pixelSize`是绝对单位。通常情况下，对于屏幕上的文本显示，使用`pixelSize`更为直观和精确，而对于印刷等需要确定物理尺寸的场景，使用`pointSize`更为合适。

### qt字体大小发现的规律

|                    | 无缩放   | 带缩放                         | 带缩放带hidpi（此时整体程序变大）                    |
| ------------------ | ----- | --------------------------- | -------------------------------------- |
| 未设置字体大小场景          | 9pt大小 | pointSize值减小，实际显示大小不变       | **pointSize值减小，实际显示维持无缩放状态，相较于整体程序小了** |
| 设置字体大小为pointSize场景 | 按设定大小 | ***pointSize值不变，实际显示大小变大*** | pointSize值不变，实际显示与缩放相同；**但字体线条粗细存在问题** |
| 设置字体大小为pixelSize场景 | 按设定大小 | pixelSize值不变，实际显示大小不变       | pixelSize值不变，实际显示随程序变大；**但字体线条粗细存在问题**  |

### qt支持hidpi后中文字体粗细不一的问题处理

使用setHintingPreference(QFont::PreferNoHinting);

## 杂

### qt获取系统字体

```cpp
// 获取字体数据库
QFontDatabase fontDatabase;

// 获取系统中的字体系列
QStringList fontFamilies = fontDatabase.families();

// 显示字体系列
qDebug() << "Available Font Families:";
foreach (const QString &family, fontFamilies) {
    qDebug() << family;
}
```

### QWheelEvent::delta换成QWheelEvent::angleDelta

使用angleDelta().y()

### windeployqt注意事项

windeployqt后添加exe文件，还要加上exe文件所在目录

### qDebug输出到文件

https://blog.csdn.net/Black_zy/article/details/127055131

### QT编译错误error: C2872: “byte不明确的符号

https://blog.csdn.net/QQ_2558030393/article/details/112853455

### 计时器

QElapsedTimer/QTimer

### qt四舍五入问题

https://blog.csdn.net/pengweimei4769/article/details/105142400/

### qt图片资源不用放到qrc中

要有个pixmap的控件

### 在Qt中如何将弧度与角度转化

qRadiansToDegrees/qDegreesToRadians

## qml

### qml修改button颜色

https://qa.1r1g.com/sf/ask/2857645241/

### property alias XXX与property string XXX区别

带alias会出现property invalid的问题，但可以同步变化

使用string如果要同步变化，要有个onXXXChanged响应进行变化

### QVariantList及QVariantMap在qml里的使用

https://blog.csdn.net/joyopirate/article/details/112647231

### QML 自定义ComboBox控件

https://blog.csdn.net/weixin_43892328/article/details/122615847

## 使用QPalette设置背景颜色

```cpp
QPalette wdtPalette = ui->widget->palette();
wdtPalette.setColor(QPalette::Window, Qt::red);
ui->widget->setPalette(wdtPalette);
ui->widget->setAutoFillBackground(true);
```

## qt多线程

https://doc.qt.io/qt-5/threads.html

https://doc.qt.io/qt-5/threads-qobject.html

例子 

- Mandelbrot Example  
- Blocking Fortune Client Example

qt gui可以调用多线程, 看imagescaling的例子

多线程内不可以调用qt gui

## qss中id选择器只作用于对象本身

```css
#myWidget {
    background-color: red;
}

#myWidget * {
    background-color: red;
}
```

此时才等价于直接在对象上设定styleSheet

## QT 默认槽函数 connectSlotsByName浅析

https://blog.csdn.net/hellokandy/article/details/105100563

## qt pushbutton中default属性有什么用？

在Qt中，QPushButton的default属性用于指定一个按钮作为默认按钮。当用户按下"Enter"键时，具有default属性的按钮将被触发，这通常用于表示在对话框中的默认操作。

通过将一个按钮的default属性设置为true，您可以指定该按钮为默认按钮。这意味着，当用户在对话框中按下"Enter"键时，与default属性设置为true的按钮相关联的操作将被触发。

默认按钮通常用于表示对话框中的主要操作，例如"确定"或"提交"。这样，用户可以通过按下"Enter"键来快速执行这些操作，而无需手动单击按钮。

以下是一个简单的示例，说明了如何在Qt中创建一个具有default属性的QPushButton：

```cpp
// 创建一个默认按钮
QPushButton *defaultButton = new QPushButton("OK", this);
defaultButton->setDefault(true);

// 监听按钮被按下的信号
connect(defaultButton, &QPushButton::clicked, [=](){
    // 执行与默认按钮相关联的操作
});
```

在这个示例中，defaultButton被设置为默认按钮，这意味着当用户在对话框中按下"Enter"键时，与defaultButton相关联的操作将被执行。

通过使用default属性，您可以改善用户界面的交互性，使用户能够更轻松地执行对话框中的默认操作。

## Qt信号槽失效的原因
很有可能sender已经被干掉了

## Qt中QStackedWidget是什么？
`QStackedWidget` 是 Qt 框架中的一个用于管理多个子窗口部件（widgets）的容器部件。它可以堆叠多个子窗口部件，并且在任意时间点只显示其中的一个。

### 主要特点：
- **堆叠多个窗口部件**：`QStackedWidget` 可以包含多个子部件（如 `QWidget`），并且这些子部件彼此堆叠。每次只能看到一个子部件，其他的则被隐藏。
- **动态切换**：可以使用 `setCurrentIndex(int index)` 或 `setCurrentWidget(QWidget *widget)` 方法来切换当前显示的子部件。
- **索引管理**：子部件按照添加的顺序排列，每个子部件都有一个从 0 开始的索引。可以使用 `currentIndex()` 获取当前显示部件的索引，也可以使用 `widget(int index)` 获取特定索引的部件。

### 常见使用场景：
- **多页面界面**：`QStackedWidget` 常用于实现多页面的界面设计，用户通过按钮、标签或其他控制部件在不同页面间切换。
- **向导模式**：在向导模式中，每一步可能都是不同的界面，`QStackedWidget` 可以用于在这些界面之间切换。

### 简单示例代码：
```cpp
#include <QApplication>
#include <QStackedWidget>
#include <QPushButton>
#include <QVBoxLayout>
#include <QWidget>

int main(int argc, char *argv[]) {
    QApplication app(argc, argv);

    QWidget *window = new QWidget;

    // 创建一个 QStackedWidget
    QStackedWidget *stackedWidget = new QStackedWidget;

    // 创建多个子窗口部件
    QWidget *page1 = new QWidget;
    page1->setStyleSheet("background-color: red;");
    
    QWidget *page2 = new QWidget;
    page2->setStyleSheet("background-color: green;");
    
    QWidget *page3 = new QWidget;
    page3->setStyleSheet("background-color: blue;");

    // 将子部件添加到 QStackedWidget 中
    stackedWidget->addWidget(page1);
    stackedWidget->addWidget(page2);
    stackedWidget->addWidget(page3);

    // 创建按钮来切换页面
    QPushButton *button1 = new QPushButton("Show Page 1");
    QPushButton *button2 = new QPushButton("Show Page 2");
    QPushButton *button3 = new QPushButton("Show Page 3");

    QObject::connect(button1, &QPushButton::clicked, [=](){
        stackedWidget->setCurrentIndex(0);
    });

    QObject::connect(button2, &QPushButton::clicked, [=](){
        stackedWidget->setCurrentIndex(1);
    });

    QObject::connect(button3, &QPushButton::clicked, [=](){
        stackedWidget->setCurrentIndex(2);
    });

    // 布局管理
    QVBoxLayout *layout = new QVBoxLayout;
    layout->addWidget(stackedWidget);
    layout->addWidget(button1);
    layout->addWidget(button2);
    layout->addWidget(button3);

    window->setLayout(layout);
    window->show();

    return app.exec();
}
```

这个示例展示了如何使用 `QStackedWidget` 来切换显示不同的页面。通过点击不同的按钮，可以在不同的页面间进行切换。

### 其他相关方法：
- `addWidget(QWidget *widget)`：向堆栈中添加子部件。
- `removeWidget(QWidget *widget)`：从堆栈中移除子部件。
- `count()`：返回堆栈中子部件的数量。
- `currentWidget()`：获取当前显示的子部件。

## qt商业版无许可移除敏感文件单独打包，配合vs2022编译
- qmake编译报license问题，cmake编译运行正常
- cmake是开源的，qmake是商业公司的

## QDialog添加确定取消等按钮
使用QDialogButtonBox

## Qt发送信号报编译问题
- 可能是moc文件未生成
- 编译时需要将头文件加入，同步编译

## Qt中QTreeWidget::itemEntered
### Qt中QTreeWidget::itemEntered这个信号的含义是什么？
在 Qt 中，`QTreeWidget::itemEntered` 信号的含义是：当鼠标指针进入 `QTreeWidget` 中某个 `QTreeWidgetItem` 的区域时，触发此信号。这个信号可以用来响应用户将鼠标悬停到树形控件的某一项上。

#### `itemEntered` 信号的定义
```cpp
void QTreeWidget::itemEntered(QTreeWidgetItem *item, int column);
```

#### 参数说明
- `item`：指针，指向鼠标指向的 `QTreeWidgetItem` 项。
- `column`：整数，指示了该 `QTreeWidgetItem` 中的具体列。

#### 使用场景
`itemEntered` 信号一般用于鼠标悬停到 `QTreeWidgetItem` 上时进行相应处理，比如显示提示信息、改变外观等。不过，触发该信号的前提是树形控件的 `QTreeWidget` 要设置了 `setMouseTracking(true)`，这样才能在鼠标经过时持续跟踪项的变化。

#### 示例代码
```cpp
// 假设你有一个 QTreeWidget *treeWidget
treeWidget->setMouseTracking(true); // 必须启用鼠标跟踪

connect(treeWidget, &QTreeWidget::itemEntered, [](QTreeWidgetItem *item, int column) {
    if (item) {
        qDebug() << "Mouse entered item:" << item->text(column);
    }
});
```

在这个例子中，当鼠标进入某个 `QTreeWidgetItem` 的区域时，会输出该项的文本内容。

### 如果未设置treeWidget->setMouseTracking(true)，为什么选中或框选的时候会触发？
在 Qt 中，`itemEntered` 信号的触发依赖于 `QTreeWidget` 是否启用了鼠标跟踪功能 (`setMouseTracking(true)`)。不过，正如你所提到的，即使没有设置鼠标跟踪，`itemEntered` 信号在某些情况下仍然会触发，比如当你**选中或框选**某个项时。

这是因为在默认情况下，Qt 控件的鼠标事件跟踪行为是与用户交互相关的。具体来说，当你执行以下操作时，Qt 内部的事件处理机制可能会导致 `itemEntered` 信号的触发：

1. **选中项时**：当你点击选中一个 `QTreeWidgetItem` 时，鼠标的点击事件会导致控件在相应的项上聚焦。即使未启用鼠标跟踪，Qt 仍会检测并发送这个事件，从而导致 `itemEntered` 信号的触发。

2. **框选项时**：框选操作时，鼠标在拖动过程中会经过多个项，这时鼠标的移动事件 (`mouseMoveEvent`) 和项的选择变更事件可能都会触发 `itemEntered` 信号。虽然没有开启鼠标跟踪，但由于拖动框选行为会涉及对各个项的检测，`itemEntered` 仍然有可能被触发。

#### 内部机制解释
`setMouseTracking(true)` 主要控制的是**鼠标没有按下**的情况下，鼠标指针在控件上移动时，是否应该发出鼠标移动事件。如果没有启用鼠标跟踪，只有当鼠标按键按下或者有其他与鼠标有关的交互（如点击、拖动）时，才会发出相应的事件。

因此，在选中和框选的情况下，虽然你没有开启鼠标跟踪，**鼠标的点击和拖动操作**已经足够触发与项相关的事件处理，从而导致 `itemEntered` 信号的发出。这种行为依赖于 Qt 内部的事件传播机制。

#### 结论
即使没有开启 `setMouseTracking(true)`，`itemEntered` 信号在某些用户交互场景下依然可能触发，这是因为选中和框选操作仍然涉及鼠标事件的传播与处理。

### 框选有没有专门的信号？
在 Qt 中，**框选（rubber band selection）**操作并没有专门的信号来直接标识框选行为完成，但可以通过一些已有的信号与事件结合，实现对框选的检测和处理。

#### 检测框选的替代方法
虽然没有专门的框选信号，但你可以利用以下信号与事件组合来间接检测和处理框选行为。

##### 1. **`QTreeWidget::itemSelectionChanged`** 信号
这是一个常用信号，当树形控件中的选中项发生任何变化时（包括框选和单项选择），都会触发该信号：

```cpp
connect(treeWidget, &QTreeWidget::itemSelectionChanged, []() {
    qDebug() << "Selection changed!";
});
```
- **优点**：简单有效，可以检测到框选后选中的项发生变化。
- **缺点**：无法区分用户是通过框选还是单击选择触发的变化。

##### 2. **事件过滤器（Event Filter）** 
使用事件过滤器可以捕获 `mousePressEvent`、`mouseMoveEvent` 和 `mouseReleaseEvent`，从而检测是否发生了框选操作。

示例代码：
```cpp
class SelectionFilter : public QObject {
protected:
    bool eventFilter(QObject *obj, QEvent *event) override {
        if (event->type() == QEvent::MouseButtonPress) {
            qDebug() << "Mouse press detected.";
        } else if (event->type() == QEvent::MouseMove) {
            qDebug() << "Mouse move detected.";
        } else if (event->type() == QEvent::MouseButtonRelease) {
            qDebug() << "Mouse release detected. Possibly a rubber band selection.";
        }
        return QObject::eventFilter(obj, event); // 继续正常事件处理
    }
};

// 在你的代码中安装事件过滤器
SelectionFilter *filter = new SelectionFilter();
treeWidget->viewport()->installEventFilter(filter);
```
- **说明**：通过检测 `MouseButtonPress`、`MouseMove` 和 `MouseButtonRelease` 事件，可以推断是否进行了框选操作。
- **优点**：能够捕捉更多细节，比如用户是否拖动鼠标来进行框选。
- **缺点**：需要手动处理事件，逻辑稍微复杂。

##### 3. **自定义框选逻辑与信号**
如果你的框选操作对某些行为有特定需求（比如需要确认框选结束后做出反应），可以在上述基础上自定义信号。

例如：
```cpp
class MyTreeWidget : public QTreeWidget {
    Q_OBJECT
signals:
    void rubberBandSelectionFinished();

protected:
    void mouseReleaseEvent(QMouseEvent *event) override {
        QTreeWidget::mouseReleaseEvent(event);  // 调用基类的事件处理
        if (event->button() == Qt::LeftButton) {
            emit rubberBandSelectionFinished();
        }
    }
};
```

使用示例：
```cpp
MyTreeWidget *treeWidget = new MyTreeWidget();
connect(treeWidget, &MyTreeWidget::rubberBandSelectionFinished, []() {
    qDebug() << "Rubber band selection finished.";
});
```
- **优点**：通过自定义信号，你可以精确控制框选结束后的处理逻辑。

#### 总结
虽然 Qt 没有专门的框选信号，但你可以通过以下方式检测和处理框选操作：
1. 使用 **`itemSelectionChanged`** 信号监控选中项的变化。
2. 利用 **事件过滤器** 捕获鼠标事件，推断是否进行了框选。
3. **自定义信号与事件处理**，实现更精确的控制逻辑。

根据需求的不同，可以选择合适的方法来处理框选操作。


