---
title: 使用Adobe Target SDK提供个性化
description: 了解如何使用实现个性化 [!UICONTROL 设备上决策].
feature: APIs/SDKs
exl-id: bac64c78-0d3a-40d7-ae2b-afa0f1b8dc4f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 0%

---

# 提供个性化

## 步骤摘要

1. 启用 [!UICONTROL 设备上决策] （贵组织）
1. 创建 [!UICONTROL 体验定位] (XT)活动
1. 按受众定义个性化体验
1. 验证每个受众的个性化体验
1. 设置报表
1. 添加用于跟踪KPI的量度
1. 在应用程序中实施个性化优惠
1. 实施代码以跟踪转化事件
1. 激活您的 [!UICONTROL 体验定位] (XT)个性化活动

假设您是一家旅游公司。 您需要提供特定旅行套餐25%的个性化优惠。 为了让选件能够引起用户的共鸣，您决定显示目标城市的里程碑。 您还希望确保以近乎零延迟的方式执行个性化选件交付，以免影响用户体验和扭曲结果。

## 1.启用 [!UICONTROL 设备上决策] （贵组织）

1. 启用设备上决策可确保在几乎零延迟的情况下执行A/B活动。 要启用此功能，请导航到 **[!UICONTROL 管理]** > **[!UICONTROL 实现]** > **[!UICONTROL 帐户详细信息]** 在 [!DNL Adobe Target]，并启用 **[!UICONTROL 设备上决策]** 切换。

   ![替代图像](assets/asset-odd-toggle.png)

   >[!NOTE]
   >
   >您必须具有管理员或审批者 [用户角色](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html) 启用或禁用 [!UICONTROL 设备上决策] 切换。

   启用 **[!UICONTROL 设备上决策]** 切换， [!DNL Adobe Target] 开始生成 *规则对象* 你的委托人。

## 2.创建一个 [!UICONTROL 体验定位] (XT)活动

1. 在 [!DNL Adobe Target]，导航到 **[!UICONTROL 活动]** 页面，然后选择 **[!UICONTROL 创建活动]** > **[!UICONTROL 体验定位]**.

   ![替代图像](assets/asset-xt.png)

1. 在 **[!UICONTROL 创建体验定位活动]** 模式，保留默认值 **[!UICONTROL Web]** 已选择选项(1)，选择 **[!UICONTROL 表单]** 作为体验编辑器(2)，选择工作区和属性(3)，然后单击 **[!UICONTROL 下一个]** （四）。

   ![替代图像](assets/asset-xt-next.png)

## 3.为每个受众定义个性化体验

1. 在 **[!UICONTROL 体验]** 活动创建步骤，单击 **[!UICONTROL 更改受众]** 创建想要前往加利福尼亚州旧金山的访客受众。

   ![替代图像](assets/asset-change-audience.png)

1. 在 **[!UICONTROL 创建受众]** 模式窗口，定义一个自定义规则，其中 `destinationCity = San Francisco`. 这定义了要前往旧金山的用户组。

   ![替代图像](assets/asset-audience-sf.png)

1. 仍在 **[!UICONTROL 体验]** 步骤，输入您的应用程序中要呈现有关Golden Gate Bridge的特别选件的位置(1)的名称，但仅限于那些前往旧金山的用户。 在此处的示例中， homepage是为HTML选件(2)选择的位置，该位置在 **[!UICONTROL 内容]** 区域。

   ![替代图像](assets/asset-content-sf.png)

1. 通过单击添加其他定向受众 **[!UICONTROL 添加体验定位]**. 这次，通过定义受众规则来定位希望前往纽约的受众，其中 `destinationCity = New York`. 在应用程序中定义您要提供有关帝国大厦的特殊优惠的位置。 在此显示的示例中， `homepage` 是为HTML选件(2)选择的位置，该位置在 **[!UICONTROL 内容]** 区域。

   ![替代图像](assets/asset-content-ny.png)

## 4.验证每个受众的个性化体验

在 **[!UICONTROL 定位]** 步骤，验证您已为每个受众配置了所需的个性化体验。

![替代图像](assets/asset-verify-sf-ny.png)

## 5.设置报表

在 **[!UICONTROL 目标和设置]** 步骤，选择 **[!UICONTROL Adobe Target]** 作为 **[!UICONTROL 报表源]** 在中查看活动结果 [!DNL Adobe Target] UI，或选择 **[!UICONTROL Adobe Analytics]** 以在Adobe Analytics UI中查看它们。

![替代图像](assets/asset-reporting-sf-ny.png)

## 6.添加用于跟踪KPI的量度

选择 **[!UICONTROL 目标量度]** 以衡量活动是否成功。 在本例中，成功的转化取决于用户是否点击了个性化目标选件。

## 7.在应用程序中实施个性化优惠

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
    execute: {
      pageLoad: {
        parameters: {
          destinationCity: "San Francisco"
        }
      }
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

Context context = new Context().channel(ChannelType.WEB);

ExecuteRequest executeRequest = new ExecuteRequest();

RequestDetails pageLoad = new RequestDetails();
pageLoad.setParameters(
    new HashMap<String, String>() {
      {
        put("destinationCity", "San Francisco");
      }
    });

executeRequest.setPageLoad(pageLoad);

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

## 8.实施代码以跟踪转化事件

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
//... Code removed for brevity

//When a conversion happens
TargetClient.sendNotifications({
    targetCookie,
    "request" : {
      "notifications" : [
        {
          type: "click",
          timestamp : Date.now(),
          id: "conversion",
          mbox : {
            name : "destinationOffer"
          }
        }
      ]
    }
})
```

>[!TAB Java]

```java {line-numbers="true"
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

Context context = new Context().channel(ChannelType.WEB);

ExecuteRequest executeRequest = new ExecuteRequest();

RequestDetails pageLoad = new RequestDetails();
pageLoad.setParameters(
    new HashMap<String, String>() {
      {
        put("destinationCity", "San Francisco");
      }
    });

executeRequest.setPageLoad(pageLoad);
NotificationDeliveryService notificationDeliveryService = new NotificationDeliveryService();

Notification notification = new Notification();
notification.setId("conversion");
notification.setImpressionId(UUID.randomUUID().toString());
notification.setType(MetricType.CLICK);
notification.setTimestamp(System.currentTimeMillis());
notification.setTokens(
    Collections.singletonList(
        "IbG2Jz2xmHaqX7Ml/YRxRGqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="));

TargetDeliveryRequest targetDeliveryRequest =
    TargetDeliveryRequest.builder()
        .context(context)
        .execute(executeRequest)
        .notifications(Collections.singletonList(notification))
        .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
notificationDeliveryService.sendNotification(request);
```

>[!ENDTABS]

## 9.激活您的体验定位(XT)活动

![替代图像](assets/asset-xt-activate.png)
