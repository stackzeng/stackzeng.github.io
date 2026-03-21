---
title: "一个平台接入图片、视频、音乐、对话模型：KIE AI 体验与接入指南"
date: 2026-03-21
draft: false
tags: ["Tutorials"]
slug: "kie-ai-integration-multimodal-platform-guide"
---

如果你最近在做 AI 产品，应该会很快发现一个现实问题：模型越来越多，但接入也越来越碎片化。

做图片要找一个平台，做视频要接另一个平台，音乐、对话、计费、回调、鉴权又各有一套。

接入各家模型很费精力。

KIE AI 做的事情，就是把这些常见的 AI 能力聚合到一个平台里，让接入变得更简单。

## **提供了哪些模型**

KIE 提供了 Video、Image、Music、Chat 对应的 API，基本覆盖了日常项目开发需要。

不管你是做图片生成、视频生成，还是聊天类、内容类工具，都可以在一个平台里统一接入，省去分别寻找和对接多个模型平台的成本。

![img](/images/2026/Snipaste_2026-03-20_15-46-03.png)

## **价格**

KIE 采用积分计价模式，1 积分 = 0.005 USD。

以图片生成为例，Nano Banana 2 生成一张 1K 图片，大概花费 0.04 USD。

这种按量付费的方式，对前期测试产品、估算成本会更方便一些，也更适合独立开发者小步试错。

![img](/images/2026/Snipaste_2026-03-20_15-54-26.png)

## **如何接入？**

### **注册**

访问官网并注册用户：

<a href="https://kie.ai?ref=01b4d8ae5861d54ac89e14d05ec4ca83" target="_blank">KIE AI</a>

### **生成密钥**

进入后台后，先创建 API Key。

![img](/images/2026/Snipaste_2026-03-20_16-06-51.png)

创建完成后，可以针对密钥增加一些风控限制，比如：

- 每小时调用上限

- 每日调用上限

- 总积分限制

这样可以避免密钥泄露后被滥用，也能更好控制成本。

![img](/images/2026/Snipaste_2026-03-20_16-07-22.png)

### **调用接口**

接下来可以直接用 Postman 测试接口。

请求地址：

```
https://api.kie.ai/api/v1/jobs/createTask
```

请求头：

```
Authorization: Bearer <token>
```

请求体示例：

```
{
  "model": "nano-banana-2",
  "callBackUrl": "https://your-domain.com/api/callback",
  "input": {
    "prompt": "一幅高度细致的插画：香蕉造型的未来飞船在夜晚的霓虹城市上空飞行，光影真实、具有电影感效果、4K 质量。",
    "aspect_ratio": "auto",
    "resolution": "2K",
    "output_format": "jpg",
    "image_input": []
  }
}
```

请求成功后，会返回一个 taskId，后续可以通过它查询任务进度。

![img](/images/2026/Snipaste_2026-03-20_16-37-34.png)

查询任务进度通常有两种方式：

- 轮询 taskId

- 通过回调接收结果

如果是线上项目，一般更推荐使用回调的方式，更适合正式业务场景。

官方文档：

<a href="https://docs.kie.ai/cn/common-api/webhook-verification?ref=01b4d8ae5861d54ac89e14d05ec4ca83" target="_blank">KIE AI 文档</a></a>

### **创建回调 Webhook HMAC Key**

为了验证回调请求是否合法，可以在后台创建 Webhook HMAC Key，用于签名校验。

![img](/images/2026/Snipaste_2026-03-20_16-47-00.png)

### **完整代码示例**

下面是一段 Java 代码示例，用来校验 KIE 回调签名：

```
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import java.nio.charset.StandardCharsets;
import java.security.InvalidKeyException;
import java.security.NoSuchAlgorithmException;
import java.util.Base64;
import java.util.Objects;

public class WebhookVerifier {

    public static boolean verifySignature(String taskId, long timestampSeconds, String receivedSignature, String secret) {
        // 重新生成签名
        String expectedSignature = generateSignature(taskId, timestampSeconds, secret);

        // 使用安全的字符串比较
        return constantTimeEquals(expectedSignature, receivedSignature);
    }

    public static String generateSignature(String taskId, long timestampSeconds, String secret) {
        try {
            // 1. 拼接待签名字符串
            String dataToSign = taskId + "." + timestampSeconds;

            // 2. 使用 HMAC-SHA256 计算签名
            Mac mac = Mac.getInstance("HmacSHA256");
            SecretKeySpec keySpec = new SecretKeySpec(
                    secret.getBytes(StandardCharsets.UTF_8), "HmacSHA256");
            mac.init(keySpec);
            byte[] hash = mac.doFinal(dataToSign.getBytes(StandardCharsets.UTF_8));

            // 3. Base64 编码
            return Base64.getEncoder().encodeToString(hash);
        } catch (NoSuchAlgorithmException | InvalidKeyException e) {
            throw new RuntimeException("Failed to generate webhook signature", e);
        }
    }

    private static boolean constantTimeEquals(String a, String b) {
        if (a == null || b == null) {
            return Objects.equals(a, b);
        }
        if (a.length() != b.length()) {
            return false;
        }
        int result = 0;
        for (int i = 0; i < a.length(); i++) {
            result |= a.charAt(i) ^ b.charAt(i);
        }
        return result == 0;
    }
}
```

以上，就完成了 KIE AI 的基础接口接入。

## **写在最后**

对于出海产品来说，技术本身并不是最重要的，而是快速验证想法的能力。

一个产品能不能跑起来，取决于你能不能用现成的能力，快速做出第一个可用版本。

像 KIE 这样的聚合型平台，意义就在这里：

它帮你省掉了重复接入多个模型平台的时间，让你把更多精力放在产品本身、用户需求和增长验证上。

独立开发很多时候拼的是谁能更快把想法做出来，推向市场，再根据反馈继续迭代。
