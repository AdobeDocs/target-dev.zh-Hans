---
keywords: Adobe Experience Platform Web SDK， aep web sdk， web sdk， sdk， adobe experience cloud，平台边缘网络， adobe experience platform边缘网络，边缘网络， aep edge network， Adobe Experience Platform Web SDK0
description: 了解如何使用[!UICONTROL Adobe Experience Platform Web SDK]通过[!UICONTROL Adobe Experience Cloud]与[!UICONTROL AEP Edge Network]中的各种服务进行交互。
title: 如何使用[!UICONTROL Experience Platform Web SDK]实施？
feature: AEP Web SDK
exl-id: 35ee60d2-3d6d-4169-9f22-b2aef4c6548b
source-git-commit: ac03d5d15875ab4945b07b3e95037ce9ecde1044
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 8%

---

# [!UICONTROL Adobe Experience Platform Web SDK]

[!UICONTROL Adobe Experience Platform Web SDK] (AEP Web SDK)是客户端JavaScript库，它允许[!UICONTROL Adobe Experience Cloud]的客户通过[!DNL Adobe Experience Cloud]与[!DNL Target]（包括[!UICONTROL Adobe Experience Platform Edge Network]）中的各种服务进行交互。 除了JavaScript库之外，还有[!UICONTROL Adobe Experience Platform]扩展可帮助您进行Web SDK配置。

有关详细信息，请参阅&#x200B;*[!UICONTROL Adobe Experience Platform Web SDK]*&#x200B;帮助中的以下链接：

* 有关全面信息： [什么是[!UICONTROL Adobe Experience Platform Web SDK]](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
* 有关[!DNL Target]的特定信息： [[!DNL Target] 概述](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html)

## 教程

以下教程可帮助您实施：

### 使用[!DNL Adobe Experience Cloud]实施[!DNL Platform Web SDK]

了解如何结合使用[!DNL Experience Cloud]和[!DNL Adobe Experience Platform Web SDK]本教程[实施](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html)应用程序。 有关[!DNL Target]的特定信息，请参阅标题为[使用Platform Web SDK设置 [!DNL Target] ](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html)的教程部分。

### 从at.js 2.[!DNL Target]*x*&#x200B;至[!DNL Platform Web SDK]

了解如何从at.js 2.[!DNL Target]通过&#x200B;*本教程*&#x200B;将[!DNL Adobe Experience Platform Web SDK]x[添加到](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html)。

## 推荐文档

除了上述[!UICONTROL Platform Web SDK]文档之外，本指南中的主题还具有特定于[!UICONTROL Platform Web SDK]的信息，因为它与[!DNL Target]特性和功能相关。

| 功能 | 描述/链接 |
| --- | --- |
| [活动 QA](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html) | 使用[!DNL Target]中的QA URL来执行简单的端到端活动QA，它提供了永不变更的预览链接、可选的受众定位以及从实时活动数据中分段的QA报表。 通过活动QA，您可以在实时启动[!DNL Target]活动之前对其进行全面测试。<p>请参阅[Target JavaScript库QA模式兼容性](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html#compatibility)和[预览URL](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html#preview)。 |
| [[!UICONTROL Analytics for Target] (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) | [!UICONTROL Adobe Analytics for Target] (A4T) 是一种跨解决方案的集成，通过它，可根据 [!DNL Analytics] 转化指标和受众区段创建活动。A4T集成让您可以使用Analytics报表检查结果。<p>请参阅[支持的活动类型](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html#section_F487896214BF4803AF78C552EF1669AA)和[Adobe Experience Platform Web SDK实现的实施步骤](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4timplementation.html#platform)。 |
| [受众](https://experienceleague.adobe.com/docs/target/using/audiences/target.html) | [!DNL Target]中的受众可决定哪些人可以看到目标活动中的内容和体验。<p>请参阅[使用受众列表](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html#use-list)和[合并多个受众](https://experienceleague.adobe.com/docs/target/using/audiences/combining-multiple-audiences.html)。 |
| [创建受众](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html?lang=zh-Hans) | 使用[!DNL Adobe Experience Platform]中创建的受众可提供更丰富的客户数据，从而带来更强大的个性化功能。<p>请参阅[使用来自Adobe Experience Platform的受众](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html#aep)。 |
| [优惠决策](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html) | 将在[!DNL Adobe Journey Optimizer]中创建的优惠决策添加到[!DNL Target]个活动（手动A/B测试或体验定位），以确定下次如何为网页版和移动版访问者提供最佳优惠。 |
| [重定向产品建议 - A4T 常见问题解答](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html) | 重定向选件会导致访客的浏览器重定向到新页面。<p>请参阅[[!UICONTROL Adobe Experience Platform Web SDK]是否支持A4T的重定向选件？](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html#platform) |
| [响应令牌](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) | 响应令牌允许您将[!DNL Target]数据发送到Google Analytics和其他第三方集成。<p>请参阅[通过Platform Web SDK将数据发送到Google Analytics](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html#sending-data-to-google-analytics-via-platform-web-sdk)，查看有关如何完成此任务的代码示例。 |
| [概述](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html)指南中的&#x200B;*[!UICONTROL Platform Web SDK]单页应用程序实施*。 | [!UICONTROL Adobe Experience Platform Web SDK]提供了丰富的功能，使您的企业能够在下一代客户端技术(如单页应用程序(SPA))上实现个性化。 |
| [TLS（传输层安全性）加密更改](/help/dev/before-implement/tls-transport-layer-security-encryption.md) | TLS（传输层安全性）帮助您维持最高安全标准并提升客户数据的安全性。 |
