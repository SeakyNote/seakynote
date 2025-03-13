## gitbook

https://segmentfault.com/a/1190000017960359

nodejs使用12.22.12版

npm换源

 `npm config set registry https://registry.npm.taobao.org`

TypeError: cb.apply is not a function 注释对应代码62-64行

## docsify

## vuepress/docute

## Obsidian

* *单星号斜体*
* **双星号粗体**
* 按住ctrl点击文件名，能打开多个一样的文件
* [[SUMMARY|sum]]
  + 双方括号链接
  + ctrl+左键打开
  + | 后面能加别名
* 建立关联：出链-当前笔记中潜在的链接
* 嵌入![[cheetSheet]]
* `[[^^]]`搜索链接
* `#`标签
* ==高亮==
* [另一种链接和嵌入方式](cheetSheet)

## 无法加载文件 C:\Users\xxx\AppData\Roaming\npm\docsify.ps1，因为在此系统上禁止运行脚本。

https://www.cnblogs.com/minjh/p/16203599.html

## docsify C++代码高亮

https://github.com/docsifyjs/docsify/discussions/1710

## docsify设置非严格换行

```js
window.$docsify = {
        markdown: {
            breaks: true,
        },
```

https://marked.js.org/using_advanced
https://stackoverflow.com/questions/76833921/how-to-render-line-breaks-to-single-newlines-in-docsifiy

## docsify设置正文与无序列表间距

```js
p + ul {
    margin - top: -20 px;
}
```

https://stackoverflow.com/questions/7759229/remove-space-between-paragraph-and-unordered-list

## docsify和mkdocs的异同

Docsify和MkDocs都是流行的文档生成工具，但它们在设计理念和使用场景上有显著差异。以下是两者的主要异同点：

---

### **相同点**

1. **Markdown支持**  
   - 两者均以Markdown为核心语法，支持快速编写文档内容。
2. **文档网站生成**  
   - 目标均为将Markdown文件转换为美观的静态文档网站。
3. **主题与插件**  
   - 均提供主题系统和插件扩展功能，支持自定义样式和功能增强。
4. **托管兼容性**  
   - 生成的网站均可轻松部署到GitHub Pages、Netlify等静态托管平台。

---

### **不同点**

| **对比维度**       | **Docsify**                              | **MkDocs**                              |
|--------------------|------------------------------------------|-----------------------------------------|
| **技术栈**         | 基于JavaScript（客户端渲染）             | 基于Python（服务端生成静态HTML）         |
| **构建方式**       | 无构建步骤，实时渲染Markdown              | 需执行 `mkdocs build` 生成静态文件         |
| **安装依赖**       | 依赖Node.js环境                          | 依赖Python环境                          |
| **性能**           | 首次加载可能较慢（依赖浏览器解析）        | 页面加载更快（预生成静态文件）           |
| **SEO友好性**      | 较差（内容动态加载）                     | 较优（内容已预渲染）                     |
| **配置复杂度**     | 配置简单，适合轻量级项目                 | 配置更灵活，适合复杂项目                 |
| **多语言支持**     | 通过插件实现                             | 原生支持多语言（i18n）                   |
| **实时预览**       | 默认支持实时刷新（无需手动构建）          | 需通过 `mkdocs serve` 启动本地服务器       |
| **插件生态**       | 插件较少，社区资源有限                   | 插件丰富（如SEO优化、PDF导出等）         |
| **典型用例**       | 快速搭建小型文档站、API文档               | 企业级文档、技术手册、多版本管理         |

---

### **选择建议**

* **选Docsify**：  
  需要快速搭建轻量级文档、偏好客户端渲染、无需复杂构建流程的场景。
  
* **选MkDocs**：  
  需要更好的SEO、多语言支持、复杂配置或生成静态站点供CDN加速的场景。

---

**总结**：  
Docsify以轻量和实时渲染见长，适合简单项目；MkDocs以稳定性和扩展性取胜，适合对文档结构和长期维护有较高要求的场景。
