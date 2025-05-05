---
keywords: 实施, at.js, javascript 库
description: 了解如何使用 [!DNL Adobe Experience Platform] 中的标记或不使用标记管理器来部署 [!DNL Adobe Target] at.js JavaScript库。
title: 如何部署at.js？
feature: Implement Server-side
exl-id: e62cb27e-ea80-462b-90f8-0a033b128031
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 10%

---

# 如何部署 at.js

有关如何使用[!DNL Adobe Experience Platform]中的标记或不使用标记管理器部署[!DNL Adobe Target] JavaScript库at.js的信息。

您可以使用以下方法部署 at.js：

* 使用Adobe Experience Platform中的标记&#x200B;[&#128279;](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md)**实施**&#x200B;标记 [!DNL Target] ： [!DNL Adobe Experience Platform]中的标记是Adobe推出的新一代标记管理功能。 标记为客户提供了一种简单的方式来部署和管理用来加强相关客户体验的分析、营销和广告标记。

>[!NOTE]
>
> [!DNL Adobe Experience Platform Launch] 已更名为 [!DNL Adobe Experience Platform] 中的一套数据收集技术。因此，产品文档中的术语有一些改动。 有关术语更改的综合参考，请参阅以下[文档](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html)。

* **[不使用标签管理器实施 [!DNL Target] ](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md)**：您可以不使用标签管理器（例如，[!DNL Adobe Experience Platform]中的标签）实施[!DNL Target]。
* **使用第三方标签管理器实施[!DNL Target]**： Adobe Experience Platform中的[标签是实施[!DNL Target]的首选方法；但是，您也可以使用第三方标签管理器(包括Tealium、Ensighten和Google标签)实施[!DNL Target]。 ](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md)有关使用Launch的好处列表，请参阅[使用 [!DNL Adobe Target] 扩展实施at.js的优势](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md#advantages-of-implementing-atjs-using-the-target-extension)。

  但是，如果您知道如何在不使用标签管理器的情况下实施[!DNL Target]，则可以使用第三方标签管理器轻松实施，而不是在网站代码中对at.js进行硬编码。

  以下两个相关主题将帮助您使用第三方标记管理器实施[!DNL Target]：

   * [实施之前](/help/dev/before-implement/prepare-to-implement-target.md)
   * [在不使用标签管理器的情况下实施 [!DNL Target] ](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md)

  有关更多信息，请务必查看第三方标签管理器的文档。

若要在使用单页应用程序(SPA)时实施[!DNL Target]，请参阅[单页应用程序实施](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md)。
