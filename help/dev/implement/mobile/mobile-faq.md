---
keywords: 移动应用程序，常见问题解答，常见问题， target移动应用程序
description: 查看有关移动应用的 [!DNL Adobe Target] 的常见问题及其答案。
title: 移动应用程序的常见问题解答 [!DNL About Target] 有哪些？
feature: Implement Mobile
exl-id: 06cae3de-83a4-4018-a832-66fb292a1d0f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 1%

---

# [!DNL Target]移动应用程序常见问题解答

有关移动设备应用程序[!DNL Target]的常见问题解答列表。

## 我应该使用[!DNL Adobe Experience Platform]中的标记来部署SDK，还是可以在不使用Launch的情况下部署SDK？

SDK在[Adobe Marketing Cloud Git](https://github.com/Adobe-Marketing-Cloud/acp-sdks/){target=_blank}上可用。 如果您未使用Adobe Experience Platform[&#128279;](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=zh-Hans){target=_blank}中的标记，则必须在您的应用程序中管理您自己的设置文件并管理它。

## 目前提供哪些SDK？

Adobe Experience Platform Mobile SDK当前支持iOS、Android和React。 有关详细信息，请参阅[Adobe Experience Cloud Platform Mobile SDK指南](https://experienceleague.adobe.com/docs/mobile.html?lang=zh-Hans){target=_blank}。

## 在基于位置的功能中，对于纬度和经度的验证频率是多少？

有关详细信息，请参阅[Adobe地标文档](https://experienceleague.adobe.com/docs/places/using/home.html?lang=zh-Hans){target=_blank}。

## Adobe Experience Platform Mobile SDK是否需要at.js才能工作？

不需要，您不需要at.js才能使用Mobile SDK。 at.js是网站的[!DNL Target] JavaScript库。 Adobe Experience Platform Mobile SDK适用于移动设备应用程序。

## [!DNL Target]移动设备是否只是[!DNL Adobe Target]高级产品SKU的一项功能？

否. 对于[!DNL Adobe Target Standard]客户，只能通过[!DNL Target Standard]移动设备应用程序加载项来将我们的Mobile SDK用于[!UICONTROL A/B Test]和[!UICONTROL Experience Targeting] (XT)活动。 如果您要在移动应用程序中使用[!UICONTROL Recommendations]或AI支持的功能，则需要[Adobe Target Premium](https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=zh-Hans#premium)许可证。

## [!DNL Adobe Experience Manager] (AEM)与[!DNL Target]移动活动之间是否存在移动应用集成？

目前，您可以将JSON [体验片段](https://experienceleague.adobe.com/docs/target/using/experiences/offers/aem-experience-fragments.html?lang=zh-Hans){target=_blank}从AEM共享到[!DNL Target]，并且之后可能在移动应用程序活动中使用它们。
