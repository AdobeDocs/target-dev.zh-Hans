---
title: 使用at.js的Recommendations实施模式
description: 了解如何将Recommendations的实施模式与at.js结合使用
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 752c52c0db5173f49fd828c297fa7afd7c53c6ce
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# [!DNL Recommendations] 使用at.js的实施模式概述

此实施模式可帮助您了解和创建 [!DNL Adobe Target Recommendations] 使用时的实施 [at.js JavaScript库](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md).

单击图像可展开到全屏。

![Adobe Target架构图](/help/dev/patterns/assets/architecture-chart.png){width="600" zoomable="yes"}

请注意，图像中的数字并不表示操作顺序：

1. 适用于的客户端SDK [!DNL Adobe Target] 和 [!DNL Experience Cloud ID Service]
1. [!DNL Target Delivery API] 调用
1. [!UICONTROL EXPERIENCE CLOUDID] (ECID)客户获取调用
1. 批量配置文件更新API和 [!DNL Customer Attributes] (CA)服务
1. 将客户数据源中的数据摄取到的配置文件 [!DNL Target] 配置文件存储
1. 收集用户档案和行为数据，并决定向访客显示哪种体验
1. 体验在页面上呈现
1. at.js渲染页面上的体验

每个模式由不同的部分组成，每个部分对应于的关键实施要求 [!DNL Target] 实现。

本指南中的单独文章对以下各部分进行了说明：

* [初始化SDK](/help/dev/patterns/recs-atjs/initialize-sdk.md)
* [配置数据收集](/help/dev/patterns/recs-atjs/data-collection.md)
* [渲染体验](/help/dev/patterns/recs-atjs/render-experiences.md)
* [通知Target](/help/dev/patterns/recs-atjs/notify-target.md)

