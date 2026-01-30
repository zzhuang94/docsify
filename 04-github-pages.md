# GitHub Pages 部署

本节介绍什么是 GitHub Pages，以及如何把 Docsify 文档站部署上去。

## GitHub Pages 是什么

GitHub Pages 是 GitHub 提供的静态网站托管服务。你把网页文件（HTML、CSS、JS、图片等）推送到仓库的指定分支，GitHub 会把这些文件当作静态站点发布，并分配一个地址，例如：

- 用户/组织页：`https://<username>.github.io/`
- 项目页：`https://<username>.github.io/<repo>/`

Docsify 站点全是静态文件，非常适合用 GitHub Pages 托管，且免费。

## 仓库与分支

1. 在 GitHub 上新建一个仓库（如 `my-docs`），或使用现有仓库。
2. 将本地的 Docsify 项目（含 `index.html`、`_sidebar.md`、所有 `.md` 和 `assets/` 等）推送到该仓库，例如 `main` 分支。

## 启用 GitHub Pages

1. 打开仓库页面，点击 **Settings** → 左侧 **Pages**。
2. 在 **Source** 中选择：
   - **Branch**：选 `main`（或你使用的分支）。
   - **Folder**：
     - 若文档在**仓库根目录**（即 `index.html` 在根目录），选 **/ (root)**。
     - 若文档在 **docs/** 子目录下，选 **/docs**。
3. 保存后，GitHub 会开始构建。几分钟后页面会提示站点已发布，并给出地址，如 `https://<username>.github.io/<repo>/`。

若选的是根目录，访问上述地址即可看到 Docsify 站点；若选的是 `/docs`，则站点根路径为 `https://<username>.github.io/<repo>/`，Docsify 会从该路径加载资源。

## .nojekyll 的作用

GitHub Pages 默认使用 Jekyll 处理仓库。Jekyll 会忽略以 `_` 开头的文件和目录（如 `_sidebar.md`、`_coverpage.md`），导致 Docsify 无法加载侧栏和封面。

在仓库根目录（或你发布的那个目录，如 `docs/`）下放一个**空文件** `.nojekyll`，可告诉 GitHub 不要用 Jekyll，直接按静态文件发布。这样 `_sidebar.md` 等会被正常提供。

```bash
# 在项目根或 docs 目录下
touch .nojekyll
git add .nojekyll
git commit -m "Add .nojekyll for GitHub Pages"
git push
```

## 推送与更新

之后每次更新文档，只需：

```bash
git add .
git commit -m "更新文档"
git push
```

GitHub Pages 会自动使用最新提交的内容，通常一两分钟内生效。

## 自定义域名（可选）

若你有自己的域名，可以在仓库 **Settings → Pages** 的 **Custom domain** 中填写域名，并按提示在域名服务商处添加 CNAME 解析。具体步骤见 GitHub 官方文档。

## 小结

- GitHub Pages 可免费托管 Docsify 等静态站点。
- 在仓库 Settings → Pages 中选择分支和目录（根目录或 `/docs`）。
- 务必添加 `.nojekyll`，否则 `_` 开头的文件会被忽略。
- 发布后通过 `https://<username>.github.io/<repo>/` 访问。

下一节介绍本地预览的几种方式以及发布前检查、常见问题。
