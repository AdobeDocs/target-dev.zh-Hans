---
title: 用户标识和分段
description: 用户标识和分段
exl-id: 4fcf235b-6a58-442c-ae13-9d05ec1033fc
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '1143'
ht-degree: 5%

---

# 用户标识和分段

## 用户标识

可以通过多种方式在中识别用户 [!DNL Adobe Target]. [!UICONTROL Target] 使用以下标识符：

| 字段名称 | 描述 |
| --- | --- |
| `tntID` | 此 `tntId` 是中的主要标识符 [!DNL Target] 对于用户。 您可以提供此ID，或者 [!DNL Target] 如果请求中不包含密码，则将自动生成密码。 |
| `thirdPartyId` | 此 `thirdPartyId` 是您公司的用户标识符，您可以在每次调用时发送该标识符。 当用户登录到某个公司的网站时，该公司通常会创建一个ID，并将其绑定到访客的帐户、会员卡、会员编号或该公司的其他适用标识符。 |
| `marketingCloudVisitorId` | 此 `marketingCloudVisitorId` 用于在不同的Adobe解决方案之间合并和共享数据。 要与Adobe Analytics和Adobe Audience Manager集成，需要marketingCloudVisitorId。 |
| `customerIds` | 除了Experience Cloud访客ID之外， [客户ID](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) 还可以利用每个访客的身份验证状态。 |

## [!DNL Target] ID (tntID)

此 [!DNL Target] ID，或 `tntId`，可以视为设备ID。 此 `tntId` 自动生成者 [!DNL Adobe Target] 请求中未提供。 后续请求需要包含此项 `tntId` 以便向同一用户使用的设备交付正确的内容。

以下示例调用演示了 `tntId` 未传递到 [!DNL Target].

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

在没有 `tntId`， [!DNL Adobe Target] 生成 `tntId` 并在回应中提供如下信息。

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

在此示例中，生成的 `tntId` 是 `10abf6304b2714215b1fd39a870f01afc.35_0`. 请注意此 `tntId` 需要跨会话用于同一用户。

## 第三方ID (thirdPartyId)

如果您的组织使用ID来识别访客，则可以使用 `thirdPartyID` 以投放内容。 A `thirdPartyID` 是一个永久性ID，您的企业可以利用该ID来识别最终用户，无论他们通过Web、移动还是物联网渠道与您的企业进行交互。 换句话说， `thirdPartyId` 引用可以跨渠道使用的用户配置文件数据。 但是，您必须提供 `thirdPartyID` 每隔 [!DNL Adobe Target] 您发出的投放API调用。

以下示例调用演示了如何使用 `thirdPartyId`.

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

在此方案中， [!DNL Adobe Target] 将生成 `tntId` 因为它未传递到原始调用，而原始调用将映射到提供的 `thirdPartyId`.

## Marketing Cloud访客ID (marketingCloudVisitorId)

此 `marketingCloudVisitorId` 是一个通用的永久性ID，用于在Adobe Experience Cloud的所有解决方案中标识您的访客。 当您的组织实施ID服务时，此ID允许您在不同的Experience Cloud解决方案中识别同一网站访客及其数据，包括 [!DNL Adobe Target]、Adobe Analytics和Adobe Audience Manager。 请注意 `marketingCloudVisitorId` 集成时需要使用 [!DNL Target] 替换为 [!DNL Adobe Analytics] 和 [!DNL Adobe Audience Manager].

以下示例调用演示了如何 `marketingCloudVisitorId` 从Experience CloudID服务检索到的内容将传递到 [!DNL Target].

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

在此方案中， [!DNL Target] 将生成 `tntId` 因为它未传递到原始调用，而原始调用将映射到提供的 `marketingCloudVisitorId`.

## 客户ID (customerIds)

[客户ID](https://experienceleague.adobe.com/docs/id-service/using/reference/authenticated-state.html) 可添加到Experience Cloud访客ID或与其关联。 无论何时发送 `customerIds`， `marketingCloudVisitorId` 还必须提供。 此外，认证状态可以与每个认证状态一起提供 `customerId` 每个访客的开销。 可以使用以下身份验证状态：

| 身份验证状态 | 用户状态 |
| --- | --- |
| `unknown` | 未知或从未验证。此状态可用于访客通过单击显示广告而登陆您的网站等场景。 |
| `authenticated` | 用户目前通过了您网站或应用程序上活动会话的身份验证。 |
| `logged_out` | 用户已经过身份验证，但已主动注销。用户打算断开与已验证状态的连接。 用户不想再被当为已经过身份验证处理。 |

请注意，仅当 `customerId` 处于已验证状态将 [!DNL Target] 引用存储和链接到customerId的用户配置文件数据。 如果 `customerId` 位于未知或 `logged_out` ，则它将被忽略，以及任何可能与其关联的用户配置文件数据 `customerId` 将不用于受众定位。

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

以上示例演示了如何发送 `customerId` 带有 `authenticatedState`. 发送时 `customerId`， `integrationCode`， `id`、和 `authenticatedState` 以及 `marketingCloudVisitorId` 是必需的。 此 `integrationCode` 的别名 [客户属性文件](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/working-with-customer-attributes.html?lang=zh-Hans) 你通过CRS提供的。

## 合并的配置文件

您可以合并 `tntId`， `thirdPartyID`、和 `marketingCloudVisitorId` 在同一请求中。 在此方案中， [!DNL Adobe Target] 将维护所有这些ID的映射，并将其固定到访客。 了解用户档案如何 [实时合并和同步](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html) 使用不同的标识符。

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

上面的示例演示了如何合并 `tntId`， `thirdPartyID`、和 `marketingCloudVisitorId` 在同一请求中。

## 分段

您的用户将分段查看体验，具体取决于您如何设置 [!DNL Adobe Target] 活动。 在 [!DNL Adobe Target]，分段为：

* **确定性**：MurmurHash3用于确保对您的用户进行分段，并在用户ID保持一致的情况下每次都看到正确的变量。
* **粘性**： [!DNL Adobe Target] 存储您的用户在用户配置文件中看到的变体，以确保在各个会话和渠道中始终向该用户显示该变体。 使用服务器端决策时，可确保变体和粘性。 使用设备上决策时，无法保证粘性。

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
1. 将余数除以10000，这会生成一个介于0和1之间的值
1. 将结果乘以活动中的体验总数
1. 舍入结果。 这会生成体验索引。

### 示例

假设以下各项：

* 带有客户端代码的客户端C `acmeclient`
* 具有ID的活动A `1111` 和三个体验 `E1`， `E2`， `E3`
* 体验具有以下分布： `E1` - 33%， `E2` - 33%， `E3` - 34%

选择流程如下所示：

1. 设备 ID `702ff4d0-83b1-4e2e-a0a6-22cbe460eb15`
1. 客户端代码 `acmeclient`
1. 活动 ID `1111`
1. 盐 `experience`
1. 要散列的值 `acmeclient.1111.702ff4d0-83b1-4e2e-a0a6-22cbe460eb15.experience`，哈希值 `-919077116`
1. 哈希的绝对值 `919077116`
1. 除以10000后的余数， `7116`
1. 余数后的值除以10000， `0.7116`
1. 将该值与体验总数相乘后的结果 `3 * 0.7116 = 2.1348`
1. 体验索引为 `2`，这表示第三个体验，因为我们使用 `0` 基于索引。
