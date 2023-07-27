---
keywords: 移动应用程序，常见问题解答，常见问题， target移动应用程序
description: 查看常见问题及其答案 [!DNL Adobe Target] 适用于移动设备应用程序。
title: 常见问题解答 [!DNL About Target] 适用于移动设备应用程序？
feature: Implement Mobile
exl-id: 06cae3de-83a4-4018-a832-66fb292a1d0f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 5%

---

# [!DNL Target] 移动应用程序版常见问题解答

关于的常见问题解答列表 [!DNL Target] 适用于移动设备应用程序。

## 我是否应在以下位置使用标记 [!DNL Adobe Experience Platform] 部署SDK，还是无需使用Launch即可部署SDK？

该SDK位于 [Adobe Marketing Cloud git](https://github.com/Adobe-Marketing-Cloud/acp-sdks/){target=_blank}. If you don't use [tags in Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html){target=_blank}，您必须管理自己的设置文件，并在应用程序中管理该文件。

## 目前提供哪些SDK？

Adobe Experience Platform Mobile SDK当前支持iOS、Android和React。 欲了解更多信息，请参见 [Adobe Experience Cloud Platform Mobile SDK指南](https://experienceleague.adobe.com/docs/mobile.html){target=_blank}.

## 在基于位置的功能中，对于纬度和经度的验证频率是多少？

请参阅 [Adobe位置文档](https://experienceleague.adobe.com/docs/places/using/home.html){target=_blank} 以了解更多信息。

## Adobe Experience Platform Mobile SDK是否需要at.js才能工作？

不需要，您不需要at.js才能使用Mobile SDK。 at.js是 [!DNL Target] 网站的JavaScript库。 Adobe Experience Platform Mobile SDK适用于移动设备应用程序。

## 是 [!DNL Target] 移动设备功能 [!DNL Adobe Target] 仅限高级产品SKU？

否. 对象 [!DNL Adobe Target Standard] 客户，您可以将我们的Mobile SDK用于 [!UICONTROL A/B测试] 和 [!UICONTROL 体验定位] (XT)仅与有关的活动 [!DNL Target Standard] 移动设备应用程序加载项。 如果您要使用 [!UICONTROL Recommendations] 或移动应用程序中的AI支持功能，您需要 [Adobe Target Premium](https://experienceleague.adobe.com/docs/target/using/introduction/intro.html#premium) 许可证。

## 之间是否有移动设备应用程序集成 [!DNL Adobe Experience Manager] (AEM)和 [!DNL Target] 移动活动？

目前，您可以共享JSON [体验片段](https://experienceleague.adobe.com/docs/target/using/experiences/offers/aem-experience-fragments.html){target=_blank} 从AEM到 [!DNL Target] 然后，也有可能在移动设备应用程序活动中使用它们。
