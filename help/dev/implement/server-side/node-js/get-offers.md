---
title: 使用Node.js SDK时，在 [!DNL Adobe Target] 中使用[!UICONTROL getOffers()]
description: 了解如何使用[!UICONTROL getOffers()]执行决策并从 [!DNL Adobe Target]检索体验。
feature: APIs/SDKs
exl-id: 3c4125ea-68d4-405e-9b9a-5fa832743153
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 21%

---

# [!UICONTROL Get Offers] (Node.js)

## 描述

`[!UICONTROL getOffers()]`用于执行决策并从[!DNL Adobe Target]检索体验。


## 方法

### getOffers

```js {line-numbers="true"}
TargetClient.getOffers(options: Object): Promise
```

## 参数

`options`对象具有以下结构：

| 名称 | 类型 | 必需 | 默认 | 描述 |
| --- |--- | --- | --- | --- |
| 请求 | 对象 | 是 | 无 | 符合[[!DNL Target] 交付API](/help/dev/implement/delivery-api/overview.md)请求 |
| visitorCookie | 字符串 | 否 | 无 | ECID (VisitorId) Cookie |
| targetCookie | 字符串 | 否 | 无 | [!DNL Target] Cookie |
| targetLocationHint | 字符串 | 否 | 无 | [!DNL Target]位置提示 |
| consumerId | 字串符 | 否 | 无 | [!UICONTROL Analytics for Target] (A4T)拼接的consumerId |
| CustomerIds | 数组 | 否 | 无 | 采用与VisitorId兼容格式的客户ID |
| sessionId | 字符串 | 否 | 无 | 用于链接多个[!DNL Target]请求 |
| visitor | 对象 | 否 | 新VisitorId | 提供外部VisitorId实例 |

## Promise

返回的`Promise`具有以下结构：

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| request | 对象 | [[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md)请求 |
| 响应 | 对象 | [[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md)个回应 |
| visitorState | 对象 | 应传递给访客API `getInstance()`的对象 |
| targetCookie | 对象 | [!DNL Target] Cookie |
| targetLocationHintCookie | 对象 | [!DNL Target]位置提示Cookie |
| analyticsDetails | 数组 | 在使用客户端Analytics的情况下，使用Analytics有效负载 |
| responseTokens | 数组 | [响应令牌](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=zh-Hans&)的列表。 |
| trace | 数组 | 所有请求mbox/视图的汇总跟踪数据 |
| status | 对象 | 包含响应状态的对象。 |
| 决策方法 | 字符串 | 确定要使用的决策方法（[设备上](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md)，服务器端，混合） |

用于将数据传递回浏览器的`targetCookie`和`targetLocationHintCookie`对象具有以下结构：

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| name | 字符串 | Cookie 名称 |
| value | “任一” | Cookie值，则将被转换为字符串 |
| maxAge | 数值 | 为方便设置`maxAge`选项相对于当前时间（以秒为单位）的过期时间 |

用于指示目标响应状态的`status`对象具有以下结构：

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| status | 数值 | HTTP状态代码 |
| message | 字符串 | 有关响应的消息。 例如，它可以指示响应是决定[在设备上](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md)还是服务器端 |
| remoteMbox | 数组 | 当决策方法为`on-device`时，会提供一个无法完全在设备上决策的mbox名称数组。 换句话说，需要[[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md)请求。 |

## 示例

### Node.js

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

const request = {
    context: {channel: "web"},
    execute: {
        mboxes: [{
            name: "a1-serverside-ab",
            index: 1
        }]
}};

const response = await targetClient.getOffers({ request });
```
