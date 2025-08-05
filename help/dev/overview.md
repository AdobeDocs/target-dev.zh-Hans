---
keywords: target开发人员指南；概述；主页
title: Adobe Target开发人员指南
description: 如何实施和管理 [!DNL Adobe Target] 以及如何使用其API和SDK？
contributors: https://github.com/icaraps
feature: APIs/SDKs
exl-id: 655cff9b-fc04-45cf-9068-5c6c32b70d79
source-git-commit: 599aa4c965e331bb2681523d50708a03fc933875
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 6%

---

# [!DNL Adobe Target] 开发人员指南

**（[查看 [!DNL Target] 文档更新](https://experienceleague.adobe.com/docs/target/using/release-notes/doc-change.html){target=_blank}）**

此&#x200B;*[!DNL Adobe Target]开发人员指南*&#x200B;为[!DNL Target]开发人员提供实施和管理[!DNL Target]所需的资源和指南，包括API和SDK文档。

>[!NOTE]
>
>除本指南外，还提供了以下 [!DNL Adobe Target] 指南：
>
>* [*[!DNL Adobe Target]商业从业者指南&#x200B;*](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=zh-Hans){target=_blank}
>
>* [*[!DNL Adobe Target]教程&#x200B;*](https://experienceleague.adobe.com/docs/target-learn/tutorials/overview.html?lang=zh-Hans){target=_blank}
>
>有关发行信息，请参阅[商业从业者指南](https://experienceleague.adobe.com/docs/target/using/release-notes/release-notes.html){target=_blank}中的&#x200B;*[!DNL Adobe Target]Target发行说明（当前版本）*。

## 实施入门

**[在实施之前](/help/dev/before-implement/considerations-before-you-implement-target.md)**：在实施[!DNL Adobe Target]之前应考虑的注意事项。

## 客户端实施

[**Adobe Experience Platform Web SDK**](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md)： [!DNL Adobe Experience Platform Web SDK]允许您通过[!DNL Experience Cloud]与[!DNL Target]（包括[!UICONTROL Adobe Experience Edge Network]）中的各种服务进行交互。

[**Target at.js JavaScript库**](/help/dev/implement/client-side/overview.md)： at.js JavaScript库可缩短Web实施的页面加载时间，增强安全性，并为单页应用程序提供更好的实施选项。

## 服务器端实施

[**Target SDK概述**](implement/server-side/server-side-overview.md)：开始使用[!DNL Adobe Target] SDK，包括设备上决策。

[**Node.js SDK**](implement/server-side/node-js/overview.md)：如何使用[!DNL Target] Node.js SDK。

[**Java SDK**](implement/server-side/java/overview.md)：如何使用[!DNL Target] Java SDK。

[**.NET SDK**](implement/server-side/net/overview.md)：如何使用[!DNL Target] .NET SDK。

[**Python SDK**](implement/server-side/python/overview.md)：如何使用[!DNL Target] Python SDK。

## 混合实施

[**混合部署**](implement/hybrid/hybrid-overview.md)：使用客户端和服务器端实现的组合实现[!DNL Target]。

## Recommendations实施

[**Recommendations实施**](implement/recommendations/recommendations.md)：计划和实施[!DNL Adobe Target Recommendations]。

## 移动应用程序实施

[**AEP Mobile SDK概述**](implement/mobile/overview.md)：有关如何使用[!DNL Adobe Target] Mobile SDK实施[!DNL Adobe Experience Platform]的概述。

[**AEP Mobile SDK引用**](https://developer.adobe.com/client-sdks/documentation/)：使用[!DNL Adobe Target] Mobile SDK实施[!DNL Adobe Experience Platform]。

## 电子邮件实施

[**电子邮件概述**](implement/email/overview.md)：如何在电子邮件中实施[!DNL Adobe Target]的概述。

## API指南

[**简介**](before-administer/target-api-overview.md)： [!DNL Adobe Target] API概述。

[**[!DNL Target Delivery API]**](/help/dev/implement/delivery-api/overview.md)：使用[!DNL Adobe Target]交付API跨Web和移动渠道以及非基于浏览器的物联网设备（如连接的电视、网亭或店内数字屏幕）交付体验。

[**[!DNL Target Admin API]**](administer/admin-api/admin-api-overview-new.md)：使用[!DNL Adobe Target]管理员API管理资产、活动、受众、选件、资产、报告、mbox、主机、环境等。

[**[!DNL Target Profile API]**](/help/dev/administer/profile-api/profiles-api.md)：检索[!DNL Adobe Target]用户配置文件信息。

[**[!DNL Target Reporting API]**](https://developer.adobe.com/target/administer/admin-api/#tag/Reports)：检索[!UICONTROL A/B Test]和[!UICONTROL Automated Personalization]活动报告数据。

[**[!DNL Target Recommendations API]**](https://developer.adobe.com/target/administer/recommendations-api/)：使用[!DNL Target Recommendations] API。

[**[!DNL Target Models API]**](administer/models-api/models-api-overview.md)：管理阻止列表以定义[!DNL Target]机器学习模型中使用的功能。

[**Admin Console API**](https://developer.adobe.com/umapi/)：通过Adobe User Management和User Sync API管理用户和产品权限。

[**[!DNL Adobe Experience Platform Edge Network Server API]**](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html)：将[!DNL Adobe Experience Platform Edge Network Server] API用于各种数据收集、个性化、广告和营销用例。

## 资源

* [Adobe开源存储库](https://github.com/adobe)
* [目标节点JS SDK Source](https://github.com/adobe/target-nodejs-sdk)
* [Target Node JS SDK示例存储库](https://github.com/adobe/target-nodejs-sdk-samples)
* [Target Java SDK Source](https://github.com/adobe/target-java-sdk)
* [Target Java SDK示例存储库](https://github.com/adobe/target-java-sdk-samples)
* [Target实施](./before-implement/prepare-to-implement-target.md)
* [Target管理](./before-administer/target-api-overview.md)
* [Adobe Target开发文档GitHub存储库](https://github.com/AdobeDocs/target-developers)
* [Adobe Target发行说明](https://experienceleague.adobe.com/docs/target/using/release-notes/release-notes.html)
* [Adobe Target商业用户指南](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=zh-Hans)

