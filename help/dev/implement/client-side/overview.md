---
keywords: 实施，at.js， adobe experience platform web sdk， aep web sdk
description: 了解如何使用 [!DNL Adobe Experience Platform Web SDK] (AEP Web SDK)或at.js JavaScript库为客户端Web实施 [!DNL Adobe Target] 。
title: '如何为客户端Web实施 [!DNL Target] '
feature: at.js
exl-id: b3a850ff-ace0-4eea-955a-aa71dfad256f
TQID: https://experienceleague.adobe.com/KgJyhvTguS8EXbwELaApI1mcs5egnEKHKpnxVYGqT4I
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 929e1f10bc5dd0741f0fe28cd46435e680a4a308
workflow-type: tm+mt
source-wordcount: 252
ht-degree: 26%

---

# 概述：为客户端Web实现[!DNL Target]

在 [!DNL Adobe Target] 的客户端实施中，[!DNL Target] 会将与活动相关联的体验直接交付给客户端浏览器。 浏览器将决定要显示的体验，然后显示该体验。 借助客户端实施，您可以使用 WYSIWYG 编辑器、[可视化体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=zh-Hans) (VEC)，或者非可视化界面（[基于表单的体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=zh-Hans)）来创建活动和个性化体验。

要实施[!DNL Target]客户端，您必须使用以下JavaScript库之一：

* [Adobe Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md)

  [!UICONTROL Adobe Experience Platform Web SDK]允许您通过[!UICONTROL Adobe Experience Edge Network]与[!DNL Adobe Experience Cloud]（包括[!DNL Target]）中的各种服务进行交互。 如果您选择迁移到[!UICONTROL Adobe Experience Platform Web SDK]，请参阅[什么是[!UICONTROL Adobe Experience Platform Web SDK]](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md)。

* [[!DNL Target] at.js JavaScript库](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md)

  at.js JavaScript库可缩短Web实施的页面加载时间，增强安全性，并为单页应用程序提供更好的实施选项。 如果选择迁移到at.js，请参阅[At.js的工作方式](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md)和[[!DNL Adobe Target] Skill Builder：开发人员聊天，将Adobe Target的mbox.js迁移到at.js](https://seminars.adobeconnect.com/ptdo6mfo6qn6/?proto=true)。


请参阅[将at.js库与Web SDK进行比较](/help/dev/implement/client-side/aep-web-sdk/web-sdk-atjs-comparison.md)，了解这两种实现方法之间的差异。
