---
keywords: Adobe Experience Platform Web SDK， aep web sdk， web sdk， sdk， adobe experience cloud， platform edge network， adobe experience platform edge network， edge network， aep edge network， Adobe Experience Platform Web SDK0
description: 了解如何使用 [!UICONTROL Adobe Experience Platform Web SDK] 与 [!UICONTROL Adobe Experience Cloud] 通过 [!UICONTROL AEP边缘网络].
title: 如何使用实施 [!UICONTROL Experience PlatformWeb SDK]？
feature: AEP Web SDK
exl-id: 35ee60d2-3d6d-4169-9f22-b2aef4c6548b
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 13%

---

# [!UICONTROL Adobe Experience Platform Web SDK]

[!UICONTROL Adobe Experience Platform Web SDK] (AEP Web SDK)是一个客户端JavaScript库，允许客户 [!UICONTROL Adobe Experience Cloud] 与 [!DNL Adobe Experience Cloud] (包括 [!DNL Target])通过 [!UICONTROL Adobe Experience Platform边缘网络]. 除了JavaScript库之外，还有 [!UICONTROL Adobe Experience Platform] 扩展可帮助配置Web SDK。

有关更多信息，请参阅以下链接： *[!UICONTROL Adobe Experience Platform Web SDK]* 帮助：

* 有关全面信息： [什么是 [!UICONTROL Adobe Experience Platform Web SDK]](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
* 有关的特定信息 [!DNL Target]： [[!DNL Target] 概述](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html)

## 教程

以下教程可帮助您实施：

### 实施 [!DNL Adobe Experience Cloud] 替换为 [!DNL Platform Web SDK]

了解如何实施 [!DNL Experience Cloud] 应用程序使用 [!DNL Adobe Experience Platform Web SDK] 替换为 [本教程](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=zh-Hans). 有关的特定信息 [!DNL Target]，请参阅标题为的教程部分 [设置 [!DNL Target] 使用Platform Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html).

### 迁移 [!DNL Target] 从at.js 2.*x* 到 [!DNL Platform Web SDK]

了解如何迁移您的 [!DNL Target] 从at.js 2.*x* 到 [!DNL Adobe Experience Platform Web SDK] 替换为 [本教程](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html).

## 推荐文档

除了 [!UICONTROL 平台Web SDK] 上述文档中，本指南中的主题也包含特定于 [!UICONTROL 平台Web SDK] 因为它与 [!DNL Target] 特性和功能。

| 功能 | 描述/链接 |
| --- | --- |
| [活动 QA](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html) | 在中使用QA URL [!DNL Target] 通过永不变更的预览链接、可选的受众定位以及从实时活动数据中分段的QA报表，轻松执行端到端活动QA。 通过活动QA，您可以全面测试 [!DNL Target] 活动在启动之前处于活动状态。<p>请参阅 [Target JavaScript库QA模式兼容性](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html#compatibility) 和 [预览URL](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html#preview). |
| [[!UICONTROL Analytics for Target] (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) | [!UICONTROL Adobe Analytics目标版] (A4T)是一种跨解决方案的集成，通过它，可根据以下内容创建活动 [!DNL Analytics] 转化量度和受众区段。 A4T 集成使您能够使用 Analytics 报表来检查结果。<p>请参阅 [支持的活动类型](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html#section_F487896214BF4803AF78C552EF1669AA) 和 [Adobe Experience Platform Web SDK实施的实施步骤](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4timplementation.html#platform). |
| [受众](https://experienceleague.adobe.com/docs/target/using/audiences/target.html) | 中的受众 [!DNL Target] 确定可在定向活动中看到内容和体验的用户。<p>请参阅 [使用受众列表](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html#use-list) 和 [合并多个受众](https://experienceleague.adobe.com/docs/target/using/audiences/combining-multiple-audiences.html). |
| [创建受众](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html?lang=zh-Hans) | 使用在 [!DNL Adobe Experience Platform] 中创建的受众可提供更丰富的客户数据，从而带来更强大的个性化功能。 <p>请参阅 [使用来自Adobe Experience Platform的受众](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html网站#aep). |
| [优惠决策](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html) | 添加在中创建的优惠决策 [!DNL Adobe Journey Optimizer] 到 [!DNL Target] 活动（手动A/B测试或体验定位）来确定下次如何为网页版和移动版访问者提供最佳选件。 |
| [重定向选件 — A4T 常见问题解答](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html) | 重定向选件会导致访客的浏览器重定向到新页面。<p>请参阅 [是否 [!UICONTROL Adobe Experience Platform Web SDK] 是否支持A4T的重定向选件？](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html#platform) |
| [响应令牌](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) | 响应令牌允许您发送 [!DNL Target] 将数据集成到Google Analytics和其他第三方集成。<p>请参阅 [通过Platform Web SDK向Google Analytics发送数据](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html#sending-data-to-google-analytics-via-platform-web-sdk) 查看有关如何完成此任务的代码示例。 |
| [单页应用程序实施](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html) 在 *[!UICONTROL 平台Web SDK] 概述* 指南。 | [!UICONTROL Adobe Experience Platform Web SDK] 提供丰富的功能，使您的企业能够在下一代客户端技术(如单页应用程序(SPA))上实现个性化。 |
| [TLS（传输层安全性）加密更改](../../before-implement/tls-transport-layer-security-encryption.md) | TLS（传输层安全性）帮助您维持最高安全标准并提升客户数据的安全性。 |
