---
title: Experience Platform Web SDK中的A4T数据的服务器端日志记录
description: 了解如何使用Experience Platform Web SDK为Adobe Analytics for Target (A4T)启用服务器端日志记录。
seo-title: Server-side logging for A4T data in Experience Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t；target；web；sdk；平台；日志记录；
feature: Implementation
exl-id: 716f7343-69a6-44d7-baec-a0a0df1b6e1f
TQID: https://experienceleague.adobe.com/I7-G2VO2AN3qFsgkk4JX2Pg6WJfZq0HZkcGL4XQNoWg
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 153
ht-degree: 1%

---

# [!DNL Experience Platform Web SDK]中A4T数据的服务器端日志记录

[!DNL Adobe Experience Platform Web SDK]允许您在[!UICONTROL Experience Platform Edge Network]上实施[!UICONTROL Adobe Analytics for Target] (A4T)功能。 启用服务器端日志记录后，通过Edge Network发送的所有[!DNL Analytics]点击在服务器端都通过[!DNL Target]详细信息增加，而无需经历点击拼合过程。

当数据流配置中启用了[!DNL Analytics]时，[!DNL Analytics]的服务器端日志记录已启用：

![Analytics数据流配置已启用](/help/dev/implement/a4t/assets/enable-analytics-datastream.png)

下图显示了启用服务器端[!DNL Analytics]日志记录时数据如何通过系统：

![服务器端日志记录流程](/help/dev/implement/a4t/assets/analytics-server-side-logging.png)

## 后续步骤

本指南介绍了Web SDK中A4T数据的服务器端日志记录。 有关如何处理客户端上A4T数据的更多信息，请参阅[客户端日志记录](/help/dev/implement/a4t/client-side-logging.md)指南。
