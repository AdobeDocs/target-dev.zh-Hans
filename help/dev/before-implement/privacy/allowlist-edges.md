---
keywords: 列入允许列表实施，白名单，白名单，允许列表，边缘，边缘， $9
description: 查看主机列表以帮助您允许列表 [!DNL Adobe Target] 边缘（地理上分散的服务节点，可确保最终用户的最佳响应时间）。
title: 如何允许列表 [!DNL Target] Edge节点？
feature: Privacy & Security
exl-id: a7e5d2fc-da8e-414d-a3da-2441ea21503d
source-git-commit: 1583cfe8ea1009fd1df5c5a0e5f3f95f72daf2b9
workflow-type: tm+mt
source-wordcount: '0'
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
>有关详细信息，请参阅&#x200B;*Adobe Analytics技术说明*&#x200B;文档中的[所有Adobe Analytics IP地址块](https://experienceleague.adobe.com/docs/analytics/technotes/ip-addresses.html?lang=en#all-adobe-analytics-ip-address-blocks){target=_blank}。
>
>正在更新[!DNL Adobe Target]基础结构，希望允许列表地址的客户必须使用这两组IP。 列入允许列表如果未能做到这一点，将会影响使用服务器端或混合实施的客户，在这些实施中，用于获取体验的Target API调用源自配置为使用的防火墙之后的网络内。
>
>以下两个表中列出的所有Edge4 *x*&#x200B;地址都计划于2023年8月9日更新。

## [!DNL Target]个边缘的网络地址转换(NAT) IP地址

[!DNL Target]个边缘的出口IP地址列表。 如果您计划让[!DNL Target]联系您的服务，请允许列表这些IP。

| Edge位置 | 出口IP地址 |
| --- | --- |
| Edge41 （孟买） | 3.6.2.221<P>13.235.112.4 <P>52.66.66.192 |
| Edge42 （东京） | 52.69.55.232<P>43.206.61.43 <P>13.113.73.214 |
| Edge44（美国东岸） | 54.164.192.223<P>52.86.86.203 <P>54.88.167.98 |
| Edge45（美国西海岸） | 52.40.124.129<P>54.148.219.69 <P>54.189.208.212 |
| Edge46（悉尼） | 54.253.144.4<P>54.66.198.142 <P>13.211.218.51 |
| Edge47 （爱尔兰） | 52.208.136.136<P>54.170.28.19 <P>99.80.111.82 |
| Edge48 （新加坡） | 3.1.141.36<P>18.143.112.116 <P>52.76.61.44 |

## [!DNL Target]个边缘IP地址

[!DNL Target]个边缘的IP地址列表。 如果要对[!DNL Target]边缘进行API调用，请允许列表这些IP。

此列表会经常更改，因为负载平衡器会根据流量配置文件进行放大和缩小。

| Edge位置 | 域 | IP 地址 |
| --- | --- | --- |
|  | `CLIENTCODE.tt.omtrdc.net`<br />（其中CLIENTCODE是您的[!DNL Target]客户端ID） |  |
| Edge41 （孟买） | `mboxedge41.tt.omtrdc.net` | 3.6.2.221<P>52.66.66.192<P>13.235.112.4 |
| Edge42 （东京） | `mboxedge42.tt.omtrdc.net` | 43.206.61.43<P>13.113.73.214<P>52.69.55.232 |
| Edge44（美国东岸） | `mboxedge44.tt.omtrdc.net` | 54.88.167.98<P>54.164.192.223<P>52.86.86.203 |
| Edge45（美国西海岸） | `mboxedge45.tt.omtrdc.net` | 52.40.124.129<P>54.148.219.69<P>54.189.208.212 |
| Edge46（悉尼） | `mboxedge46.tt.omtrdc.net` | 54.66.198.142<P>54.253.144.4<P>13.211.218.51 |
| Edge47 （爱尔兰） | `mboxedge47.tt.omtrdc.net` | 54.170.28.19<P>52.208.136.136<P>99.80.111.82 |
| Edge48 （新加坡） | `mboxedge48.tt.omtrdc.net` | 52.76.61.44<P>3.1.141.36<P>18.143.112.116 |

当负载平衡器检测到通信量配置文件中的更改时，它将进行放大或缩小。 根据检测到的更改，Elastic Load Balancing进行扩展所需的时间可在1到7分钟之间。 当负载平衡器扩展时，它们使用新的IP地址列表来更新DNS记录。 为确保您利用增加的容量，Elastic Load Balancing在DNS记录上使用60秒的TTL设置。
