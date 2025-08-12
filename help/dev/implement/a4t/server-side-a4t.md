---
title: Experience Platform Web SDK中的A4T数据的服务器端日志记录
description: 了解如何使用Experience Platform Web SDK为Adobe Analytics for Target (A4T)启用服务器端日志记录。
seo-title: Server-side logging for A4T data in Experience Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t；target；web；sdk；平台；日志记录；
feature: Implementation
source-git-commit: b1b0424bfe61fb8b4e88723e6bb2c565d75f8351
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 1%

---

# [!DNL Experience Platform Web SDK]中A4T数据的服务器端日志记录

[!DNL Adobe Experience Platform Web SDK]允许您在[!UICONTROL Adobe Analytics for Target]上实施[!UICONTROL Experience Platform Edge Network] (A4T)功能。 启用服务器端日志记录后，通过Edge Network发送的所有[!DNL Analytics]点击在服务器端都通过[!DNL Target]详细信息增加，而无需经历点击拼合过程。

当数据流配置中启用了[!DNL Analytics]时，[!DNL Analytics]的服务器端日志记录已启用：

![Analytics数据流配置已启用](/help/dev/implement/a4t/assets/enable-analytics-datastream.png)

下图显示了启用服务器端[!DNL Analytics]日志记录时数据如何通过系统：

![服务器端日志记录流程](/help/dev/implement/a4t/assets/analytics-server-side-logging.png)

## 后续步骤

本指南介绍了Web SDK中A4T数据的服务器端日志记录。 有关如何处理客户端上A4T数据的更多信息，请参阅[客户端日志记录](/help/dev/implement/a4t/client-side-logging.md)指南。