---
keywords: target开发人员指南；概述；主页
title: Adobe Target开发人员指南
description: 如何实施和管理 [!DNL Adobe Target] 以及如何使用其API和SDK？
contributors: https://github.com/icaraps
feature: APIs/SDKs
exl-id: 655cff9b-fc04-45cf-9068-5c6c32b70d79
TQID: https://experienceleague.adobe.com/lTn4veG9PKL-ZXohH3qv1UH7lpyLfn80nwuxgehXSy0
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
  - id: b050e0cd-2ddd-42cd-a71b-5d9e1fdf75e0
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
  - id: dfc8a233-f2b5-4811-bf63-b4262aebc5a5
subfeature_v2:
  - id: a94ced60-8199-4549-b453-ede2acb4101e
  - id: c011fe9c-b94b-4a88-93d8-f2acece55112
  - id: c5abb976-5170-45d6-bcac-66d15d10a4d4
  - id: cd7b6938-5837-4ee0-9790-5840997133d9
  - id: e22d67ea-317b-44f8-abd1-52e07f636ca8
  - id: fc9c2184-9102-403f-bd6c-0055021e4bea
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 501
ht-degree: 11%

---

# [!DNL Adobe Target] 开发人员指南

**（[查看 [!DNL Target] 文档更新](https://experienceleague.adobe.com/docs/target/using/release-notes/doc-change.html?lang=zh-Hans){target=_blank}）**

此&#x200B;*[!DNL Adobe Target]开发人员指南*&#x200B;为[!DNL Target]开发人员提供实施和管理[!DNL Target]所需的资源和指南，包括API和SDK文档。

>[!NOTE]
>
>除本指南外，还提供了以下 [!DNL Adobe Target] 指南：
>
>* [*[!DNL Adobe Target]商业从业者指南&#x200B;*](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=zh-Hans){target=_blank}
>
>* [*[!DNL Adobe Target]教程&#x200B;*](https://experienceleague.adobe.com/docs/target-learn/tutorials/overview.html?lang=zh-Hans){target=_blank}
>
>有关发行信息，请参阅&#x200B;*[!DNL Adobe Target]商业从业者指南*&#x200B;中的[Target发行说明（当前版本）](https://experienceleague.adobe.com/docs/target/using/release-notes/release-notes.html?lang=zh-Hans){target=_blank}。

## 实施入门

**[在实施之前](/help/dev/before-implement/considerations-before-you-implement-target.md)**：在实施[!DNL Adobe Target]之前应考虑的注意事项。

## 客户端实施

[**Adobe Experience Platform Web SDK**](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md)： [!DNL Adobe Experience Platform Web SDK]允许您通过[!UICONTROL Adobe Experience Edge Network]与[!DNL Experience Cloud]（包括[!DNL Target]）中的各种服务进行交互。

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

[**AEP Mobile SDK概述**](implement/mobile/overview.md)：有关如何使用[!DNL Adobe Experience Platform] Mobile SDK实施[!DNL Adobe Target]的概述。

[**AEP Mobile SDK引用**](https://developer.adobe.com/client-sdks/documentation/)：使用[!DNL Adobe Experience Platform] Mobile SDK实施[!DNL Adobe Target]。

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

[**[!DNL Adobe Experience Platform Edge Network Server API]**](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html?lang=zh-Hans)：将[!DNL Adobe Experience Platform Edge Network Server] API用于各种数据收集、个性化、广告和营销用例。

## 资源

* [Adobe开源存储库](https://github.com/adobe)
* [Target节点JS SDK Source](https://github.com/adobe/target-nodejs-sdk)
* [Target节点JS SDK示例存储库](https://github.com/adobe/target-nodejs-sdk-samples)
* [Target Java SDK Source](https://github.com/adobe/target-java-sdk)
* [Target Java SDK示例存储库](https://github.com/adobe/target-java-sdk-samples)
* [Target实施](./before-implement/prepare-to-implement-target.md)
* [Target管理](./before-administer/target-api-overview.md)
* [Adobe Target开发文档GitHub存储库](https://github.com/AdobeDocs/target-developers)
* [Adobe Target发行说明](https://experienceleague.adobe.com/docs/target/using/release-notes/release-notes.html?lang=zh-Hans)
* [Adobe Target商业用户指南](https://experienceleague.adobe.com/docs/target/using/target-home.html?lang=zh-Hans)

