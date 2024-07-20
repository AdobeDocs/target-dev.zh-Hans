---
title: Adobe Target交付API客户端提示
description: 如何在 [!DNL Adobe Target] 交付API中使用客户端提示？
exl-id: 317b9d7d-5b98-464e-9113-08b899ee1455
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# 客户端提示和[!UICONTROL Adobe Target Delivery API]

必须根据优惠请求将客户端提示发送到[!DNL Adobe Target]。

通常，建议将所有可用的客户端提示发送到[!DNL Target]。 有关详细信息，请参阅[客户端实现](../../implement/client-side/overview.md)部分中的[用户代理和客户端提示](/help/dev/implement/client-side/atjs/user-agent-and-client-hints.md)。

## 投放API直接调用

### 从浏览器

在这种情况下，浏览器将通过请求标头自动向[!DNL Target]发送低熵客户端提示。 但是，此实施存在一些浏览器级别的限制。 第一 — 除非通过https发出请求，否则将不会从浏览器发送任何客户端提示标头。 第二 — 客户端提示不会在首次请求时发送到页面上的[!DNL Target]。 客户端提示标头将仅在第二次请求时发送，并且其后会发送所有请求。 这意味着[!DNL Target]在首次访问页面时无法执行受众分段和个性化。 为了绕过这两个限制，我们强烈建议在浏览器中使用用户代理客户端提示API直接收集客户端提示，并在请求有效负载上发送它们。

### 从服务器

在这种情况下，必须在交付API请求上手动将客户端提示从浏览器转发到[!DNL Target]。

```
curl -X POST 'http://mboxedge28.tt.omtrdc.net/rest/v1/delivery?client=myClientCode&sessionId=abcdefghijkl00014' -d '{
  "context": {
    "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Safari/537.36",
    "clientHints": {
      "Sec-CH-UA-Model": "iPhone",
      "Sec-CH-UA-Mobile": true,
      "Sec-CH-UA-Platform": "iOS",
      "Sec-CH-UA": "[ { \"brand\": \"Chromium\", \"version\": \"91\" }, { \"brand\": \" Not;A Brand\", \"version\": \"99\" } ]",
      "Sec-CH-UA-Full-Version-List": "[ { \"brand\": \"Chromium\", \"version\": \"91.1.1.1\" }, { \"brand\": \" Not;A Brand\", \"version\": \"99.1.1.1\" } ]",
      "Sec-CH-UA-Platform-Version": "10.0.0",
      "Sec-CH-UA-Arch": "x86",
      "Sec-CH-UA-Bitness": "64"
    }
  },
  "execute": {
    "mboxes": [{
      "name": "home",
      "index": 1
    }]
  }
}'
```

## 格式设置

客户端提示标头Sec-CH-UA和Sec-CH-UA-Full-Version-List的格式与客户端提示浏览器API的结果(navigator.userAgentData.brands/navigator.userAgentData.getHighEntropyValues)的格式不同。 交付API接受这两种格式。 投放API会将值标准化为请求标头中使用的格式，在访问配置文件脚本中的客户端提示时，请务必牢记。
