---
keywords: 实施, at.js, javascript 库
description: 了解如何部署 [!DNL Adobe Target]  at.js JavaScript库使用中的标记 [!DNL Adobe Experience Platform] 或者没有标签管理器。
title: 如何部署at.js？
feature: Implement Server-side
exl-id: e62cb27e-ea80-462b-90f8-0a033b128031
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 15%

---

# 如何部署 at.js

有关如何部署的信息 [!DNL Adobe Target]  JavaScript库at.js，使用中的标记 [!DNL Adobe Experience Platform] 或者没有标签管理器。

您可以使用以下方法部署 at.js：

* **[实施 [!DNL Target] 使用Adobe Experience Platform中的标记](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md)**：中的标记 [!DNL Adobe Experience Platform] 是Adobe推出的新一代标签管理功能。 标记为客户提供了一种简单的方式来部署和管理用来加强相关客户体验的分析、营销和广告标记。

>[!NOTE]
>
> [!DNL Adobe Experience Platform Launch] 已更名为 [!DNL Adobe Experience Platform] 中的一套数据收集技术。因此，产品文档中的术语有一些改动。请参阅以下内容 [文档](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html) 以获取术语更改的综合参考。

* **[实施 [!DNL Target] 不使用标签管理器](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md)**：您可以实施 [!DNL Target] 不使用标签管理器(例如， [!DNL Adobe Experience Platform])。
* **实施 [!DNL Target] 使用第三方标记管理器**： [Adobe Experience Platform中的标记](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) 是首选的实施方法 [!DNL Target]；但是，您也可以实施 [!DNL Target] 使用第三方标签管理器，包括Tealium、Ensighten和Google Tag。 有关使用Launch的好处列表，请参阅 [使用实施at.js的优势 [!DNL Adobe Target]  扩展](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md#advantages-of-implementing-atjs-using-the-target-extension).

  但是，如果您知道如何实施 [!DNL Target] 如果没有标签管理器，您可以使用第三方标签管理器轻松实施，而不是在网站代码中硬编码at.js。

  以下是两个将帮助您实施的相关主题 [!DNL Target] 使用第三方标记管理器：

   * [实施之前](/help/dev/before-implement/prepare-to-implement-target.md)
   * [实施 [!DNL Target] 没有标签管理器](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md)

  有关更多信息，请务必查看第三方标签管理器的文档。

实施 [!DNL Target] 使用单页应用程序(SPA)时，请参阅 [单页应用程序实施](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md).
