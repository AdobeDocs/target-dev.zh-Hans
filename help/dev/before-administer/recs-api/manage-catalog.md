---
title: 如何使用API管理Recommendations目录
description: 使用Adobe Target API创建、更新、保存、获取和删除Recommendations目录中的实体所需的步骤。
feature: APIs/SDKs, Recommendations, Administration & Configuration
kt: 3815
thumbnail: null
author: Judy Kim
exl-id: aea82607-cde4-456a-8dfb-2967badce455
source-git-commit: 2fba03b3882fd23a16342eaab9406ae4491c9044
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 1%

---

# 使用API管理Recommendations目录

同时确保您符合 [使用Recommendations API的要求](/help/dev/before-administer/recs-api/overview.md#prerequisites)，您已学习如何 [生成访问令牌](/help/dev/before-administer/configure-authentication.md) 使用JWT身份验证流程使用 [!DNL Adobe Target] 上的管理员API [Adobe Developer控制台](https://developer.adobe.com/console/home).

您现在可以使用 [RECOMMENDATIONS API](https://developer.adobe.com/target/administer/recommendations-api/) 以添加、更新或删除推荐目录中的项目。 与其他Adobe Target管理员API一样，Recommendations API需要身份验证。

>[!NOTE]
>
>发送 **[!UICONTROL IMS：JWT通过用户令牌生成+身份验证]** 请求时刷新您的访问令牌以进行身份验证，因为它在24小时后过期。 请参阅 [配置AdobeAPI身份验证](../configure-authentication.md) 以获取说明。

![JWT3ff](assets/configure-io-target-jwt3ff.png)

在继续操作之前，请先获取 [Recommendations Postman收藏集](https://developer.adobe.com/target/administer/recommendations-api/#section/Postman).

## 使用保存实体API创建和更新项目

要使用API而不是CSV产品信息源或产品页面上触发的Target请求填充您的Recommendations产品数据库，请使用 [保存实体API](https://developer.adobe.com/target/administer/recommendations-api/#operation/saveEntities). 此请求在单一Target环境中添加或更新项目。 语法为：

```
POST https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities
```

例如，当满足某些阈值时（例如库存或价格的阈值），可以使用保存实体来更新项目，以便标记这些项目并阻止推荐它们。

1. 导航到 **[!UICONTROL Target]** > **[!UICONTROL 设置]** > **[!UICONTROL 主机]** > **[!UICONTROL 控制环境]** ，以获取要添加或更新项目的目标环境ID。

   ![SaveEntities1](assets/SaveEntities01.png)

1. 验证 `TENANT_ID` 和 `API_KEY` 引用之前建立的Postman环境变量。 使用下图进行比较。 如有必要，请修改API请求中的标头和路径，使其与下图中的标头和路径相匹配。

   ![SaveEntities3](assets/SaveEntities03.png)

1. 输入您的JSON为 **原始** 中的代码 **正文**. 不要忘记使用指定环境ID `environment` 变量。 （在以下示例中，环境ID为6781。）

   ![SaveEntities4.png](assets/SaveEntities04.png)

   以下是将entity.id kit2001与Toaster Oven产品的关联实体值添加到环境6781中的示例JSON。

   ```
       {
       "entities": [{
               "name": "Toaster Oven",
               "id": "kit2001",
               "environment": 6781,
               "categories": [
                   "housewares:appliances"
               ],
               "attributes": {
                   "inventory": 77,
                   "margin": 23,
                   "message": "crashing helicopter",
                   "pageUrl": "www.foobar.foo.com/helicopter.html",
                   "thumbnailUrl": "www.foobar.foo.com/helicopter.jpg",
                  "value": 19.2
               }
           }]
       }
   ```

1. 单击&#x200B;**[!UICONTROL 发送]**。您应会收到以下响应。

   ![SaveEntities5.png](assets/SaveEntities05.png)

   可以对JSON对象进行缩放以发送多个产品。 例如，此JSON指定两个实体。

   ```
       {
           "entities": [{
                   "name": "Toaster Oven",
                   "id": "kit2001",
                   "environment": 6781,
                   "categories": [
                       "housewares:appliances"
                   ],
                   "attributes": {
                       "inventory": 89,
                       "margin": 11,
                       "message": "Toaster Oven",
                       "pageUrl": "www.foobar.foo.com/helicopter.html",
                       "thumbnailUrl": "www.foobar.foo.com/helicopter.jpg",
                       "value": 102.5
                   }
               },
               {
                   "name": "Blender",
                   "id": "kit2002",
                   "environment": 6781,
                   "categories": [
                       "housewares:appliances"
                   ],
                   "attributes": {
                       "inventory": 36,
                       "margin": 5,
                       "message": "Blender",
                       "pageUrl": "www.foobar.foo.com/helicopter.html",
                       "thumbnailUrl": "www.foobar.foo.com/helicopter.jpg",
                       "value": 54.5
                   }
               }
           ]
       }
   ```

1. 现在轮到你了！ 使用 **[!UICONTROL 保存实体]** 用于将以下项目添加到目录的API。 使用上面的JSON示例作为起点。 （您需要扩展JSON以包含其他实体。）

   ![SaveEntities6.png](assets/SaveEntities06.png)

似乎后两个项目不属于该组。 让我们使用 **[!UICONTROL 获取实体]** API，如有必要，请使用 **[!UICONTROL 删除实体]** API。

## 使用获取实体API获取项目详细信息

要检索现有项目的详细信息，请使用 [获取实体API](https://developer.adobe.com/target/administer/recommendations-api/#operation/getEntity). 语法为：

```
GET https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities/[entity.id]
```

一次只能检索单个实体的实体详细信息。 您可以使用获取实体来确认按预期在目录中进行了更新，或者审核目录的内容。

1. 在API请求中，使用变量指定实体ID `entityId`. 以下示例将返回entityId=kit2004的实体的详细信息。

   ![GetEntity1](assets/GetEntity1.png)

1. 验证 `TENANT_ID` 和 `API_KEY` 引用之前建立的Postman环境变量。 使用下图进行比较。 如有必要，请修改API请求中的标头和路径，使其与下图中的标头和路径相匹配。

   ![GetEntity2](assets/GetEntity2.png)

1. 发送请求。

   ![GetEntity3](assets/GetEntity3.png)
如果您收到错误消息指出未找到实体，如上面的示例所示，请验证您是否向正确的Target环境提交请求。



   >[!NOTE]
   >
   >如果没有明确指定环境，则获取实体会尝试从获取实体。 [默认环境](https://experienceleague.adobe.com/docs/target/using/administer/environments.html) 仅限。 如果要从默认环境以外的任何环境提取，则必须指定环境ID。

1. 如有必要，请添加 `environmentId` 参数，然后重新发送请求。

   ![GetEntity4](assets/GetEntity4.png)

1. 发送另一个 **[!UICONTROL 获取实体]** 请求，这次检查其entityId=kit2005的实体。

   ![GetEntity5](assets/GetEntity5.png)

假设您决定需要从目录中删除这些实体。 让我们使用 **[!UICONTROL 删除实体]** API。

## 使用删除实体API删除项目

要从目录中删除项目，请使用 [删除实体API](https://developer.adobe.com/target/administer/recommendations-api/#operation/deleteEntities). 语法为：

```
DELETE https://mc.adobe.io/{{TENANT_ID}}/target/recs/entities?ids=[comma-delimited-entity-ids]&environment=[environmentId]
```

>[!WARNING]
>
>删除实体API会删除由您指定的ID引用的实体。 如果未提供实体ID，则给定环境中的所有实体都将被删除。 如果未指定环境ID，将从所有环境中删除实体。 请谨慎使用！

1. 导航到 **[!UICONTROL Target]** > **[!UICONTROL 设置]** > **[!UICONTROL 主机]** > **[!UICONTROL 环境]** ，以获取从中删除项目的目标环境ID。

   ![DeleteEntities1](assets/SaveEntities01.png)

1. 在API请求中，使用语法指定要删除的实体的实体ID `&ids=[comma-delimited-entity-ids]` （一个查询参数）。 删除多个实体时，使用逗号分隔ID。

   ![DeleteEntities2](assets/DeleteEntities2.png)

1. 使用语法指定环境ID `&environment=[environmentId]`，否则将删除所有环境中的实体。

   ![DeleteEntities3](assets/DeleteEntities3.png)

1. 验证 `TENANT_ID` 和 `API_KEY` 引用之前建立的Postman环境变量。 使用下图进行比较。 如有必要，请修改API请求中的标头和路径，使其与下图中的标头和路径相匹配。

   ![DeleteEntities4](assets/DeleteEntities4.png)

1. 发送请求。

   ![DeleteEntities5](assets/DeleteEntities5.png)

1. 使用验证您的结果 **[!UICONTROL 获取实体]**，现在应指示无法找到已删除的实体。

   ![DeleteEntities6](assets/DeleteEntities6.png)

   ![DeleteEntities6](assets/DeleteEntities7.png)

恭喜！您现在可以使用Recommendations API创建、更新、删除和获取有关目录中的实体的详细信息。 在下一部分中，您将了解如何管理自定义标准。

&lt;!— [下一课程“管理自定义标准”>](manage-custom-criteria.md) —>
