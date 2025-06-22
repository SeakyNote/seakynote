## obs来源只要添加画面就行，混音器自动会添加麦克风和音频

## 墨刀缩放问题

注意桌面缩放和浏览器缩放

## 打包工具

https://learn.microsoft.com/zh-cn/windows/msix/desktop/desktop-to-uwp-third-party-installer

## 同一个目录clang-format在不同用户电脑结果不同；看是不是调的clang-format程序不一致，调整下用户环境变量的路径

## ppt调整通用模板

视图-幻灯片母板

## CCNET

https://blog.csdn.net/xqj198404/article/details/24397129

## 解析一个dll依赖的dll

dumpbin(vs自带)

 `dumpbin /dependents YourLibrary.dll`

## 下载chrome

https://chromeenterprise.google/download/

## doxygen

https://www.eet-china.com/mp/a127830.html

## ppt中表格行高

布局-高度

## excel表格自动换行

开始-自动换行

## ffmpeg转gif

输入和输出之间夹参数可压缩大小
 `ffmpeg -i 20241008_093728.mp4 -s 958x580 20241008_093728.gif`

 `ffmpeg -i 20241008_093728.mp4 -r 5 20241008_093728.gif`

## notepad++ 变灰无法编辑

https://blog.csdn.net/Ellen_Tangxiang/article/details/128913882

## graphviz模板

```
digraph template{
    fontname = "SimHei";
    node [penwidth=3, fontname="SimHei"];
    node [color="#c46747"];
    node [shape = box, style=rounded];
    node [margin="0.3,0.055"]
}
```

## 对于GUI交互型的桌面程序，如何进行自动化测试？

对于GUI交互型的桌面程序，如何进行自动化测试？

针对GUI交互型桌面程序的自动化测试，可以采用以下方法和工具：

---

### 1. **明确测试目标与范围**

#### 需要回答的问题：

* 你要测试的是哪些功能？（按钮点击、菜单操作、表单输入、窗口导航等）
* 是否需要进行UI布局测试或跨平台兼容性测试？

---

### 2. **选择合适的自动化测试工具**

不同工具有各自的优点，具体选择取决于你的开发技术栈和需求：

#### **常见工具**：

* **SikuliX**：
  + 通过屏幕截图和图像识别技术实现操作模拟。
  + 优点：支持任意GUI技术栈。
  + 缺点：对分辨率和界面外观较敏感。

* **AutoIt**：
  + 一个轻量级的Windows自动化工具，专注于键盘、鼠标和窗口控制。
  + 优点：脚本易于编写，适合小型程序的自动化测试。
  + 缺点：不适合复杂的GUI测试。

* **Pywinauto**（针对Windows）：
  + 基于Python，用于Windows GUI的自动化。
  + 优点：可直接操作窗口组件，支持多种窗口库（如Win32、UIA）。
  + 缺点：仅适用于Windows平台。

* **Selenium + Appium**（针对跨平台或Web/Hybrid程序）：
  + Selenium更适合Web应用，但结合Appium可以测试桌面应用。
  + 优点：跨平台支持，功能强大。
  + 缺点：配置复杂，启动成本较高。

* **TestComplete**：
  + 一款商业化的自动化测试工具，支持多种技术栈（如WPF、WinForms、JavaFX）。
  + 优点：功能全面，提供脚本录制功能。
  + 缺点：昂贵。

* **Robot Framework**：
  + 一个基于关键字的自动化测试框架，可通过扩展支持桌面应用。
  + 优点：代码可读性高，支持多平台。

#### **选择的考虑因素**：

* 你的桌面应用技术栈（例如C++/Qt，C#/WPF等）。
* 脚本语言熟悉程度（如Python、VBScript等）。
* 是否需要跨平台支持。

---

### 3. **设计测试用例**

* 按**功能点**划分：
  + **基础操作**：按钮点击、文本输入、菜单选择。
  + **窗口导航**：页面跳转、对话框打开与关闭。
  + **输入验证**：检查输入错误时的反馈。
  + **边界测试**：处理极限数据或不符合预期的操作。

* 按**用户行为**划分：
  + 正常流程：模拟用户典型操作。
  + 异常流程：测试用户误操作（如非法输入）。

---

### 4. **编写脚本并运行**

#### **步骤**：

1. **录制与回放**：
   - 使用工具（如TestComplete、Selenium IDE）录制交互操作。
   - 回放测试，确保脚本运行正常。

2. **自定义脚本**：
   - 如果录制无法覆盖全部需求，可编写自定义脚本。
   - 使用工具API模拟鼠标点击、键盘输入、窗口切换等。

3. **断言检查**：
   - 验证预期结果是否正确，如UI元素是否存在、文本内容是否匹配。

---

### 5. **处理动态元素**

* 对于动态生成或内容不断变化的UI元素，可通过以下方式定位：
  + 使用唯一属性（如ID、Class、AutomationID）。
  + 通过层级定位（如父子关系）。

---

### 6. **集成与持续交付**

* 将测试脚本集成到CI/CD管道（如Jenkins、GitHub Actions）。
* 确保每次代码提交后自动运行测试，及时捕获问题。

---

### 7. **报告与维护**

* 自动生成测试报告，记录通过/失败的测试用例及其原因。
* 定期更新测试脚本以适应UI变化。

---

### 示例代码

以下是一个简单的**Pywinauto**示例：

```python
from pywinauto import Application

# 启动应用程序
app = Application(backend="uia").start("your_application.exe")

# 获取主窗口
window = app.window(title="Your App Title")

# 模拟用户操作
window['Button1'].click()
window['TextBox1'].type_keys("Hello, World!")
window['SubmitButton'].click()

# 断言检查
assert window['ResultLabel'].window_text() == "Success", "Test Failed!"
```

## 对于Qt软件，选择哪个比较合适？

对于基于 **Qt** 的桌面软件，自动化测试工具的选择主要取决于需求的复杂度、技术栈以及预算。以下是几个特别适合 **Qt** 软件的自动化测试工具及其优劣对比：

---

### **1. Squish for Qt**

**官方推荐工具**，由 Froglogic 专门针对 Qt 开发。

#### **优点**：

* **深度集成 Qt**：支持所有 Qt 技术（Qt Widgets、Qt Quick/QML 等）。
* **跨平台支持**：支持 Windows、Linux、macOS 等。
* **脚本灵活性**：支持多种脚本语言（Python、JavaScript、TCL 等）。
* **对象识别强大**：通过 Qt 对象层直接访问 GUI 元素（不依赖图像识别）。
* **录制回放功能**：可通过录制生成测试用例，减少脚本编写工作。
* 提供 **BDD（行为驱动开发）支持**，可编写自然语言风格的测试用例。

#### **缺点**：

* **高成本**：为商业软件，许可证费用较高。
* 配置复杂性：初次设置需要一定的学习成本。

#### **适用场景**：

* 复杂的 Qt 项目，特别是需要测试 QML 或 Qt Quick 的场景。
* 企业级项目，有预算支持。

---

### **2. Pywinauto + Qt Accessibility API**

**开源方案**，基于 Python 和 Qt 的辅助功能（Accessibility）。

#### **优点**：

* **免费开源**：无需任何许可费用。
* **轻量级**：适合简单的 Qt 应用。
* 可通过 Qt 的 `Accessible` 属性访问 UI 元素。
* Python 编程语言友好，社区支持良好。

#### **缺点**：

* **支持有限**：复杂控件（如自定义绘制的控件）可能无法被识别。
* 脚本编写工作量较大，不支持录制与回放。

#### **适用场景**：

* 简单的 Qt Widgets 应用。
* 希望避免高额成本，并且对测试自动化有基本要求的项目。

---

### **3. AutoIt（结合Qt控件识别工具）**

**轻量级方案**，主要通过鼠标和键盘事件来控制。

#### **优点**：

* 简单易用，适合入门用户。
* 适合固定界面布局的应用。
* 免费。

#### **缺点**：

* **界面变化敏感**：对动态界面或分辨率适应性较差。
* 缺乏对 Qt 控件的直接访问能力。

#### **适用场景**：

* 小型项目，测试工作主要是模拟简单操作。

---

### **4. TestComplete**

一款商业化的通用自动化测试工具，支持多种技术栈，包括 **Qt**。

#### **优点**：

* **广泛支持**：支持多种 GUI 技术，包括 Qt Widgets 和 QML。
* 提供脚本录制功能，降低入门门槛。
* 强大的报告和分析功能。

#### **缺点**：

* **高成本**：与 Squish 类似，许可证费用高。
* 对 Qt 的支持不如 Squish 原生。

#### **适用场景**：

* 跨技术栈的桌面应用测试（如 Qt + 非 Qt 混合开发）。
* 企业级团队。

---

### **5. Katalon Studio + Qt WebView/Hybrid Apps**

如果你的 Qt 应用使用了 **WebView** 或包含 Web 元素，可以结合 Katalon 进行测试。

#### **优点**：

* 对 WebView 及混合应用的支持较好。
* 免费基础版本。

#### **缺点**：

* 对 Qt 原生控件的支持较弱。
* 适用于特定场景（如基于 Web 技术的 Qt 应用）。

#### **适用场景**：

* Qt 应用包含大量 WebView 或 Hybrid 元素。

---

### **推荐的选择**

#### **企业级项目或复杂需求**：

* 首选 **Squish**：专门针对 Qt 开发，深度支持复杂控件。
* 备选 **TestComplete**：如果项目涉及多技术栈的混合测试。

#### **开源或预算有限的项目**：

* 使用 **Pywinauto** 配合 Qt Accessibility API。
* 对于简单需求，可考虑 **AutoIt**。

#### **特殊需求**：

* 如果包含 Web 技术，可引入 **Katalon** 或 Selenium 作为补充。

---

### **示例：使用 Squish 测试 Qt 应用**

```python
def main():
    startApplication("your_qt_application")
    
    # 访问按钮并点击
    clickButton(waitForObject(":MainWindow.Button"))
    
    # 输入文本
    type(waitForObject(":MainWindow.TextInput"), "Hello, World!")
    
    # 验证标签内容
    test.compare(waitForObject(":MainWindow.Label").text, "Expected Text")
```

## 通过pywinauto+Qt Accessibility API的自动化测试

**通过 Pywinauto 和 Qt Accessibility API 进行自动化测试** 是一种轻量化的开源方案，适用于 **Windows 平台** 的 Qt 应用程序。以下是详细的介绍和实现方法：

---

## **1. 基本原理**

* **Pywinauto** 是一个 Python 库，专用于自动化 Windows GUI 应用程序。它可以通过 UI Automation (UIA) 或 Win32 接口操作 GUI 元素。
* **Qt Accessibility API** 是 Qt 提供的辅助功能接口（基于 Windows UIA 的实现），允许自动化工具识别 Qt 界面上的控件。

通过 Pywinauto 与 Qt Accessibility 的结合，可以识别和操作 Qt 应用中的窗口、按钮、输入框等控件，达到自动化测试的目的。

---

## **2. 环境准备**

### **安装必要工具**

1. 安装 Python 3.x
2. 安装 Pywinauto 库：
   

```bash
   pip install pywinauto
```

3. 确保你的 Qt 应用启用了 **Accessibility** 支持（Qt 默认开启）。
   - 可以通过命令行设置：

     

```bash
     set QT_ACCESSIBILITY=1
```

   - 或在代码中手动启用：

     

```cpp
     QCoreApplication::setAttribute(Qt::AA_EnableHighDpiScaling);
```

### **检查 Accessibility 状态**

使用 Microsoft 提供的工具 **Inspect.exe**（随 Windows SDK 提供）检查你的 Qt 应用是否暴露了 UIA 控件信息：
* 启动 `Inspect.exe`，将鼠标悬停在控件上，查看其属性是否能被识别。
* 如果控件未显示 `AutomationId` 或 `Name` 等属性，请确保 Qt 的 Accessibility 配置无误。

---

## **3. 测试用例设计与实现**

### **基本操作**

#### **识别窗口**

通过 Pywinauto 获取目标窗口的句柄：

```python
from pywinauto import Application

# 启动 Qt 应用程序
app = Application(backend="uia").start("path_to_your_qt_application.exe")

# 获取主窗口
window = app.window(title="Main Window Title")
```

#### **操作控件**

1. **点击按钮**：
   

```python
   window.Button.click()
```

2. **输入文本**：
   

```python
   window.TextBox.type_keys("Hello, World!")
```

3. **选择菜单项**：
   

```python
   window.menu_select("File->Open")
```

4. **读取控件属性**：
   

```python
   label_text = window.Label.window_text()
   print(label_text)
```

---

### **复杂操作**

#### **动态控件识别**

如果控件名称不固定，可以通过控件属性进行筛选：

```python
button = window.child_window(title="Submit", control_type="Button")
button.click()
```

#### **通过 AutomationId 操作**

Qt 提供的控件一般暴露了 `AutomationId` 属性，可以使用它进行精确定位：

```python
submit_button = window.child_window(auto_id="submit_button_id", control_type="Button")
submit_button.click()
```

#### **处理表格和列表**

```python
# 操作表格控件
table = window.child_window(control_type="Table")
rows = table.children(control_type="DataItem")
for row in rows:
    print(row.window_text())
```

#### **等待控件出现**

对于动态加载的界面，可以使用 `wait` 方法等待控件出现：

```python
window.wait("exists", timeout=10)
```

---

## **4. 断言与测试验证**

在自动化测试中，断言是验证操作正确性的关键。

### **基本断言**

使用 Pywinauto 的 `test` 模块：

```python
from pywinauto import test

# 验证按钮文本
test.compare(window.Button.window_text(), "Expected Text")
```

### **窗口存在性检查**

```python
assert window.exists(), "Main Window not found!"
```

### **控件状态验证**

```python
assert window.Button.is_enabled(), "Submit button is disabled!"
```

---

## **5. 处理常见问题**

### **控件识别失败**

* **检查 Accessibility 是否启用**：使用 Inspect 工具确认控件是否暴露。
* **使用不同定位方式**：
  + 按控件标题：`title="Control Title"`
  + 按类型和层级关系：`control_type="Button", found_index=0`
* **调整 Pywinauto 后端**：
  + 对于现代 Qt 应用，优先使用 `uia` 后端。

### **多窗口切换**

如果应用有多个窗口：

```python
dialog = app.window(title="Dialog Title")
dialog.wait("visible")
dialog.Button.click()
```

### **控件动态加载**

对延迟加载的控件，需要明确等待逻辑：

```python
window.child_window(title="Loading", control_type="ProgressBar").wait_not("exists", timeout=20)
```

---

## **6. 完整测试脚本示例**

以下是一个简单的完整测试脚本，用于测试一个包含按钮、输入框和标签的 Qt 应用：

```python
from pywinauto import Application

# 启动应用
app = Application(backend="uia").start("path_to_your_qt_app.exe")

# 获取主窗口
window = app.window(title="Main Window Title")

# 操作输入框
window.Edit.type_keys("Automated Test")

# 点击按钮
window.Button.click()

# 验证标签内容
label_text = window.Label.window_text()
assert label_text == "Expected Output", f"Unexpected label text: {label_text}"

# 关闭窗口
window.close()
```

---

## **7. 优缺点总结**

### **优点**：

* **轻量开源**：不需要昂贵的商业化工具。
* **灵活扩展**：Python 生态丰富，易于集成其他测试工具。
* **跨平台**：Qt 的 Accessibility API 支持多种平台。

### **缺点**：

* **依赖 Accessibility 支持**：控件的识别依赖于 Qt 是否正确实现了 Accessibility。
* **复杂界面支持不足**：对于自定义绘制的控件可能需要额外工作。

## pywinauto recorder

如果没响应的话，中间插入sleep，时间在1s-2s之间，多了或者不睡都可能出问题
能识别到qt窗口和按钮，模拟鼠标点击，但拖拽做不了

## wps打开word文档后编辑出现文档大小暴减的问题

word进行类似操作没有问题
