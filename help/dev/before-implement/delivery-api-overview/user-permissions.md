---
title: Adobe Target Delivery API用户权限
description: Adobe Target Delivery API用户权限
badgePremium: label="Premium" type="Positive" url="https://experienceleague.adobe.com/docs/target/using/introduction/intro.html?lang=zh-Hans#premium newtab=true" tooltip="查看Target Premium中包含的内容。"
keywords: 投放api
exl-id: 332f90bd-4079-4653-aa38-b35837631c94
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# 用户权限(Premium)

[!DNL Adobe]允许客户在使用Adobe Target时管理其用户的权限。 为了成功进行[!UICONTROL Adobe Target Delivery API]调用，必须在API调用中传递具有正确权限的令牌。 要了解有关用户权限以及如何检索令牌的更多信息，请访问[本文档](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html?lang=zh-Hans)。

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

一旦您拥有了相应的令牌，请将其传递给每个API调用的`property` -> `token`。 如果未在每个API调用中传递`property` -> `token`，则您将无法从Adobe Target中获取任何`content`。

```
{
    "status": 200,
    "requestId": "07ce783d-58b9-461c-9f4c-6873aeb00c01",
    "client": "demo",
    "id": {
        "tntId": "d359234570e04f14e1faeeba02d6ab9914e.28_7"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    "execute": {
        "mboxes": [
            {
                "index": 1,
                "name": "homepage"
            }
        ]
    }
}
```

如上所示，如果不传递`property` -> `token`，您将无法获取任何内容。 如果您需要从API调用中获取内容，但未从响应中检索任何内容，则很可能是因为未提供`property` -> `token`，或者传递时没有正确的权限。
