---
title: "10 分钟搞定：Spaceship 域名接入 Cloudflare 全流程图文教程"
date: 2026-08-02
draft: false
slug: "10-min-spaceship-cloudflare-guide"
---

之前我在 namesilo 上注册域名，但是界面实在太过古老，操作非常不方便。

最近尝试了下 spaceship 体验确实好了很多。

如果域名注册在 Spaceship，网站部署在 Cloudflare Workers 或 Pages 上，需要先将域名接入 Cloudflare，再把 Spaceship 的名称服务器修改为 Cloudflare 提供的地址。

下面按照实际操作流程，介绍如何完成整个配置。

## 一、在 Cloudflare 添加域名

进入 Cloudflare 后台，点击添加站点，选择 **Connect a domain**。

![Cloudflare 选择添加域名](/images/2026/viral-referral.png)

## 二、输入需要接入的域名

输入在 Spaceship 注册的域名，例如：

```text
example.com
```

这里只填写根域名，不需要添加 `https://`，也不需要填写 `www`。

Cloudflare 会自动扫描并导入当前域名的 DNS 记录。

然后点击 Continue。

![输入需要绑定的域名](/images/2026/viral-referral.png)

## 三、选择 Free 套餐

Cloudflare 会让我们选择套餐。

对于普通个人网站、工具站和刚上线的新网站，选择 Free 免费套餐即可。

![选择 Cloudflare Free 套餐](/images/2026/viral-referral.png)

## 四、检查导入的 DNS 记录

进入 DNS 检查页面后，如果能够看到 Cloudflare 扫描出的 A、CNAME 等记录，说明现有 DNS 记录已经成功导入。

![检查 Cloudflare 导入的 DNS 记录](/images/2026/viral-referral.png)

如果域名之前已经绑定网站、邮箱或其他服务，建议检查记录是否完整，重点关注以下类型：

- A
- AAAA
- CNAME
- MX
- TXT

确认没有遗漏后，继续下一步。

## 五、复制 Cloudflare 提供的名称服务器

Cloudflare 会为当前域名分配两个名称服务器，格式类似：

```text
xxx.ns.cloudflare.com
xxx.ns.cloudflare.com
```

将这两个地址复制下来，可以暂时保存到记事本中，后面需要填写到 Spaceship。

![复制 Cloudflare 名称服务器](/images/2026/viral-referral.png)

每个域名获得的 Cloudflare 名称服务器可能不同，需要以页面实际显示的地址为准。

## 六、打开 Spaceship 域名管理器

登录 Spaceship 后台，在应用列表中找到并打开 **域名管理器**。

![打开 Spaceship 域名管理器](/images/2026/viral-referral.png)

## 七、进入名称服务器和 DNS

找到需要接入 Cloudflare 的域名，在域名管理页面中打开 **名称服务器和 DNS**。

![进入名称服务器和 DNS](/images/2026/viral-referral.png)

## 八、打开高级 DNS

在 DNS 管理区域中，点击 **高级 DNS**。

![打开 Spaceship 高级 DNS](/images/2026/viral-referral.png)

## 九、更改名称服务器

找到名称服务器设置，可以看到域名当前使用的是 Spaceship 默认名称服务器。

点击右侧的 **更改**。

![点击更改名称服务器](/images/2026/viral-referral.png)

## 十、填写 Cloudflare 名称服务器

在弹出的窗口中选择 **自定义名称服务器**。

将之前从 Cloudflare 复制的两个名称服务器，分别填写到对应的输入框中，然后点击 **保存名称服务器设置**。

![填写 Cloudflare 自定义名称服务器](/images/2026/viral-referral.png)

填写格式如下：

```text
第一个输入框：xxx.ns.cloudflare.com
第二个输入框：xxx.ns.cloudflare.com
```

## 十一、回到 Cloudflare 检查状态

保存完成后，回到 Cloudflare 页面，点击 **I updated my nameservers**。

Cloudflare 会开始检查域名的名称服务器是否已经修改成功。

![通知 Cloudflare 已更新名称服务器](/images/2026/viral-referral.png)

名称服务器的更新可能不会立即生效。

如果暂时没有验证成功，可以等待一段时间后再次检查。

## 十二、域名接入成功

当页面出现 **Your domain is now protected by Cloudflare**，代表域名已经成功接入 Cloudflare。

![域名成功接入 Cloudflare](/images/2026/viral-referral.png)

完成接入后，域名的 DNS、SSL、缓存和安全防护等功能将由 Cloudflare 管理。

接下来可以继续在 Cloudflare 中绑定 Workers、Pages 或其他网站服务。
