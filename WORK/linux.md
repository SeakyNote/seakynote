## ubuntu虚拟机静态ip联网问题

https://blog.csdn.net/Nuo_nuoi/article/details/126902930

dns要手动填写

## ubuntu虚机可以连docsify网站，本机连不上原因:

宝塔防火墙将端口限制住了

## ubuntu to go

https://www.cnblogs.com/alanjiang/p/16322156.html

## Linux 执行命令为什么要加 ./（点斜杠） ？

https://blog.csdn.net/Albert52856/article/details/121554779

## ubuntu监控进程流量

nethogs

## bash与shell的关系

`bash`和`shell`有密切的关系，理解它们的区别和联系有助于更好地使用命令行脚本。

### `shell`
`shell`是指任何命令行解释器，它为用户提供了与操作系统进行交互的界面。在Unix/Linux系统中，shell 是一种允许用户运行命令、脚本和程序的软件层。常见的shell包括：

- **sh**（Bourne Shell）
- **csh**（C Shell）
- **ksh**（Korn Shell）
- **zsh**（Z Shell）
- **bash**（Bourne Again Shell）

### `bash`
`bash`（Bourne Again Shell）是`shell`的一种具体实现。它是由GNU项目开发的，用来替代Bourne Shell（sh）。`bash`是目前大多数Linux系统的默认shell，因为它功能强大，兼容性好。`bash`包含了Bourne Shell的所有特性，并且增加了许多新功能，比如：

- 命令行编辑
- 命令和文件名的自动补全
- 更丰富的脚本编写功能（如数组和更复杂的条件判断）

### `bash`和`shell`的关系
- **广义和狭义**：`shell`是一个广义的术语，指任何命令行解释器。而`bash`是`shell`的一种具体实现。
- **多样性**：除了`bash`，还有许多其他类型的`shell`，每种都有自己的特色和功能。例如，`csh`有C语言风格的语法，`zsh`提供了更强的可定制性。
- **选择**：用户可以在系统上安装和使用不同的`shell`，例如可以在一个系统上同时使用`bash`、`zsh`和`ksh`。通过修改用户的shell设置（通常是通过`chsh`命令），用户可以选择默认使用哪种`shell`。

### 总结
- **shell**是一个统称，表示任何命令行解释器。
- **bash**是`shell`的一种具体实现，是目前最流行和广泛使用的shell之一。
- 虽然`bash`和`shell`的语法和功能有相似之处，但`bash`扩展和改进了传统的Bourne Shell（sh），提供了更丰富的功能。

通过理解这两者的关系，可以更好地选择和使用适合自己的命令行工具和脚本语言。