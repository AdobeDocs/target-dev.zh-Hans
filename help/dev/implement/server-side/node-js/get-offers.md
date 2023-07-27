---
title: 使用 [!UICONTROL getOffers()] 在 [!DNL Adobe Target] 使用Node.js SDK时
description: 了解如何使用 [!UICONTROL getOffers()] 执行决策并从中检索体验 [!DNL Adobe Target].
feature: APIs/SDKs
exl-id: 3c4125ea-68d4-405e-9b9a-5fa832743153
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 21%

---

# [!UICONTROL 获取优惠] (Node.js)

## 描述

`[!UICONTROL getOffers()]` 用于执行决策并从以下位置检索体验 [!DNL Adobe Target].


## 方法

### getOffers

```js {line-numbers="true"}
TargetClient.getOffers(options: Object): Promise
```

## 参数

此 `options` 对象具有以下结构：

| 名称 | 类型 | 必需 | 默认 | 描述 |
| --- |--- | --- | --- | --- |
| 请求 | 对象 | 是 | 无 | 符合 [[!DNL Target] 投放API](/help/dev/implement/delivery-api/overview.md) 请求 |
| visitorCookie | 字符串 | 否 | 无 | ECID (VisitorId) Cookie |
| targetCookie | 字符串 | 否 | 无 | [!DNL Target] Cookie |
| targetLocationHint | 字符串 | 否 | 无 | [!DNL Target] 位置提示 |
| consumerId | 字串符 | 否 | 无 | consumerIds用于 [!UICONTROL 目标分析] (A4T)拼接 |
| CustomerIds | 数组 | 否 | 无 | 采用与VisitorId兼容格式的客户ID |
| sessionId | 字符串 | 否 | 无 | 用于链接多个 [!DNL Target] 请求 |
| visitor | 对象 | 否 | 新VisitorId | 提供外部VisitorId实例 |

## Promise

`Promise` 返回具有以下结构：

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| request | 对象 | [[!UICONTROL Target投放API]](/help/dev/implement/delivery-api/overview.md) 请求 |
| 响应 | 对象 | [[!UICONTROL Target投放API]](/help/dev/implement/delivery-api/overview.md) 响应 |
| visitorState | 对象 | 应传递给访客API的对象 `getInstance()` |
| targetCookie | 对象 | [!DNL Target] Cookie |
| targetLocationHintCookie | 对象 | [!DNL Target] 位置提示Cookie |
| analyticsDetails | 数组 | 在使用客户端Analytics的情况下，使用Analytics有效负载 |
| responseTokens | 数组 | 列表 [响应令牌](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?). |
| trace | 数组 | 所有请求mbox/视图的汇总跟踪数据 |
| status | 对象 | 包含响应状态的对象。 |
| 决策方法 | 字符串 | 确定要使用的决策方法([设备端](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md)，服务器端，混合) |

`targetCookie` 和 `targetLocationHintCookie` 用于将数据传递回浏览器的对象具有以下结构：

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| name | 字符串 | Cookie 名称 |
| value | “任一” | Cookie值，则将被转换为字符串 |
| maxAge | 数值 | 此 `maxAge` 选项可以方便地设置相对于当前时间（以秒为单位）的过期时间 |

此 `status` 用于指示目标响应状态的对象具有以下结构：

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| status | 数值 | HTTP状态代码 |
| message | 字符串 | 有关响应的消息。 例如，它可以指明是否对答复作出了决定 [设备端](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md) 或服务器端 |
| remoteMbox | 数组 | 当决策方法为 `on-device`，则给出了设备上无法完全决定的mbox名称数组。 换句话说， [[!UICONTROL Target投放API]](/help/dev/implement/delivery-api/overview.md) 需要请求。 |

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
