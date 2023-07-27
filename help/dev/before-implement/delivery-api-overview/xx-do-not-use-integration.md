---
title: 与Experience Cloud集成
description: 与Experience Cloud集成
keywords: 投放api
source-git-commit: f16903556954d2b1854acd429f60fbf6fc2920de
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 7%

---

<!-- The content on this page was originally pulled from the legacy Delivery API doc site, and was subsequently found to be an outdated version of information now found on [Implement > Server-side > Integration > A4T Reporting](../../implement/server-side/sdk-guides/integration-with-experience-cloud/a4t-reporting.md) and [Implement > Server-side > Integration > AAM Segments](../../implement/server-side/sdk-guides/integration-with-experience-cloud/aam-segments.md). Therefore sunsetting this page, but not deleting it from the repo immediately, pending a more thorough examination to avoid inadvertently deleting relevant content. -->


# 与Experience Cloud集成

## Adobe Analytics for Target (A4T)

当从服务器触发Target交付API调用时，Adobe Target会为该用户返回体验，除此之外，Adobe Target会将Adobe Analytics有效负载返回给调用方，或自动将其转发到Adobe Analytics。 要在服务器端将Target活动信息发送到Adobe Analytics，需要满足以下几个先决条件：

1. 在Adobe Target UI中设置活动，将Adobe Analytics作为报表源，并为A4T启用帐户
1. Adobe Marketing Cloud访客ID由API用户生成，并在触发Target交付API调用时可用

### Adobe Target自动转发分析有效负载

如果提供了以下标识符，Adobe Target则可以通过服务器端自动将analytics有效负载转发到Adobe Analytics：

1. `supplementalDataId`  — 用于在Adobe Analytics和Adobe Target之间拼接的ID
1. `trackingServer` - Analytics服务器Adobe，以便Adobe Target和Adobe Analytics能够正确地将数据拼合在一起，这一点相同 `supplementalDataId` 需要传递给Adobe Target和Adobe Analytics。

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359234570e04f14e1faeeba02d6ab9914e' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
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
      "id": {
        "marketingCloudVisitorId": "2304820394812039"
      },
      "property" : {
        "token": "08b62abd-c3e7-dfb2-da93-96b3aa724d81"
      },
      "experienceCloud": {
        "analytics": {
          "supplementalDataId" : "23423498732598234",
          "trackingServer": "ags041.sc.omtrdc.net",
          "logging": "server_side"
        }
      },
        "execute": {
        "mboxes" : [
          {
            "name" : "homepage",
            "index" : 1
          }
        ]
      }
    }'
```

### 从Adobe Target检索Analytics有效负荷

Adobe Target交付API的使用者可以检索相应mbox的Adobe Analytics有效负荷，以便该使用者可以通过以下方式将有效负荷发送到Adobe Analytics [数据插入API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md). 触发服务器端Adobe Target调用时，传递 `client_side` 到 `logging` 字段。 如果将Analytics用作报表源的活动中存在有mbox，则此操作将返回有效负载。

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359234570e04f14e1faeeba02d6ab9914e' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
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
      "property" : {
        "token": "08b62abd-c3e7-dfb2-da93-96b3aa724d81"
      },
      "experienceCloud": {
        "analytics": {
          "logging": "client_side"
        }
      },
        "execute": {
        "mboxes" : [
          {
            "name" : "homepage",
            "index" : 1
          },
          {
            "name" : "SummerShoesOffer",
            "index" : 2       
          },
          {
            "name" : "SummerDressOffer",
            "index" : 3       
          }      
        ]
      }
    }'
```

指定后 `logging` = `client_side`，您将在以下位置收到有效负载： `mbox` 字段，如下所示。

```
{
    "status": 200,
    "requestId": "4b8855a5-8354-4ac4-8ae7-c551f7c0bb8a",
    "client": "demo",
    "id": {
        "tntId": "d359234570e04f14e1faeeba02d6ab9914e.28_7"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "execute": {
        "mboxes": [
            {
                "index": 1,
                "name": "homepage",
                "options": [
                    {
                        "content": "<p><b>Enjoy this 15% discount on your next purchase</b></p>",
                        "type": "html",

                    }
                ],
                "analytics": {
                    "payload": {
                        "pe": "tnt",
                        "tnta": "285408:0:0|2"
                    }
                }
            },
            {
                "index": 2,
                "name": "SummerShoesOffer",
                "options": [
                    {
                        "content": "<p><b>Enjoy this 15% discount on your next shoe purchase</b></p>",
                        "type": "html",
                    }
                ]
            },
            {
                "index": 3,
                "name": "SummerDressOffer",
                "options": [
                    {
                        "content": "<p><b>Enjoy this 15% discount on your next dress purchase</b></p>",
                        "type": "html",
                    }
                ]
            }
        ]
    }
}
```

如果来自Target的响应包含 `analytics` -> `payload` 资产，按原样将其转发到Adobe Analytics。 Analytics知道如何处理此有效负载。 这可以在GET请求中完成，可使用以下格式：

```
https://{datacollectionhost.sc.omtrdc.net}/b/ss/{rsid}/0/CODEVERSION?pe=tnt&tnta={payload}&mid={mid}&vid={vid}&aid={aid}
```

### 查询字符串参数和变量

| 字段名称 | 必需 | 描述 |
| --- | --- | --- |
| `rsid` | 是 | 点击 |
| `pe` | 是 | 页面事件。 始终设置为 `tnt` |
| `tnta` | 是 | Target服务器返回的分析有效负载位于 `analytics` -> `payload` -> `tnta` |
| `mid` | Marketing Cloud 访客 ID |

### 必需的标头值

| 标题名称 | 标头值 |
| --- | --- |
| 主机 | Analytics数据收集服务器(如： adobeags421.sc.omtrdc.net) |

### 示例A4T数据插入HTTP Get调用

```
https://demo.sc.omtrdc.net/b/ss/myCustomRsid/0/MOBILE-1.0?pe=tnt&tnta=285408:0:0|2&mid=2304820394812039
```

## Adobe Audience Manager

Adobe Audience Manager (AAM)区段也可以通过Adobe Target交付API来利用。 为了利用AAM区段，必须提供以下字段：

| 字段名称 | 必需 | 描述 |
| --- | --- | --- |
| `locationHint` | 是 | DCS位置提示用于确定点击哪个AAM DCS端点以检索配置文件。 必须为>= 1。 |
| `marketingCloudVisitorId` | 是 | Marketing Cloud 访客 ID |
| `blob` | 是 | AAM Blob用于将其他数据发送到AAM。 不得为空且大小小于= 1024。 |

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359234570e04f14e1faeeba02d6ab9914e' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
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
      "id": {
        "marketingCloudVisitorId": "2304820394812039"
      },
      "property" : {
        "token": "08b62abd-c3e7-dfb2-da93-96b3aa724d81"
      },
      "experienceCloud": {
        "audienceManager": {
          "locationHint": 9,
          "blob": "32fdghkjh34kj5h43"
        }
      },
        "execute": {
        "mboxes" : [
          {
            "name" : "homepage",
            "index" : 1
          },
          {
            "name" : "SummerShoesOffer",
            "index" : 2       
          },
          {
            "name" : "SummerDressOffer",
            "index" : 3       
          }      
        ]
      }
    }'
```
