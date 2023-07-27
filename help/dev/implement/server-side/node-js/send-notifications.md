---
title: 将显示通知或单击通知发送到 [!DNL Adobe Target] 使用Node.js SDK
description: 了解如何使用sendNotifications()将显示通知或单击通知发送至 [!DNL Adobe Target] 用于衡量和报告。
feature: APIs/SDKs
exl-id: 84bb6a28-423c-457f-8772-8e3f70e06a6c
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 4%

---

# 发送通知(Node.js)

## 描述

`[!UICONTROL sendNotifications()]` 用于将显示通知或单击通知发送至 [!DNL Adobe Target] 用于衡量和报告。

>[!NOTE]
>
>当 `execute` 具有所需参数的对象位于请求本身中，展示次数将自动递增以用于符合条件的活动。

将自动增加展示次数的SDK方法为：

* `getOffers()`
* `getAttributes()`

当 `prefetch` 对象在请求中传递，则对于具有mbox的活动，展示次数不会自动递增 `prefetch` 对象。 `sendNotifications()` 必须用于预获取的体验，以增加展示次数和转化次数。

## 方法

### 创建

```js {line-numbers="true"}
TargetClient.sendNotifications(options: Object): Promise
```

### 参数

`options` 具有以下结构：

| 名称 | 类型 | 必需 | 默认 |
| --- | --- | --- | --- |
| request | 对象 | 是 | 无 |

## 示例

首先，我们构建Target D用于预取内容的投放API请求 `home` 和 `product1` mbox。

### Node.js

```js {line-numbers="true"}
const prefetchMboxesRequest = {
  prefetch: {
    mboxes: [
      { name: "home" },
      { name: "product1" }
    ]
  }
};
// Next, we fetch the offers via Target Node.js SDK getOffers() API
const targetResponse = await targetClient.getOffers({ request: prefetchMboxesRequest });
```

成功的响应将包含 [!UICONTROL Target投放API] 响应对象，其中包含所请求mbox的预获取内容。 示例 `targetResponse.response` 对象可能如下所示：

### Node.js

```js {line-numbers="true"}
{
  "status": 200,
  "requestId": "e8ac2dbf5f7d4a9f9280f6071f24a01e",
  "id": {
    "tntId": "08210e2d751a44779b8313e2d2692b96.21_27"
  },
  "client": "adobetargetmobile",
  "edgeHost": "mboxedge21.tt.omtrdc.net",
  "prefetch": {
    "mboxes": [
      {
        "index": 0,
        "name": "home",
        "options": [
          {
            "type": "html",
            "content": "HOME OFFER",
            "eventToken": "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
            "responseTokens": {
              "profile.memberlevel": "0",
              "geo.city": "dublin",
              "activity.id": "302740",
              "experience.name": "Experience B",
              "geo.country": "ireland"
            }
          }
        ],
        "state": "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"
      },
      {
        "index": 1,
        "name": "product1",
        "options": [
          {
            "type": "html",
            "content": "TEST OFFER 1",
            "eventToken": "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
            "responseTokens": {
              "profile.memberlevel": "0",
              "geo.city": "dublin",
              "activity.id": "302740",
              "experience.name": "Experience B",
              "geo.country": "ireland"
            }
          }
        ],
        "state": "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"
      }
    ]
  }
}
```

记下mbox `name` 和 `state` 字段以及 `eventToken` 字段，位于 [!DNL Target] 内容选项。 这些文件应在 `sendNotifications()` 请求，以便在显示每个内容选项后立即发送。 假设 `product1` mbox已在非浏览器设备上显示。 通知请求将显示如下：

### Node.js

```js {line-numbers="true"}
const mboxNotificationRequest = {
  notifications: [{
    id: "1",
    timestamp: Date.now(),
    type: "display",
    mbox: {
      name: "product1",
      state: "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"
    },
    tokens: [ "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==" ]
  }]
};
```

请注意，我们已经包括了与 [!DNL Target] 在预获取响应中投放的选件。 构建通知请求后，我们可以将其发送至 [!DNL Target] 通过 `sendNotifications()` API方法：

### Node.js

```js {line-numbers="true"}
const notificationResponse = await targetClient.sendNotifications({ request: mboxNotificationRequest });
```
