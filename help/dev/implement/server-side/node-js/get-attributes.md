---
title: 如何在中使用异步请求 [!DNL Adobe Target] Node.js SDK
description: 了解如何 [!DNL Target] Node.js SDK支持异步请求，这可以将有效目标时间减少为零。
feature: APIs/SDKs
exl-id: aa06f3ca-7d2a-4334-8092-730a8705dfb0
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 18%

---

# 获取属性(Node.js)

## 描述

`[!UICONTROL getAttributes()]` 用于从获取试验性和个性化体验 [!DNL Target] 和提取属性值。

## 方法

### getAttributes

```js {line-numbers="true"}
TargetClient.getAttributes(mboxNames: Array, options: Object): Promise
```

## 参数

| 名称 | 类型 | 必需 | 默认 |
| --- | --- | --- |--- |
| mboxNames | 数组 | 是 | 无 |
| options | 对象 | 否 | 无 |

## Promise

此 `Promise` 返回者 `TargetClient.getAttributes()` 使用以下方法解析对象：

| 方法 | 返回类型 | 描述 |
| --- | --- | --- |
| getValue(mboxName， key) | “任一” | 返回指定mbox名称和属性键的值 |
| asObject(mboxName) | 对象 | 返回具有键值对的简单json对象 |
| getResponse() | [getOffers响应](https://github.com/jasonwaters/target-nodejs-sdk#targetclientgetoffers) | 返回通常由返回的响应对象 `getOffers` |

## 示例

### Node.js

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);
const offerAttributes = await targetClient.getAttributes(["demo-engineering-flags"]);


//returns just the value of searchProviderId from the mbox offer
const searchProviderId = offerAttributes.getValue("demo-engineering-flags", "searchProviderId");

//returns a simple JSON object representing the mbox offer
const engineeringFlags = offerAttributes.asObject("demo-engineering-flags");

//  the value of engineeringFlags looks like this
//  {
//      "cdnHostname": "cdn.cloud.corp.net",
//      "searchProviderId": 143,
//      "hasLegacyAccess": false
//  }

const assetUrl = `http://${engineeringFlags.cdnHostname}/path/to/asset`;
```
