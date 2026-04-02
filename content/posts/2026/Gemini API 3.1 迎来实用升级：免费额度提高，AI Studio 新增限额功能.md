---
title: "Gemini API 3.1 迎来实用升级：免费额度提高，AI Studio 新增限额功能"
date: 2026-04-02
draft: false
slug: "gemini-api-free-tier-limits"
---

Google Gemini API 3.1 最近迎来了一些值得关注的更新。

对于正在使用 Gemini API 的开发者来说，这些变化主要集中在免费额度、后台成本控制，以及项目级限额管理上，实用性都比较强。

## 1. Google Gemini API 最新 3.1 版本的免费额度提高

以 Gemini 3.1 Flash Lite 为例，目前免费额度如下：

- **每分钟请求数（RPM）**：15
- **每分钟输入 Token 数（TPM）**：250k
- **每日请求数（RPD）**：500

其中，每日请求数（RPD）会在太平洋时间（UTC-8）午夜重置。

## 2. AI Studio 后台新增限额功能

AI Studio 后台现已增加限额功能。

用户可以设置每月限额，从而避免因调用超额而产生额外费用。

这一功能对于控制成本非常实用。

![img](/images/2026/Snipaste_2026-03-30_16-23-12.png)

## 3. 额度限制按项目计算

![img](/images/2026/Snipaste_2026-03-31_15-34-04.png)

需要注意的是，速率限制是按项目（Project）计算的，而不是按 API Key 计算的。

这意味着，在自己的网站或应用正式上线时，最好为每个网站单独创建项目，不要共用同一个项目。

这样更方便管理额度，也能避免不同业务之间相互影响。
