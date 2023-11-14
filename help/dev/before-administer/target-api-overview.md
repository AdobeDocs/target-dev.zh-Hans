---
title: Adobe Target API概述
description: 其他Adobe Target API的概述，包括投放API、报表API、管理员API、配置文件API、推荐API以及指向Postman集合的链接。
exl-id: bf886103-36af-4061-b8be-2fe645f45ff3
feature: APIs/SDKs
source-git-commit: 2fba03b3882fd23a16342eaab9406ae4491c9044
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 1%

---

# Target API概述

在重点介绍特定于管理员和配置文件API的需求之前，本文通常介绍了不同的Target API。 如果您希望通过UI管理Target，请参阅 [管理部分 *Adobe Target商业用户指南*](https://experienceleague.adobe.com/docs/target/using/administer/administrating-target.html?lang=en).

## API类型

Adobe Target API是支持Adobe Target产品(例如Adobe Recommendations)的API集合。 这些API允许创建可用于处理和集成数据的富数据用户界面。

Adobe Target API可按类型分组：管理员、配置文件、交付和报表。

>[!NOTE]
>
>管理员API和配置文件API通常统称为“管理员API和配置文件API”)，但也可以单独称为（“管理员API”和“配置文件API”）。 Recommendations API是Target管理员API的特定实施。

| API类型 | 它让您能够执行的操作 | 下载链接 | 其他有用链接 |
| --- | --- | --- |--- |
| [管理员](../administer/admin-api/admin-api-overview-new.md) | 创建、修改和删除活动、受众、选件和其他对象(包括Recommendations实体、标准、设计等)。 Recommendations API是一类管理员API。) | <UL><li>[Target管理员API Postman收藏集](https://developers.adobetarget.com/api/#admin-postman-collection)</li><li>[Recommendations API Postman收藏集](https://developer.adobe.com/target/administer/recommendations-api/#section/Postman)</li></UL> | [使用Recommendations API](../before-administer/recs-api/overview.md) |
| 配置文件 | 检索和修改存储在Adobe Target中的用户配置文件。 | [Target配置文件API Postman收藏集](https://developers.adobetarget.com/api/#profiles) |  |
| [交付](../implement/delivery-api/overview.md) | 从Target中检索要交付给最终用户的优化和个性化内容。 | [Target投放API Postman收藏集](/help/dev/before-implement/delivery-api-overview/getting-started.md#postman) |  |
| [报表](../administer/admin-api/admin-api-overview-new.md) | 导出活动结果和其他报告结果。 | 报表API包含在中 [Target管理员API Postman收藏集](https://developers.adobetarget.com/api/#admin-postman-collection). |  |
| [模型](../administer/models-api/models-api-overview.md) | 管理您希望Target从其机器学习模型中排除的功能列表(“阻止列表”)。 列入阻止列表模型API是一种管理员API，但由于其对无法通过UI访问的对象()的唯一操作，此处单独列出模型API。 |  |  |

## API 差异

Target管理员API(包括Recommendations API)与Target投放API之间存在重要区别：

* 管理员API允许您配置Target的各个方面，您也可以在Target UI中配置这些方面。 模型API是一个例外，它允许您配置UI中不可用的Target的各个方面。 不管怎样， **所有管理员API都需要身份验证。**

* 投放API允许您检索内容。 投放API不需要身份验证。

要使用Target管理员API，您必须使用 [Adobe Developer控制台](https://developer.adobe.com/console/home). 有关更多信息，请参阅 [如何配置身份验证](../before-administer/configure-authentication.md).
