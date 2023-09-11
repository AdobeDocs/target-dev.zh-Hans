---
title: 实施模式概述
description: 了解如何使用实施模式
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 7a79eb1d263cf42529a5a1b1ca1f9de4db218a49
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---

# 实施模式概述

[!DNL Adobe Target] 实施模式帮助您了解和创建以下体系结构 [!DNL Target] 实现。

单击图像可展开到全屏。

![Adobe Target架构图](/help/dev/patterns/assets/architecture-chart.png){width="600" zoomable="yes"}

请注意，图像中的数字并不表示操作顺序：

1. 适用于的客户端SDK [!DNL Adobe Target] 和 [!DNL Experience Cloud ID Service]
1. [!DNL Target Delivery API] 调用
1. ECID客户获取调用
1. 批量配置文件更新API和 [!DNL Customer Attributes] (CA)服务
1. 将客户数据源中的数据摄取到的配置文件 [!DNL Target] 配置文件存储
1. 收集用户档案/行为数据，并决定向最终用户显示何种体验
1. 体验在页面上呈现
1. at.js渲染页面上的体验

每个阵列由不同的部分组成。 每个部分对应于贵机构的关键实施要求 [!DNL Target] 实现。

本指南在一个单独的页面中对每个部分进行了说明。 例如， [[!DNL Recommendations] 使用at.js的实施模式](/help/dev/patterns/recs-atjs/recs-implementation-pattern-atjs.md) 包含以下页面：

* 初始化SDK
* 配置数据收集
* 渲染体验
* 通知 [!DNL Target]

