---
title: "Cloudflare 悄悄更新了 AI 爬虫规则，记得检查这 6 个选项"
date: 2026-08-02
draft: false
slug: "cloudflare-ai-crawler-rules"
---

Cloudflare 最近增加了两个与 AI 爬虫和 `robots.txt` 有关的设置：

- **Block AI training bots**
- **Manage your robots.txt**

这两个功能分别用于拦截 AI 训练爬虫，以及管理网站的 `robots.txt` 文件。

新接入 Cloudflare 的网站会默认开启 AI 训练爬虫拦截。

Cloudflare 推出这些功能，一方面可以减少无效爬虫带来的带宽消耗，另一方面也有可能是竞争关系导致。

对于依靠 SEO 和 GEO 获取流量的网站，建议不要直接屏蔽所有类型的爬虫。

可以允许搜索引擎和 AI 搜索产品引用内容。

## 设置入口

进入 Cloudflare 后台：

`dash.cloudflare.com`

在左侧菜单选择 **Domains**，进入需要设置的域名，然后找到对应的 AI 爬虫和 `robots.txt` 设置。

![网站生成的商品图片案例](/images/2026/Snipaste_2026-08-02_16-30-04.png)

## Block AI training bots

![网站生成的商品图片案例](/images/2026/Snipaste_2026-08-02_16-25-01.png)

### Block on all pages

在整个网站上拦截 AI 训练爬虫。

### Block only on pages with ads

只在包含广告的页面上拦截 AI 训练爬虫。

### Allow / Do not block

不通过 Cloudflare 拦截 AI 训练爬虫。

## Manage your robots.txt

![网站生成的商品图片案例](/images/2026/Snipaste_2026-08-02_16-27-48.png)

### Content Signals Policy

在 `robots.txt` 中展示网站内容是否允许被搜索、引用和用于 AI 训练。

### Set your preference to block training in robots.txt

自动在 `robots.txt` 中声明禁止 AI 爬虫将网站内容用于模型训练。

### Disable robots.txt configuration

关闭 Cloudflare 的自动管理，使用网站项目中原有的 `robots.txt` 文件。
