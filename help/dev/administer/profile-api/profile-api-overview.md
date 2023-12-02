---
title: Adobe Target配置文件API概述
description: 了解如何使用Adobe Target配置文件API将访客数据发送至 [!DNL Target].
contributors: https://github.com/icaraps
exl-id: 482a4175-1d02-47e9-a5c0-dd00e8560773
feature: APIs/SDKs
source-git-commit: 1a1c3d96cf6ef5c337a63fdec8c700da695ff5d1
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 1%

---

# [!DNL Adobe Target Profile APIs overview]

用户配置文件包含网页访客的人口统计和行为信息，如年龄、性别、购买的产品、上次访问时间等。 [!DNL Adobe Target] 使用此信息将它提供给每位访客的内容个性化。

每个访客的配置文件信息存储在Cookie或第三方应用程序中。

如果您的网页实施了 [!DNL Target] 代码([at.js](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md) 或 [Adobe Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk.md))，则Cookie中的用户档案信息将传递到 [!DNL Target] 使用配置文件参数。 [!DNL Target] 通过 `pcID` 它会在访客的Cookie中生成的ID。 但是，您可以使用通过mbox调用从外部应用程序传递配置文件参数 `mbox3rdPartyIds`.

使用 [!DNL Adobe Target] 当您有要发送到的访客的配置文件数据时，可使用配置文件API [!DNL Target] ，并且您不能或不希望将其作为基于页面的集成的一部分发送 [!DNL Target]. 这可能是来自客户关系管理(CRM)或销售点(POS)系统的数据，在页面上不可用。 或者，此数据可能具有更敏感的性质，在页面上传递可能没有意义。

可通过两种方式通过API更新用户档案：

* [单个配置文件更新 API](/help/dev/administer/profile-api/profile-single-api.md)
* [批量更新配置文件](/help/dev/administer/profile-api/profile-bulk-api.md)

旧版配置文件API文档可在以下位置找到： [https://developers.adobetarget.com/api/#profiles](https://developers.adobetarget.com/api/#profiles){target=_blank}
