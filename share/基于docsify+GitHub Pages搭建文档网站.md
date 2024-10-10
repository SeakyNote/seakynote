## 1.docsify介绍
一个神奇的文档网站生成器，将多组markdown文档整合成网页。

docsify 可以快速帮你生成文档网站。不同于 GitBook、Hexo 的地方是它不会生成静态的 `.html` 文件，所有转换工作都是在运行时。如果你想要开始使用它，只需要创建一个 `index.html` 就可以开始编写文档并直接部署在 GitHub Pages。

https://docsify.js.org/#/zh-cn/
## 2.docsify网站例子
https://bytesfly.github.io/island/#/

更多例子：

https://docsify.js.org/#/awesome
## 3.docsify安装
安装nodejs，通过npm安装docsify-cli，详见

https://docsify.js.org/#/quickstart

如果是linux环境，直接通过包管理器安装docsify-cli即可（如果有该包的话）
## 4.目录结构
对于新手，建议基于一个例子来搭建文档网站。

以侠客岛为例 https://github.com/bytesfly/island

以下为该项目的目录结构：
```
├── antlr4  
├── book-notes  
├── design-pattern  
├── guide  
├── index.html  
├── LICENSE  
├── life  
├── mysql  
├── netty  
├── pwa.js  
├── README.md  
├── regex  
└── SUMMARY.md
```
其中，antlr4、book-notes、design-pattern、life、mysql、netty、regex为作者编写的文档，重写项目时直接删除即可。

guide中包含了两个markdown文件、图片文件夹，这些是作者写的文档及内置图片，直接删除即可。另有css及js文件夹，需要保留，后续可按需新增或变更。

index.html为网站的配置，按需调整。

LICENSE为项目许可文件，按需调整。

pwa.js为离线化相关脚本，按需保留或移除。

README.md为网站的首页，按需调整。

SUMMARY.md为网站的目录，按需调整。
## 5.index.html关键配置
head-title：网站的标题，需重新调整。

head-meta-description/keywords：网站的描述、关键字，影响不大，可直接置空。

head-link-stylesheet：网站样式，可按需保留或移除。（比如darklight-theme可能有些人不需要）
`<div id="app">`：其下字符串内容为网站加载时的信息，按需变更。

window.$docsify-name/logo：为左侧目录上方的返回主页按钮所对应的字符串或图片（可以不使用图片，仅仅用字符串）

window.$docsify-repo：对应的仓库地址。如果不需要在文档网站中访问仓库的话可直接将该键值对移除。

window.$docsify-subMaxLevel：markdown文档在左侧目录树展示的最大层级数，按需调整。

window.$docsify-search-placeholder：搜索框默认展示文本，按需调整。

window.$docsify-plugins-footer代码段：每个markdown文档在网页中展示时自动添加的字符串，按需对该代码段移除或变更。

`<script src="guide/js/xxx.js"></script>`：加载的js脚本，按需移除或新增。
回到顶部功能/实现离线化代码段：按需保留或移除。
## 6.支持C/C++语法高亮
在以下网址（或其它渠道）下载prism-c.js和prism-cpp.js

https://github.com/PrismJS/prism/tree/master/components

将这两个文件放到guide/js目录下，然后index.html添加语句（放在其它加载js脚本语句附近）：
```html
<script src="guide/js/prism-c.js"></script>
<script src="guide/js/prism-cpp.js"></script>
```
注意：对于C++代码段，需要标记为"cpp"，否则无法高亮。
## 7.添加文档
将markdown文档按组分到项目的文件夹中。在SUMMARY.md中添加其入口。若文档需要在首页中展示，则同时在README.md中添加其入口。
## 8.本地部署
命令行切换至项目目录，执行

docsify serve

浏览器中打开 http://localhost:3000 即可。

网页中显示的内容随markdown文档变化而变化。
## 9.GitHub Pages部署
将docsify项目推送至个人github仓库

在仓库主页：上方Settings-左侧Pages-Build and deployment，选择分支，选择部署目录（默认根目录），保存。

回到上方Code标签，点击右侧Deployments，即可找到发布的网页链接，点击后进入搭建的文档网站。