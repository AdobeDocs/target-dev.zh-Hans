---
keywords: 实施，at.js， adobe experience platform web sdk， aep web sdk
description: 了解如何使用 [!DNL Adobe Target] (AEP Web SDK)或at.js JavaScript库为客户端Web实施 [!DNL Adobe Experience Platform Web SDK] 。
title: '如何为客户端Web实施 [!DNL Target] '
feature: at.js
exl-id: b3a850ff-ace0-4eea-955a-aa71dfad256f
source-git-commit: 315e8fbe67938588c3c9a0135e0cd85fa1f12187
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 28%

---

# 概述：为客户端Web实现[!DNL Target]

在 [!DNL Adobe Target] 的客户端实施中，[!DNL Target] 会将与活动相关联的体验直接交付给客户端浏览器。浏览器将决定要显示的体验，然后显示该体验。借助客户端实施，您可以使用 WYSIWYG 编辑器、[可视化体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC)，或者非可视化界面（[基于表单的体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html)）来创建活动和个性化体验。

要实施[!DNL Target]客户端，您必须使用以下JavaScript库之一：

* [Adobe Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md)

  [!UICONTROL Adobe Experience Platform Web SDK]允许您通过[!DNL Adobe Experience Cloud]与[!DNL Target]（包括[!UICONTROL Adobe Experience Edge Network]）中的各种服务进行交互。 如果您选择迁移到[!UICONTROL Adobe Experience Platform Web SDK]，请参阅[什么是[!UICONTROL Adobe Experience Platform Web SDK]](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md)。

* [[!DNL Target] at.js JavaScript库](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md)

  at.js JavaScript库可缩短Web实施的页面加载时间，增强安全性，并为单页应用程序提供更好的实施选项。 如果选择迁移到at.js，请参阅[At.js的工作方式](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md)和[[!DNL Adobe Target] Skill Builder：开发人员聊天，将Adobe Target的mbox.js迁移到at.js](https://seminars.adobeconnect.com/ptdo6mfo6qn6/?proto=true)。


请参阅[将at.js库与Web SDK进行比较](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/adobe-target/web-sdk-atjs-comparison){target=_blank}，了解这两种实现方法之间的差异。