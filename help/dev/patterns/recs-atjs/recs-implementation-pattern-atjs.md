---
title: 使用at.js的“推荐”实施模式
description: 了解如何将Recommendations实施模式用于at.js
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: d568cd1d-acc3-42e0-ae2c-5787e6f361f8
TQID: https://experienceleague.adobe.com/uYNa5mL-8ffPS-ddjnQzILnPFMbjNJqKZDmQT8qFeGA
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 155
ht-degree: 0%

---

# 使用at.js的[!DNL Recommendations]实施模式概述

使用[at.js JavaScript库](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md)时，此实施模式可帮助您了解和创建您的[!DNL Adobe Target Recommendations]实施。

单击图像可展开到全屏。

![Adobe Target架构图](/help/dev/patterns/assets/architecture-chart.png){width="600" zoomable="yes"}

请注意，图像中的数字并不表示操作顺序：

1. [!DNL Adobe Target]和[!DNL Experience Cloud ID Service]的客户端SDK
1. [!DNL Target Delivery API]呼叫
1. [!UICONTROL Experience Cloud ID] (ECID)客户获取调用
1. 批量配置文件更新API和[!DNL Customer Attributes] (CA)服务
1. 配置文件数据从客户的数据源摄取到[!DNL Target]配置文件存储
1. 收集用户档案和行为数据，并决定向访客显示哪种体验
1. 体验在页面上呈现
1. at.js渲染页面上的体验

每个模式由不同的部分组成，每个部分对应于[!DNL Target]实现的关键实施要求。

本指南中的单独文章对以下各部分进行了说明：

* [初始化SDK](/help/dev/patterns/recs-atjs/initialize-sdk.md)
* [配置数据收集](/help/dev/patterns/recs-atjs/data-collection.md)
* [渲染体验](/help/dev/patterns/recs-atjs/render-experiences.md)
* [通知Target](/help/dev/patterns/recs-atjs/notify-target.md)
