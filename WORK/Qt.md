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

### QHBoxLayout, QVBoxLayout的setStretch的作用

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

使用setMaximumBlockCount(1), setWordWrapMode(QTextOption:: NoWrap)

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

yes or no用 `QMessageBox::StandardButton result=QMessageBox::question(&widget, "Title","text");`

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

构造里加上 `setAttribute(Qt::WA_DeleteOnClose)`

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

综上所述， `QStringLiteral` 适用于编译时已知且不需要字符编码转换的字符串，而 `QString::fromLocal8Bit` 更适用于需要在运行时进行字符编码转换的情况。

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

### qss格式化给: 与! 之间加空格问题

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

toDouble/QString::number(d, 'f', 2)

## 文件

### 检查文件是否可读

_access未生效

QFileInfo::isReadable未生效

QFile::isReadable生效	也未生效，为中文路径时返回false

QFile::open(QIODevice:: ReadOnly)生效

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

1. 假的多线程，可以适时调用 QCoreApplication::processEvents()，这样各种状态条都能刷新，比如for里面 i %1000==0时刷一次。

2. 真的双线程，用子线程做，主线程进度条。适时emit signal_process(v)，刷进度条

3. 线程池，比如 QFuture Mapreduce，适合批量密集均衡计算（每个核心预计在差不多的时间完成）。流水线线程池，适合批量密集的非均衡计算，每个事务分为微粒，最多一次处理100个微粒就重新排队，避免阻塞他人。

4. 控制刷新速率，子线程不断刷新一个曲线的数据缓存，主线程每秒只读30次。我们做过频谱仪，FFT缓存在后台均衡，主界面的刷新周期是固定的，就是30次。足够了。要刷新的东西是在另一个线程形成了最终产品才显示的。比如你65536点fft，但当前视窗就1024x768，则进行下归并。

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

在Qt中， `pointSize` 和 `pixelSize` 是用于字体大小的两个属性。它们之间的区别在于单位和用途：

1. **pointSize（磅值）**：`pointSize`属性表示字体大小的磅值（point），磅值是印刷行业常用的长度单位，等于1/72英寸。在Qt中，1磅等于1/72英寸，因此设置字体大小为10点意味着字母“M”的高度为10/72英寸。

2. **pixelSize（像素值）**：`pixelSize`属性表示字体大小的像素值。这是字体实际在屏幕上显示时的像素大小。不同的显示设备有不同的像素密度，因此在不同的屏幕上，相同的像素大小可能会看起来不同大小。

因此， `pointSize` 是相对单位，而 `pixelSize` 是绝对单位。通常情况下，对于屏幕上的文本显示，使用 `pixelSize` 更为直观和精确，而对于印刷等需要确定物理尺寸的场景，使用 `pointSize` 更为合适。

### qt字体大小发现的规律

|                    | 无缩放   | 带缩放                         | 带缩放带hidpi（此时整体程序变大）                    |
| ------------------ | ----- | --------------------------- | -------------------------------------- |
| 未设置字体大小场景          | 9pt大小 | pointSize值减小，实际显示大小不变       | **pointSize值减小，实际显示维持无缩放状态，相较于整体程序小了** |
| 设置字体大小为pointSize场景 | 按设定大小 | ***pointSize值不变，实际显示大小变大*** | pointSize值不变，实际显示与缩放相同；**但字体线条粗细存在问题** |
| 设置字体大小为pixelSize场景 | 按设定大小 | pixelSize值不变，实际显示大小不变       | pixelSize值不变，实际显示随程序变大；**但字体线条粗细存在问题**  |

### qt支持hidpi后中文字体粗细不一的问题处理

使用setHintingPreference(QFont:: PreferNoHinting); 

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

* Mandelbrot Example  
* Blocking Fortune Client Example

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

* **堆叠多个窗口部件**：`QStackedWidget` 可以包含多个子部件（如 `QWidget`），并且这些子部件彼此堆叠。每次只能看到一个子部件，其他的则被隐藏。
* **动态切换**：可以使用 `setCurrentIndex(int index)` 或 `setCurrentWidget(QWidget *widget)` 方法来切换当前显示的子部件。
* **索引管理**：子部件按照添加的顺序排列，每个子部件都有一个从 0 开始的索引。可以使用 `currentIndex()` 获取当前显示部件的索引，也可以使用 `widget(int index)` 获取特定索引的部件。

### 常见使用场景：

* **多页面界面**：`QStackedWidget` 常用于实现多页面的界面设计，用户通过按钮、标签或其他控制部件在不同页面间切换。
* **向导模式**：在向导模式中，每一步可能都是不同的界面，`QStackedWidget` 可以用于在这些界面之间切换。

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

* `addWidget(QWidget *widget)`：向堆栈中添加子部件。
* `removeWidget(QWidget *widget)`：从堆栈中移除子部件。
* `count()`：返回堆栈中子部件的数量。
* `currentWidget()`：获取当前显示的子部件。

## qt商业版无许可移除敏感文件单独打包，配合vs2022编译

* qmake编译报license问题，cmake编译运行正常
* cmake是开源的，qmake是商业公司的

## QDialog添加确定取消等按钮

使用QDialogButtonBox

## Qt发送信号报编译问题

* 可能是moc文件未生成
* 编译时需要将头文件加入，同步编译

## Qt中QTreeWidget::itemEntered

### Qt中QTreeWidget::itemEntered这个信号的含义是什么？

在 Qt 中， `QTreeWidget::itemEntered` 信号的含义是：当鼠标指针进入 `QTreeWidget` 中某个 `QTreeWidgetItem` 的区域时，触发此信号。这个信号可以用来响应用户将鼠标悬停到树形控件的某一项上。

#### `itemEntered` 信号的定义

```cpp
void QTreeWidget::itemEntered(QTreeWidgetItem *item, int column);
```

#### 参数说明

* `item`：指针，指向鼠标指向的 `QTreeWidgetItem` 项。
* `column`：整数，指示了该 `QTreeWidgetItem` 中的具体列。

#### 使用场景

`itemEntered` 信号一般用于鼠标悬停到 `QTreeWidgetItem` 上时进行相应处理，比如显示提示信息、改变外观等。不过，触发该信号的前提是树形控件的 `QTreeWidget` 要设置了 `setMouseTracking(true)` ，这样才能在鼠标经过时持续跟踪项的变化。

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

在 Qt 中， `itemEntered` 信号的触发依赖于 `QTreeWidget` 是否启用了鼠标跟踪功能 ( `setMouseTracking(true)` )。不过，正如你所提到的，即使没有设置鼠标跟踪， `itemEntered` 信号在某些情况下仍然会触发，比如当你**选中或框选**某个项时。

这是因为在默认情况下，Qt 控件的鼠标事件跟踪行为是与用户交互相关的。具体来说，当你执行以下操作时，Qt 内部的事件处理机制可能会导致 `itemEntered` 信号的触发：

1. **选中项时**：当你点击选中一个 `QTreeWidgetItem` 时，鼠标的点击事件会导致控件在相应的项上聚焦。即使未启用鼠标跟踪，Qt 仍会检测并发送这个事件，从而导致 `itemEntered` 信号的触发。

2. **框选项时**：框选操作时，鼠标在拖动过程中会经过多个项，这时鼠标的移动事件 (`mouseMoveEvent`) 和项的选择变更事件可能都会触发 `itemEntered` 信号。虽然没有开启鼠标跟踪，但由于拖动框选行为会涉及对各个项的检测，`itemEntered` 仍然有可能被触发。

#### 内部机制解释

`setMouseTracking(true)` 主要控制的是**鼠标没有按下**的情况下，鼠标指针在控件上移动时，是否应该发出鼠标移动事件。如果没有启用鼠标跟踪，只有当鼠标按键按下或者有其他与鼠标有关的交互（如点击、拖动）时，才会发出相应的事件。

因此，在选中和框选的情况下，虽然你没有开启鼠标跟踪，**鼠标的点击和拖动操作**已经足够触发与项相关的事件处理，从而导致 `itemEntered` 信号的发出。这种行为依赖于 Qt 内部的事件传播机制。

#### 结论

即使没有开启 `setMouseTracking(true)` ， `itemEntered` 信号在某些用户交互场景下依然可能触发，这是因为选中和框选操作仍然涉及鼠标事件的传播与处理。

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

* **优点**：简单有效，可以检测到框选后选中的项发生变化。
* **缺点**：无法区分用户是通过框选还是单击选择触发的变化。

##### 2. **事件过滤器（Event Filter）** 

使用事件过滤器可以捕获 `mousePressEvent` 、 `mouseMoveEvent` 和 `mouseReleaseEvent` ，从而检测是否发生了框选操作。

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

* **说明**：通过检测 `MouseButtonPress`、`MouseMove` 和 `MouseButtonRelease` 事件，可以推断是否进行了框选操作。
* **优点**：能够捕捉更多细节，比如用户是否拖动鼠标来进行框选。
* **缺点**：需要手动处理事件，逻辑稍微复杂。

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

* **优点**：通过自定义信号，你可以精确控制框选结束后的处理逻辑。

#### 总结

虽然 Qt 没有专门的框选信号，但你可以通过以下方式检测和处理框选操作：
1. 使用 **`itemSelectionChanged`** 信号监控选中项的变化。
2. 利用 **事件过滤器** 捕获鼠标事件，推断是否进行了框选。
3. **自定义信号与事件处理**，实现更精确的控制逻辑。

根据需求的不同，可以选择合适的方法来处理框选操作。

## qt使用connect函数连接信号槽时，信号和槽参数使用SLOT/SIGNAL宏与使用函数对象指针有什么区别？

在Qt中， `connect` 函数用于连接信号和槽，其调用方式主要有两种：使用 `SLOT` / `SIGNAL` 宏和直接使用函数指针。这两种方法的区别如下：

---

### 1. 使用 `SLOT` / `SIGNAL` 宏

**特点：**
* 使用字符串的形式指定信号和槽，比如 `SIGNAL(clicked())` 和 `SLOT(onButtonClicked())`。
* 通过 Qt 的元对象系统（Meta-Object System）进行信号和槽的查找与绑定。
* 需要在类中使用 `Q_OBJECT` 宏并在槽方法上声明 `public slots`、`protected slots` 或 `private slots`。

**优点：**
* 向后兼容 Qt 4 及更早版本。
* 代码中信号和槽关系直观明确，适合初学者。

**缺点：**
* 编译器无法检查信号和槽的匹配（如参数类型和数量），问题只能在运行时暴露。
* 使用字符串会使代码难以重构和维护，例如重命名信号或槽时可能导致运行时错误。

**示例代码：**

```cpp
connect(button, SIGNAL(clicked()), this, SLOT(onButtonClicked()));
```

---

### 2. 使用函数指针（Qt 5 引入的方式）

**特点：**
* 使用标准 C++ 的函数指针语法，明确指定信号和槽。
* 信号和槽的匹配在编译时由编译器检查，能有效减少运行时错误。
* 无需 `SIGNAL`/`SLOT` 宏，只需传递信号和槽的成员函数指针。

**优点：**
* 编译器对类型和参数进行静态检查，安全性更高。
* 代码更现代化，容易维护。
* 与 C++11+ 的语法一致，便于与标准库或其他现代库协作。

**缺点：**
* 不支持向前兼容（Qt 4 不支持）。
* 初学者可能不习惯。

**示例代码：**

```cpp
connect(button, &QPushButton::clicked, this, &MyClass::onButtonClicked);
```

---

### 区别对比总结

| 特性                       | `SLOT` / `SIGNAL` 宏                   | 函数指针                                 |
|--------------------------|--------------------------------|----------------------------------|
| **参数检查**               | 运行时检查                           | 编译时检查                             |
| **兼容性**                 | Qt 4 及更早版本                      | Qt 5 及更高版本                        |
| **代码现代化**             | 使用 Qt 特有的字符串语法，较过时         | 使用标准 C++ 语法，符合现代编程习惯          |
| **代码维护性**             | 重命名信号或槽时需手动修改宏中的字符串    | 自动适应重命名操作                       |
| **错误暴露时机**           | 运行时                              | 编译时                               |
| **学习曲线**               | 对初学者友好，容易理解                 | 需要一定的 C++ 基础                     |

---

### 推荐使用场景

1. **新项目：** 推荐使用函数指针方式，更安全、更现代化。
2. **旧项目：** 如果需要兼容旧代码，继续使用 `SLOT`/`SIGNAL` 宏。
3. **重构：** 逐步将旧项目中的宏方式迁移为函数指针方式。

总之，函数指针方式是更推荐的现代化选择，但需要根据实际需求平衡兼容性和安全性。

## 参数为 `std::string_view` 及 `const QString&` 的重载函数的坑

对于 `const char*` 会出现二义性

## Qt中在非主线程中对QGraphicsScene调用update有什么影响，是否会造成程序崩溃？

在 Qt 中， `QGraphicsScene` 是一个和 GUI 相关的对象，它不是线程安全的。根据 Qt 的文档要求，与 GUI 相关的操作，包括对 `QGraphicsScene` 的操作，通常必须在主线程（也称为 GUI 线程）中执行。

### 具体问题分析

1. **非主线程调用 `update` 的问题**：
   - `update()` 方法会触发场景的重新绘制。虽然 `update()` 本身不会直接执行绘制操作，而是发出一个请求，但它会操作一些内部的数据结构，例如场景中的项的几何信息或绘制队列。
   - 如果在非主线程中调用它，可能会导致与主线程中的其他操作发生竞争，从而引发数据不一致的问题。

2. **可能导致的问题**：
   - **数据竞争**：非主线程调用 `update()` 可能与主线程同时访问场景内部的数据结构，导致数据竞争。
   - **程序崩溃**：由于 `QGraphicsScene` 的线程不安全特性，非主线程调用可能会引发未定义行为，包括程序崩溃。
   - **图形异常**：即使程序没有崩溃，也可能导致渲染结果异常。

3. **Qt 的事件循环机制**：
   - Qt 使用事件循环来调度 GUI 更新。如果需要从非主线程更新 GUI 对象，应通过信号-槽机制将请求传递到主线程。

### 正确的做法

如果需要从非主线程触发 `QGraphicsScene::update()` ，可以使用以下方法：

#### 方法 1：使用信号-槽机制

```cpp
// 在非主线程中发出信号
emit requestSceneUpdate();
```

```cpp
// 在主线程中连接信号到槽
connect(this, &YourClass::requestSceneUpdate, scene, &QGraphicsScene::update);
```

#### 方法 2：使用 `QMetaObject::invokeMethod`

通过 `Qt::QueuedConnection` 将调用转移到主线程：

```cpp
QMetaObject::invokeMethod(scene, "update", Qt::QueuedConnection);
```

#### 方法 3：使用 `QTimer` 定时更新（如果适合）

在主线程中定期触发更新操作：

```cpp
QTimer::singleShot(0, scene, &QGraphicsScene::update);
```

### 总结

直接在非主线程中调用 `QGraphicsScene::update` 可能会导致未定义行为，甚至程序崩溃。推荐的做法是通过信号-槽机制或 `QMetaObject::invokeMethod` 将更新请求转移到主线程，以确保线程安全性和程序稳定性。

## `QMetaObject::invokeMethod` 和信号槽机制有什么区别？

`QMetaObject::invokeMethod` 和信号槽机制（Signal-Slot）的主要区别在于它们的使用场景和底层机制。以下是它们的比较和应用场景：

---

### **1. 基本定义**

* **信号槽机制**：
  + 是 Qt 的核心特性，用于在对象之间传递事件或通知。
  + 信号由对象发出，槽是一个普通函数或 lambda，连接到信号以响应事件。
  + 连接后，信号的发出会自动调用连接的槽函数。

* **QMetaObject::invokeMethod**：
  + 是一个用于动态调用 Qt 对象的成员函数的方法。
  + 通过函数名字符串和参数动态调用成员函数。
  + 可以指定调用的线程上下文（同步调用或异步调用）。

---

### **2. 底层机制**

* **信号槽**：
  + 基于 Qt 的元对象系统，编译时通过 `moc` 生成元信息。
  + 默认使用直接调用（Direct Connection）或事件队列（Queued Connection）来触发槽函数。
  + 自动类型检查，编译时发现连接错误。

* **QMetaObject::invokeMethod**：
  + 运行时通过反射机制调用，依赖于函数名字符串和参数列表。
  + 可以动态指定调用的线程上下文，例如：
    - `Qt::DirectConnection`（直接调用）。
    - `Qt::QueuedConnection`（跨线程异步调用，依赖事件队列）。
  + 不提供编译时检查，调用错误只能在运行时发现。

---

### **3. 使用场景**

* **信号槽**：
  + **强绑定**：用于对象间的长期连接。适合事件驱动的场景。
  + **类型安全**：连接的信号和槽的参数类型需要匹配，编译时检查错误。
  + **适合重复调用**：信号槽通常用于对象之间的持续通信，比如按钮点击触发操作。

* **QMetaObject::invokeMethod**：
  + **动态调用**：适合需要在运行时决定调用哪个函数的场景。
  + **跨线程调用**：在非 GUI 线程中调用 GUI 线程的成员函数，常用 `Qt::QueuedConnection`。
  + **无需预定义信号或槽**：用于临时操作，而无需像信号槽那样定义固定的接口。
  + **反射性调用**：适合插件系统或动态框架中通过名称调用方法。

---

### **4. 对比总结**

| 特性                  | 信号槽机制                         | QMetaObject::invokeMethod         |
|-----------------------|------------------------------------|------------------------------------|
| **类型检查**          | 编译时检查                          | 运行时检查，易出错                |
| **动态性**            | 需要预定义信号和槽                  | 无需预定义，动态调用              |
| **线程支持**          | 支持跨线程（通过 `QueuedConnection` ）| 支持跨线程（通过 `QueuedConnection` ）|
| **性能**              | 较高（直接调用）                    | 较低（反射机制，运行时解析）       |
| **主要用途**          | 事件驱动机制                        | 动态、临时调用                     |

---

### **5. 示例对比**

#### 信号槽机制

```cpp
// 定义信号和槽
class MyClass : public QObject {
    Q_OBJECT
signals:
    void mySignal(int value);

public slots:
    void mySlot(int value) {
        qDebug() << "Slot called with value:" << value;
    }
};

// 使用
MyClass obj;
QObject::connect(&obj, &MyClass::mySignal, &obj, &MyClass::mySlot);
emit obj.mySignal(42); // 调用槽函数
```

#### QMetaObject::invokeMethod

```cpp
// 动态调用成员函数
class MyClass : public QObject {
    Q_OBJECT
public:
    Q_INVOKABLE void mySlot(int value) {
        qDebug() << "Slot called with value:" << value;
    }
};

// 使用
MyClass obj;
QMetaObject::invokeMethod(&obj, "mySlot", Qt::DirectConnection, Q_ARG(int, 42)); // 动态调用槽函数
```

---

### **6. 选择建议**

* **长期绑定的事件驱动**：使用信号槽机制。
* **动态、临时调用（如跨线程调用或插件系统）**：使用 `QMetaObject::invokeMethod`。
* **跨线程调用**：两者都可以，但 `QMetaObject::invokeMethod` 更灵活。

## Qt高缩放下字体存在问题

 `QFont::setHintingPreference`

 `QFont::PreferFullHinting`

## `QFont::setHintingPreference` 作用

`QFont::setHintingPreference` 是 Qt 中 `QFont` 类的一个方法，用于设置字体的 Hinting（字形微调）首选项。Hinting 是一种字体优化技术，通过调整字体轮廓以适应像素网格，从而提高文本在屏幕上的可读性，尤其是在小尺寸字体上。

### 用法

```cpp
void QFont::setHintingPreference(QFont::HintingPreference hintingPreference)
```

### 参数说明

* `QFont::HintingPreference` 是一个枚举类型，用于指定 Hinting 的偏好设置。它包括以下值：
  1. `QFont::PreferDefaultHinting`  
     默认 Hinting 设置，由字体引擎决定。

  2. `QFont::PreferNoHinting`  
     禁用 Hinting，适合更平滑的矢量字体渲染。

  3. `QFont::PreferVerticalHinting`  
     仅使用垂直方向的 Hinting。

  4. `QFont::PreferFullHinting`  
     启用完全 Hinting，通常用于需要锐利边缘的文本。

### 示例

```cpp
QFont font;
font.setFamily("Arial");
font.setPointSize(12);
font.setHintingPreference(QFont::PreferFullHinting);
```

在上述代码中，字体 `Arial` 被设置为 12pt，并启用了完全 Hinting。

### 使用场景

* **提高小字体的可读性**：在小字体上启用 Hinting（如 `PreferFullHinting`），可以减少模糊感。
* **渲染矢量字体**：对于高分辨率显示器或大字体，禁用 Hinting（如 `PreferNoHinting`）通常会得到更平滑的外观。
* **兼容性调整**：根据目标平台和显示设备调整 Hinting 策略，以达到最佳效果。

### 注意事项

1. **平台相关性**：Hinting 效果可能因操作系统和字体渲染引擎而异。例如，在 Linux 上可能依赖 FreeType，而在 Windows 上依赖 DirectWrite。
2. **字体支持**：某些字体可能不支持 Hinting，设置可能无效。

通过合理设置 `setHintingPreference` ，可以显著优化文本的渲染效果。

## Qt添加三方字体

* 字体文件放入项目中
* qrc文件引用之

```cpp
    auto ret = QFontDatabase::addApplicationFont(":/fontFiles/SourceHanSansCN-Regular.otf");
    auto families = QFontDatabase::applicationFontFamilies(0);
    f.setHintingPreference(QFont::PreferFullHinting);
    f.setFamily("Source Han Sans CN");
```

## Qt如何让程序在高缩放下用一种字体，在低缩放下用另一种字体？

在Qt中，你可以通过检测显示器的DPI（Dots Per Inch）来判断当前的缩放比例，然后根据不同的DPI设置不同的字体。以下是一个示例代码，展示了如何实现这一点：

```cpp
#include <QApplication>
#include <QLabel>
#include <QScreen>
#include <QFont>

int main(int argc, char *argv[]) {
    QApplication app(argc, argv);

    // 获取主屏幕的DPI
    QScreen *screen = app.primaryScreen();
    float dpi = screen->logicalDotsPerInch();

    // 创建一个标签来显示文本
    QLabel label("Hello, Qt!");

    // 根据DPI设置不同的字体
    QFont font;
    if (dpi > 120) { // 例如高缩放
        font.setFamily("HighDpiFont");
        font.setPointSize(14);
    } else { // 例如低缩放
        font.setFamily("LowDpiFont");
        font.setPointSize(10);
    }
    label.setFont(font);

    // 显示标签
    label.show();

    return app.exec();
}
```

解释：
1. 获取主屏幕的DPI：`QScreen *screen = app.primaryScreen();` 和 `float dpi = screen->logicalDotsPerInch();` 用于获取主屏幕的逻辑DPI。
2. 根据DPI选择不同的字体：通过判断DPI值，如果DPI大于120（表示高缩放），则设置为高DPI字体；否则设置为低DPI字体。
3. 设置字体并显示标签。

你可以根据自己的需求调整DPI的阈值和字体属性，以确保在不同缩放比例下显示适当的字体。

## QGridLayout::addWidget

在Qt中，如果你想更改一个控件在QGridLayout中的跨度，而不移除它，可以直接使用addWidget重新设置控件的位置和跨度。addWidget方法会自动更新控件的布局参数，而不会重复添加控件。

## QString的复制开销是怎样的？

QString 使用隐式共享（拷贝写时复制）机制，因此复制一个 QString 的操作非常高效。具体来说：

* **浅拷贝操作**：复制时仅仅复制内部指针和引用计数，这个操作是常数时间 O(1) 的，开销非常低。
* **写时复制**：只有当你对复制后的 QString 进行修改时，才会触发数据的实际拷贝（分离），这时的复制开销才会和字符串的长度相关。

这种设计使得在大多数情况下，即使频繁传递 QString 作为值参数，其性能也不会成为瓶颈。

## Qt断言当前是在主线程中

```cpp
assert(QThread::currentThread() == QCoreApplication::instance()->thread());
```

## Qt信号槽连接时信号和槽的参数数量可以不一致吗？

在Qt的信号槽机制中，信号和槽的参数数量可以不一致，但需要满足以下条件：

1. **槽的参数数量 ≤ 信号的参数数量**  
   槽的参数数量可以比信号少，此时槽会忽略信号多余的参数。但槽的参数类型和顺序必须与信号的前N个参数完全匹配。

   *示例：*  
   信号： `void mySignal(int, QString, bool)`

   槽： `void mySlot(int, QString)` ✅ 合法（忽略第三个参数）  
   槽： `void mySlot(int)` ✅ 合法（忽略后两个参数）  
   槽： `void mySlot(QString, int)` ❌ 非法（顺序和类型不匹配）

2. **槽的参数数量不能多于信号**  
   如果槽的参数数量超过信号，连接会失败（编译错误或运行时警告）。

   *示例：*  
   信号： `void mySignal(int)`

   槽： `void mySlot(int, QString)` ❌ 非法

3. **类型必须严格匹配**  
   参数类型需要完全一致（允许隐式转换的类型，如 `int` 到 `double` ，但依赖Qt的元对象系统支持）。

4. **连接方式的影响**  
   - **旧式语法（Qt4的 `SIGNAL` / `SLOT` 宏）**：  

     允许参数数量不一致，但可能在运行时报错（如 `QObject::connect: Incompatible sender/receiver arguments` ）。

   
   - **新式语法（Qt5的函数指针或Lambda）**：  

     要求参数数量和类型严格匹配，否则直接编译错误。

*总结*：  
* **允许槽的参数少于信号**（需类型和顺序一致）  
* **禁止槽的参数多于信号**  
* 推荐使用新式语法（编译期检查更安全），若需要灵活性，可结合Lambda适配参数。

## Qt中connect函数，槽函数是lambda表达式，receiver参数的作用

在Qt中使用 `connect` 函数时，即使槽函数是lambda表达式， `receiver` 参数仍然起着关键作用。以下是详细解释：

### `receiver` 参数的核心作用

1. **生命周期管理**  
`receiver` 参数用于将信号槽连接的生存期绑定到该对象。当 `receiver` 对象被销毁时，Qt会自动断开连接，避免在对象已销毁时调用槽函数（包括lambda表达式），从而防止悬空指针和未定义行为。

2. **作用域与`this`访问**  
   当lambda中需要访问类的成员变量或方法时，通常需要显式捕获 `this` （例如 `[this]{}` ）。此时，将 `receiver` 设为 `this` （即当前对象）可确保：如果当前对象被销毁，连接会被自动断开，避免lambda调用时访问已释放的内存。

---

### 不同场景下的表现

#### 1. 指定 `receiver` 为 `this`

```cpp
connect(sender, &Sender::signal, this, [this]() {
    this->doSomething(); // 访问成员方法
});
```

* **行为**：当`this`（接收者对象）被销毁时，连接自动断开，后续信号不会触发lambda。
* **安全性**：避免在对象销毁后调用lambda，确保安全。

#### 2. 省略 `receiver` 或设为 `nullptr`

```cpp
connect(sender, &Sender::signal, nullptr, []() {
    // 不依赖外部对象
});
```

* **行为**：连接的生命周期仅与`sender`绑定。当`sender`被销毁时，连接断开。
* **风险**：如果lambda隐式依赖其他对象（如通过捕获`this`），但未指定`receiver`，则这些对象销毁后，lambda仍可能被调用，导致未定义行为。

#### 3. `receiver` 为局部对象

```cpp
void MyClass::setupConnection() {
    QObject* localObj = new QObject(this);
    connect(sender, &Sender::signal, localObj, [=]() {
        // 使用localObj或其他捕获变量
    });
}
```

* **行为**：当`localObj`被销毁时，连接自动断开，即使lambda未直接使用`localObj`。
* **注意**：lambda可能通过捕获（如`[=]`）隐式依赖其他对象，需确保其生存期。

---

### 关键结论

* **始终显式设置`receiver`**：除非明确需要全局/静态生命周期，否则应指定`receiver`为相关对象（如`this`），以利用Qt的自动连接管理。
* **避免悬空调用**：通过`receiver`的生命周期绑定，确保lambda仅在相关对象存活时被调用。
* **lambda捕获与`receiver`无关**：即使lambda未捕获任何变量，`receiver`仍独立管理连接生存期。捕获变量需自行确保有效性。

### 示例：安全用法

```cpp
class MyClass : public QObject {
    Q_OBJECT
public:
    void setupConnection() {
        connect(sender, &Sender::signal, this, [this]() {
            // 安全访问成员，当this销毁时连接自动断开
            this->updateUI();
        });
    }
};
```

通过正确设置 `receiver` ，可兼顾代码简洁性与内存安全性。

## Qt要不要用emit发送信号，emit有什么用？

在Qt中， `emit` 关键字用于显式地发送信号，但其本质是一个宏，在编译时会被替换为空。以下是关于 `emit` 的详细说明：

### **1. `emit` 的作用**

* **代码可读性**：`emit`的主要作用是提高代码的可读性。通过添加`emit`，开发者可以直观地区分**信号发射**和普通函数调用。

```cpp
  emit mySignal(); // 明确表示这是一个信号发射
  mySlot();        // 普通槽函数调用
```

* **语法提示**：它向阅读代码的人表明，此处触发了对象间的通信（信号-槽机制），而非执行普通逻辑。

### **2. 技术必要性**

* **非必需**：从技术上讲，`emit`并非必须。以下两种写法完全等效：

```cpp
  emit mySignal(arg1, arg2); // 使用emit
  mySignal(arg1, arg2);      // 不使用emit
```

  + 因为`emit`在预处理阶段会被替换为空，编译器实际看到的代码是`mySignal(arg1, arg2);`。

### **3. 编码规范建议**

* **推荐使用**：尽管技术上可省略，但建议遵循以下规范：
  + **清晰性**：在复杂代码中，`emit`能快速标识信号发射位置。
  + **团队协作**：统一代码风格，减少理解成本。
* **项目约定**：若团队规定不使用`emit`，则需保持一致性，但需注意代码的可读性。

### **4. 信号的本质**

* **自动生成函数**：Qt的MOC（元对象编译器）会为信号生成对应的函数。调用信号时，实际是调用MOC生成的代码，进而触发连接的槽。
* **底层机制**：信号函数内部通过`QMetaObject::activate()`实现槽的调用，与`emit`无关。

### **5. 特殊情况**

* **旧代码兼容**：某些遗留代码可能依赖`emit`宏的其他定义（极罕见情况），需检查项目配置。
* **宏冲突**：若自定义了`emit`宏，可能导致问题，此时可通过`#undef emit`恢复默认。

### **总结**

| 使用场景      | 建议使用 `emit` 以提高代码可读性   |
| --------- | -------------------- |
| **技术必要性** | **非必需，编译后与直接调用信号等效** |
| **规范建议**  | **遵循团队或项目约定，保持一致性**  |

通过合理使用 `emit` ，可以使Qt代码更易于维护和理解，尤其是在多人协作项目中。

## Qt对话框打开时移除焦点

重写showEvent，增加setFocus激活自身

## QString传参测试

```cpp
#include <iostream>
#include <QString>         // QCoreApplication for QString initialization
#include <QCoreApplication> // QCoreApplication for QString functionality
#include <chrono>          // For high-resolution timing
#include <string>          // For std::string conversion (optional)
#include <iomanip>

// 全局 volatile 变量，用于防止编译器将对参数的使用优化掉
// 通过将字符串长度赋值给它，确保s.length()被调用，且结果不被优化掉
volatile int dummy_length_sink = 0;

// 函数1: 按值传递 QString
void funcByValue(QString s) {
    // 访问字符串的长度，确保s被“使用”了，防止编译器优化掉整个函数调用
    // 将结果赋值给volatile变量，进一步阻止优化
    dummy_length_sink = s.length();
}

// 函数2: 按const引用传递 QString
void funcByReference(const QString& s) {
    // 访问字符串的长度，确保s被“使用”了，防止编译器优化掉整个函数调用
    // 将结果赋值给volatile变量，进一步阻止优化
    dummy_length_sink = s.length();
}

// 测量函数执行时间的通用模板
template <typename Func>
long long measureExecutionTime(Func func, const QString& testString, long long iterations) {
    auto start = std::chrono::high_resolution_clock::now();

    for (long long i = 0; i < iterations; ++i) {
        func(testString);
    }

    auto end = std::chrono::high_resolution_clock::now();
    return std::chrono::duration_cast<std::chrono::nanoseconds>(end - start).count();
}

int main(int argc, char *argv[]) {
    // QCoreApplication是Qt应用程序的基础，确保QString等Qt类正常工作
    QCoreApplication a(argc, argv);

    long long numIterations = 10000000; // 1000万次迭代，以获得可测量的结果

    std::cout << "--- QString Parameter Passing Efficiency Test ---" << std::endl;
    std::cout << "Number of iterations per test: " << numIterations << std::endl << std::endl;

    // --- 测试短字符串 ---
    QString shortString = "Hello, world!";
    std::cout << "Testing with a short string (length: " << shortString.length() << "):" << std::endl;

    // 测试按值传递
    long long timeByValueShort = measureExecutionTime(
        [](const QString& s){ funcByValue(s); }, // Lambda wrapper to pass QString by const ref to measureExecutionTime
        shortString,
        numIterations
        );
    std::cout << "  By Value (short string):      " << timeByValueShort << " ns" << std::endl;

    // 测试按引用传递
    long long timeByReferenceShort = measureExecutionTime(
        [](const QString& s){ funcByReference(s); }, // Lambda wrapper
        shortString,
        numIterations
        );
    std::cout << "  By Const Reference (short string): " << timeByReferenceShort << " ns" << std::endl;
    std::cout << std::endl;

    // --- 测试长字符串 ---
    // 创建一个包含10000个字符的长字符串
    QString longString(10000, 'A');
    std::cout << "Testing with a long string (length: " << longString.length() << "):" << std::endl;

    // 测试按值传递
    long long timeByValueLong = measureExecutionTime(
        [](const QString& s){ funcByValue(s); },
        longString,
        numIterations
        );
    std::cout << "  By Value (long string):       " << timeByValueLong << " ns" << std::endl;

    // 测试按引用传递
    long long timeByReferenceLong = measureExecutionTime(
        [](const QString& s){ funcByReference(s); },
        longString,
        numIterations
        );
    std::cout << "  By Const Reference (long string):  " << timeByReferenceLong << " ns" << std::endl;
    std::cout << std::endl;

    // 总结
    std::cout << "--- Summary ---" << std::endl;
    if (timeByValueShort > 0) {
        double ratioShort = static_cast<double>(timeByValueShort) / timeByReferenceShort;
        std::cout << "Short string: By value is " << std::fixed << std::setprecision(2) << ratioShort << "x slower than by const reference." << std::endl;
    }
    if (timeByValueLong > 0) {
        double ratioLong = static_cast<double>(timeByValueLong) / timeByReferenceLong;
        std::cout << "Long string: By value is " << std::fixed << std::setprecision(2) << ratioLong << "x slower than by const reference." << std::endl;
    }

    // 对于这种简单的控制台程序，不需要 QApplication 的事件循环
    // return a.exec();
    return 0;
}
```

```cpp
#include <QString>
#include <QElapsedTimer>
#include <iostream>

// 测试函数1：直接传递QString
void testByValue(QString str) {
    // 防止优化
    volatile int dummy = str.length();
    (void)dummy;
}

// 测试函数2：传递const QString引用
void testByReference(const QString& str) {
    // 防止优化
    volatile int dummy = str.length();
    (void)dummy;
}

// 测试函数3：传递QString右值引用
void testByRvalueReference(QString&& str) {
    // 防止优化
    volatile int dummy = str.length();
    (void)dummy;
}

int main() {
    const int iterations = 1000000;
    QString testString = "This is a test string that is long enough to avoid SSO (Small String Optimization)";

    // 测试直接传递QString
    QElapsedTimer timer;
    timer.start();
    for (int i = 0; i < iterations; ++i) {
        testByValue(testString);
    }
    qint64 byValueTime = timer.elapsed();

    // 测试传递const QString引用
    timer.restart();
    for (int i = 0; i < iterations; ++i) {
        testByReference(testString);
    }
    qint64 byReferenceTime = timer.elapsed();

    // 测试传递QString右值引用
    timer.restart();
    for (int i = 0; i < iterations; ++i) {
        testByRvalueReference(QString(testString)); // 创建临时对象
    }
    qint64 byRvalueReferenceTime = timer.elapsed();

    // 输出结果
    std::cout << "Test results (iterations: " << iterations << "):\n";
    std::cout << "By value: " << byValueTime << " ms\n";
    std::cout << "By const reference: " << byReferenceTime << " ms\n";
    std::cout << "By rvalue reference: " << byRvalueReferenceTime << " ms\n";
    std::cout << "Difference (value - reference): " << (byValueTime - byReferenceTime) << " ms\n";

    return 0;
}

```
