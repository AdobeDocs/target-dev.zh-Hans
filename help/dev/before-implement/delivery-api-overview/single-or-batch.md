---
title: Adobe Target交付API单次或批量交付
description: 如何使用 [!UICONTROL Adobe Target交付API] 是单次还是批量交付调用？
keywords: 投放api
exl-id: 525cd1f2-616a-486c-8f49-8117615500bb
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 0%

---

# 单次或批量交付

此 [!UICONTROL Adobe Target交付API] 支持单个或批量投放调用。 可以为单个或多个mbox发出内容服务器请求。

在决定进行单次呼叫与批量呼叫时权衡性能成本。 如果您知道需要为用户显示的所有内容，则最佳实践是通过单个批量投放调用检索所有mbox的内容，以避免发出多个单个投放调用。

## 单个投放调用

您可以通过以下方式检索要向用户显示的一种mbox体验 [!UICONTROL Adobe Target交付API]. 请注意，如果您进行单个交付调用，则需要启动另一个服务器调用，以便为用户的mbox检索其他内容。 随着时间的推移，这可能变得非常昂贵，因此，请确保在使用单个交付API调用时评估您的方法。

```
curl -X POST \
'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=7abf6304b2714215b1fd39a870f01afc#1555632114' \
-H 'Content-Type: application/json' \
-H 'cache-control: no-cache' \
-d '
{
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
    "execute": {
    "mboxes" : [
      {
        "name" : "SummerOffer",
        "index" : 1
      }
    ]
  }
}'
```

在上述单个投放调用示例中，通过检索体验来向用户显示 `tntId`： `abcdefghijkl00023.1_1` 对于 `mbox`：`SummerOffer` 在Web渠道上。 此单个投放调用将生成以下响应：

```
{
  "status": 200,
  "requestId": "25e0cc42-3d7b-456a-8b49-af60c1fb23d9",
  "client": "demo",
  "id": {
      "tntId": "abcdefghijkl00023.1_1"
  },
  "edgeHost": "mboxedge28.tt.omtrdc.net",
  "execute": {
      "mboxes": [
          {
              "index": 1,
              "name": "SummerOffer",
              "options": [
                  {
                      "content": "<p><b>Enjoy this 15% discount on your next purchase</b></p>",
                      "type": "html",
                  }
              ]
          }
      ]
    }
}
```

在响应中，请注意 `content` 字段包含的HTML描述了要向用户显示的与SummerOffer mbox对应的Web体验。

### 执行页面加载

如果在Web渠道中进行页面加载时应该显示一些体验（例如AB测试页脚或页眉中的字体），则可以指定 `pageLoad` 在 `execute` 字段以检索应应用的所有修改。

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
    "window": {
      "width": 1819,
      "height": 842
    },
    "browser": {
      "host": "target.enablementadobe.com"
    },
    "address": {
      "url": "https://target.enablementadobe.com/react/demo/#/"
    }
  },
  "execute": {
    "pageLoad": {}
  }
}'
```

上述示例调用会检索任何体验，以在页面时向用户显示 `https://target.enablementadobe.com/react/demo/#/` 加载。

```
{
      "status": 200,
      "requestId": "355ebc47-edb6-481f-aeae-ae55d71afaca",
      "client": "demo",
      "id": {
          "tntId": "84e8d0e211054f18af365d65f45e902b.28_131"
      },
      "edgeHost": "mboxedge28.tt.omtrdc.net",
      "execute": {
          "pageLoad": {
              "options": [
                  {
                      "content": [
                          {
                              "type": "setHtml",
                              "selector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(1) > NAV.nav:eq(0) > DIV.container:eq(0) > DIV.nav-right:eq(0) > A.nav-item:eq(0)",
                              "cssSelector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(1) > NAV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(2) > A:nth-of-type(1)",
                              "content": "Modified Home"
                          }
                      ],
                      "type": "actions"
                  }
              ],
              "metrics": [
                  {
                      "type": "click",
                      "selector": "#app > DIV:nth-of-type(1) > DIV:nth-of-type(2) > SECTION.section:eq(0) > DIV.container:eq(0) > FORM.col-md-4:eq(0) > DIV.form-group:eq(0) > BUTTON.btn:eq(0)",
                      "eventToken": "QPaLjCeI9qKCBUylkRQKBg=="
                  }
              ]
          }
      }
  }
```

在 `content` 字段，则可以检索需要对页面加载应用的修改。 在上面的示例中，请注意，需要命名标头上的链接 *修改的主页*.

## 已分批投放调用

与通过每个调用中的单个mbox进行多次投放调用不同，通过批量mbox进行一次投放调用可减少不必要的服务器调用。 调用服务器调用应尽可能最小化，以便获得高性能。

```
curl -X POST \
'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=7abf6304b2714215b1fd39a870f01afc#1555632114' \
-H 'Content-Type: application/json' \
-H 'cache-control: no-cache' \
-d '
{
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
    "execute": {
    "mboxes" : [
      {
        "name" : "SummerOffer",
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

在上面的批量投放调用示例中，将检索体验，以便为用户显示 `tntId`： `abcdefghijkl00023.1_1` 表示多个 `mbox`：`SummerOffer`， `SummerShoesOffer`、和 `SummerDressOffer`. 由于我们知道需要为此用户显示多个mbox的体验，因此我们可以批量处理这些请求，并进行一次服务器调用，而不是三次单独的投放调用。

```
{
  "status": 200,
  "requestId": "fe15286f-effb-434f-85d8-c3db804075ce",
  "client": "demo",
  "id": {
      "tntId": "abcdefghijkl00023.28_120"
  },
  "edgeHost": "mboxedge28.tt.omtrdc.net",
  "execute": {
      "mboxes": [
          {
              "index": 1,
              "name": "SummerOffer",
              "options": [
                  {
                      "content": "<p><b>Enjoy this 15% discount on your next purchase</b></p>",
                      "type": "html",

                  }
              ]
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

在上面的响应中，您可以看到在 `content` 字段中，可以检索要向每个mbox的HTML显示的体验呈现形式。
