# blog

Hugo + PaperMod 搭的个人博客，部署在 Cloudflare Pages。

## 写新文章

```bash
hugo new content posts/文章英文短名.md   # 生成带模板的草稿
hugo server -D                           # 本地预览 http://localhost:1313
```

写完把文章开头的 `draft: true` 改成 `false`，然后：

```bash
git add . && git commit -m "新文章：xxx" && git push
```

推送后 Cloudflare Pages 会自动构建发布，一两分钟后上线。

## 首次克隆

主题是 git submodule，克隆时要带上：

```bash
git clone --recurse-submodules https://github.com/williamwang10000-source/NewOrOldQingHistory.git
```

## Cloudflare Pages 部署设置

- Framework preset：Hugo
- Build command：`hugo --gc --minify`
- Build output directory：`public`
- 环境变量：`HUGO_VERSION` = `0.169.0`（必须设，否则默认版本太旧，主题会构建失败）

## 上线后要改的

- `hugo.toml` 里的 `baseURL` 改成你的域名
- `title`、`params.author`、`params.description`、首页介绍
- `content/about.md`

## 搜索引擎和 AI 收录

- `layouts/robots.txt` 已放行所有搜索引擎和 AI 爬虫，sitemap 自动生成在 `/sitemap.xml`
- 在 Google Search Console、Bing Webmaster Tools 提交 sitemap
- Cloudflare 后台检查 AI 爬虫是否被默认屏蔽（Security → Bots / AI Crawl Control），确保搜索类爬虫没有被挡
