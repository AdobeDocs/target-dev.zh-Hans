---
title: 识别访客的Adobe Target交付API
description: 如何在中识别用户 [!DNL Adobe Target]？
keywords: 投放api
exl-id: 5b8c28aa-caad-44a9-880a-3c5f844e47b2
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 9%

---

# 识别访客

可以通过多种方式在中识别访客 [!DNL Adobe Target].

Target使用三个标识符：

| 字段名称 | 描述 |
| --- | --- |
| `tntId` | 此 `tntId` 是中的主要标识符 [!DNL Target] 对于用户。 您可以提供此ID或 [!DNL Target] 如果请求中不包含密码，则将自动生成密码。 |
| `thirdPartyId` | 此 `thirdPartyId` 是您公司的标识符，表示您可以在每次调用时发送该标识符。 当用户登录到某个公司的网站时，该公司通常会创建一个ID，并将其绑定到访客的帐户、会员卡、会员编号或该公司的其他适用标识符。 |
| `marketingCloudVisitorId` | 此 `marketingCloudVisitorId` 用于在不同的Adobe解决方案之间合并和共享数据。 此 `marketingCloudVisitorId` 要与Adobe Analytics和Adobe Audience Manager集成，需要使用。 |
| `customerIds` | 除了Experience Cloud访客ID之外， [客户ID](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) 并且可以利用每个访客的身份验证状态。 |

## [!DNL Target] ID

此 [!DNL Target] ID或 `tntId` 可视为设备ID。 此 `tntId` 自动生成者 [!DNL Target] 请求中未提供。 此后，后续请求需要包含此项 `tntId` 以便向用户使用的设备交付正确的内容。

```http {line-numbers="true"}
curl -X POST \
'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=10abf6304b2714215b1fd39a870f01afc#1555632114' \
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

上面的示例调用表明 `tntId` 无需传入。 在此方案中， [!DNL Target]  生成 `tntId` 并在响应中提供，如下所示：

```URI {line-numbers="true"}
{
  "status": 200,
  "requestId": "5b586f83-890c-46ae-93a2-610b1caa43ef",
  "client": "demo",
  "id": {
      "tntId": "10abf6304b2714215b1fd39a870f01afc.28_20"
  },
  "edgeHost": "mboxedge28.tt.omtrdc.net",
  ...
}
```

生成的 `tntId` 是 `10abf6304b2714215b1fd39a870f01afc.28_20`. 请注意此 `tntId` 需要在调用 [!UICONTROL Adobe Target交付API] 对于同一用户，跨会话。

## Marketing Cloud 访客 ID

此 `marketingCloudVisitorId` 是一个通用的永久性ID，用于在Experience Cloud的所有解决方案中标识您的访客。 当您的组织实施ID服务时，此ID允许您在不同的Experience Cloud解决方案(如Adobe Target、Adobe Analytics或Adobe Audience Manager)中识别同一网站访客及其数据。 请注意 `marketingCloudVisitorId` 当利用并与Analytics和Audience Manager集成时，需要使用。

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=10abf6304b2714215b1fd39a870f01afc#1555632114' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
  "id": {
    "marketingCloudVisitorId": "10527837386392355901041112038610706884"
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

上述示例调用演示了如何 `marketingCloudVisitorId` 从Experience CloudID服务检索到的内容将传递到Adobe Target。 在此方案中， [!DNL Target] 生成 `tntId` 因为它未传递到原始调用，而原始调用将映射到提供的 `marketingCloudVisitorId` 如下面的响应所示。

## 第三方ID

如果您的组织使用ID来识别访客，则可以使用 `thirdPartyID` 以投放内容。 但是，您必须提供 `thirdPartyID` 每隔 [!UICONTROL Adobe Target交付API] 打电话给你。

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=10abf6304b2714215b1fd39a870f01afc#1555632114' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
  "id": {
    "thirdPartyId": "B234A029348"
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

上面的示例调用显示了 `thirdPartyId`，这是一个永久ID，您的企业可以利用此ID来识别最终用户，无论他们通过Web、移动还是物联网渠道与您的企业进行交互。 换句话说， `thirdPartyId` 将引用可以跨渠道使用的用户配置文件数据。 在此方案中， [!DNL Target] 生成 `tntId`，因为它未传递到原始调用，而原始调用将映射到提供的 `thirdPartyId` 如下面的响应所示。

```
{
    "status": 200,
    "requestId": "55de9886-bd14-4dee-819c-7d1633b79b90",
    "client": "demo",
    "id": {
        "tntId": "10abf6304b2714215b1fd39a870f01afc.28_20",
        "thirdPartyId": "B234A029348"
    },
    "edgeHost": "mboxedge28.tt.omtrdc.net",
    ...
}
```

## Customer ID

[客户ID](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) 可添加并与Experience Cloud访客ID关联。 无论何时发送 `customerIds` 该 `marketingCloudVisitorId` 还必须提供。 此外，认证状态可以与每个认证状态一起提供 `customerId` 每个访客的开销。 可考虑以下身份验证状态：

| 身份验证状态 | 用户状态 |
| --- | --- |
| `unknown` | 未知或从未验证。此状态可用于诸如访客通过单击显示广告登录到您的网站等场景。 |
| `authenticated` | 用户目前通过了您网站或应用程序上活动会话的身份验证。 |
| `logged_out` | 用户已经过身份验证，但已主动注销。用户想要并打算与已经过身份验证状态断开连接。用户不想再被当为已经过身份验证处理。 |

请注意，仅当客户ID为 `authenticated` state将Target引用存储和链接到客户ID的用户配置文件数据。 如果客户ID位于 `unknown` 或 `logged_out` ，则客户id将被忽略，并且任何可能与其关联的用户配置文件数据都不会用于受众定位。

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359234570e044f14e1faeeba02d6ab23439914e' \
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
        "marketingCloudVisitorId" : "2304820394812039",
        "customerIds": [{
          "id": "134325423",
          "integrationCode" : "crm_data",
          "authenticatedState" : "authenticated"
        }]
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

上面的示例调用演示了如何发送 `customerId` 带有 `authenticatedState`. 发送时 `customerId`， `integrationCode`， `id`、和 `authenticatedState` 以及 `marketingCloudVisitorId` 是必需的。 此 `integrationCode` 的别名 [客户属性文件](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/working-with-customer-attributes.html?lang=zh-Hans) 你通过CRS提供的。

## 合并的配置文件

您可以合并 `tntId`， `thirdPartyID`、和 `marketingCloudVisitorId` 在同一请求中。 在此方案中，Adobe Target将维护所有这些ID的映射，并将其固定到访客中。 了解用户档案如何 [实时合并和同步](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html) 使用不同的标识符。

```
curl -X POST \
  'https://demo.tt.omtrdc.net/rest/v1/delivery?client=demo&sessionId=d359234570e044f14e1faeeba02d6ab23439914e' \
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
        "marketingCloudVisitorId" : "2304820394812039",
        "tntId": "d359234570e044f14e1faeeba02d6ab23439914e.28_78",
        "thirdPartyId":"23423432"
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

上面的示例调用演示了如何将 `tntId`， `thirdPartyID`、和 `marketingCloudVisitorId` 在同一请求中。 响应中还会返回所有三个ID。
