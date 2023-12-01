---
keywords: target开发人员指南；概述；主页
title: Adobe Target 开发人员指南
description: 如何实施和管理  [!DNL Adobe Target]  并使用其 API 和 SDK？
contributors: https://github.com/icaraps
feature: APIs/SDKs
exl-id: 655cff9b-fc04-45cf-9068-5c6c32b70d79
source-git-commit: a72d3ee76b25702b186565e86ec6b0e67c9d5d1b
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 13%

---

# [!DNL Adobe Target] 开发人员指南

**([视图 [!DNL Target] 文档更新](https://experienceleague.adobe.com/docs/target/using/release-notes/doc-change.html){target=_blank})**

此 *[!DNL Adobe Target]开发人员指南* 提供资源和指南 [!DNL Target] 开发人员，包括用于实施和管理的API和SDK文档 [!DNL Target].

>[!NOTE]
>
>除本指南外，还提供了以下 [!DNL Adobe Target] 指南：
>
>* [*[!DNL Adobe Target] 商业从业者指南&#x200B;*](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=zh-Hans){target=_blank}
>
>* [*[!DNL Adobe Target] Tutorials *](https://experienceleague.adobe.com/docs/target-learn/tutorials/overview.html?lang=zh-Hans){target=_blank}
>
>有关发行信息，请参阅 [Target发行说明（当前版本）](https://experienceleague.adobe.com/docs/target/using/release-notes/release-notes.html){target=_blank} 在 *[!DNL Adobe Target]商业从业者指南*.

## 实施入门

**[实施之前](/help/dev/before-implement/considerations-before-you-implement-target.md)**：实施之前应考虑的注意事项 [!DNL Adobe Target].

## 客户端实施

[**Adobe Experience Platform Web SDK**](/help/dev/implement/client-side/aep-web-sdk.md)：和 [!DNL Adobe Experience Platform Web SDK] 允许您与 [!DNL Experience Cloud] (包括 [!DNL Target])通过 [!UICONTROL AdobeExperience Edge Network].

[**Target at.js JavaScript库**](/help/dev/implement/client-side/overview.md)： at.js JavaScript库可缩短Web实施的页面加载时间，增强安全性，并为单页应用程序提供更好的实施选项。

## 服务器端实施

[**Target SDK概述**](implement/server-side/server-side-overview.md)：开始使用 [!DNL Adobe Target] SDK，包括设备上决策。

[**Node.js SDK**](implement/server-side/node-js/overview.md)：如何使用 [!DNL Target] Node.js SDK.

[**Java SDK**](implement/server-side/java/overview.md)：如何使用 [!DNL Target] Java SDK。

[**.NET SDK**](implement/server-side/net/overview.md)：如何使用 [!DNL Target] .NET SDK.

[**Python SDK**](implement/server-side/python/overview.md)：如何使用 [!DNL Target] Python SDK.

## 混合实施

[**混合部署**](implement/hybrid/hybrid-overview.md)：实施 [!DNL Target] 使用客户端和服务器端实施的组合。

## Recommendations实施

[**Recommendations实施**](implement/recommendations/recommendations.md)：计划和实施 [!DNL Adobe Target Recommendations].

## 移动应用程序实施

[**AEP Mobile SDK概述**](implement/mobile/overview.md)：实施方法概述 [!DNL Adobe Target] 替换为 [!DNL Adobe Experience Platform] 移动SDK。

[**AEP Mobile SDK参考**](https://developer.adobe.com/client-sdks/documentation/)：实施 [!DNL Adobe Target] 替换为 [!DNL Adobe Experience Platform] 移动SDK。

## 电子邮件实施

[**电子邮件概述**](implement/email/overview.md)：实施方法概述 [!DNL Adobe Target] 在电子邮件中。

## API指南

[**介绍**](before-administer/target-api-overview.md)：概述 [!DNL Adobe Target] API。

[**[!DNL Target Delivery API]**](/help/dev/implement/delivery-api/overview.md)：使用 [!DNL Adobe Target] 投放API用于跨Web和移动渠道以及非基于浏览器的物联网设备（如联网电视、网亭或店内数字屏幕）投放体验。

[**[!DNL Target Admin API]**](administer/admin-api/admin-api-overview-new.md)：使用 [!DNL Adobe Target] 管理员API用于管理资产、活动、受众、选件、资产、报表、mbox、主机、环境等。

[**[!DNL Target Profile API]**](/help/dev/administer/profile-api/profile-api-overview.md)：检索 [!DNL Adobe Target] 用户配置文件信息。

[**[!DNL Target Reporting API]**](https://developer.adobe.com/target/administer/admin-api/#tag/Reports)：检索 [!UICONTROL A/B测试] 和 [!UICONTROL Automated Personalization] 活动报表数据。

[**[!DNL Target Recommendations API]**](https://developer.adobe.com/target/administer/recommendations-api/)：使用 [!DNL Target Recommendations] API。

[**[!DNL Target Models API]**](administer/models-api/models-api-overview.md)：管理阻止列表以定义中使用的功能 [!DNL Target] 机器学习模型。

[**ADMIN CONSOLEAPI**](https://developer.adobe.com/umapi/)：通过AdobeUser Management和User Sync API管理用户和产品权限。

[**[!DNL Adobe Experience Platform Edge Network Server API]**](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html)：使用 [!DNL Adobe Experience Platform Edge Network Server] 适用于各种数据收集、个性化、广告和营销用例的API。

## 资源

* [Adobe开源存储库](https://github.com/adobe)
* [目标节点JS SDK源](https://github.com/adobe/target-nodejs-sdk)
* [目标节点JS SDK示例存储库](https://github.com/adobe/target-nodejs-sdk-samples)
* [定位Java SDK源](https://github.com/adobe/target-java-sdk)
* [Target Java SDK示例存储库](https://github.com/adobe/target-java-sdk-samples)
* [Target实施](./before-implement/prepare-to-implement-target.md)
* [Target管理](./before-administer/target-api-overview.md)
* [Adobe Target开发文档GitHub存储库](https://github.com/AdobeDocs/target-developers)
* [Adobe Target发行说明](https://experienceleague.adobe.com/docs/target/using/release-notes/release-notes.html)
* [Adobe Target商业用户指南](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=zh-Hans)

