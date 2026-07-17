---
keywords: 服务器端，服务器端， api， sdk， node.js， nodejs， node js， recommendations api， api， api，服务器端1
description: 了解 [!DNL Adobe Target] 服务器端交付API、SDK和 [!DNL Target Recommendations] API。
title: 可在何处了解 [!DNL Target] 服务器端交付API和SDK？
feature: Implement Server-side
exl-id: 3eb0a789-cf1a-4d02-acf7-3c895bcb662f
TQID: https://experienceleague.adobe.com/x5WKb9Eenz2bw-idOnxlpWdtiivTx05n38sNXEt3DNc
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: b050e0cd-2ddd-42cd-a71b-5d9e1fdf75e0
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: a6cc21b9-1a36-4fa6-9c61-4acd04d9c88c
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 45af56b5ac64eb1db67c1bfdfecd6887dce990ff
workflow-type: tm+mt
source-wordcount: 825
ht-degree: 9%

---

# 服务器端：实现[!DNL Target]

有关[!DNL Adobe Target]服务器端交付API、SDK和[!DNL Target Recommendations] API的信息。

>[!NOTE]
>
>如果您的实施在客户端使用at.js和[!DNL AppMeasurement]，则您应该使用下面讨论的[!UICONTROL Target投放API]和服务器端SDK。
>
>如果您的实施使用[!UICONTROL Adobe Experience Platform Web SDK]，则您应该使用[[!UICONTROL Adobe Experience Platform] [!UICONTROL Edge Network服务器API]](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview){target=_blank}。

以下过程会在 [!DNL Target] 的服务器端实施中发生：

1. 客户端设备通过您的服务器请求获取体验。
1. 您的服务器将该请求发送至 [!DNL Target]。
1. [!DNL Target] 将响应发送回服务器。
1. 您的服务器决定将哪些体验交付给客户端设备以供其呈现。

体验不需要显示在浏览器中。 体验可以显示在电子邮件或网亭中、通过语音助手或者通过某些其他非可视化体验或非基于浏览器的设备显示。 由于您的服务器位于客户端和 [!DNL Target] 之间，因此如果您需要更好地控制体验并提高其安全性，或者您希望在服务器上运行复杂的后端进程，则此类实施是最佳选择。

>[!NOTE]
>
>只能在客户端初始化首次访客。 无法在服务器端初始化首次访客&#x200B;**。 这是由于ECID，它依赖于第三方Demdex Cookie，因此需要在涉及浏览器的实施上通过访客API.js进行初始化。

以下部分提供了有关各种服务器端API和SDK的更多信息：

## 服务器端交付 API

链接： [服务器端交付API](/help/dev/implement/delivery-api/overview.md)

`/rest/v1/delivery`

通过[!DNL Target]投放API，您可以：

* 跨Web（包括SPA）和移动频道以及非基于浏览器的物联网设备（如联网电视、网亭或店内数字屏幕）交付体验。
* 从任何可进行HTTP/s调用的服务器端平台或应用程序交付体验。
* 向访客提供一致的个性化体验，无论访客使用哪些渠道或设备与您的业务进行互动。
* 将访客的体验缓存在服务器上的一个会话中，这样可以避免多个API调用，从而提高性能。
* 从服务器端无缝地与Adobe Experience Cloud产品(如Adobe Analytics、Adobe Audience Manager (AAM)和Experience Cloud ID服务)集成。

## 服务器端SDK

[!DNL Adobe Target]服务器端SDK文档可帮助您在服务器上以所选语言实施[!DNL Target]。

* [Node.js](node-js/overview.md)
* [Java](java/overview.md)
* [.NET](net/overview.md)
* [Python](python/overview.md)

通过[!DNL Adobe Target]的服务器端SDK，您可以：

* 在&#x200B;**近零延迟**&#x200B;处执行并运行&#x200B;**功能标记**、**转出**&#x200B;和&#x200B;**A/B实验**。
* 跨&#x200B;**Web**&#x200B;交付体验，包括&#x200B;**SPA**&#x200B;和&#x200B;**移动渠道**，以及基于非浏览器的&#x200B;**物联网(IoT)设备**，例如联网电视、网亭或店内数字屏幕。
* 向该用户提供&#x200B;**机器学习(ML)驱动的个性化体验**，无论该用户与您的业务使用哪个渠道或设备。
* **从服务器端无缝地与Adobe Experience Cloud**&#x200B;产品（如&#x200B;**Adobe Analytics**、**Adobe Audience Manager**&#x200B;和&#x200B;**Experience Cloud ID服务**）集成。

请参阅[快速入门](sdk-guides/getting-started/getting-started.md)页面，了解如何通过[设备上决策](sdk-guides/on-device-decisioning/overview.md)运行简单的功能标记用例。

请查看我们的[示例应用程序](sdk-guides/sample-apps/sample-apps.md)，以便尽情享受和娱乐！

## [!DNL Target Recommendations] API

链接： [Target推荐API](https://developers.adobetarget.com/api/recommendations)和[Adobe Recommendations API概述](../../before-administer/recs-api/overview.md)。

推荐API允许您以编程方式与[!DNL Target]推荐服务器交互。 这些API可与一系列应用程序栈集成，以执行通常将通过[!DNL Target]用户界面执行的功能。

## 不使用SDK的[!DNL Platform Edge Network]个API调用 {#platform-edge-api-user-agent}

[!UICONTROL Adobe Experience Platform Web SDK]和其他支持的SDK集成在调用[!DNL Experience Platform Edge Network]时，在HTTP请求标头中包含类似浏览器的`User-Agent`值。 使用公共[Interact API](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/server-api/interact){target=_blank}而不使用SDK的服务器端集成必须显式提供此标头。

对于非SDK Interact API调用，请遵循以下要求：

* 在HTTP请求标头中包含有效的类似浏览器的`User-Agent`。 仅仅JSON请求正文中的访客或用户代理值不符合此集成模式的机器人检测要求。
* 请勿使用占位符或非浏览器值，例如`MyApp/1.0`，此类值可能会导致机器人分类。
* 公共SDK API调用不需要Edge名称或SDK版本。 对于此方案，有效的`User-Agent` HTTP标头是必需的元素。

当[!DNL Target]将请求分类为机器人流量时，由于配置文件查找、区段评估和诸如[!UICONTROL 推荐]和[!UICONTROL 自动定位]等活动的个性化内容被禁止（如下所述），个性化可能会失败或看起来间歇性异常。

在[[!DNL Adobe Experience Platform Web SDK] 概述](https://experienceleague.adobe.com/en/docs/target-dev/developer/client-side/aep/aep-web-sdk-overview){target=_blank}中了解有关使用SDK实施的更多信息。

**Interact API请求示例（标头必须包含`User-Agent`）：**

```http
POST https://edge.adobedc.net/ee/v2/interact?dataStreamId=YOUR_DATASTREAM_ID&requestId=YOUR_REQUEST_ID
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/26.5 Safari/605.1.15
Accept: */*
Content-Type: text/plain; charset=UTF-8
```
