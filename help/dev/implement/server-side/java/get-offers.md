---
title: 在中使用getOffers() [!DNL Adobe Target] 使用Java SDK时
description: 了解如何使用getOffers()执行决策并从中检索体验 [!DNL Adobe Target].
feature: APIs/SDKs
exl-id: 9d7bf956-9d6a-4b4f-a401-2e6814f17f3d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 13%

---

# 获取选件(Java)

## 描述

`getOffers()` 用于执行决策并从以下位置检索体验 [!DNL Adobe Target].

## 方法

### getOffers

此 `TargetClient.getOffers` 方法签名如下所示。

**请求**

```javascript {line-numbers="true"}
TargetDeliveryResponse TargetClient.getOffers(TargetDeliveryRequest request)
```

TargetDeliveryRequest使用以下方式创建 `TargetDeliveryRequest.builder`.

**响应**

```javascript {line-numbers="true"}
TargetDeliveryRequestBuilder TargetDeliveryRequest.builder()
```

## 参数

此 `[!UICONTROL TargetDeliveryRequestBuilder]` 对象具有以下结构：

| 名称 | 类型 | 必需 | 描述 |
| --- | --- | --- | --- |
| 上下文 | 上下文 | 是 | 指定请求的上下文 |
| sessionId |  | 字符串 | 否 | 用于链接多个 [!DNL Target] 请求 |
| thirdPartyId | 字符串 | 否 | 可随每次调用发送的用户的公司标识符 |
| cookie | 列表 | 否 | 上一页返回的Cookie列表 [!DNL Target] 同一用户的请求。 |
| customerIds | 地图 | 否 | 采用与VisitorId兼容格式的客户ID |
| 执行 | ExecuteRequest | 否 | 要执行的PageLoad或mbox请求。 将立即在服务器端进行评估 |
| 预取 | PrefetchRequest | 否 | Views、PageLoad或mbox请求进行预获取。 会返回转换时要返回的带有通知令牌的标记。 |
| 通知 | 列表 | 否 | 用于发送有关所显示预取内容的通知 |
| requestId | 字符串 | 否 | 将在响应中返回的请求ID。 如果未出现，则自动生成。 |
| impressionId | 字符串 | 否 | 如果存在，则具有相同ID的第二个和后续请求将不会增加活动/量度的展示次数。 如果未出现，则自动生成。 |
| environmentId | 长整型 | 否 | 有效的客户端环境ID。 如果未指定，则将根据提供的主机确定主机。 |
| 属性 | 属性 | 否 | 通过令牌字段指定at_property。 它可用于控制投放的范围。 |
| trace | 跟踪 | 否 | 启用投放API的跟踪。 |
| qaMode | QAMode | 否 | 使用此对象可在请求中启用QA模式。 |
| locationHint | 字符串 | 否 | [!DNL Target] 边缘群集位置提示。 用于为此请求定位给定的边缘群集。 |
| visitor | 访客 | 否 | 用于提供自定义访客API对象。 |
| ID | VisitorId | 否 | 包含访客标识符的对象。 例如 tntId、thirdParyId、mcId、customerIds。 |
| experienceCloud | ExperienceCloud | 否 | 指定与Audience Manager和Analytics的集成。 如果未提供，则使用Cookie自动填充。 |
| tntId | 字符串 | 否 | 中的主要标识符 [!DNL Target] 对于用户。 已从targetCookies获取。 如果未提供，则自动生成。 |
| mcId | 字符串 | 否 | 用于在不同的报表包之间合并和共享数据 [!DNL Adobe] 解决方案(ECID)。 已从targetCookies获取。 如果未提供，则自动生成。 |
| trackingServer | 字符串 | 否 | Adobe Analytics服务器用于 [!DNL Adobe Target] 和 [!DNL Adobe Analytics] 以正确地将数据拼合在一起。 |
| trackingServerSecure | 字符串 | 否 | 此 [!UICONTROL Adobe Analytics Secure Server] 为了 [!DNL Adobe Target] 和 [!DNL Adobe Analytics] 以正确地将数据拼合在一起。 |
| 决策方法 | 决策方法 | 否 | 可用于为设备上决策明确设置ON_DEVICE或HYBRID决策方法 |

每个字段的值应符合 *[!UICONTROL Target视图交付API]* 请求规范。 要了解有关 *[!UICONTROL Target视图交付API]*，请参见 [http://developers.adobetarget.com/api/#view-delivery-overview](http://developers.adobetarget.com/api/#view-delivery-overview)


## 响应

此 `TargetDeliveryResponse` 返回者 `TargetClient.getOffers(`)具有以下结构：

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| request | TargetDeliveryRequest&#x200B; | *[!DNL Target]* request |
| 响应 | DeliveryResponse | *[!DNL Target]* 响应 |
| cookie | 列表 | 此用户的会话元数据列表。 需要在此用户的下一个目标请求中传递。 |
| visitorState | 地图 | 要在客户端设置的访客状态，供访客API使用 |
| responsestatus | 响应状态 | 表示响应状态的对象 |

此 `ResponseStatus` 响应中包含以下字段：

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| status | int | 从返回的HTTP状态 [!DNL Target] |
| message | 字符串 | 如果HTTP状态不是200，则显示状态消息 |
| remoteMbox | 字符串列表 | 用于设备上决策。 包含具有无法完全在设备上决定的远程活动的mbox列表。 |
| remoteView | 字符串列表 | 用于设备上决策。 包含具有无法完全在设备上决定的远程活动的视图列表。 |

此 `TargetCookie` 用于保存用户会话数据的对象具有以下结构：

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| name | 字符串 | Cookie 名称 |
| value | 字符串 | Cookie值，该值将转换为字符串 |
| maxAge | 数值 | 通过maxAge选项，可以方便地设置相对于当前时间（以秒为单位）的过期时间 |

你不必担心Cookie会过期。 Target处理SDK中的maxAge。

## 示例

**请求**

```javascript {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .build();

TargetClient targetJavaClient = TargetClient.create(clientConfig);

List<MboxRequest> mboxRequests = new ArrayList<>();
mboxRequests.add((MboxRequest) new MboxRequest().name("a1-serverside-ab").index(1));

TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
        .context(new Context().channel(ChannelType.WEB))
        .execute(new ExecuteRequest().setMboxes(mboxRequests))
        .build();
```

**响应**

```javascript {line-numbers="true"}
TargetDeliveryResponse targetResponse = targetJavaClient.getOffers(targetDeliveryRequest);
```
