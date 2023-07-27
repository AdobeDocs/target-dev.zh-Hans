---
keywords: 系统图，闪烁， at.js，实施， javascript库， js， atjs， $8
description: 了解 [!DNL Target] at.js JavaScript 库函数，包括用于帮助您了解页面加载时的工作流的系统图。
title: at.js Javascript 库如何工作？
feature: at.js
exl-id: 9183797c-857b-4b7f-a573-6bb1d583f7b1
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 74%

---

# at.js 的工作原理

在客户端实施 [!DNL Adobe Target] 必须使用 at.js JavaScript 库。

在 [!DNL Adobe Target] 的客户端实施中，[!DNL Target] 会将与活动相关联的体验直接交付给客户端浏览器。浏览器将决定要显示的体验，然后显示该体验。借助客户端实施，您可以使用 WYSIWYG 编辑器、[可视化体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC)，或者非可视化界面（[基于表单的体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html)）来创建测试和个性化体验。

## 什么是 at.js？

at.js库是适用于的客户端实施的实施库 [!DNL Adobe Target]. 使用 at.js 库可缩短 Web 实施的页面加载时间，并为单页应用程序提供更好的实施选项。at.js 是推荐使用的实施库，会经常更新功能。我们建议所有客户都实施或迁移到[最新版本的 at.js](/help/dev/implement/client-side/atjs/target-atjs-versions.md)。

有关更多信息，请参阅 [Target JavaScript 库](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html#libraries)。

在 [!DNL Target]实施如下图所示，我们实施了以下Adobe Experience Cloud解决方案： [!DNL Analytics]、Target和 [!DNL Audience Manager]. 此外，以下各项 [!DNL Experience Cloud] 核心服务已实施： [!DNL Adobe Experience Platform]， [!UICONTROL 受众]、和 [!UICONTROL 访客ID服务].

## at.js 1.*x* 和 at.js 2.x 工作流程图之间有何差异？

请参阅[从 at.js 1.x 升级到 at.js 2.x](/help/dev/implement/client-side/atjs/upgrading-from-atjs-1x-to-atjs-20.md)，以了解有关 2.O 与 1.*x* 之间的差异。

从高层次来看，两个版本之间存在一些差异：

* at.js 2.x 没有全局 mbox 请求概念，但有页面加载请求概念。页面加载请求可以视为检索应该被应用于网站初始页面加载的内容的请求。
* at.js 2.x管理一个概念，称为 [!UICONTROL 视图]，用于单页应用程序(SPA)。 at.js 1.*x* 并没有此概念。

## at.js 2.x 图

下图可帮助您了解at.js 2.x的工作流程 [!UICONTROL 视图] 以及这如何增强SPA集成。 要更好地了解 at.js 2.x 中使用的概念，请参阅[单页应用程序实施](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md)。

（单击图像可展开至全宽。）

![使用at.js 2.x的Target流程](/help/dev/implement/client-side/assets/system-diagram-atjs-20.png "使用at.js 2.x的Target流程"){zoomable=&quot;yes&quot;}

| 步骤 | 详细信息 |
| --- | --- |
| 1 | 调用返回 [!UICONTROL EXPERIENCE CLOUDID] 如果用户通过了身份验证；另一调用会同步客户ID。 |
| 2 | at.js 库会同步加载，并隐藏文档正文。<br />也可以选择预先隐藏页面上实施的代码段，以异步方式加载 at.js。 |
| 3 | 将会发出页面加载请求，其中包括已配置的所有参数（例如，MCID、SDID 和客户 ID）。 |
| 4 | 配置文件脚本先执行，然后注入到 [!UICONTROL 配置文件存储]. Sto重新从请求符合条件的受众 [!UICONTROL 受众库] (例如，受众共享自 [!DNL Adobe Analytics]， [!DNL Audience Manager]、等)。<br />[!UICONTROL 客户属性会以批量过程发送到配置文件存储区。] |
| 5 | 根据 URL 请求参数和配置文件数据，[!DNL Target] 可决定将哪些活动和体验返回给查看当前页面和未来视图的访客。 |
| 6 | 目标内容会发送回页面，其中可能包含其他个性化的配置文件值。<br />当前页面上的目标内容会在默认内容不发生闪烁的情况下尽快显示。<br />作为用户在 SPA 中操作结果而显示的视图的针对性内容，将缓存在浏览器中，这样便可在通过 `triggerView()` 触发视图时即时应用而无需额外的服务器调用。 |
| 7 | Analytics数据发送到 [!UICONTROL 数据收集] 服务器。 |
| 8 | 目标数据会通过SDID匹配到Analytics数据，并且会进行相应处理以保存到 [!DNL Analytics] 报告存储。之后，便可以在 <br />[!DNL Analytics] 和 [!DNL Analytics] 中通过  (A4T) 报表查看 [!DNL Target] 数据。 |

现在，无论在 SPA 上的什么位置实施 `triggerView()`，都会从缓存中检索查看次数和操作，并在没有服务器调用的情况下显示给用户。`triggerView()` 还会向 [!DNL Target] 后端发出通知请求，以增加和记录展示次数计数。有关带有视图的 SPA 的 at.js 的更多信息，请参阅[单页应用程序实施](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md)。

（单击图像可展开至全宽。）

![Target流程at.js 2.x triggerView](/help/dev/implement/client-side/assets/atjs-20-triggerview.png "Target流程at.js 2.x triggerView"){zoomable=&quot;yes&quot;}

| 步骤 | 详细信息 |
| --- | --- |
| 1 | 在 SPA 中调用 `triggerView()`[!UICONTROL  以渲染视图并应用操作来修改可视化元素。] |
| 2 | 从缓存中读取视图的目标内容。 |
| 3 | 目标内容会在默认内容不发生闪烁的情况下尽快显示。 |
| 4 | 通知请求将发送到 [!DNL Target] 配置文件存储区，以计算活动中的访客和递增量度。 |
| 5 | [!DNL Analytics] 数据发送至 [!UICONTROL 数据收集服务器]. |
| 6 | [!DNL Target] 数据会通过 SDID 匹配到 [!DNL Analytics] 数据，并且会进行相应处理以保存到 [!DNL Analytics] 报表存储中。[!DNL Analytics] 然后，便可以在以下两个位置查看数据 [!DNL Analytics] 和 [!DNL Target] 通过A4T报表。 |

### 视频 - at.js 2.x 架构图

at.js 2.x 增强了 Adobe Target 对 SPA 的支持，并与其他 Experience Cloud 解决方案集成。该视频介绍了如何将所有内容结合到一起。

>[!VIDEO](https://video.tv.adobe.com/v/26250/?quality=12)

有关更多信息，请参阅[了解 at.js 2.x 的工作方式](https://experienceleague.adobe.com/docs/target-learn/tutorials/implementation/understanding-how-atjs-20-works.html)。

## at.js 1.x 流程图

下图可帮助您了解at.js 1.x的工作流程。

（单击图像可展开至全宽。）

![Target流程at.js 1.x](/help/dev/implement/client-side/assets/target-flow.png "Target流程at.js 1.x"){zoomable=&quot;yes&quot;}

| 步骤 | 描述 | 调用 | 描述 |
|--- |--- |--- |--- |
| 1 | 如果用户通过了身份验证，则调用会返回 Experience Cloud ID (MCID)；另一调用会同步客户 ID。 | 2 | at.js 库会同步加载，并隐藏文档正文。 |
| 3 | 将会发出全局 mbox 请求，其中包括已配置的所有参数，例如 MCID、SDID 和访客 ID（可选）。 | 4 | 配置文件脚本在执行后进入配置文件存储区。存储区向受众库请求符合条件的受众(例如，从Adobe Analytics、Audience Manager等共享的受众)。<br />客户属性会以批量过程发送到配置文件存储区。 |
| 5 | [!DNL Target] 根据 URL、mbox 参数和配置文件数据确定要返回给访客的活动和体验。 | 6 | 目标内容会发送回页面，其中可能包含其他个性化的配置文件值。<br />体验会在默认内容不发生闪烁的情况下尽快显示。 |
| 7 | Analytics 数据会发送到数据收集服务器。 | 8 | Target 数据会通过 SDID 匹配到 Analytics 数据，并且会进行相应处理以保存到 Analytics 报表存储中。之后，便可以在 Analytics 和 <br /> 中通过 [!DNL Target]Analytics for Target[!UICONTROL  (A4T) 报表查看 ]Analytics 数据。 |

### 视频 - 办公时间：at.js 提示和概述（2019 年 6 月 26 日）

这段视频是“办公时间”的录像，“办公时间”是一项由 [!UICONTROL Adobe客户关怀] 团队。

* 使用 at.js 的优点
* at.js 设置
* 处理闪烁的情况
* 调试 at.js
* 已知问题
* 常见问题解答

>[!VIDEO](https://video.tv.adobe.com/v/27959/?quality=12)

## at.js 如何渲染带有 HTML 内容的选件

在渲染带有 HTML 内容的选件时，at.js 会应用以下算法：

1. 预先加载图像（如果 HTML 内容中包含任何 `<img>` 标记）。

1. 将 HTML 内容附加到 DOM 节点。

1. 执行内联脚本（代码包含在 `<script>` 标记中）。

1. 以异步方式加载并执行远程脚本（`<script>` 标记具有 `src` 属性）。

重要说明：

* at.js 对远程脚本的执行顺序不提供任何保证，因为它们是异步加载的。
* 内联脚本不应对远程脚本有任何依赖关系，因为远程脚本稍后才会加载和执行。
