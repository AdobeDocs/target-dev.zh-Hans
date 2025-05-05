---
title: 使用Python SDK向 [!DNL Adobe Target] 发送显示或单击通知
description: 了解如何使用sendNotifications()向 [!DNL Adobe Target] 发送显示通知或单击通知以进行测量和报告。
feature: APIs/SDKs
exl-id: 03827b18-a546-4ec8-8762-391fcb3ac435
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 8%

---

# 发送通知(Python)

## 描述

`send_notifications()`用于向[!DNL Adobe Target]发送显示或单击通知以进行测量和报告。

>[!NOTE]
>
>当具有所需参数的`execute`对象位于请求本身中时，展示次数将自动递增，以用于符合条件的活动。

将自动增加展示次数的SDK方法为：

* `get_offers()`
* `get_attributes()`

在请求中传递`prefetch`对象时，对具有`prefetch`对象中的mbox的活动，展示次数不会自动递增。 `Send_notifications()`必须用于预获取的体验，以增加展示次数和转化次数。

## 方法

### send_notifications

```python {line-numbers="true"}
target_client.send_notifications(options)
```

## 参数

`options`具有以下结构：

| 名称 | 类型 | 必需 | 默认 | 描述 |
| --- | --- | --- | --- | --- |
| request | DeliveryRequest | 是 | 无 | 符合[[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md)请求 |
| target_cookie | str | 否 | 无 | [!DNL Target] Cookie |
| target_location_hint | str | 否 | 无 | [!DNL Target]位置提示 |
| consumer_id | str | 否 | 无 | 在拼接多个调用时，应提供不同的消费者ID |
| customer_ids | 列表[CustomerId] | 否 | 无 | 与VisitorId兼容的格式的客户ID列表 |
| session_id | str | 否 | 无 | 用于链接多个请求 |
| callback | 可调用 | 否 | 无 | 如果异步处理请求，则会在响应就绪时调用回调 |
| err_callback | 可调用 | 否 | 无 | 如果异步处理请求，则在引发异常时会调用错误回调 |

## 返回值

`Returns` `TargetDeliveryResponse`（如果同步调用）（默认），或`AsyncResult`（如果使用回调调用）。 `TargetDeliveryResponse`具有以下结构：

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| 响应 | DeliveryResponse | 符合[[!DNL Target Delivery API]](/help/dev/implement/delivery-api/overview.md)响应 |
| target_cookie | dict | [!DNL Target] Cookie |
| target_location_hint_cookie | dict | [!DNL Target]位置提示Cookie |
| analytics_details | 列表[AnalyticsResponse] | [!DNL Analytics]有效负载，适用于客户端[!DNL Analytics] |
| trace |  | 列表[dict] | 所有请求mbox/视图的汇总跟踪数据 |
| response_tokens | 列表[dict] | [&#x200B;响应令牌](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=zh-Hans)列表 |
| meta | dict | 用于设备上决策的其他决策元数据 |

## 示例

首先，让我们构建[!UICONTROL Target Delivery API]请求以预取`home`和`product1` mbox的内容。

### Python

```python {line-numbers="true"}
mboxes = [MboxRequest(name="home"),
          MboxRequest(name="product1")]
prefetch = PrefetchRequest(mboxes=mboxes)
delivery_request = DeliveryRequest(prefetch=prefetch)

# Next, we fetch the offers via Target Python SDK getOffers() API
response = target_client.get_offers({ "request": delivery_request })
```

成功的响应将包含[!UICONTROL Target Delivery API]响应对象，其中包含所请求mbox的预获取内容。 示例`target_response["response"]`对象（格式为dict）可能如下所示：

### Python

```python {line-numbers="true"}
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

记下每个Target内容选项中的mbox `name`和`state`字段以及`eventToken`字段。 每个内容选项显示后，即应在`send_notifications()`请求中提供这些选项。 假设`product1` mbox已显示在非浏览器设备上。 通知请求将显示如下：

### Python

```python {line-numbers="true"}
notification_mbox = NotificationMbox(name="product1",
                                     state="J+W1Fq18hxliDDJonTPfV0S+mzxapAO3d14M43EsM9f12A6QaqL+E3XKkRFlmq9U")
notification = Notification(
    id="1",
    type=MetricType.DISPLAY,
    timestamp=1621530726000,  # Epoch time in milliseconds
    mbox=notification_mbox,
    tokens=["t0FRvoWosOqHmYL5G18QCZNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="]
)
notification_request = DeliveryRequest(notifications=[notification])
```

请注意，我们已在预获取响应中包含与投放的[!DNL Target]选件相对应的mbox状态和事件令牌。 生成通知请求后，我们可以通过`send_notifications()` API方法将其发送给[!DNL Target]：

### Python

```python {line-numbers="true"}
response = target_client.send_notifications({ "request": notification_request })
```
