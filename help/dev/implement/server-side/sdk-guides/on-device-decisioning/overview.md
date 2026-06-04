---
keywords: 服务器端，服务器端， sdk， sdk，设备上，决策，设备上， ondevice，零延迟，延迟，近零， node.js，服务器端3
description: 了解如何使用[!UICONTROL [！UICONTROL设备上决策]]在服务器上缓存 [!DNL Target] A/B和MVT活动，以便在几乎零延迟的情况下执行内存中决策。
title: 什么是设备上决策？
feature: Implement Server-side
exl-id: 22ed3072-56f0-4075-9d1a-d642afe3b649
TQID: https://experienceleague.adobe.com/-HHGn3lG5fOh2GLXQ6jOLRQmX7H24lN-2fseOg4y5H4
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: adee20bd-51f4-461d-b9db-d215f8756eebid: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: bcc5edb5-84c3-4940-9f84-ed88b6c16274id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1id: e0eb8757-182f-49f3-94a4-1587d16f5094id: e1e0219c-f879-479f-8427-888ed2a6e9c2id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 1349
ht-degree: 8%

---

# 设备上决策概述

新一代[!DNL Adobe Target] SDK现在提供[!UICONTROL 设备上决策]，它能够在您的服务器上缓存您的A/B和Experience Targeting (XT)营销活动并以接近零延迟的速度执行内存中决策，而不会阻止对[!DNL Adobe Target]的Edge Network的网络请求。

[!DNL Adobe Target]还提供了灵活性，通过实时服务器调用从您的实验和ML驱动的个性化营销活动中提供最相关和最新的体验。 换言之，当性能最为重要时，您可以选择使用[!UICONTROL 设备上决策]，但在需要最相关的最新体验时，可以改为进行服务器调用。 查看[何时使用设备上决策与边缘决策](../../sdk-guides/on-device-decisioning/supported-features.md)，以了解支持使用一种方案而非另一种方案的用例。

>[!NOTE]
>
>设备上决策可用于客户端和服务器端实施。 本文介绍了服务器端的[!UICONTROL 设备上决策]。 有关客户端的[!UICONTROL 设备上决策]的信息，请参阅客户端实施文档[此处](../../../client-side/atjs/on-device-decisioning/on-device-decisioning.md)。

## 它是如何工作的？

当您安装和初始化启用了[!UICONTROL 设备上决策]的[!DNL Adobe Target]SDK时，将从距离您服务器最近的Akamai CDN下载&#x200B;*规则工件*&#x200B;并将其缓存在您的服务器上。 当在服务器端应用程序中提出检索[!DNL Adobe Target]体验的请求时，将根据缓存的规则工件中编码的元数据在内存中做出有关返回哪个内容的决策，这将定义您的所有[!UICONTROL 设备上决策] A/B和XT活动。

下图显示了[!UICONTROL 设备上决策]架构。 单击以展开图像。

（单击图像可展开至全宽。）

![设备上决策架构图](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/assets/asset-sdk-local-decisioning-architecture-diagram.png "设备上决策架构图"){zoomable="yes"}

## 有哪些好处？

* **提供几乎零延迟的决策。** 在内存中和设备上执行分段和决策，以避免阻塞网络请求。
* **增强应用程序性能。** 在不影响最终用户体验的情况下运行实验并向客户和用户提供个性化。
* **提高Google网站质量分数。** 由于决策发生在内存和服务器端，因此可提高您在线业务的Google网站质量分数，使消费者更容易发现它。
* **从实时分析中学习。** 通过[!DNL Adobe Target]或A4T报表实时了解您的活动表现，让您能够在关键时刻旋转策略。

## 支持的功能

### 活动

设备上决策支持由[基于表单的体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html)创建的以下活动类型：

* [!UICONTROL A/B 测试]
* [!UICONTROL 体验定位] (XT)

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
| [访客轮廓](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html) | 否 |
| [流量源](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html) | 否 |
| [时间范围](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html) | 是 |
| [Experience Cloud受众](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html)（来自Adobe Audience Manager、Adobe Analytics和Adobe Experience Manager的受众） | 否 |

## 如何配置我的客户端以使用[!UICONTROL 设备上决策]？

设备上决策适用于使用[!DNL Adobe Target]服务器端SDK的所有[!DNL Adobe Target]客户。 要启用此功能，请在[!DNL Adobe Target]用户界面中导航到&#x200B;**[!UICONTROL 管理]** > **[!UICONTROL 实施]** > **[!UICONTROL 帐户详细信息]**，并启用&#x200B;**[!UICONTROL 设备上决策]**&#x200B;切换开关。

>[!NOTE]
>
>您必须具有管理员或审批者&#x200B;*用户角色*&#x200B;才能启用或禁用[!UICONTROL 设备上决策]切换开关。

![替代图像](assets/asset-odd-toggle.png)

启用“设备端决策”切换后，[!DNL Adobe Target]将开始为您的客户端生成和传播&#x200B;*规则工件*。

>[!NOTE]
>
>在初始化[!DNL Adobe Target] SDK以使用[!UICONTROL 设备上决策]之前，请确保启用此切换功能。 规则工件将首先需要生成并传播到Akamai CDN，以便[!UICONTROL 设备上决策]正常工作。

### 在工件切换中包括所有现有的[!UICONTROL 设备上决策]符合条件的活动

当您希望所有符合[!UICONTROL 设备上决策]条件的实时[!DNL Target]活动自动包含在工件中时，请切换此&#x200B;**开启**。

将此切换保持为&#x200B;**关闭**&#x200B;表示您需要重新创建和激活任何[!UICONTROL 设备上决策]活动，才能将其包含在生成的规则工件中。

## 我如何知道某个活动具有[!UICONTROL 设备上决策]功能？

创建活动后，活动详细信息页面中显示的名为&#x200B;**[!UICONTROL 决策方法]**&#x200B;的标签指示该活动是否支持[!UICONTROL 设备上决策]。

![替代图像](assets/asset-odd9.png)

您还可以在&#x200B;**[!UICONTROL 活动]**&#x200B;页面上看到支持[!UICONTROL 设备上决策]的所有活动，方法是将列&#x200B;**[!UICONTROL 决策方法]**&#x200B;添加到活动列表中。

![替代图像](assets/asset-odd7.png)

>[!NOTE]
>
>创建和激活具有[!UICONTROL 设备上决策]功能的活动后，可能需要20分钟才能将其包含在生成并传播到Akamai CDN PoP的规则工件中。

## 要确保通过[!DNL Adobe Target]的服务器端SDK成功交付我的[!UICONTROL 设备上决策]活动，需要遵循的步骤概要是什么？

1. 访问[!DNL Adobe Target] UI并导航到&#x200B;**[!UICONTROL 管理]** > **[!UICONTROL 实施]** > **[!UICONTROL 帐户详细信息]**&#x200B;以启用&#x200B;**[!UICONTROL 设备上决策]**&#x200B;切换开关。
1. 在项目&#x200B;]**中启用**[!UICONTROL &#x200B;包含所有现有的[!UICONTROL 设备上决策]限定活动。
1. 创建并激活[!UICONTROL 设备上决策]支持的活动类型，并验证该活动的&#x200B;**[!UICONTROL 决策方法]**&#x200B;是否为&#x200B;**[!UICONTROL 设备上决策]**。
1. 使用`decisioningMethod = on-device`安装并初始化[Node.js](../../node-js/overview.md)或[Java](../../java/overview.md) SDK。
1. 在您的代码中实施`getOffers()`或`getAttributes()`以检索设备上的体验。
1. 部署代码。

有关说明如何开始使用上述步骤1-3的示例，请参阅[快速入门](../getting-started/getting-started.md)部分。


## 其他资源

### 网络研讨会：通过 [!DNL Adobe Target] 的设备上决策进行无延迟的个性化和测试

相比以往，营销人员、产品所有者和开发人员需要更多地在网站上、应用程序中以及他们与客户联系的其他各个环节优化整体客户体验。 具有数据孤岛和复杂实现的多种工具是不够的。

在此录制的网络研讨会中，[!DNL Adobe Target]产品专家讨论了将关键体验优化决策转移到设备上以便在几乎无延迟的情况下在本地执行，在为客户提高网站性能的同时创造激动人心的新用例。

>[!VIDEO](https://video.tv.adobe.com/v/328148/?quality=12)


### 教程：设备上决策

[!DNL Adobe Target] [!UICONTROL 设备上决策]启用几乎零延迟的内容交付。

这个7分钟的视频：

* 描述[!UICONTROL 设备上决策]，包括它与[!DNL Target]实现的其他方法的比较
* 演示如何在Target中启用[!UICONTROL 设备上决策]
* 检查已配置JSON内容的基于表单的编辑器活动示例
* 显示Node.JS SDK代码示例，该代码包含[!UICONTROL 设备上决策]所需的键配置
* 在浏览器中演示结果

>[!VIDEO](https://video.tv.adobe.com/v/329032/?quality=12)

有关更多视频和教程，请参阅[[!DNL Adobe Target] 教程](https://experienceleague.adobe.com/docs/target-learn/tutorials/overview.html?lang=zh-Hans)。

### Adobe Tech Blog — 第1部分：在Edge平台上运行[!DNL Adobe Target] NodeJS SDK以提供试验性和个性化（Akamai Edge员工）

[单击此处访问博客帖子](https://medium.com/adobetech/part-1-run-adobe-target-nodejs-sdk-for-experimentation-and-personalization-on-edge-platforms-4d8660964ed9)。

### Adobe Tech Blog — 第 2 部分：在 Edge 平台上运行 [!DNL Adobe Target] NodeJS SDK 以提供试验性和个性化 (AWS Lambda@Edge)

[单击此处访问博客帖子](https://medium.com/adobetech/part-2-run-adobe-target-nodejs-sdk-for-experimentation-and-personalization-on-edge-platforms-aws-4d6bdac24563)。
