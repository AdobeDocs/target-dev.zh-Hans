---
keywords: 列入允许列表实施，白名单，白名单，允许列表，边缘，边缘， $9
description: 查看主机列表以帮助您允许列表 [!DNL Adobe Target] 边缘（地理上分散的服务节点，可确保最终用户的最佳响应时间）。
title: 如何允许列表 [!DNL Target] Edge节点？
feature: Privacy & Security
exl-id: a7e5d2fc-da8e-414d-a3da-2441ea21503d
source-git-commit: 662d415bc3c216bcd038f07dcaa0fd83f6518690
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# 允许列表[!DNL Target]个边缘节点

帮助您允许列表[!DNL Adobe Target]边缘的信息和最新的主机列表。

边缘是一种地理上分散的服务架构，它确保请求内容的最终用户无论身在何处，均可获得最佳响应时间。 每个边缘节点都具有响应用户的内容请求并跟踪该请求上的分析数据所需的所有信息。 用户请求被路由到最近的边缘节点。 有关详细信息，请参阅[边缘网络](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html#concept_0AE2ED8E9DE64288A8B30FCBF1040934)。

如果需要，您可以允许列表[!DNL Target]边缘节点。

>[!IMPORTANT]
>
>除了列入允许列表列入允许列表文章中讨论的[!DNL Target]个边缘和[!DNL Target]个边缘IP地址的网络地址转换(NAT) IP地址外，您还应转换所有[!DNL Adobe Analytics] IP地址块。
>
>有关详细信息，请参阅[Adobe Analytics技术说明](https://experienceleague.adobe.com/docs/analytics/technotes/ip-addresses.html?lang=en#all-adobe-analytics-ip-address-blocks){target=_blank}文档中的&#x200B;*所有Adobe Analytics IP地址块*。
>
>正在更新[!DNL Adobe Target]基础结构，希望允许列表地址的客户必须使用这两组IP。 列入允许列表如果未能做到这一点，将会影响使用服务器端或混合实施的客户，在这些实施中，用于获取体验的Target API调用源自配置为使用的防火墙之后的网络内。

为确保通过[!DNL Target]对[!DNL Experience Edge Connector]的访问不中断，客户可以更新其网络配置以允许流量流向代理服务。

## 代理服务概述

* **服务终结点**： `https://tnt-web-proxy.adobe.io`。
* **基础架构**：托管在[!DNL Adobe] Ethos平台上。
* **注意**：此服务使用基于延迟的DNS路由，不依赖静态IP地址。

## CNAME目标

代理服务使用CNAME记录在多个区域间动态路由流量。 这些是当前的目标：

| Edge位置 | 出口IP地址 |
| --- | --- |
| 区域 | CNAME目标 |
| 欧洲(eu-west-1) | `ethos.pub.ethos11-prod-nld2.ethos.adobe.net` |
| 美国东部(us-east-2) | `ethos.pub.ethos11-prod-va7.ethos.adobe.net` |
| 美国东部(us-east-1) | `ethos.pub.ethos11-prod-aus5.ethos.adobe.net` |

## 建议的允许列表条目

为确保可靠的连接，请允许列表以下主机名：

* `ethos.pub.ethos11-prod-nld2.ethos.adobe.net`
* `ethos.pub.ethos11-prod-va7.ethos.adobe.net`
* `ethos.pub.ethos11-prod-aus5.ethos.adobe.net`

## 可选： IP发现

如果您的网络策略需要基于IP的列入允许列表，则可以使用此工具查看与代理服务关联的当前公共IP地址：

* `DNSChecker – A Record Lookup for tnt-web-proxy.adobe.io`