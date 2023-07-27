---
title: 将显示通知或单击通知发送到 [!DNL Adobe Target] 使用.NET SDK
description: 了解如何使用sendNotifications()将显示通知或单击通知发送至 [!DNL Adobe Target] 用于衡量和报告。
feature: APIs/SDKs
exl-id: 724e787c-af53-4152-8b20-136f7b5452e1
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 1%

---

# 发送通知(.NET)

## 描述

`SendNotifications()` 用于将显示通知或单击通知发送至 [!DNL Adobe Target] 用于衡量和报告。

>[!NOTE]
>
>当 `Execute` 具有所需参数的对象位于请求本身中，展示次数将自动递增以用于符合条件的活动。

将自动增加展示次数的SDK方法为：

* `GetOffers()`
* `GetAttributes()`

当 `Prefetch` 对象在请求中传递，则对于具有mbox的活动，展示次数不会自动递增 `Prefetch` 对象。 `SendNotifications()` 必须用于预获取的体验，以增加展示次数和转化次数。

## 方法

### 创建

```dotnet {line-numbers="true"}
TargetDeliveryResponse TargetClient.SendNotifications(TargetDeliveryRequest request)
```

## 示例

首先，让我们构建 [!UICONTROL Target投放API] 请求预取的内容 `home` 和 `product1` mbox。

### \.NET

```dotnet {line-numbers="true"}
var mboxRequests = new List<MboxRequest>
    {
        new (index: 1, name: "home"),
        new (index: 2, name: "product1"),
    };

var targetDeliveryRequest = new TargetDeliveryRequest.Builder()
    .SetPrefetch(new PrefetchRequest(mboxes: mboxRequests))
    .Build();

// Next, we fetch the offers via Target .NET SDK GetOffers() API
var targetResponse = targetClient.GetOffers(targetDeliveryRequest);
```

成功的响应将包含 [!DNL Target Delivery API] 响应对象，其中包含所请求mbox的预获取内容。 示例 `targetResponse.Response` 对象可能如下所示：

### \.NET

```dotnet {line-numbers="true"}
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

请注意 `mbox` 名称和 `state` 字段以及 `eventToken` 字段，位于 [!DNL Target] 内容选项。 这些文件应在 `SendNotifications()` 请求，以便在显示每个内容选项后立即发送。 假设 `product1` mbox已在非浏览器设备上显示。 通知请求将显示如下：

### \.NET

```dotnet {line-numbers="true"}
var mboxNotifications = new List<Notification>
{
    new (id: "1", type: MetricType.Display, timestamp: DateTimeOffset.UtcNow.ToUnixTimeMilliseconds(),
        mbox: new NotificationMbox("product1", "J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U"),
        tokens: new List<string> { "t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==" })
}; 

var mboxNotificationRequest = new TargetDeliveryRequest.Builder()
    .SetNotifications(mboxNotifications)
    .Build();
```

请注意，我们已包含与 [!DNL Target] 在预获取响应中投放的选件。 构建通知请求后，我们可以将其发送至 [!DNL Target] 通过 `SendNotifications()` API方法：

### \.NET

```dotnet {line-numbers="true"}
var notificationResponse = targetClient.SendNotifications(mboxNotificationRequest);
```
