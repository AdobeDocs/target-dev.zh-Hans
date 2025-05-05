---
keywords: 服务器端，服务器端， sdk， sdk，设备上，决策，设备上， ondevice，零延迟，延迟，近零， node.js，服务器端3
description: 了解如何使用[!UICONTROL on-device decisioning]在服务器上缓存 [!DNL Target] A/B和MVT活动，以近乎零延迟的方式执行内存中决策。
title: 什么是设备上决策？
feature: Implement Server-side
exl-id: 22ed3072-56f0-4075-9d1a-d642afe3b649
source-git-commit: ff0becf3fe3a6fd6694e13243b6a93b910316434
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 9%

---

# 设备上决策概述

新一代[!DNL Adobe Target] SDK现在提供[!UICONTROL on-device decisioning]，它能够在您的服务器上缓存A/B和Experience Targeting (XT)营销活动并以接近零延迟的速度执行内存中决策，而不会阻止对[!DNL Adobe Target]的Edge Network的网络请求。

[!DNL Adobe Target]还提供了灵活性，通过实时服务器调用从您的实验和ML驱动的个性化营销活动中提供最相关和最新的体验。 换言之，当性能最重要时，您可以选择使用[!UICONTROL on-device decisioning]，但在需要最相关的最新体验时，可以改为进行服务器调用。 查看[何时使用设备上决策与边缘决策](../../sdk-guides/on-device-decisioning/supported-features.md)，以了解支持使用一种方案而非另一种方案的用例。

>[!NOTE]
>
>设备上决策可用于客户端和服务器端实施。 本文介绍了服务器端的[!UICONTROL on-device decisioning]。 有关客户端的[!UICONTROL on-device decisioning]的信息，请参阅客户端实施文档[此处](../../../client-side/atjs/on-device-decisioning/on-device-decisioning.md)。

## 它是如何工作的？

当您安装和初始化启用了[!UICONTROL on-device decisioning]的[!DNL Adobe Target] SDK时，将从距离您服务器最近的Akamai CDN下载&#x200B;*规则工件*&#x200B;并将其缓存在您的服务器上。 当在服务器端应用程序中提出检索[!DNL Adobe Target]体验的请求时，将根据缓存规则工件中编码的元数据在内存中做出有关返回哪个内容的决策，这将定义您的所有[!UICONTROL on-device decisioning] A/B和XT活动。

下图显示了[!UICONTROL on-device decisioning]架构。 单击以展开图像。

（单击图像可展开至全宽。）

![设备上决策架构图](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/assets/asset-sdk-local-decisioning-architecture-diagram.png "设备上决策架构图"){zoomable="yes"}

## 有哪些好处？

* **提供几乎零延迟的决策。**&#x200B;在内存中和设备上执行分段和决策，以避免阻止网络请求。
* **增强应用程序性能。**&#x200B;在不影响最终用户体验的情况下运行实验并向您的客户和用户提供个性化。
* **提高Google网站质量分数。**&#x200B;由于决策在内存中和服务器端进行，因此请提高您在线业务的Google网站质量分数，使其更易于消费者发现。
* **从实时分析中学习。**&#x200B;通过[!DNL Adobe Target]或A4T报表实时获取有关您的活动表现的洞察，从而使您能够在关键时刻旋转策略。

## 支持的功能

### 活动

设备上决策支持由[基于表单的体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html)创建的以下活动类型：

* [!UICONTROL A/B Test]
* [!UICONTROL Experience Targeting] (XT)

### 分配方法

设备上决策支持以下分配方法：

* 手动

### 受众定位

设备上决策支持以下受众规则：

| 受众规则 | 设备上决策 |
| --- | --- |
| [地域](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html) | 是<P>使用设备上决策时，支持以下地理属性：<ul><li>国家/地区</li><li>城市</li><li>纬度</li><li>经度</li></ul> |
| [网络](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html) | 否 |
| [移动设备](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html) | 否 |
| [自定义参数](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html) | 是 |
| [操作系统](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html) | 是 |
| [网页](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html) | 是 |
| [浏览器](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html) | 是 |
| [访客资料](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html) | 否 |
| [流量源](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html) | 否 |
| [时间范围](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html) | 是 |
| [Experience Cloud受众](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html)(来自Adobe Audience Manager、Adobe Analytics和Adobe Experience Manager的受众) | 否 |

## 如何配置我的客户端以使用[!UICONTROL on-device decisioning]？

设备上决策适用于使用[!DNL Adobe Target]服务器端SDK的所有[!DNL Adobe Target]客户。 要启用此功能，请在[!DNL Adobe Target] UI中导航到&#x200B;**[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]**，然后启用&#x200B;**[!UICONTROL On-Device Decisioning]**&#x200B;切换开关。

>[!NOTE]
>
>您必须具有管理员或审批者&#x200B;*用户角色*&#x200B;才能启用或禁用[!UICONTROL On-Device Decisioning]切换开关。

![替代图像](assets/asset-odd-toggle.png)

启用“设备端决策”切换后，[!DNL Adobe Target]将开始为您的客户端生成和传播&#x200B;*规则工件*。

>[!NOTE]
>
>在初始化[!DNL Adobe Target] SDK以使用[!UICONTROL on-device decisioning]之前，请确保启用此切换功能。 规则工件将首先需要生成并传播到Akamai CDN，才能使[!UICONTROL on-device decisioning]正常工作。

### 在工件切换中包含所有现有的[!UICONTROL on-device decisioning]个符合条件的活动

当您希望所有符合[!UICONTROL on-device decisioning]条件的实时[!DNL Target]活动自动包含在工件中时，将此&#x200B;**切换为**。

将此切换保持为&#x200B;**关闭**&#x200B;表示您需要重新创建和激活任何[!UICONTROL on-device decisioning]活动，才能将其包含在生成的规则工件中。

## 我如何知道某个活动具有[!UICONTROL on-device decisioning]功能？

创建活动后，活动详细信息页面中显示的名为&#x200B;**[!UICONTROL Decisioning Method]**&#x200B;的标签指示该活动是否支持[!UICONTROL on-device decisioning]。

![替代图像](assets/asset-odd9.png)

您还可以通过将列&#x200B;**[!UICONTROL Decisioning Method]**&#x200B;添加到活动列表，查看&#x200B;**[!UICONTROL Activities]**&#x200B;页面上所有支持[!UICONTROL on-device decisioning]的活动。

![替代图像](assets/asset-odd7.png)

>[!NOTE]
>
>创建和激活支持[!UICONTROL on-device decisioning]的活动后，可能需要20分钟才能将其包含在生成并传播到Akamai CDN Po的规则工件中。

## 为确保通过[!DNL Adobe Target]的服务器端SDK成功交付我的[!UICONTROL on-device decisioning]活动，需要遵循的步骤概要是什么？

1. 访问[!DNL Adobe Target] UI并导航到&#x200B;**[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]**&#x200B;以启用&#x200B;**[!UICONTROL On-Device Decisioning]**&#x200B;切换。
1. 启用&#x200B;**[!UICONTROL Include all existing [!UICONTROL on-device decisioning] qualified activities in the artifact]**&#x200B;切换。
1. 创建并激活[!UICONTROL on-device decisioning]支持的活动类型，并验证该活动的&#x200B;**[!UICONTROL Decisioning Method]**&#x200B;是否为&#x200B;**[!UICONTROL On-Device Decisioning]**。
1. 使用`decisioningMethod = on-device`安装并初始化[Node.js](../../node-js/overview.md)或[Java](../../java/overview.md) SDK。
1. 在您的代码中实施`getOffers()`或`getAttributes()`以检索设备上的体验。
1. 部署代码。

有关说明如何开始使用上述步骤1-3的示例，请参阅[快速入门](../getting-started/getting-started.md)部分。


## 其他资源

### 网络研讨会：通过 [!DNL Adobe Target] 的设备上决策进行无延迟的个性化和测试

相比以往，营销人员、产品所有者和开发人员需要更多地在网站上、应用程序中以及他们与客户联系的其他各个环节优化整体客户体验。具有数据孤岛和复杂实现的多种工具是不够的。

在此录制的网络研讨会中，[!DNL Adobe Target]产品专家讨论了将关键体验优化决策转移到设备上以便在几乎无延迟的情况下在本地执行，在为客户提高网站性能的同时创造激动人心的新用例。

>[!VIDEO](https://video.tv.adobe.com/v/328148/?quality=12)


### 教程：设备上决策

[!DNL Adobe Target] [!UICONTROL on-device decisioning]启用了几乎零延迟的内容交付。

这个7分钟的视频：

* 描述[!UICONTROL on-device decisioning]，包括它与[!DNL Target]实现的其他方法的比较
* 演示如何在Target中启用[!UICONTROL on-device decisioning]
* 检查已配置JSON内容的基于表单的编辑器活动示例
* 显示包含[!UICONTROL on-device decisioning]所需的键配置的示例Node.JS SDK代码
* 在浏览器中演示结果

>[!VIDEO](https://video.tv.adobe.com/v/329032/?quality=12)

有关更多视频和教程，请参阅[[!DNL Adobe Target] Tutorials](https://experienceleague.adobe.com/docs/target-learn/tutorials/overview.html?lang=zh-Hans)。

### Adobe技术博客 — 第1部分：在Edge平台上运行[!DNL Adobe Target] NodeJS SDK以提供试验性和个性化(Akamai Edge工作者)

[单击此处访问博客帖子](https://medium.com/adobetech/part-1-run-adobe-target-nodejs-sdk-for-experimentation-and-personalization-on-edge-platforms-4d8660964ed9)。

### Adobe Tech Blog — 第 2 部分：在 Edge 平台上运行 [!DNL Adobe Target] NodeJS SDK 以提供试验性和个性化 (AWS Lambda@Edge)

[单击此处访问博客帖子](https://medium.com/adobetech/part-2-run-adobe-target-nodejs-sdk-for-experimentation-and-personalization-on-edge-platforms-aws-4d6bdac24563)。
