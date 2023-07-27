---
title: 在中使用getAttributes [!DNL Adobe Target] 使用.NET SDK
description: 了解如何使用getAttributes()从获取试验性和个性化体验 [!DNL Target] 和提取属性值。
feature: APIs/SDKs
exl-id: 808da83d-3077-468b-a2ad-e35c25905f7d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 10%

---

# 获取属性(.NET)

## 描述

`GetAttributes()` 用于从获取试验性和个性化体验 [!DNL Target] 和提取属性值。

## 方法

### getAttributes

```dotnet {line-numbers="true"}
TargetAttributes TargetClient.GetAttributes(TargetDeliveryRequest targetRequest, params string[] mboxes)
```

## 参数

| 名称 | 类型 | 必需 | 默认 | 描述 |
| --- | --- | --- | --- | --- |
| targetRequest | TargetDeliveryRequest | 否 | null | 相同 [!DNL Target] 请求用于 [获取优惠&#x200B;](get-offers.md) |
| mboxNames | 参数字符串[] | 否 | null | mbox名称的参数数组 |

## 结果

A `TargetAttributes` 对象返回自 `TargetClient.GetAttributes()` 具有以下属性和方法：

| 属性/方法 | 返回类型 | 描述 |
| --- | --- | --- |
| 响应 | TargetDeliveryResponse | 返回通常由返回的响应对象 [获取优惠](get-offers.md) |
| ToDictionary | IReadOnlyDictionary | 返回词典以及按mbox名称分组的键值对 |
| ToMboxDictionary(mboxName) | IReadOnlyDictionary | 为提供的mbox返回一个包含键值对的字典 |
| GetBoolean(mboxName， key， defaultValue) | bool | 返回指定mbox名称和属性键的值 |
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
