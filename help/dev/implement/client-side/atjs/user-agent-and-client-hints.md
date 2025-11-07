---
keywords: at.js，浏览器用户代理，用户代理，客户端提示，用户代理
description: 了解Adobe Target如何使用用户代理和客户端提示，使访问者符合分段和个性化的条件。
title: 用户代理和客户端提示
feature: at.js
exl-id: e0d87d95-ee95-4ca9-8632-222ae1fb9a91
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 72%

---

# 用户代理和客户端提示

Adobe Target使用用户代理，使访问者符合分段和个性化的条件。

>[!NOTE]
>
>本文中的信息适用于 [at.js 2.9.0 或更高版本](target-atjs-versions.md)。

每次Web浏览器向服务器发出请求时，请求的标头中都会包含有关浏览器和浏览器运行环境的信息。 自互联网出现之初，这些数据就被聚合在一个称为用户代理的字符串中。

以下文本是使用 Safari 浏览器的基于 Mac OS X 的计算机的用户代理示例：

```
Mozilla/5.0 (Linux; Android 12; SM-S908E) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.41 Mobile Safari/537.36 
```

通过此用户代理，接收请求的服务器可以识别有关浏览器和操作系统的以下信息：

| 信息 | 详细信息 |
| --- | --- |
| 软件名称 | Chrome |
| 软件版本 | 101 |
| 完整软件版本 | 101.0.4951.41 |
| 版面引擎名称 | AppleWebKit |
| 版面引擎版本 | 537.36 |
| 操作系统 | Android |
| 操作系统版本 | Android 12 (Snow Cone) |
| 设备 | SM-S908E (Samsung Galaxy S22 Ultra) |

多年来，用户代理字符串中包含的浏览器和设备信息量不断增加。

## 用户代理用例

长期以来，用户代理一直被用来为营销和开发团队提供有关浏览器、操作系统和设备如何显示网站内容以及用户如何与网站交互的重要见解。 出于其他各种目的，用户代理还用于阻止垃圾邮件并过滤抓取站点的机器人程序。

然而，近年来，一些网站所有者和营销供应商通过用户代理以及请求标头中包含的其他信息来创建数字指纹，以在用户不知情的情况下识别用户。尽管用户代理对于网站所有者来说具有重要用途，但浏览器开发人员已决定更改用户代理的操作方式，以限制网站访客面临的潜在隐私问题。

浏览器开发人员创建了用户代理客户端提示作为此难题的解决方案。 客户端提示仍然允许站点收集必要的浏览器、操作系统和设备信息，同时还可以增强对隐蔽跟踪方法（如指纹）的防范。

## 客户端提示

用户代理客户端提示可在保护隐私的情况下，使网站所有者能够访问用户代理中的许多可用信息。当现代的浏览器向 Web 服务器发送用户代理时，无论是否需要，都会为每个请求发送整个用户代理。而客户端提示则会强制执行一种模型，其中服务器必须向浏览器询问它想要了解的有关客户端的其他信息。收到此请求后，浏览器可以应用自己的策略或用户配置来确定返回的数据。与默认情况下对所有请求公开整个用户代理不同，现在可以明确且可审核的方式管理相关的访问。

自 89 版以来，Chrome 中就提供了用户代理客户端提示。基于 Chromium 的浏览器的最新版本，如 Microsoft Edge、Opera、Brave、Chrome Android、Opera Android 和 Samsung Internet 等，也支持客户端提示 API。

浏览器向 Web 服务器发出的第一个请求的标头中包含的客户端提示包含浏览器品牌、浏览器的主要版本以及客户端是否为移动设备的指示信息。每段数据都有自己的标题值，而不是分组到单个用户代理字符串中。

例如，以下是一些客户端提示：

```
Sec-CH-UA: "Chromium";v="101", "Google Chrome";v="101", " Not;A Brand";v="99" 
Sec-CH-UA-Mobile: ?0 
Sec-CH-UA-Platform: "macOS"
```

...而这是同一浏览器的用户代理：

```
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36 
```

尽管所含的信息类似，但对服务器的第一个请求包含客户端提示，其中仅包含用户代理字符串中可用内容的子集。该请求中缺少的信息包括操作系统体系结构、完整操作系统版本、版面引擎名称、版面引擎版本和完整的浏览器版本。但是，在后续请求中，客户端提示 API 允许 Web 服务器询问有关设备的其他高熵详情。当请求这些高熵值时，根据浏览器策略或用户设置，浏览器响应可以包含该信息。

以下示例是请求高熵值时客户端提示 API 返回的 JSON 对象：

```
{ 

    "architecture":"x86", 
    "bitness":"64", 
    "brands":[ 
        { 
            "brand":" Not A;Brand", 
            "version":"99" 
        }, 
        { 
            "brand":"Chromium", 
            "version":"100" 
        }, 
        { 
            "brand":"Google Chrome", 
            "version":"100" 
        } 
    ], 
    "fullVersionList":[ 
        { 
            "brand":" Not A;Brand", 
            "version":"99.0.0.0" 
        }, 
        { 
            "brand":"Chromium", 
            "version":"100.0.4896.127" 
        }, 
        { 
            "brand":"Google Chrome", 
            "version":"100.0.4896.127" 
        } 
    ], 
    "mobile":false, 
    "model":"", 
    "platformVersion":"12.2.1" 
} 
```

高熵值包括默认客户端提示信息中不可用的其他几条信息。下表包含默认请求与高熵用户代理客户端提示信息中可用数据的详细信息。

| HTTP 页头 | JavaScript | 用户代理 | 客户端提示 | 高熵客户端提示 |
| --- | --- | --- | --- | --- |
| Sec-CH-UA | 品牌 | 是 | 是 | 否 |
| Sec-CH-UA-Platform | Platform | 是 | 是 | 否 |
| Sec-CH-UA-Mobile | 移动 | 是 | 是 | 否 |
| Sec-CH-UA-Platform-Version | platformVersion | 是 | 否 | 是 |
| Sec-CH-UA-Arch | 体系结构 | 是 | 否 | 是 |
| Sec-CH-UA-Model | 模型 | 是 | 否 | 是 |
| Sec-CH-UA-Bitness | 位数 | 是 | 否 | 是 |
| Sec-CH-UA-Full-Version-List | fullVersionList | 是 | 否 | 是 |

## 迁移到客户端提示

目前，基于 Chromium 的浏览器仍会在向 Web 服务器发出的请求标头中发送用户代理和客户端提示。但是，从 2022 年 4 月开始，一直到 2023 年 2 月，用户代理字符串中包含的数据量将减少。其他浏览器，如 Safari 和 Firefox，会继续利用用户代理字符串；但是，他们也会减少其中包含的信息量。

## 需要客户端提示的目标用例

Target 中的以下用例需要客户端提示：

### 受众属性

如果您使用Target受众并使用以下任何受众属性，则Target需要客户端提示来执行正确的分段：

* 浏览器
* 操作系统
* 移动设备

### 轮廓脚本

如果使用轮廓脚本并引用 `user.browser` 属性（指用户代理），则可能需要更新轮廓脚本以同时检查一个或多个客户端提示。您可以使用功能 `user.clientHint('sec-ch-ua-xxxxx')` 访问任何客户端提示。客户端提示标头名称必须全部小写。

以下示例显示如何在轮廓脚本中正确检测 Windows 操作系统：

```
"return (((user.browser != null) && (user.browser.indexOf(\"Windows\") > -1)) || " + 
      "((user.clientHint('sec-ch-ua-platform') != null) && 
(user.clientHint('sec-ch-ua-platform') === 'Windows')));" 
```

下表列出了客户端提示及其对应的配置文件脚本使用语义。

| 客户端提示标头 | 熵 | 受众属性 | 配置文件脚本用法 |
| --- | --- | --- | --- |
| [Sec-CH-UA](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA) | 低 | 浏览器 | `user.clientHint('sec-ch-ua')` |
| [Sec-CH-UA-Arch](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Arch) | 高 | 通过配置文件脚本向用户公开 | `user.clientHint('sec-ch-ua-arch')` |
| [Sec-CH-UA-Bitness](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Bitness) | 高 | 通过配置文件脚本向用户公开 | `user.clientHint('sec-ch-ua-bitness')` |
| [Sec-CH-UA-Full-Version-List](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Full-Version-List) | 高 | 浏览器 | `user.clientHint('sec-ch-ua-full-version-list')` |
| [Sec-CH-UA-Mobile](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Mobile) | 低 | 移动设备 | `user.clientHint('sec-ch-ua-mobile')` |
| [Sec-CH-UA-Model](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Model) | 高 | 移动设备 | `user.clientHint('sec-ch-ua-model')` |
| [Sec-CH-UA-Platform](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Platform) | 低 | 操作系统 | `user.clientHint('sec-ch-ua-platform')` |
| [Sec-CH-UA-Platform-Version](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Sec-CH-UA-Platform-Version) | 高 | 通过配置文件脚本向用户公开 | `user.clientHint('sec-ch-ua-platform-version')` |

## 如何将客户端提示传递给Adobe Target

以下部分包含有关如何传递客户端提示的更多信息，其具体取决于您的Target实施。

### at.js 2.9.0 或更高版本

从at.js 2.9.0开始，用户代理客户端提示将从浏览器自动收集，并在调用`getOffer/getOffers()`时发送到Target。 默认情况下，at.js 只收集“低熵”客户端提示。如果执行受众分段或使用基于前几节中归类为“高熵”的数据的轮廓脚本，则需要配置 at.js，以通过 `targetGlobalSettings` 从浏览器收集“高熵”客户端提示。

```
window.targetGlobalSettings = { allowHighEntropyClientHints: true };
```

### 服务器端 SDK

有关如何通过服务器端SDK传递客户端提示的更多信息，请参阅服务器端实施文档下的[客户端提示](../../server-side/sdk-guides/core-principles/audience-targeting.md#client-hints)。
