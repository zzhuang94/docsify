# 本地预览与发布

本节介绍如何在本地预览 Docsify 站点，以及发布前检查与常见问题。

## 本地预览方式

Docsify 通过 AJAX 加载 Markdown，必须在 HTTP（或 HTTPS）环境下打开，不能直接双击 `index.html` 用 `file://` 打开。下面几种方式均可。

### 方式一：docsify-cli（推荐）

无需全局安装，使用 npx 即可：

```bash
npx docsify-cli serve .
```

若文档在 `docs` 目录下：

```bash
npx docsify-cli serve docs
```

终端会提示本地地址（如 `http://localhost:3000`），在浏览器打开即可。支持热更新：修改 Markdown 后刷新页面即可看到效果。

### 方式二：Python

已安装 Python 时可直接起一个简单 HTTP 服务：

```bash
# Python 3
python -m http.server 3000
```

然后在浏览器访问 `http://localhost:3000/#/`（注意带 `/#/`，因为 Docsify 默认使用 hash 路由）。

### 方式三：Node 的 serve 包

```bash
npx serve .
```

然后访问 `http://localhost:3000/#/`。

### 方式四：VS Code 插件

安装 “Live Server” 等插件，右键 `index.html` 选择 “Open with Live Server”，也会以 HTTP 方式打开。若根路径不是仓库根，可能需在插件或浏览器中确认访问路径带 `/#/`。

## 发布前检查清单

在推送到 GitHub 前，建议确认：

| 检查项 | 说明 |
|--------|------|
| **侧栏** | 存在 `_sidebar.md`，且 `index.html` 中 `loadSidebar: true`。 |
| **搜索** | 若需搜索，已引入 search 插件并配置 `search: 'auto'`。 |
| **链接** | 侧栏和正文中的链接路径正确（根目录用 `xxx.md`，首页用 `/`）。 |
| **.nojekyll** | 发布目录（根或 docs）下有空文件 `.nojekyll`。 |
| **本地验证** | 用上述方式本地预览，点击侧栏各条目、搜索、封面均正常。 |

## 常见问题

### 搜索无结果

- 确保已引入搜索插件脚本，且配置了 `search: 'auto'`（或 `paths` 包含要索引的路径）。
- 必须有 `_sidebar.md` 且 `loadSidebar: true`，搜索插件依赖侧栏爬取页面。若侧栏未加载或不全，索引会不完整。
- 若使用子目录（如 `/docs`），确认 CDN 和资源路径在部署环境下可访问。

### 404 或侧栏/封面不显示

- **GitHub Pages**：检查是否添加了 `.nojekyll`，否则 `_sidebar.md`、`_coverpage.md` 会被 Jekyll 忽略。
- **路径**：若站点部署在子路径（如 `https://xxx.github.io/repo/`），确认 `index.html` 中引用资源使用相对路径（如 `./assets/custom.css`），一般无需改 `basePath`。

### 路径大小写

部分环境对 URL 大小写敏感。侧栏和正文中的文件名建议与磁盘上的文件名完全一致（包括大小写），避免在 Linux 服务器或 GitHub 上出现链接失效。

### 修改后未生效

- 本地：确认保存文件后刷新浏览器，必要时强刷（Ctrl+F5）。
- GitHub Pages：推送后等待 1–2 分钟，并清除浏览器缓存或使用无痕模式再试。

## 小结

- 本地预览用 `npx docsify-cli serve .` 或 Python/Node 的 HTTP 服务，并保证通过 `http://.../#/` 访问。
- 发布前检查侧栏、搜索、链接和 `.nojekyll`。
- 搜索无结果时重点检查侧栏与搜索插件配置；404 或 `_` 文件不显示时检查 `.nojekyll` 与路径。

至此，你已掌握从零搭建、写作到本地预览和 GitHub Pages 发布的完整流程。可根据需要继续扩展侧栏、封面、主题和插件。
