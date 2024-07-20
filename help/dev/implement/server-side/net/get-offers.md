---
title: 使用.NET SDK时，在 [!DNL Adobe Target] 中使用getOffers()
description: 了解如何使用getOffers()执行决策并从 [!DNL Adobe Target]检索体验。
feature: APIs/SDKs
exl-id: 4d1d1cbd-c7e5-4146-9fea-08e01923874d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 13%

---

# 获取选件(.NET)

## 描述

`GetOffers()`用于执行决策并从[!DNL Adobe Target]检索体验。

## 方法

`TargetClient.GetOffers`方法签名。

## \.NET

```dotnet {line-numbers="true"}
TargetDeliveryResponse TargetClient.GetOffers(TargetDeliveryRequest request)
```

`TargetDeliveryRequest`是使用`TargetDeliveryRequest.Builder`创建的。

## \.NET

```dotnet {line-numbers="true"}
TargetDeliveryRequest.Builder TargetDeliveryRequest.Builder()
```

## 参数

`TargetDeliveryRequest.Builder`对象具有以下结构：

| 名称 | 类型 | 必需 | 描述 |
| --- | --- | --- | --- |
| 上下文 | 上下文 | 是 | 指定请求的上下文 |
| sessionId | 字符串 | 否 | 用于链接多个[!DNL Target]请求 |
| thirdPartyId | 字符串 | 否 | 可随每次调用发送的用户的公司标识符 |
| cookie | 列表 | 否 | 同一用户的前[!DNL Target]个请求中返回的Cookie列表。 |
| customerIds | 地图 | 否 | 采用与VisitorId兼容格式的客户ID |
| 执行 | ExecuteRequest | 否 | 要执行的PageLoad或mbox请求。 将立即在服务器端进行评估 |
| 预取 | PrefetchRequest | 否 | Views、PageLoad或mbox请求进行预获取。 会返回转换时要返回的带有通知令牌的标记。 |
| 通知 | 列表 | 否 | 用于发送有关所显示预取内容的通知 |
| requestid | 字符串 | 否 | 将在响应中返回的请求ID。 如果未出现，则自动生成。 |
| impressionId | 字符串 | 否 | 如果存在，则具有相同ID的第二个和后续请求将不会增加活动/量度的展示次数。 如果未出现，则自动生成。 |
| environmentId | 长 | 否 | 有效的客户端环境ID。 如果未指定，则将根据提供的主机确定主机。 |
| 属性 | 属性 | 否 | 通过令牌字段指定at_property。 它可用于控制投放的范围。 |
| trace | 跟踪 | 否 | 启用投放API的跟踪。 |
| qaMode | QAMode | 否 | 使用此对象可在请求中启用QA模式。 |
| locationHint | 字符串 | 否 | [!DNL Target]边缘群集位置提示。 用于为此请求定位给定的边缘群集。 |
| visitor | 访客 | 否 | 用于提供自定义访客API对象。 |
| ID | VisitorId | 否 | 包含访客标识符的对象。 例如 tntId、thirdParyId、mcId、customerIds。 |
| experienceCloud | ExperienceCloud | 否 | 指定与Audience Manager和Analytics的集成。 如果未提供，则使用Cookie自动填充。 |
| tntId | 字符串 | 否 | [!DNL Target]中用户的主要标识符。 已从targetCookies获取。 如果未提供，则自动生成。 |
| mcId | 字符串 | 否 | 用于在不同的Adobe解决方案(ECID)之间合并和共享数据。 已从targetCookies获取。 如果未提供，则自动生成。 |
| trackingServer | 字符串 | 否 | Adobe Analytics服务器，以便[!DNL Adobe Target]和[!DNL Adobe Analytics]将数据正确拼合在一起。 |
| trackingServerSecure | 字符串 | 否 | 为了[!DNL Adobe Target]和[!DNL Adobe Analytics]将数据正确拼合在一起，请使用[!UICONTROL Adobe Analytics Secure Server]。 |
| 决策方法 | 决策方法 | 否 | 可用于为设备上决策明确设置ON_DEVICE或HYBRID决策方法 |

每个字段的值应符合[Target投放API](/help/dev/implement/delivery-api/overview.md)请求规范。

## 响应

`TargetClient.GetOffers()`返回的`TargetDeliveryResponse`具有以下结构：

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| 请求 | TargetDeliveryRequest&#x200B; | [Target投放API](/help/dev/implement/delivery-api/overview.md)请求 |
| 响应 | DeliveryResponse&#x200B; | [Target投放API](/help/dev/implement/delivery-api/overview.md)*响应 |
| 状态 | HttpStatusCode | 响应HTTP状态代码 |
| 消息 | 字符串 | 响应状态消息或错误消息 |
| 位置 | 位置 | [!DNL Target]位置名称，包括全局mbox名称和mbox/视图，仅对此位置提供远程决策 |
| GetCookies | 词典 | 返回此用户的会话元数据的字典。 此用户需要在下一个[!DNL Target]请求中传递。 |
| 访客状态 | IDictionary | 要在客户端为访客API Javascript库初始化设置的访客状态 |

用于保存用户会话数据的`TargetCookie`对象具有以下结构：

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| 名称 | 字符串 | Cookie 名称 |
| 值 | 字符串 | Cookie值 |
| MaxAge | int | 使用`MaxAge`选项可以方便地设置相对于当前时间（以秒为单位）的过期时间 |

你不必担心Cookie会过期。 [!DNL Target]处理SDK中的`MaxAge`。

## 示例

## \.NET

```dotnet {line-numbers="true"}
var targetClientConfig = new TargetClientConfig.Builder("acmeClient", "ABCDEF012345677890ABCDEF0@AdobeOrg")
    .Build();

var targetClient = TargetClient.Create(targetClientConfig);

var mboxRequests = new List<MboxRequest> { new (index: 1, name: "a1-serverside-ab") };

var targetDeliveryRequest = new TargetDeliveryRequest.Builder()
    .SetExecute(new ExecuteRequest(mboxes: mboxRequests))
    .Build();

var targetResponse = targetClient.GetOffers(targetDeliveryRequest);
```
