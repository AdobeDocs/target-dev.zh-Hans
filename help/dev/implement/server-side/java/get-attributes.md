---
title: 在Java SDK中使用 [!DNL Adobe Target] 中的getAttributes
description: 了解如何使用getAttributes()从 [!DNL Target] 获取试验性和个性化体验并提取属性值。
feature: APIs/SDKs
exl-id: e493e1b9-7180-4a7c-b98d-be84cc3a57c3
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 13%

---

# 获取属性(Java)

## 描述

`getAttributes()`用于从[!DNL Target]获取试验性和个性化体验并提取属性值。

## 方法

### getAttributes

```javascript {line-numbers="true"}
Attributes TargetClient.getAttributes(TargetDeliveryRequest targetRequest, String ...mboxes)
```

## 参数

| 名称 | 类型 | 必需 | 默认 | 描述 |
| --- | --- | --- | --- | --- |
| targetRequest | TargetDeliveryRequest | 是 | 无 | 与[获取选件](get-offers.md)使用的相同&#x200B;目标请求 |
| mboxNames | var-args数组 | 否 | 无 | mbox名称的变量数组 |


## 结果

从具有以下方法的`TargetClient.getAttributes()`返回的`Attributes`对象：

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| getBoolean(mboxName， key) | 布尔值 | 返回指定mbox名称和属性键的值 |
| getString(mboxName， key) | 字符串 | 返回指定mbox名称和属性键的值 |
| getInteger(mboxName， key) | 整数 | 返回指定mbox名称和属性键的值 |
| getDouble(mboxName， key) | 双精度 | 返回指定mbox名称和属性键的值 |
| Tomboxmap(mboxname) | 地图 | 返回带有键值对的简单映射 |
| getResponse() | TargetDeliveryResponse | 返回通常由getOffers返回的响应对象 |

## 示例

### Java

```javascript {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .build();

TargetClient targetJavaClient = TargetClient.create(clientConfig);

TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
        .context(new Context().channel(ChannelType.WEB))
        .build();

Attributes offerAttributes = targetJavaClient.getAttributes(targetDeliveryRequest, "demo-engineering-flags");

//returns just the value of searchProviderId from the mbox offer
String searchProviderId = offerAttributes.getString("demo-engineering-flags", "searchProviderId");

//returns a simple Map representing the mbox offer
Map<String, Object> engineeringFlags = offerAttributes.toMboxMap("demo-engineering-flags");

//  the value of engineeringFlags looks like this
//  {
//      "cdnHostname": "cdn.cloud.corp.net",
//      "searchProviderId": 143,
//      "hasLegacyAccess": false
//  }

String assetUrl = "http://" + engineeringFlags.cdnHostname + "/path/to/asset";
```
