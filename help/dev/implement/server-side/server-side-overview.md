---
keywords: 服务器端，服务器端， api， sdk， node.js， nodejs， node js， recommendations api， api， api，服务器端1
description: 了解 [!DNL Adobe Target] 服务器端交付API、SDK和 [!DNL Target Recommendations] API。
title: 我可以从何处了解 [!DNL Target] 服务器端交付API和SDK？
feature: Implement Server-side
exl-id: 3eb0a789-cf1a-4d02-acf7-3c895bcb662f
source-git-commit: 75af30045684b95d5989b0a1f877ba95bb8cd883
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 13%

---

# 服务器端：实施 [!DNL Target]

有关信息 [!DNL Adobe Target] 服务器端交付API、SDK和 [!DNL Target Recommendations] API。

>[!NOTE]
>
>如果您的实施使用at.js和 [!DNL AppMeasurement] 在客户端，您应使用 [!UICONTROL Target Delivery API] 和服务器端SDK一起使用。
>
>如果您的实施使用 [!UICONTROL Adobe Experience Platform Web SDK]，您应使用 [[!UICONTROL Adobe Experience Platform] [!UICONTROL Edge Network Server API]](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview){target=_blank}.

以下过程会在 [!DNL Target] 的服务器端实施中发生：

1. 客户端设备通过您的服务器请求获取体验。
1. 您的服务器将该请求发送至 [!DNL Target]。
1. [!DNL Target] 将响应发送回服务器。
1. 您的服务器决定将哪些体验交付给客户端设备以供其呈现。

体验不需要显示在浏览器中。 体验可以显示在电子邮件或网亭中、通过语音助手或者通过某些其他非可视化体验或非基于浏览器的设备显示。 由于您的服务器位于客户端和 [!DNL Target] 之间，因此如果您需要更好地控制体验并提高其安全性，或者您希望在服务器上运行复杂的后端进程，则此类实施是最佳选择。

>[!NOTE]
>
>只能在客户端初始化首次访客。 首次来访的访客 *无法* 在服务器端初始化。 这是由于ECID，它依赖于第三方Demdex Cookie，因此需要在涉及浏览器的实施上通过访客API.js进行初始化。

以下部分提供了有关各种服务器端API和SDK的更多信息：

## 服务器端交付 API

链接： [服务器端交付API](/help/dev/implement/delivery-api/overview.md)

`/rest/v1/delivery`

通过 [!DNL Target] 投放API后，您可以：

* 跨Web(包括SPA)和移动频道以及非基于浏览器的物联网设备（例如联网电视、网亭或店内数字屏幕）交付体验。
* 从任何可进行HTTP/s调用的服务器端平台或应用程序交付体验。
* 向访客提供一致的个性化体验，无论访客使用哪些渠道或设备与您的业务进行互动。
* 将访客的体验缓存在服务器上的一个会话中，这样可以避免多个API调用，从而提高性能。
* 从服务器端与Adobe Experience Cloud产品(如Adobe Analytics、Adobe Audience Manager (AAM)和Experience CloudID服务)无缝集成。

## 服务器端SDK

此 [!DNL Adobe Target] 服务器端SDK文档可帮助您实施 [!DNL Target] 在您选择的语言下在服务器上运行。

* [Node.js](node-js/overview.md)
* [Java](java/overview.md)
* [.NET](net/overview.md)
* [Python](python/overview.md)

到 [!DNL Adobe Target]的服务器端SDK，您可以：

* 执行并运行 **功能标记**， **转出**、和 **A/B实验** 在 **近零延迟**.
* 跨以下渠道交付体验 **Web**，包括 **SPA**、和 **移动渠道**&#x200B;以及非基于浏览器的 **物联网(IoT)设备** 例如联网电视、网亭或店内数字屏幕。
* Deliver **机器学习(ML)驱动的个性化体验** 对于用户，无论该用户通过哪个渠道或设备与您的业务进行互动。
* **与Adobe Experience Cloud无缝集成** 产品，例如 **Adobe Analytics**， **Adobe Audience Manager**，和 **Experience CloudID服务** 从服务器端。

请参阅 [快速入门](sdk-guides/getting-started/getting-started.md) 页面以了解如何通过运行简单的功能标记用例 [设备上决策](sdk-guides/on-device-decisioning/overview.md).

查看我们的 [示例应用程序](sdk-guides/sample-apps/sample-apps.md) 玩得开心！

## [!DNL Target Recommendations] API

链接： [Target Recommendations API](https://developers.adobetarget.com/api/recommendations) 和 [Adobe Recommendations API概述](../../before-administer/recs-api/overview.md).

Recommendations API允许您以编程方式与 [!DNL Target] 推荐服务器。 这些API可与一系列应用程序栈集成，以执行您通常通过执行的功能 [!DNL Target] 用户界面。
