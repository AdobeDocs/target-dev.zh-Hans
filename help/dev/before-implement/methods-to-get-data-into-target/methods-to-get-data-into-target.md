---
keywords: 实施，实施，设置，设置，页面参数， tomcat， url编码，页面内配置文件属性， mbox参数，页面内配置文件属性，脚本配置文件属性，批量配置文件更新API，单个文件更新API，客户属性，实施5，实施6，实施7，实施8，实施9，实施0，实施1，实施2，实施3，实施4，实施5，数据提供程序，数据提供程序
description: 将数据导入 [!DNL Target] （页面参数、配置文件属性、脚本配置文件属性、数据提供程序、单个和批量配置文件更新API、客户属性）。
title: 如何将数据导入Target？
feature: Implementation
exl-id: a54e306a-ea8e-4d3f-bc5d-b5895b6b9a84
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 44%

---

# 方法概述

此信息介绍了可用于将数据导入Adobe Target的各种方法。

可用方法包括：

| 方法 | 详细信息 |
| --- | --- |
| [页面参数](page-parameters.md)<br />（也称为“mbox参数”） | 页面参数是直接通过页面代码传入的名称/值对，它们未存储在访客的配置文件中供将来使用。<br />页面参数可用于将页面数据发送到 [!DNL Target] 这些资源无需与访客的配置文件一起存储以供将来定位使用。 而是用来描述页面或用户在特定页面上执行的操作。 |
| [页面内配置文件属性](in-page-profile-attributes.md)<br />（也称为“in-mbox”配置文件属性） | 页面内配置文件属性是直接通过页面代码传递的名称/值对，它们存储在访客的配置文件中供将来使用。<br />页面内配置文件属性允许将特定于用户的数据存储在 Target 的配置文件中，供以后进行定位和分段。 |
| [脚本配置文件属性](script-profile-attributes.md) | 脚本配置文件属性是在 [!DNL Target] 解决方案。 该值是在每个服务器调用时，通过在 Target 服务器上执行一段 JavaScript 代码来确定。<br />为访客评估受众和活动用户编写一小段代码，该代码片段会在每次 mbox 调用时、且在评估访客的受众群体和活动成员资格之前执行。 |
| [数据提供程序](data-providers.md) | 通过数据提供商，您可以轻松将数据从第三方传递到Target。 |
| [批量配置文件更新 API](bulk-profile-update-api.md) | 通过API，将.csv文件发送到 [!DNL Target] 包含许多访客的访客配置文件更新。 每个访客配置文件均可以在一次调用中通过多个页面内配置文件属性进行更新。 |
| [单个配置文件更新 API](single-profile-update-api.md) | 与批量配置文件更新API几乎相同，但一次更新一个访客配置文件，在API调用中排队，而不是使用.csv文件更新。 |
| [客户属性](customer-attributes.md) | 客户属性可让您通过 FTP 将访客配置文件数据上传到 Experience Cloud。上传后，即可在Adobe Analytics和Adobe Target中使用这些数据。 |
