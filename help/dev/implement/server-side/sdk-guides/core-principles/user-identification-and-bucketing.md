---
title: 用户标识和分段
description: 用户标识和分段
exl-id: 4fcf235b-6a58-442c-ae13-9d05ec1033fc
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '1130'
ht-degree: 3%

---

# 用户标识和分段

## 用户标识

有多种方法可以识别[!DNL Adobe Target]中的用户。 [!UICONTROL Target]使用以下标识符：

| 字段名称 | 描述 |
| --- | --- |
| `tntID` | `tntId`是用户[!DNL Target]中的主要标识符。 您可以提供此ID，否则[!DNL Target]将在请求中不包含此ID时自动生成此ID。 |
| `thirdPartyId` | `thirdPartyId`是您公司的用户标识符，您可以随每次调用发送该标识符。 当用户登录到某个公司的网站时，该公司通常会创建一个ID，并将其绑定到访客的帐户、会员卡、会员编号或该公司的其他适用标识符。 |
| `marketingCloudVisitorId` | `marketingCloudVisitorId`用于在不同Adobe解决方案之间合并和共享数据。 要与Adobe Analytics和Adobe Audience Manager集成，需要marketingCloudVisitorId。 |
| `customerIds` | 除了Experience Cloud访客ID之外，还可以使用其他[客户ID](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html)以及每个访客的身份验证状态。 |

## [!DNL Target] ID (tntID)

[!DNL Target] ID或`tntId`可视为设备ID。 如果未在请求中提供，此`tntId`将由[!DNL Adobe Target]自动生成。 后续请求需要包含此`tntId`，才能将正确内容交付给同一用户使用的设备。

以下示例调用演示了未将`tntId`传递到[!DNL Target]的情况。

>[!BEGINTABS]

>[!TAB Node.js SDK]

```javascript {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {
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

>[!TAB Java SDK]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

在缺少`tntId`的情况下，[!DNL Adobe Target]将生成`tntId`并在响应中提供它，如下所示。

```json {line-numbers="true"}
{
  "status": 200,
  "requestId": "5b586f83-890c-46ae-93a2-610b1caa43ef",
  "client": "acmeclient",
  "id": {
      "tntId": "10abf6304b2714215b1fd39a870f01afc.35_0"
  },
  "edgeHost": "mboxedge35.tt.omtrdc.net",
  ...
}
```

在此示例中，生成的`tntId`是`10abf6304b2714215b1fd39a870f01afc.35_0`。 请注意，此`tntId`需要跨会话用于同一用户。

## 第三方ID (thirdPartyId)

如果您的组织使用ID来标识访客，则可以使用`thirdPartyID`来传递内容。 `thirdPartyID`是您的企业用来标识最终用户的永久ID，无论最终用户是从Web、移动还是IoT渠道与您的企业进行交互。 换言之，`thirdPartyId`引用了可在各频道间使用的用户配置文件数据。 但是，您必须为发出的每个[!DNL Adobe Target]传递API调用提供`thirdPartyID`。

以下示例调用演示如何使用`thirdPartyId`。

>[!BEGINTABS]

>[!TAB Node.js SDK]

```javascript {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {
    id: {
      thirdPartyId: "B234A029348"
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

>[!TAB Java SDK]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

VisitorId id = new VisitorId()
  .thirdPartyId("B234A029348");
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

在此方案中，[!DNL Adobe Target]将生成`tntId`，因为它未传递到原始调用中，而原始调用将映射到提供的`thirdPartyId`。

## Marketing Cloud访客ID (marketingCloudVisitorId)

`marketingCloudVisitorId`是一个通用的永久性ID，用于在Adobe Experience Cloud的所有解决方案中标识您的访客。 当您的组织实施ID服务时，此ID允许您在不同的Experience Cloud解决方案(包括[!DNL Adobe Target]、Adobe Analytics和Adobe Audience Manager)中识别同一网站访客及其数据。 请注意，将[!DNL Target]与[!DNL Adobe Analytics]和[!DNL Adobe Audience Manager]集成时需要`marketingCloudVisitorId`。

以下示例调用演示了如何将从Experience CloudID服务检索的`marketingCloudVisitorId`传递到[!DNL Target]。

>[!BEGINTABS]

>[!TAB Node.js SDK]

```javascript {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {
    id: {
      marketingCloudVisitorId: "10527837386392355901041112038610706884"
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

>[!TAB Java SDK]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

VisitorId id = new VisitorId()
  .marketingCloudVisitorId("10527837386392355901041112038610706884");
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

在此方案中，[!DNL Target]将生成`tntId`，因为它未传递到原始调用中，而原始调用将映射到提供的`marketingCloudVisitorId`。

## 客户ID (customerIds)

[客户ID](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html)可以添加到Experience Cloud访客ID或与其关联。 无论何时发送`customerIds`，都必须提供`marketingCloudVisitorId`。 此外，可以为每个访客随每个`customerId`提供身份验证状态。 可以使用以下身份验证状态：

| 身份验证状态 | 用户状态 |
| --- | --- |
| `unknown` | 未知或从未验证。 此状态可用于访客通过单击显示广告而登陆您的网站等场景。 |
| `authenticated` | 用户目前通过了您网站或应用程序上活动会话的身份验证。 |
| `logged_out` | 用户已经过身份验证，但已主动注销。用户打算断开与已验证状态的连接。 用户不想再被当为已经过身份验证处理。 |

请注意，只有当`customerId`处于身份验证状态时，[!DNL Target]才引用已存储并链接到customerId的用户配置文件数据。 如果`customerId`处于未知或`logged_out`状态，则将忽略它，并且任何可能与该`customerId`关联的用户配置文件数据都不会用于受众定位。

>[!BEGINTABS]

>[!TAB Node.js SDK]

```javascript {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {
    id: {
      marketingCloudVisitorId : "10527837386392355901041112038610706884",
      customerIds: [{
        id: "134325423",
        integrationCode : "crm_data",
        authenticatedState : "authenticated"
      }]
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

>[!TAB Java SDK]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

CustomerId customerId = new CustomerId()
  .id("134325423")
  .integrationCode("crm_data")
  .authenticatedState(AuthenticatedState.AUTHENTICATED);
VisitorId id = new VisitorId()
  .marketingCloudVisitorId("10527837386392355901041112038610706884")
  .customerIds(Arrays.asList(customerId));
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

以上示例演示了如何使用`authenticatedState`发送`customerId`。 发送`customerId`时，`integrationCode`、`id`、`authenticatedState`以及`marketingCloudVisitorId`是必需的。 `integrationCode`是您通过CRS提供的[客户属性文件](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/working-with-customer-attributes.html?lang=zh-Hans)的别名。

## 合并的配置文件

您可以在同一请求中合并`tntId`、`thirdPartyID`和`marketingCloudVisitorId`。 在此方案中，[!DNL Adobe Target]将维护所有这些ID的映射，并将其固定到访客。 了解如何使用不同的标识符实时[合并和同步配置文件](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html)。

>[!BEGINTABS]

>[!TAB Node.js SDK]

```javascript {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {
    id: {
      tntId: "d359234570e044f14e1faeeba02d6ab23439914e.35_0",
      thirdPartyId: "B234A029348",
      marketingCloudVisitorId : "10527837386392355901041112038610706884"
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

>[!TAB Java SDK]

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

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

以上示例演示了如何在同一个请求中组合`tntId`、`thirdPartyID`和`marketingCloudVisitorId`。

## 分段

系统会根据您设置[!DNL Adobe Target]活动的方式，将您的用户分段以便于查看体验。 在[!DNL Adobe Target]中，分段为：

* **Deterministic**：使用MurmurHash3以确保对用户进行存储段，并且只要用户ID一致，每次都能看到正确的变量。
* **粘性**： [!DNL Adobe Target]存储您的用户在用户配置文件中看到的变体，以确保该用户在会话和渠道中都能始终如一地看到该变体。 使用服务器端决策时，可确保变体和粘性。 使用设备上决策时，无法保证粘性。

## 端到端分段工作流程

在深入研究实际的分段算法之前，请务必强调，类似的步骤既可用于根据其流量分配百分比选择活动，也可用于在活动中选择体验。

### 活动选择步骤

1. 生成设备ID，通常为UUID
1. 获取客户端代码
1. 获取活动ID
1. 获取盐，这通常是一些字符串，如“activity”
1. 使用MurmurHash3计算哈希
1. 获取哈希的绝对值
1. 将散列绝对值除以10000
1. 将余数除以10000，这会生成一个介于0和1之间的值
1. 将结果乘以100%
1. 将活动流量分配百分比与获得的百分比进行比较。 如果流量分配百分比较低，则会选择活动。 否则，将跳过活动。

### 体验选择步骤

1. 生成设备ID，通常为UUID
1. 获取客户端代码
1. 获取活动ID
1. 获取盐，这通常是一个字符串，如“experience”
1. 使用MurmurHash3计算哈希
1. 获取哈希的绝对值
1. 将散列绝对值除以10000
1. 将余数除以10000，这将生成一个介于0和1之间的值
1. 将结果乘以活动中的体验总数
1. 对结果进行四舍五入。 这应该会产生经验指数。

### 示例

假设以下各项：

* 客户端代码为`acmeclient`的客户端C
* 具有ID `1111`和三个体验`E1`、`E2`、`E3`的活动A
* 体验具有以下分布： `E1` - 33%、`E2` - 33%、`E3` - 34%

选择流程如下所示：

1. 设备ID `702ff4d0-83b1-4e2e-a0a6-22cbe460eb15`
1. 客户端代码`acmeclient`
1. 活动ID `1111`
1. 盐`experience`
1. 哈希`acmeclient.1111.702ff4d0-83b1-4e2e-a0a6-22cbe460eb15.experience`的值，哈希值`-919077116`
1. 哈希`919077116`的绝对值
1. 按10000除后的剩余数，`7116`
1. 余数之后的值除以10000， `0.7116`
1. 将值与体验总数`3 * 0.7116 = 2.1348`相乘后的结果
1. 体验索引为`2`，这意味着第三次体验，因为我们正在使用基于`0`的索引。
