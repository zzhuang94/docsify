# Docsify 入门

本节介绍 Docsify 是什么、核心概念，以及常用配置。

## Docsify 是什么

[Docsify](https://docsify.js.org/) 是一个轻量级文档站点生成器。它**不需要构建步骤**：不把 Markdown 预先编译成 HTML，而是在浏览器里动态加载并渲染 Markdown。因此你只需要：

- 一个 `index.html` 入口
- 若干 `.md` 文件（正文）
- 可选：`_sidebar.md`（侧栏）、`_coverpage.md`（封面）等

部署时直接把整个目录当作静态网站上传（例如到 GitHub Pages）即可。

## 核心概念

| 概念 | 说明 |
|------|------|
| **sidebar（侧栏）** | 左侧导航菜单，由 `_sidebar.md` 定义，支持多级。 |
| **cover（封面）** | 首次进入站点时显示的封面页，由 `_coverpage.md` 定义。 |
| **navbar（顶栏）** | 顶部导航，由 `_navbar.md` 定义，可选。 |

本教程使用侧栏 + 封面，未使用顶栏。

## index.html 配置说明

在 `index.html` 里通过 `window.$docsify` 对象配置 Docsify，常用选项如下。

### loadSidebar

设为 `true` 时，从根目录加载 `_sidebar.md` 作为左侧导航；也可指定文件名，例如 `loadSidebar: 'summary.md'`。

```javascript
window.$docsify = {
  loadSidebar: true,
};
```

### subMaxLevel

在侧栏中展开当前文档的标题层级，形成多级子菜单。例如 `subMaxLevel: 2` 表示在侧栏里显示当前页的 h1、h2（以及其下的 h3，取决于主题实现）。

```javascript
window.$docsify = {
  loadSidebar: true,
  subMaxLevel: 2,
};
```

### name

站点名称，显示在侧栏顶部。

```javascript
window.$docsify = {
  name: 'Docsify + Markdown + GitHub 教程',
};
```

### themeColor

主题色，用于链接、按钮等。使用 CSS 变量，需主题支持。

```javascript
window.$docsify = {
  themeColor: '#3F51B5',
};
```

### search

启用搜索插件。设为 `'auto'` 时自动根据侧栏爬取页面并建索引。

```javascript
window.$docsify = {
  search: 'auto',
};
```

要生效，必须在 `index.html` 中引入搜索插件脚本：

```html
<script src="https://cdn.jsdelivr.net/npm/docsify@4/lib/plugins/search.min.js"></script>
```

### coverpage

启用封面。设为 `true` 时加载根目录的 `_coverpage.md`。

```javascript
window.$docsify = {
  coverpage: true,
};
```

## _sidebar.md 写法与多级菜单

`_sidebar.md` 使用普通 Markdown 列表，一层列表对应一级菜单，缩进表示下一级。例如：

```markdown
- [首页](/)
- [快速开始](01-quickstart.md)
- [Docsify 入门](02-docsify.md)
  - [核心概念](02-docsify.md#核心概念)
  - [配置说明](02-docsify.md#index-html-配置说明)
- [Markdown 写作](03-markdown.md)
```

链接格式：

- 首页：`/` 或 `README.md`
- 其他页：`文件名.md`，无需写路径时表示根目录下的文件
- 锚点：`文件名.md#锚点`，锚点由标题自动生成（一般为标题的英文或拼音，视主题而定）

多级展示除了手写子项，还可依赖 `subMaxLevel`：当前页打开时，其标题会作为子菜单自动出现在该页对应的侧栏项下。

## 小结

- Docsify 无构建、纯前端，适合与 Markdown + 静态托管（如 GitHub Pages）配合。
- 通过 `index.html` 的 `window.$docsify` 配置侧栏、搜索、封面、主题色等。
- `_sidebar.md` 用列表写导航，`subMaxLevel` 控制当前页标题在侧栏中的层级展示。

下一节介绍如何用 Markdown 写正文并与 Docsify 配合。
