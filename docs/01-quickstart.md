# 快速开始

本节用约 5 分钟，从零跑起一个可本地预览的 Docsify 文档站。

## 1. 创建项目目录

新建一个空文件夹，例如 `my-docs`，作为文档站根目录：

```bash
mkdir my-docs
cd my-docs
```

## 2. 创建 index.html

在根目录下创建 `index.html`，内容如下（可直接复制使用）：

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>我的文档</title>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/docsify@4/lib/themes/vue.css">
</head>
<body>
  <div id="app">加载中...</div>
  <script>
    window.$docsify = {
      name: '我的文档',
      loadSidebar: true,
      subMaxLevel: 2,
      search: 'auto',
    };
  </script>
  <script src="https://cdn.jsdelivr.net/npm/docsify@4"></script>
  <script src="https://cdn.jsdelivr.net/npm/docsify@4/lib/plugins/search.min.js"></script>
</body>
</html>
```

说明：`loadSidebar: true` 表示从 `_sidebar.md` 加载左侧导航；`search: 'auto'` 启用全局搜索。

## 3. 创建 _sidebar.md

在同一目录下创建 `_sidebar.md`，定义左侧菜单：

```markdown
- [首页](/)
- [指南](guide.md)
```

首页对应根目录的 `README.md`，`guide.md` 是另一篇文档（需自行创建）。

## 4. 创建 README.md

创建 `README.md` 作为站点首页内容，例如：

```markdown
# 欢迎

这是用 Docsify 搭建的文档站。

- [指南](guide.md)
```

## 5. 本地预览

任选一种方式在本地启动静态服务器：

**方式一：docsify-cli（推荐）**

```bash
npx docsify-cli serve .
```

**方式二：若已全局安装**

```bash
npm i -g docsify-cli
docsify serve .
```

**方式三：Python**

```bash
# Python 3
python -m http.server 3000
```

然后在浏览器打开提示的地址（如 `http://localhost:3000`）。若使用 Python，需在地址后加 `/#/`，例如 `http://localhost:3000/#/`，因为 Docsify 默认使用 hash 路由。

## 6. 可选：添加 guide.md

在根目录创建 `guide.md`，写几句说明，保存后刷新页面即可在侧栏点击「指南」查看。

至此，你已经完成了一个最简 Docsify 站点的搭建。下一节将介绍 Docsify 的核心概念与更多配置。
