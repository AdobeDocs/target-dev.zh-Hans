---
title: 与Experience Cloud A4T报表集成
description: 与Experience Cloud、A4T报表、Analytics for Target的集成
keywords: 投放api，服务器端，服务器端，集成， a4t
exl-id: 0d09d7a1-528d-4e6a-bc6c-f7ccd61f5b75
feature: Implement Server-side
source-git-commit: cbae0f1758fb0dee4837e8c237f8617ecb46eb25
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 6%

---

# [!UICONTROL Analytics for Target] (A4T)报告

[!DNL Adobe Target]支持设备上决策和服务器端[!DNL Target]活动的A4T报告。 启用A4T报表的配置选项有两种：

* [!DNL Adobe Target]自动将分析有效负载转发到[!DNL Adobe Analytics]，或者
* 用户从[!DNL Adobe Target]请求分析有效负载。 （[!DNL Adobe Target]将[!DNL Adobe Analytics]有效负载返回给调用方。）

>[!NOTE]
>
>设备上决策仅支持A4T报表，其中的[!DNL Adobe Target]自动将分析有效负载转发到[!DNL Adobe Analytics]。 不支持从[!DNL Adobe Target]检索分析有效负载。

## 先决条件

1. 在[!DNL Adobe Target] UI中将活动配置为将[!DNL Adobe Analytics]作为报表源，并确保已为A4T启用这些帐户。
1. API用户生成Adobe [!UICONTROL Marketing Cloud Visitor ID]并确保此ID在执行[!DNL Target]请求时可用。

## [!DNL Adobe Target]自动转发[!DNL Analytics]有效负载

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

用户可以检索给定mbox的[!DNL Adobe Analytics]有效负荷，然后通过[!DNL Adobe Analytics]数据插入API[将其发送给](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md)。 触发[!DNL Adobe Target]请求时，将`client_side`传递到请求中的`logging`字段。 如果指定的mbox存在于使用[!DNL Analytics]作为报表源的活动中，则此请求将返回有效负载。

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

如果来自[!DNL Target]的响应在`analytics -> payload`属性中包含任何内容，请将其转发给[!DNL Adobe Analytics]。 [!DNL Adobe Analytics]知道如何处理此有效负载。 这可以在GET请求中完成，使用以下格式：

```
https://{datacollectionhost.sc.omtrdc.net}/b/ss/{rsid}/{content_type_num}/{code_ver}/{session}?pe=tnt&tnta={payload}&c.&a.&target.&sessionId={sessionId}&.target&.a&.c&mid={mid}
```

### 查询字符串参数和变量

| 字段名称 | 必需 | 描述 |
| --- | --- | --- |
| `rsid` | 是 | 点击 |
| `content_type_num` | 是 | 始终设置为“0” |
| `code_ver` | 是 | 始终设置为“MOBILE-1.0” |
| `session` | 是 | 始终设置为“0” |
| `pe` | 是 | 页面事件。 始终设置为`tnt` |
| `tnta` | 是 | [!DNL Analytics]中的[!DNL Target]服务器返回了`analytics -> payload -> tnta`有效负载 |
| `sessionId` | 是 | 正在进行会话的[!DNL Target]会话ID |
| `mid` | 是 | Marketing Cloud 访客 ID |

### 必需的标头值

| 标头名称 | 标头值 |
| --- | --- |
| 主机 | Analytics数据收集服务器（如： `adobeags421.sc.omtrdc.net`） |

### 示例A4T数据插入HTTP Get调用

非URL编码版本以提高可读性（格式不用于API调用）：

```
https://demo.sc.omtrdc.net/b/ss/myCustomRsid/0/MOBILE-1.0/0?tnta=253236:0:0|0,253236:0:0|2,253236:0:0|1,253613:0:0|0,253613:0:0|2,253613:0:0|1&c.&a.&target.&sessionId=45c08980-f4b9-4e11-96db-067d58e49f74&.target&.a&.c&pe=tnt&mid=69170113867710665996968872592584719577
```

URL编码版本（用于API调用的格式）：

```
https://demo.sc.omtrdc.net/b/ss/myCustomRsid/0/MOBILE-1.0/0?tnta=253236%3A0%3A0%7C0%2C253236%3A0%3A0%7C2%2C253236%3A0%3A0%7C1%2C253613%3A0%3A0%7C0%2C253613%3A0%3A0%7C2%2C253613%3A0%3A0%7C1&c.%26a.%26target.%26sessionId=45c08980-f4b9-4e11-96db-067d58e49f74%26.target%26.a%26.c&pe=tnt&mid=69170113867710665996968872592584719577 
```
