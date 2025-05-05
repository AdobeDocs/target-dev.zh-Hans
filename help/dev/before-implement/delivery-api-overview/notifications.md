---
title: Adobe Target投放API通知
description: 如何使用[!UICONTROL Adobe Target Delivery API]触发通知？
keywords: 投放api
exl-id: 711388fd-2c1f-4ca4-939f-c56dc4bdc04a
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# 通知

在面向最终用户访问或呈现预取的mbox或视图时，应触发通知。

为了针对正确的mbox或视图触发通知，请确保跟踪每个mbox或视图的对应`eventToken`。 必须触发对应mbox或视图具有正确`eventToken`的通知，才能正确反映报表。

## 预取Mbox的通知

可以通过单个投放调用发送一个或多个通知。 确定需要跟踪的量度是每个mbox的`click`还是`display`，以便能够正确反映通知的`type`。 此外，请为每个通知传入`id`，以便可以确定是否通过[!UICONTROL &#x200B; Adobe Target Delivery API]正确发送了通知。 `timestamp`转发到[!DNL Target]也很重要，以指示给定mbox何时发生`click`或`display`以用于报告。

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

上述示例调用将导致一个响应，指示已成功处理`notifications`请求。

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

如果发送到[!DNL Target]的所有`notifications`都得到了正确处理，它们将显示在响应的`notifications`数组中。 但是，如果缺少`notifications` `id`，则该特定`notification`未通过。 在这种情况下，在检索到`notification`响应之前，可以设置重试逻辑。 请确保为重试逻辑指定了超时，以便API调用不会阻塞并导致性能延迟。

## 预获取视图的通知

可以通过单个投放调用发送一个或多个通知。 确定需要跟踪的指标是每个mbox的`click`还是`display`，以便正确反映通知的类型。 此外，请为每个通知传入`id`，以便可以确定是否通过[!UICONTROL Adobe Target Delivery API]正确发送了通知。 时间戳也很重要以转发到[!DNL Target]，以指示针对给定视图何时发生`click`或`display`以用于报告。

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

上述示例调用将导致一个响应，指示已成功处理`notifications`请求。

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

如果发送到[!DNL Target]的所有`notifications`都得到了正确处理，它们将显示在响应的`notifications`数组中。 但是，如果缺少`notifications` `id`，则该特定通知未通过。 在这种情况下，可以实施重试逻辑，直到检索到成功的通知响应。 请确保为重试逻辑指定了超时，以便API调用不会阻塞并导致性能延迟。
