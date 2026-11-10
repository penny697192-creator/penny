# 部署开放网页版

这个文件夹是独立的静态站点。把 `public/` 里的**全部内容**上传到静态托管即可，不要上传上一级的 `us-masters-kb/`（那里有原始 PDF、提取文本和工作底稿）。

## 方式 1：GitHub Pages

1. 新建 GitHub 仓库，把 `public/` 里的内容放到仓库根目录。
2. 推到 `main` 分支。
3. 仓库 Settings → Pages → Build and deployment → Source 选 **GitHub Actions**。
4. 自带的工作流 `.github/workflows/pages.yml` 会自动部署。

## 方式 2：Cloudflare Pages

1. Cloudflare Pages → Create a project → Direct Upload。
2. 上传 `public/` 文件夹。
3. 不需要 build command，输出目录就是根目录。

## 方式 3：Netlify

1. 把 `public/` 直接拖到 Netlify Drop，或连接仓库。
2. `netlify.toml` 已设置 publish = "."。

## 正式域名与 SEO

部署后建议用正式域名重新构建一次，让 canonical / sitemap / OG 图使用绝对地址：

```bash
cd us-masters-kb
SITE_URL=https://your-domain.com python3 tools/build_public.py
```

然后把 `public/` 重新上传。`robots.txt`、`sitemap.xml` 和 Open Graph 会使用该域名。

## 公开前检查

- [ ] 没有上传 `sources/*.pdf` 或 `sources/raw/*.txt`
- [ ] `about.html` 的开放使用说明已确认
- [ ] 如需公开联系邮箱，已在 `about.html` 补充
- [ ] 排名页标注了 2027 U.S. News 口径
- [ ] 没有把内部案例、学员姓名、公司话术放进去
- [ ] 如使用自定义域名，`SITE_URL` 已重跑

## 开放版边界

开放版只发布摘要、排名与项目清单；原始 PDF、全文提取和内部工作底稿不在 `public/` 内。若你拥有原始资料版权并希望公开全文，需要单独确认授权后再调整。
