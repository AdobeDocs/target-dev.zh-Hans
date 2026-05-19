---
keywords: 实施，实施，设置，设置，页面参数， tomcat， url编码，页面内配置文件属性， mbox参数，页面内配置文件属性，脚本配置文件属性，批量配置文件更新API，单个文件更新API，客户属性，实施5，实施6，实施7，实施8，实施9，实施0，实施1，实施2，实施3，实施4，实施5，数据提供程序，数据提供程序
description: 将数据导入 [!DNL Target] （页面参数、配置文件属性、脚本配置文件属性、数据提供程序、单个和批量配置文件更新API、客户属性）。
title: 如何将数据导入Target？
feature: Implementation
exl-id: a54e306a-ea8e-4d3f-bc5d-b5895b6b9a84
TQID: https://experienceleague.adobe.com/pmlPWRHb9tnrdSFm7s5OZ-RRsJJOxw-ntBY5AeswIcM
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 377
ht-degree: 27%

---

# 方法概述

此信息介绍了可用于将数据导入Adobe Target的各种方法。

可用方法包括：

| 方法 | 详细信息 |
| --- | --- |
| [页面参数](page-parameters.md)<br />（也称为“mbox参数”） | 页面参数是直接通过页面代码传入的名称/值对，它们未存储在访客的配置文件中供将来使用。<br />页面参数对于将页面数据发送到[!DNL Target]非常有用，无需与访客的配置文件存储在一起以供将来定位使用。 而是用来描述页面或用户在特定页面上执行的操作。 |
| [页面内配置文件属性](in-page-profile-attributes.md)<br />（也称为“mbox内配置文件属性”） | 页面内配置文件属性是指通过页面代码直接传递的名称/值对，这些页面代码存储在访客的配置文件中以供将来使用。<br />页面内配置文件属性允许将用户特定的数据存储在Target的配置文件中，以供将来定位和分段。 |
| [脚本轮廓属性](script-profile-attributes.md) | 脚本配置文件属性是在[!DNL Target]解决方案中定义的名称/值对。 该值是在每个服务器调用时，通过在 Target 服务器上执行一段 JavaScript 代码来确定。<br />用户编写小代码段，在评估访客的受众和活动成员资格之前，每次mbox调用都会执行该代码段。 |
| [数据提供程序](data-providers.md) | 通过数据提供商，您可以轻松将数据从第三方传递到Target。 |
| [批量轮廓更新 API](bulk-profile-update-api.md) | 通过API，向[!DNL Target]发送.csv文件，其中包含许多访客的访客配置文件更新。 每个访客配置文件均可以在一次调用中通过多个页面内配置文件属性进行更新。 |
| [单个轮廓更新 API](single-profile-update-api.md) | 与批量配置文件更新API几乎相同，但一次更新一个访客配置文件，在API调用中排队，而不是使用.csv文件更新。 |
| [客户属性](customer-attributes.md) | 客户属性可让您通过 FTP 将访客配置文件数据上传到 Experience Cloud。 上传后，即可在Adobe Analytics和Adobe Target中使用这些数据。 |
