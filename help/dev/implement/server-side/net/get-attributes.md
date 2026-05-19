---
title: 将 [!DNL Adobe Target] 中的getAttributes用于.NET SDK
description: 了解如何使用getAttributes()从 [!DNL Target] 获取试验性和个性化体验并提取属性值。
feature: APIs/SDKs
exl-id: 808da83d-3077-468b-a2ad-e35c25905f7d
TQID: https://experienceleague.adobe.com/aflHPozCwJ-6fB7X-2jLaBvs42Ohz6OzwZ7AvkahCE8
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: bcc5edb5-84c3-4940-9f84-ed88b6c16274
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 209
ht-degree: 10%

---

# 获取属性(.NET)

## 描述

`GetAttributes()`用于从[!DNL Target]获取试验性和个性化体验并提取属性值。

## 方法

### getAttributes

```dotnet {line-numbers="true"}
TargetAttributes TargetClient.GetAttributes(TargetDeliveryRequest targetRequest, params string[] mboxes)
```

## 参数

| 名称 | 类型 | 必需 | 默认 | 描述 |
| --- | --- | --- | --- | --- |
| targetRequest | TargetDeliveryRequest | 否 | null | 与[获取选件](get-offers.md)使用的&#x200B;[!DNL Target]请求相同 |
| mboxNames | 参数字符串[] | 否 | null | mbox名称的参数数组 |

## 结果

从`TargetClient.GetAttributes()`返回的`TargetAttributes`对象具有以下属性和方法：

| 属性/方法 | 返回类型 | 描述 |
| --- | --- | --- |
| 响应 | TargetDeliveryResponse | 返回通常由[获取选件](get-offers.md)返回的响应对象 |
| ToDictionary | IReadOnlyDictionary | 返回词典以及按mbox名称分组的键值对 |
| ToMboxDictionary(mboxName) | IReadOnlyDictionary | 为提供的mbox返回一个包含键值对的字典 |
| GetBoolean(mboxName， key， defaultValue) | 布尔 | 返回指定mbox名称和属性键的值 |
| GetString(mboxName， key， defaultValue) | 字符串 | 返回指定mbox名称和属性键的值 |
| GetInteger(mboxName， key， defaultValue) | int | 返回指定mbox名称和属性键的值 |
| GetDouble(mboxName， key， defaultValue) | 双精度 | 返回指定mbox名称和属性键的值 |
| GetValue(mboxName， key， defaultValue) | T | 返回指定mbox名称和属性键的值 |

## 示例

### \.NET

```dotnet {line-numbers="true"}
var targetClientConfig = new TargetClientConfig.Builder("acmeClient", "ABCDEF012345677890ABCDEF0@AdobeOrg")
    .Build();

var targetClient = TargetClient.Create(targetClientConfig);

var mboxRequests = new List<MboxRequest> { new (index: 1, name: "a1-serverside-ab") };

var targetDeliveryRequest = new TargetDeliveryRequest.Builder()
    .Build();

var offerAttributes = targetClient.GetAttributes(targetDeliveryRequest, "demo-engineering-flags");

//returns just the value of searchProviderId from the mbox offer
var searchProviderId = offerAttributes.GetString("demo-engineering-flags", "searchProviderId");

//returns a simple Dictionary representing the mbox offer
var engineeringFlags = offerAttributes.ToMboxDictionary("demo-engineering-flags");

//  the value of engineeringFlags looks like this
//  {
//      "cdnHostname": "cdn.cloud.corp.net",
//      "searchProviderId": 143,
//      "hasLegacyAccess": false
//  }

var assetUrl = $"http://{engineeringFlags["cdnHostname"]}/path/to/asset";
```
