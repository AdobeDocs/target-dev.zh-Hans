---
title: Adobe Target投放API通知
description: 如何使用触发通知 [!UICONTROL Adobe Target交付API]？
keywords: 投放api
exl-id: 711388fd-2c1f-4ca4-939f-c56dc4bdc04a
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# 通知

在面向最终用户访问或呈现预取的mbox或视图时，应触发通知。

为了针对正确的mbox或视图触发通知，请确保跟踪相应的 `eventToken` 每个mbox或视图的位置。 使用正确内容的通知 `eventToken` 要正确反映报表，需要触发相应的mbox或视图。

## 预取Mbox的通知

可以通过单个投放调用发送一个或多个通知。 确定需要跟踪的量度是否为 `click` 或 `display` ，以便 `type` 可以正确反映通知。 此外，传入 `id` ，以便可以确定通知是否通过[!UICONTROL  Adobe Target交付API]. 此 `timestamp` 转发到也很重要 [!DNL Target] 以指示何时 `click` 或 `display` 针对给定mbox发生的事件，以便进行报告。

```
curl -X POST \
'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=10abf6304b2714215b1fd39a870f01afc#1555632114' \
-H 'Content-Type: application/json' \
-H 'cache-control: no-cache' \
-d '{
    "id": {
      "tntId": "abcdefghijkl00023.1_1"
    },
    "context": {
      "channel": "web",
      "browser" : {
        "host" : "demo"
      },
      "address" : {
        "url" : "http://demo.dev.tt-demo.com/demo/store/index.html"
      },
      "screen" : {
        "width" : 1200,
        "height": 1400
      }
    },
      "notifications": [
      {
      "id" : "SummerOfferNotification",
        "timestamp" : 1555705311051,
        "type" : "display",
        "mbox" : {
          "name" :"SummerOffer"   
        },
        "tokens" : [
          "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q"
        ]
      },
    {
      "id" : "SummerShoesOfferNotification",
        "timestamp" : 1555705311051,
        "type" : "display",
        "mbox" : {
          "name" :"SummerShoesOffer"   
        },
        "tokens" : [
          "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q"
        ]
      },
    {
      "id" : "SummerDressOfferNotification",
        "timestamp" : 1555705311051,
        "type" : "display",
        "mbox" : {
          "name" :"SummerDressOffer"   
        },
        "tokens" : [
          "GcvBXDhdJFNR9E9r1tgjfmqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q"
        ]
    } 
    ]
  }'
```

上述示例调用将导致一个响应，指示 `notifications` 已成功处理请求。

```
{
  "status": 200,
  "requestId": "36014eed-4772-4c48-a9e2-e532762b6a85",
  "client": "demo",
  "id": {
      "tntId": "abcdefghijkl00023.28_20"
  },
  "edgeHost": "mboxedge28.tt.omtrdc.net",
  "notifications": [
      {
          "id": "SummerOfferNotification"
      },
      {
          "id": "SummerDressOfferNotification"
      },
      {
          "id": "SummerShoesOfferNotification"
      }
  ]
}
```

如果所有 `notifications` 发送至 [!DNL Target] 正确处理之后，它们将显示在 `notifications` 数组。 但是，如果 `notifications` `id` 缺失了，那个特殊的 `notification` 没有通过。 在这种情况下，重试逻辑可以一直实施，直到成功为止 `notification` 已检索响应。 请确保为重试逻辑指定了超时，以便API调用不会阻塞并导致性能延迟。

## 预获取视图的通知

可以通过单个投放调用发送一个或多个通知。 确定需要跟踪的量度是否为 `click` 或 `display` ，以便能够正确反映通知的类型。 此外，传入 `id` ，以便可以确定通知是否通过 [!UICONTROL Adobe Target交付API]. 时间戳转发到也很重要 [!DNL Target] 以指示何时 `click` 或 `display` 发生于给定视图以用于报表目的。

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359570e04f14e1faeeba02d6ab9914e' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
  "id": {
    "tntId": "84e8d0e211054f18af365d65f45e902b.28_131"
  },
  "context": {
    "channel": "web",
    "browser": {
      "host": "target.enablementadobe.com"
    },
    "address": {
      "url": "https://target.enablementadobe.com/react/demo/#/"
    }
  },
  "notifications": [{
      "id": "228",
      "type": "display",
      "timestamp": 1556226121884,
      "tokens": ["N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="],
      "view": {
        "name": "checkout-express",
      }
    },
    {
      "id": "5",
      "type": "display",
      "timestamp": 1556226121884,
      "tokens": ["N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="],
      "view": {
        "name": "home",
      }
    },
    {
      "id": "6",
      "type": "display",
      "timestamp": 1556226121884,
      "tokens": ["N3C13I0M2PH8iaKtONJlFJNWHtnQtQrJfmRrQugEa2qCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="],
      "view": {
        "name": "products",
      }
    }
  ]
}'
```

上述示例调用将导致一个响应，指示 `notifications` 已成功处理请求。

```
{
    "status": 200,
    "requestId": "85cc7394-c19a-4398-9b8b-bbee1e4c4579",
    "client": "demo",
    "id": {
        "tntId": "84e8d0e211054f18af365d65f45e902b.28_131"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "notifications": [
        {
            "id": "5"
        },
        {
            "id": "6"
        },
        {
            "id": "228"
        }
    ]
}
```

如果所有 `notifications` 发送至  [!DNL Target] 正确处理之后，它们将显示在 `notifications` 数组。 但是，如果 `notifications` `id` 缺失，该特定通知未通过。 在这种情况下，可以实施重试逻辑，直到检索到成功的通知响应。 请确保为重试逻辑指定了超时，以便API调用不会阻塞并导致性能延迟。
