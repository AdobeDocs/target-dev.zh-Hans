---
title: Experience Platform Web SDK中的Adobe Analytics for Target (A4T)日志记录
description: 了解如何使用Experience Platform Web SDK控制Adobe Analytics for Target (A4T)数据的收集。
seo-title: Adobe Analytics for Target (A4T) Logging in the Experience Platform Web SDK
seo-description: Learn how to control the collection of Adobe Analytics for Target (A4T) data using the Experience Platform Web SDK.
keywords: a4t；日志记录；analytics；sdk；web sdk；
feature: Implementation
exl-id: 886588bf-4416-4f1e-aecc-467e48c8fb23
TQID: https://experienceleague.adobe.com/cShqvj3wSialxA-ajnROnIpzjuz66pNg3CLM6l2xPLg
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: a94ced60-8199-4549-b453-ede2acb4101e
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 265
ht-degree: 1%

---

# [!DNL Experience Platform Web SDK]中的[!DNL Adobe Analytics for Target] (A4T)日志记录

当使用[!DNL Adobe Target]进行个性化时，您可以选择要用于性能测量的系统。 每个[Target活动](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html)都允许您在[!DNL Target]报表和Adobe [!DNL Analytics]报表之间进行选择。

如果您正在使用[!DNL Analytics]报表，[!DNL Target]必须向[!DNL Analytics]传达以下信息：

* 您的访客已进入哪个[!DNL Target]活动
* 他们看到的体验
* 已达到哪个转化

[!DNL Adobe Experience Platform Web SDK]支持[!UICONTROL Analytics for Target] (A4T)用例的两种类型的[!DNL Analytics]日志记录：

| 日志记录方法 | 描述 |
| --- | --- |
| 服务器端[!DNL Analytics]日志记录 | 通过Edge Network发送的所有[!DNL Analytics]点击量在服务器端都通过[!DNL Target]详细信息进行了增强，无需经历点击拼合过程。 |
| 客户端[!DNL Analytics]日志记录 | [!DNL Target]数据在客户端返回，允许您使用[数据插入API](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html)手动扩充数据并将其发送到[!DNL Analytics]。 |

日志记录方法取决于您是否对配置的[数据流](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview)启用了[!DNL Adobe Analytics]：

![正在记录方法决策流程](/help/dev/implement/a4t/assets/analytics-logging.png)

## 后续步骤

本文档简要介绍Web SDK中A4T数据的各种记录方法。 有关每种方法的更多详细信息，请参阅以下文档：

* [Experience Platform Web SDK中的A4T数据的服务器端日志记录](/help/dev/implement/a4t/client-side-logging.md)
* [Experience Platform Web SDK中的A4T数据的客户端日志记录](/help/dev/implement/a4t/client-side-logging.md)
