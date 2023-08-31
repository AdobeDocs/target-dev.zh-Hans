---
keywords: 服务器端，服务器端， sdk， sdk，设备上，决策，设备上， ondevice，零延迟，延迟，近零， node.js，服务器端3
description: 了解如何使用 [!UICONTROL [！UICONTROL设备上决策]]以缓存您的 [!DNL Target] A/B和MVT活动可在您的服务器上执行内存中决策，并且几乎没有延迟。
title: 什么是设备上决策？
feature: Implement Server-side
exl-id: 22ed3072-56f0-4075-9d1a-d642afe3b649
source-git-commit: 79ffa3f58d780f587fe1202b82d3860395504dfe
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 8%

---

# 设备上决策概述

新一代 [!DNL Adobe Target] SDK现在提供 [!UICONTROL 设备上决策]，可在服务器上缓存A/B和体验定位(XT)营销活动，并以接近零延迟的速度执行内存中决策，而不会阻止网络请求 [!DNL Adobe Target]的边缘网络。

[!DNL Adobe Target] 还提供了灵活性，通过实时服务器调用从实验性和ML驱动的个性化营销活动中提供最相关和最新的体验。 换言之，当性能最重要时，您可以选择利用 [!UICONTROL 设备上决策]但是，当需要最相关和最新的体验时，可以改为进行服务器调用。 请参阅 [何时使用设备上决策和边缘决策](../../sdk-guides/on-device-decisioning/supported-features.md) 了解应使用其中一个而不使用另一个的用例。

>[!NOTE]
>
>设备上决策可用于客户端和服务器端实施。 本文介绍 [!UICONTROL 设备上决策] 用于服务器端。 有关信息 [!UICONTROL 设备上决策] 对于客户端，请参阅客户端实施文档 [此处](../../../client-side/atjs/on-device-decisioning/on-device-decisioning.md).

## 它是如何工作的？

安装和初始化 [!DNL Adobe Target] SDK与 [!UICONTROL 设备上决策] 已启用，a *规则构件* 从距离您服务器最近的Akamai CDN下载并缓存到您服务器上的本地。 当请求检索 [!DNL Adobe Target] 体验是在服务器端应用程序内做出的，根据缓存的规则工件中编码的元数据在内存中做出有关返回哪个内容的决策，该工件定义了 [!UICONTROL 设备上决策] A/B和XT活动。

下图显示了 [!UICONTROL 设备上决策] 架构。 单击以展开图像。

（单击图像可展开至全宽。）

![设备上决策架构图](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/assets/asset-sdk-local-decisioning-architecture-diagram.png "设备上决策架构图"){zoomable=&quot;yes&quot;}

## 有哪些好处？

* **提供几乎零延迟的决策。** 在内存中和设备上执行分段和决策，以避免阻塞网络请求。
* **增强应用程序性能。** 在不影响最终用户体验的情况下运行实验并向客户和用户提供个性化。
* **提高Google网站质量分数。** 由于决策发生在内存和服务器端，因此可提高您在线业务的Google网站质量分数，使消费者更容易发现它。
* **向实时分析学习。** 通过以下方式实时了解您的活动表现 [!DNL Adobe Target] 或A4T报表，以便能够在关键时刻引导策略。

## 支持的功能

### 活动

设备上决策支持由创建的以下活动类型 [基于表单的体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html)：

* [!UICONTROL A/B 测试]
* [!UICONTROL 体验定位] (XT)

### 分配方法

设备上决策支持以下分配方法：

* 手动

### 受众定位

设备上决策支持以下受众规则：

| 受众规则 | 设备上决策 |
| --- | --- |
| [地域](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html) | 是<P>使用设备上决策时，支持以下地理属性：<ul><li>国家/区域</li><li>城市</li><li>纬度</li><li>经度</li></ul> |
| [网络](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html) | 否 |
| [移动设备](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html) | 否 |
| [自定义参数](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html) | 是 |
| [操作系统](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html) | 是 |
| [网页](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html) | 是 |
| [浏览器](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html) | 是 |
| [访客资料](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html) | 否 |
| [流量源](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html) | 否 |
| [期限](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html) | 是 |
| [Experience Cloud受众](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html) (Adobe Audience Manager、Adobe Analytics和Adobe Experience Manager的受众 | 否 |

## 如何配置要使用的客户 [!UICONTROL 设备上决策]？

设备上决策适用于所有用户 [!DNL Adobe Target] 使用的客户 [!DNL Adobe Target] 服务器端SDK。 要启用此功能，请导航到 **[!UICONTROL 管理]** > **[!UICONTROL 实现]** > **[!UICONTROL 帐户详细信息]** 在 [!DNL Adobe Target] UI，并启用 **[!UICONTROL 设备上决策]** 切换。

>[!NOTE]
>
>您必须具有管理员或审批者 *用户角色* 启用或禁用 [!UICONTROL 设备上决策] 切换。

![替代图像](assets/asset-odd-toggle.png)

启用“设备端决策”切换功能后， [!DNL Adobe Target] 将开始生成和传播 *规则对象* 你的委托人。

>[!NOTE]
>
>在初始化 [!DNL Adobe Target] 要使用的SDK [!UICONTROL 设备上决策]. 规则工件将首先需要生成并传播到Akamai CDN，以便 [!UICONTROL 设备上决策] 去工作。

### 包括所有现有 [!UICONTROL 设备上决策] 工件切换中的符合条件的活动

切换此项 **日期** 当你想要活下来的时候 [!DNL Target] 符合条件的活动 [!UICONTROL 设备上决策] 自动包含在工件中。

正在离开此切换 **关** 这意味着您需要重新创建和激活任何 [!UICONTROL 设备上决策] 活动，以便将它们包含在生成的规则工件中。

## 我如何知道一个活动是 [!UICONTROL 设备上决策] 有能力？

创建活动后，会创建一个名为的标签 **[!UICONTROL 决策方法]**&#x200B;在活动详细信息页面中可见，指示活动是否 [!UICONTROL 设备上决策] 能力。

![替代图像](assets/asset-odd9.png)

您还可以看到以下所有活动： [!UICONTROL 设备上决策] 功能位于 **[!UICONTROL 活动]** 通过添加列页面 **[!UICONTROL 决策方法]** 添加到活动列表。

![替代图像](assets/asset-odd7.png)

>[!NOTE]
>
>创建和激活具有以下特征的活动后： [!UICONTROL 设备上决策] 该代码支持，则可能需要经过5 - 10分钟才能将其包含在生成并传播到Akamai CDN Po的规则工件中。

## 需要遵循的步骤概述是什么，才能确保 [!UICONTROL 设备上决策] 通过以下方式成功交付活动 [!DNL Adobe Target]的服务器端SDK？

1. 访问 [!DNL Adobe Target] UI并导航到 **[!UICONTROL 管理]** > **[!UICONTROL 实现]** > **[!UICONTROL 帐户详细信息]** 以启用 **[!UICONTROL 设备上决策]** 切换。
1. 启用 **[!UICONTROL 包括所有现有 [!UICONTROL 设备上决策] 工件中符合条件的活动]** 切换。
1. 创建和激活支持的活动类型 [!UICONTROL 设备上决策]，并验证 **[!UICONTROL 决策方法]** 是 **[!UICONTROL 设备上决策]** ，以了解该活动。
1. 安装和初始化 [Node.js](../../node-js/overview.md) 或 [Java](../../java/overview.md) SDK与 `decisioningMethod = on-device`.
1. 实施 `getOffers()` 或 `getAttributes()` 以检索设备上体验。
1. 部署代码。

有关演示如何开始使用上述步骤1-3的示例，请参阅 [快速入门](../getting-started/getting-started.md) 部分。


## 其他资源

### 网络研讨会：通过 [!DNL Adobe Target] 的设备上决策进行无延迟的个性化和测试

相比以往，营销人员、产品所有者和开发人员需要更多地在网站上、应用程序中以及他们与客户联系的其他各个环节优化整体客户体验。具有数据孤岛和复杂实现的多种工具是不够的。

在本网络研讨会录制中， [!DNL Adobe Target] 产品专家将讨论将关键的体验优化决策转移到设备上，以便在几乎无延迟的情况下在本地执行，在为客户提高网站性能的同时创造激动人心的新用例。

>[!VIDEO](https://video.tv.adobe.com/v/328148/?quality=12)


### 教程：设备上决策

[!DNL Adobe Target] [!UICONTROL 设备上决策] 支持几乎零延迟的内容交付。

这个7分钟的视频：

* 描述 [!UICONTROL 设备上决策]，包括与其他方法的比较 [!DNL Target] 实现
* 演示如何启用 [!UICONTROL 设备上决策] 在Target
* 检查已配置JSON内容的基于表单的编辑器活动示例
* 显示示例Node.JS SDK代码，其中包含进行以下操作所需的关键配置： [!UICONTROL 设备上决策]
* 在浏览器中演示结果

>[!VIDEO](https://video.tv.adobe.com/v/329032/?quality=12)

有关更多视频和教程，请参阅 [[!DNL Adobe Target] Tutorials](https://experienceleague.adobe.com/docs/target-learn/tutorials/overview.html?lang=zh-Hans).

### Adobe技术博客 — 第1部分：运行 [!DNL Adobe Target] 适用于Edge平台上的测试和个性化的NodeJS SDK（Akamai Edge员工）

[单击此处访问博客帖子](https://medium.com/adobetech/part-1-run-adobe-target-nodejs-sdk-for-experimentation-and-personalization-on-edge-platforms-4d8660964ed9).

### Adobe Tech Blog — 第 2 部分：在 Edge 平台上运行 [!DNL Adobe Target] NodeJS SDK 以提供试验性和个性化 (AWS Lambda@Edge)

[单击此处访问博客帖子](https://medium.com/adobetech/part-2-run-adobe-target-nodejs-sdk-for-experimentation-and-personalization-on-edge-platforms-aws-4d6bdac24563).
