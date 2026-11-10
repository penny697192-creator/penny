# 放到 GitHub Pages

## 最快路径（推荐）

1. 在 GitHub 新建一个 **Public** 仓库，例如 `us-masters-kb`。
2. 在本机执行：

```bash
cd us-masters-kb/github-pages
git init -b main
git add .
git commit -m "Publish open knowledge base"
git remote add origin https://github.com/<你的用户名>/<仓库名>.git
git push -u origin main
```

3. 打开仓库 **Settings → Pages**。
4. **Build and deployment → Source** 选 **GitHub Actions**。
5. 打开 **Actions**，等 `Deploy public knowledge base` 跑完。
6. 访问：

```text
https://<你的用户名>.github.io/<仓库名>/
```

如果仓库名是 `<你的用户名>.github.io`，地址就是 `https://<你的用户名>.github.io/`。

## 不用命令行（网页上传）

1. 新建 Public 仓库。
2. 解压 `美国硕士申请知识库-GitHubPages.zip`。
3. 进入解压后的文件夹，**全选里面的文件**（不要只拖外层文件夹），上传到仓库根目录。
4. Settings → Pages → Source 选 **Deploy from a branch** → `main` / `(root)` → Save。
5. 等 1–2 分钟，访问 `https://<用户名>.github.io/<仓库名>/`。

> 网页上传通常不会保留 `.github/` 隐藏目录；这不影响 branch 方式。`.nojekyll` 用于避免 Jekyll 处理静态资源；如果网页上传漏了它，在仓库根目录新建一个空文件 `.nojekyll` 即可。

## 设置正式网址（canonical / sitemap / OG）

首次部署后，建议用真实地址重建一次：

```bash
cd us-masters-kb
SITE_URL=https://<用户名>.github.io/<仓库名> python3 tools/build_public.py
```

然后把 `github-pages/` 重新提交/推送。这样 canonical、sitemap、robots、Open Graph 都会用正式地址。

> 本机如果 `python3` 不可用，用知识库之前使用的 Python 环境运行同一条命令。

## 自定义域名

1. 仓库 Settings → Pages → Custom domain 填域名。
2. DNS 按 GitHub 提示配置 CNAME。
3. 用 `SITE_URL=https://你的域名 python3 tools/build_public.py` 重建并推送。
4. 勾选 Enforce HTTPS。

## 常见问题

- **404**：确认 Pages Source 已设置；Actions 是否成功；仓库是否是 Public（免费账户）。
- **页面没样式**：确认上传的是 `assets/`、`index.html` 等文件在仓库根目录，而不是多了一层文件夹。
- **只有首页能开**：确认整包上传，不要只上传 `index.html`。
- **链接还是 your-domain.example**：用 `SITE_URL` 重建后再推送。
- **不要上传**：`sources/`、`content/`、原始 PDF、`team_server.py`、`team-config.json`。只上传 `github-pages/` 的内容。
