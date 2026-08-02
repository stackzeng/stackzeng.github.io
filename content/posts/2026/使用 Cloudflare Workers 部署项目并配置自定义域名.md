此前我一直使用 Pages 部署项目，但是 Cloudflare 逐渐将 Pages 和 Workers 统一。

单独的 Pages 入口经常变，很难找，最近新项目直接部署到了 Workers 上，记录并整理过程。
## 一、创建并部署 Workers 项目

进入 Cloudflare 控制台，打开 **Workers & Pages** 页面，然后点击右上角的 **Create application**。

![进入 Workers & Pages 页面](Snipaste_2026-08-02_14-48-18.png)

在创建应用页面中，选择 **Continue with GitHub**，并授权 Cloudflare 访问对应的 GitHub 仓库。

![选择连接 GitHub](Snipaste_2026-08-02_14-49-40.png)

选择需要部署的仓库后，填写项目的构建命令和部署命令。

构建命令：

```bash
npm run build
```

部署命令：

```bash
npx wrangler deploy --config dist/server/wrangler.json
```

确认配置无误后，点击 **Deploy** 开始部署。

![填写构建命令](Snipaste_2026-08-02_14-58-33.png)

当日志中出现以下提示时，说明项目已经构建并部署成功：

```text
Success: Deploy command completed
Success! Build completed.
```

![构建成功](Snipaste_2026-08-02_15-03-39.png)

部署完成后，访问 Cloudflare 分配的 Worker 地址，确认网站能够正常打开。

## 二、配置自定义域名

进入已经部署完成的 Workers 项目，点击顶部的 **Domains** 选项卡。

![选择 Domains 选项卡](Snipaste_2026-08-02_15-07-01.png)

点击 **Add Domain**。

![点击 Add Domain](Snipaste_2026-08-02_15-07-44.png)

分别添加以下两个域名：

```text
www.domain.com
domain.com
```

添加两个域名的目的是为了访问 domain.com 时跳转到 www 域名下。

## 三、处理 DNS 记录冲突

添加 `domain.com` 时，可能会出现以下错误：

```text
Hostname 'domain.com' already has externally managed DNS records (A, CNAME, etc). Delete them first or try a different hostname.
```

这表示当前域名已经存在冲突的 DNS 记录，例如 `A` 记录或 `CNAME` 记录。

进入该域名的 **DNS 管理**页面，找到与 `domain.com` 对应的默认 `A` 记录，并将其删除。

![删除冲突的 A 记录](Snipaste_2026-08-02_15-13-15.png)

删除冲突的 DNS 记录后，返回 Workers 项目的 **Domains** 页面，再次添加该域名即可。

添加成功后，等待 DNS 配置生效，然后分别访问以下地址进行验证：

```text
https://domain.com
https://www.domain.com
```

