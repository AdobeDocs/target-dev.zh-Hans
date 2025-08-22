---
title: Adobe Target交付API概述
description: Adobe Target交付API概述
keywords: 投放api
exl-id: e760bddc-b1ae-4b7b-bff2-aba81c6b6d34
feature: APIs/SDKs
source-git-commit: ccc27e66207e58dcd33865e5d28a51644e8e1931
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# 投放API概述

[!DNL Adobe Target Delivery API]基于REST。 本文档介绍了构成[!DNL Adobe Target] [!DNL Delivery API]的资源。 HTTP方法用于对这些资源执行操作。

使用[!UICONTROL Adobe Target's Delivery API]，您可以：

* 跨Web（包括SPA）和移动频道以及非基于浏览器的物联网设备（例如联网电视、网亭或店内数字屏幕）交付体验。
* 从任何可进行HTTP/s调用的服务器端平台或应用程序交付体验。
* 无论用户通过哪些渠道或设备与您的业务合作，都可为用户提供一致的个性化体验。
* 在服务器的会话中缓存用户的体验，这样可以避免多个API调用，从而提高性能。
* 从服务器端无缝地与[!DNL Adobe Experience Cloud]产品（如[!DNL Adobe Analytics]、[!DNL Adobe Audience Manager]和[!DNL Experience Cloud ID Service]）集成。

>[!IMPORTANT]
>
>通过[!DNL Recommendations]更新[!UICONTROL Catalog] [!DNL Delivery API]时请务必谨慎。 [!DNL Delivery API]是公共的，因此请避免使用它来填充推荐目录中的可点击项。 这样做可能会引入失效的内容并污染您的目录。
>
>最佳实践：
>
>仅使用[!DNL Delivery API]来更新符合以下条件的目录属性：
>* 经常更改（例如，价格、库存水平）。
>* 遵循可在您的网站上轻松验证的预定义格式。
>* 请勿将其用于添加或修改可单击项目或其他未经验证的内容。
>
>如果需要，您可以通过交付API请求客户支持禁用目录更新。

有关详细信息，请参阅[[!UICONTROL Adobe Target Delivery API]](https://developer.adobe.com/target/implement/delivery-api/){target=_blank}文档。

>[!NOTE]
>
>您仍然可以访问[旧版/v1/mbox和/v2/batchmbox API文档](https://developers.adobetarget.com/api/legacy-api/index.html)。 但是，将在交付API中开发的功能（如此处所述）将不会作为旧版API的后盾。
