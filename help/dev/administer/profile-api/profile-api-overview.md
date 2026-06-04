---
title: 更新用户档案
description: 了解如何使用Adobe Target配置文件API将访客数据发送到 [!DNL Target]。
contributors: https://github.com/icaraps
exl-id: 482a4175-1d02-47e9-a5c0-dd00e8560773
feature: APIs/SDKs
TQID: https://experienceleague.adobe.com/jclCuF4pe3JwAN-2RhQ9NfA5KtEfKUuawlmrE3aS0bQ
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 217
ht-degree: 1%

---

# 更新用户档案

用户配置文件包含网页访客的人口统计和行为信息，如年龄、性别、购买的产品、上次访问时间等。 [!DNL Adobe Target]使用此信息来个性化它提供给每位访客的内容。

每个访客的配置文件信息存储在Cookie或第三方应用程序中。

如果您的网页实现了[!DNL Target]代码（[at.js](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md)或[Adobe Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md)），则来自Cookie的配置文件信息将使用配置文件参数传递到[!DNL Target]。 [!DNL Target]通过它在访客Cookie中生成的`pcID`唯一标识每个访客。 但是，您可以使用`mbox3rdPartyIds`通过mbox调用从外部应用传递配置文件参数。

当您有访客的配置文件数据要发送到[!DNL Target]时，请使用[!DNL Adobe Target]配置文件API，您不能或不希望将这些配置文件数据作为您与[!DNL Target]的基于页面的集成的一部分发送。 这可能是来自客户关系管理(CRM)或销售点(POS)系统的数据，在页面上不可用。 或者，此数据可能具有更敏感的性质，在页面上传递可能没有意义。

可通过两种方式通过API更新用户档案：

* [单个轮廓更新 API](/help/dev/administer/profile-api/profile-single-api.md)
* [批量更新配置文件](/help/dev/administer/profile-api/profile-bulk-api.md)
