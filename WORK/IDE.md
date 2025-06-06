## vscode无法删除文件夹，要清理终端

## vscode编译c++

https://blog.csdn.net/o_0ava0_o/article/details/124740167

注意重启vscode

## 重置Visual Studio 2017的配置

https://www.cnblogs.com/yitouniu/p/10329057.html

## 安装 visual assist x 出现security key required问题

https://blog.csdn.net/xueyuxueyuxueyu/article/details/78739177

## vscode qt插件

qt tools

qt configuration

launch qt creator 右键根据项目打开qtctrator cmake/pro/ui

qml

## vscode copyright tag

```json
"doxdocgen.generic.authorName":"Seaky",
"doxdocgen.generic.authorTag":"@author      {author}",
"doxdocgen.file.customTag":[
    "@license      Private Lisense, XXX"
],
"doxdocgen.file.fileOrder":[
    "copyright",
    "custom",
    "file",
    "brief",
    "author",
    "date"
],
"doxdocgen.file.copyrightTag":[
    "@copyright   Shanghai XXX {year}"
],
"doxdocgen.file.fileTemplate":"@file    {name}",
"doxdocgen.generic.dateTemplate":"@date      {date}"
```

## vscode变量含义

https://code.visualstudio.com/docs/editor/variables-reference

## vscode文件树可以用空格展开

## vscode搜索中文

[^\x00-\xff]

## vs utf-8 无bom 编译失败

https://blog.csdn.net/sendinn/article/details/128865797

增加/utf-8

## VScode用户代码片段

https://blog.csdn.net/qq_44998582/article/details/122236803

```json
"test":{
    "prefix":"\\",
    "body":[
        "//--------------------------------------",
        ""
    ]
}
```

## vscode高亮出现问题

主题设置成Dark Modern或Dark+

主题会影响代码颜色

## vscode看文件本地历史

explore左下角timeline

## vscode下载替换

vscode.cdn.azure.cn

## 清除 Visual Studio Code 的 workspaceStorage 文件夹

https://www.coder.work/article/7770501

## qt creator去除警告提示

help-about-关闭clangCodeModel

## 解决VSC中使用Unity插件时“download the . NET Runtime.”的问题

https://zhuanlan.zhihu.com/p/660879053

## vscode qt debug

```json
"cmake.debugConfig":{
	"visualizerFile":"XXX\\qt5.natvis",
    "console":"integratedTerminal"
}
```

直接调vs2022的qt natvis文件

## json格式化

使用插件js-css-html formatter

## vscode正则替换

编辑框复制，左侧search开启正则

## vscode正则搜索

(.*)表示任意

## 保存代码自动变成utf-8了

vscode要设置autoGuessEncoding

## 文件改名

注意把match whole word开开

## vscode左侧栏的explorer消失恢复

https://blog.csdn.net/qq_21237549/article/details/137559757

## vscode中cmake底部栏问题

找status bar visibility

## vscode clang-format格式化头文件顺序不对

* vscode设置中editor: Default Formatter设置不正确
* 或者尝试代码文件tab内右键Format Document With...
  + Configure Default Formatter...
* 与C_Cpp: Formatting无关

## vs2022添加类

* 解决方案管理器
* 选中节点
* 右键添加-新建项

## msvc C++版本显示错误

编译增加 `/Zc:__cplusplus`

## 正则表达式替换空行

^\s*\n

## vs2022高级保存选项开启

https://blog.csdn.net/weixin_44335538/article/details/125263750

## vscode因C++版本造成的红色波浪线

**配置IntelliSense的C++标准**
* **打开命令面板**：`Ctrl+Shift+P`（Windows/Linux）或 `Cmd+Shift+P`（macOS）。
* **输入并选择**：`C/C++: Edit Configurations (UI)`。
* **设置C++标准**：
  + 在 **`C++ Standard`** 下拉菜单中选择项目所需的版本（如 `C++17` 或 `C++20`）。
* **保存配置**：更改后会自动更新到 `.vscode/c_cpp_properties.json`。

## vscode格式化设置

Editor: Default Formatter
