---
title: 与Experience CloudA4T报表集成
description: 与Experience Cloud、A4T报表、Analytics for Target集成
keywords: 投放api，服务器端，服务器端，集成， a4t
exl-id: 0d09d7a1-528d-4e6a-bc6c-f7ccd61f5b75
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 7%

---

# Analytics for Target (A4T) 报表

[!DNL Adobe Target]支持设备上决策和服务器端Target活动的A4T报告。 启用A4T报表的配置选项有两种：

* [!DNL Adobe Target]自动将分析有效负载转发到[!DNL Adobe Analytics]，或者
* 用户从[!DNL Adobe Target]请求分析有效负载。 （[!DNL Adobe Target]将[!DNL Adobe Analytics]有效负载返回给调用方。）

>[!NOTE]
>
>设备上决策仅支持A4T报表，其中的[!DNL Adobe Target]自动将分析有效负载转发到[!DNL Adobe Analytics]。 不支持从[!DNL Adobe Target]检索分析有效负载。

## 先决条件

1. 在[!DNL Adobe Target] UI中将活动配置为将[!DNL Adobe Analytics]作为报表源，并确保已为A4T启用这些帐户。
1. API用户会生成Adobe Marketing Cloud访客ID，并确保此ID在执行Target请求时可用。

## [!DNL Adobe Target]自动转发分析有效负载

如果提供了以下标识符，[!DNL Adobe Target]可以自动将分析有效负载转发到[!DNL Adobe Analytics]：

1. `supplementalDataId`：用于在[!DNL Adobe Analytics]和[!DNL Adobe Target]之间拼接的ID。 为了使[!DNL Adobe Target]和[!DNL Adobe Analytics]能够正确拼合数据，需要将`supplementalDataId`传递给[!DNL Adobe Target]和[!DNL Adobe Analytics]。
1. `trackingServer`： [!DNL Adobe Analytics]服务器。

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {     
    id: {
      marketingCloudVisitorId : "2304820394812039",
      tntId: "d359234570e044f14e1faeeba02d6ab23439914e.35_0",
      thirdPartyId:"23423432"
    },
    experienceCloud: {
      analytics: {
        logging: "server_side",
        supplementalDataId: "7D3AA246CC99FD7F-1B3DD2E75595498E",
        trackingServer: "jimsbrims.sc.omtrds.net"
      }
    }, 
    execute: {
      mboxes: [{
        name: "some-mbox"
      }]
    }       
  }
})
.then(console.log)
.catch(console.error);
```

>[!TAB Java]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

VisitorId id = new VisitorId()
  .tntId("d359234570e044f14e1faeeba02d6ab23439914e.35_0")
  .thirdPartyId("B234A029348")
  .marketingCloudVisitorId("10527837386392355901041112038610706884");
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

AnalyticsRequest analyticsRequest =
    new AnalyticsRequest()
        .trackingServer("jimsbrims.sc.omtrds.net")
        .logging(LoggingType.SERVER_SIDE)
        .supplementalDataId("7D3AA246CC99FD7F-1B3DD2E75595498E");
ExperienceCloud expCloud =
    new ExperienceCloud()
        .setAnalytics(analyticsRequest);

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .experienceCloud(expCloud)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

## 用户从[!DNL Adobe Target]中检索分析有效负载

用户可以检索给定mbox的[!DNL Adobe Analytics]有效负荷，然后通过[数据插入API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md)将其发送给[!DNL Adobe Analytics]。 触发[!DNL Adobe Target]请求时，将`client_side`传递到请求中的`logging`字段。 如果在使用Analytics作为报表源的活动中存在指定的mbox，则将返回有效负载。

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};
const targetClient = TargetClient.create(CONFIG);
targetClient.getOffers({
  request: {     
    id: {
      marketingCloudVisitorId : "2304820394812039",
      tntId: "d359234570e044f14e1faeeba02d6ab23439914e.35_0",
      thirdPartyId:"23423432"
    },
    experienceCloud: {
      analytics: {
        logging: "client_side"
      }
    },  
    execute: {
      mboxes: [{
        name: "some-mbox"
      }]
    }       
  }
})
.then(console.log)
.catch(console.error);
```

>[!TAB Java]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

VisitorId id = new VisitorId()
  .tntId("d359234570e044f14e1faeeba02d6ab23439914e.35_0")
  .thirdPartyId("B234A029348")
  .marketingCloudVisitorId("10527837386392355901041112038610706884");
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

AnalyticsRequest analyticsRequest =
    new AnalyticsRequest()
        .logging(LoggingType.CLIENT_SIDE);
ExperienceCloud expCloud =
    new ExperienceCloud()
        .setAnalytics(analyticsRequest);

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .experienceCloud(expCloud)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

指定`logging = client_side`后，您将在mbox字段中接收有效负载。

如果来自Target的响应在`analytics -> payload`属性中包含任何内容，请将其转发到[!DNL Adobe Analytics]。 [!DNL Adobe Analytics]知道如何处理此有效负载。 这可以在GET请求中完成，可使用以下格式：

```
https://{datacollectionhost.sc.omtrdc.net}/b/ss/{rsid}/0/CODEVERSION?pe=tnt&tnta={payload}&mid={mid}&vid={vid}&aid={aid}
```

### 查询字符串参数和变量

| 字段名称 | 必需 | 描述 |
| --- | --- | --- |
| `rsid` | 是 | 点击 |
| `pe` | 是 | 页面事件。 始终设置为`tnt` |
| `tnta` | 是 | Target服务器在`analytics -> payload -> tnta`中返回的分析有效负载 |
| `mid` | 是 | Marketing Cloud 访客 ID |

### 必需的标头值

| 标头名称 | 标头值 |
| --- | --- |
| 主机 | Analytics数据收集服务器（如： `adobeags421.sc.omtrdc.net`） |

### 示例A4T数据插入HTTP Get调用

```
https://demo.sc.omtrdc.net/b/ss/myCustomRsid/0/MOBILE-1.0?pe=tnt&tnta=285408:0:0|2&mid=2304820394812039
```
