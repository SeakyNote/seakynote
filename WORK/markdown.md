## markdown首行空两格

https://blog.csdn.net/xdg15294969271/article/details/120176955

## markdown中如何输入尖括号？

使用```&lt;```和```&gt;```

## 两种链接形式
在Markdown中，链接有两种常见的语法格式：`[[]]`和`[]()`，它们有不同的用途和行为。

### 1. `[[]]` 形式

`[[]]` 这种形式通常用于某些特定的Markdown扩展或是维基风格的链接。在标准的Markdown中，这种形式并不被支持，但在某些Wiki系统或扩展中，它被用来创建内部链接。比如在一些Wiki语法中，`[[PageName]]` 会自动创建一个链接到名为"PageName"的页面。

**例子：**

```markdown
这是一个内部链接到 [[HomePage]]。
```

在某些Wiki系统中，上述例子会生成一个链接，指向名为"HomePage"的页面。

### 2. `[]()` 形式

`[]()` 是标准的Markdown语法，用于创建超链接。方括号 `[]` 中的文本是链接的显示文本，圆括号 `()` 中的内容是链接的目标URL。

**例子：**

```markdown
这是一个 [Google](https://www.google.com) 链接。
```

上述例子会生成一个超链接，显示文本为"Google"，点击后会跳转到 `https://www.google.com`。

**更详细的例子：**

```markdown
[OpenAI](https://www.openai.com)
```

显示效果为：[OpenAI](https://www.openai.com)

### 总结

- `[[]]` 形式用于某些特定的Markdown扩展或Wiki语法，创建内部链接。
- `[]()` 形式是标准Markdown语法，用于创建普通的超链接，链接到外部URL。

标准Markdown文档中通常推荐使用 `[]()` 形式，因为它是普遍支持的标准格式。如果你在使用特定的Wiki系统或者某些支持扩展的Markdown编辑器，那么可以使用 `[[]]` 形式来创建内部链接。

## markdown添加图片
`![可填可不填](文件路径)`
注意：添加图片后需要空一行，否则后面的直接贴着图片了