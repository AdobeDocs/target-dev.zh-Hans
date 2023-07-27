---
title: Target SDK快速入门
description: 如何使用Adobe Target SDK？
feature: APIs/SDKs
exl-id: a5ae9826-7bb5-41de-8796-76edc4f5b281
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '664'
ht-degree: 0%

---

# 快速入门 [!DNL Target] SDK

为了启动并运行，我们鼓励您创建您的第一个 [设备上决策](../on-device-decisioning/overview.md) 以您选择的语言进行的功能标记活动：

* Node.js
* Java
* .NET
* Python

## 步骤摘要

1. 为您的组织启用设备上决策
1. 安装SDK
1. 初始化SDK
1. 在中设置功能标记 [!DNL Adobe Target] [!UICONTROL A/B测试] 活动
1. 在应用程序中实施和渲染功能
1. 对应用程序中的事件实施跟踪
1. 激活您的 [!UICONTROL A/B测试] 活动

## 1.为您的组织启用设备上决策

启用设备上决策可确保 [!UICONTROL A/B测试] 活动以几乎零延迟的方式执行。 要启用此功能，请导航到 **[!UICONTROL 管理]** > **[!UICONTROL 实现]** > **[!UICONTROL 帐户详细信息]** 并启用 **[!UICONTROL 设备上决策]** 切换。

![替代图像](assets/asset-odd-toggle.png)

>[!NOTE]
>
>您必须拥有 **[!UICONTROL 管理员]** 或 **[!UICONTROL 审批者]** [用户角色](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html) 启用或禁用 **[!UICONTROL 设备上决策]** 切换。

启用 **[!UICONTROL 设备上决策]** 切换， [!DNL Adobe Target] 开始生成 [规则对象](../on-device-decisioning/rule-artifact-overview.md) 你的委托人。

## 2.安装SDK

对于Node.js、Java和Python，请在终端的项目目录中运行以下命令。 对于.NET，将其添加为依赖项，方法为 [从NuGet安装](https://www.nuget.org/packages/Adobe.Target.Client).

>[!BEGINTABS]

>[!TAB Node.js (NPM)]

```js {line-numbers="true"}
npm i @adobe/target-nodejs-sdk -P
```

>[!TAB Java (Maven)]

```javascript {line-numbers="true"}
<dependency>
   <groupId>com.adobe.target</groupId>
   <artifactId>java-sdk</artifactId>
   <version>2.0</version>
</dependency>
```

>[!TAB .NET (Bash)]

```bash {line-numbers="true"}
dotnet add package Adobe.Target.Client
```

>[!TAB Python (pip)]

```python {line-numbers="true"}
pip install target-python-sdk
```

>[!ENDTABS]

## 3.初始化SDK

规则工件将在SDK初始化步骤中下载。 您可以自定义初始化步骤以确定如何下载和使用工件。

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
   client: "<your target client code>",
   organizationId: "your EC org id",
   decisioningMethod: "on-device",
   events: {
      clientReady: targetClientReady
      }
};

const tClient = TargetClient.create(CONFIG);

function targetClientReady() {
   //Adobe Target SDK has now downloaded the JSON artifact locally, which contains the activity details.
   //We will see how to use the artifact here very soon.
}
```

>[!TAB Java (Maven)]

```javascript {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
   .client("testClient")
   .organizationId("ABCDEF012345677890ABCDEF0@AdobeOrg")
   .build();
TargetClient targetClient = TargetClient.create(config);
```

>[!TAB .NET (C#)]

```csharp {line-numbers="true"}
var targetClientConfig = new TargetClientConfig.Builder("testClient", "ABCDEF012345677890ABCDEF0@AdobeOrg")
   .Build();
this.targetClient.Initialize(targetClientConfig);
```

>[!TAB Python]

```python {line-numbers="true"}
from target_python_sdk import TargetClient

def target_client_ready():
   # Adobe Target SDK has now downloaded the JSON artifact locally, which contains the activity details.
   # We will see how to use the artifact here very soon.

CONFIG = {
   "client": "<your target client code>",
   "organization_id": "your EC org id",
   "decisioning_method": "on-device",
   "events": {
      "client_ready": target_client_ready
   }
}

target_client = TargetClient.create(CONFIG)
```

>[!ENDTABS]

## 4.在 [!DNL Adobe Target] [!UICONTROL A/B测试] 活动

1. 在 [!DNL Target]，导航到 **[!UICONTROL 活动]** 页面，然后选择 **[!UICONTROL 创建活动]** > **[!UICONTROL A/B测试]**.

   ![替代图像](assets/asset-ab.png)

1. 在 **[!UICONTROL 创建A/B测试活动]** 模式窗口，保持默认Web选项处于选中状态(1)，选择 **[!UICONTROL 表单]** 作为体验编辑器(2)，选择 **[!UICONTROL 默认工作区]** 替换为 **[!UICONTROL 无属性限制]**(3)，然后单击 **[!UICONTROL 下一个]** （四）。

   ![替代图像](assets/asset-form.png)

1. 在 **[!UICONTROL 体验]** 创建活动的步骤，为您的活动提供一个名称(1)并添加第二个体验，即体验B，方法是单击 **[!UICONTROL 添加体验]** (2)。 输入您选择的位置名称(3)。 例如， `ondevice-featureflag` 或 `homepage-addtocart-featureflag` 是指示功能标志测试目标的位置名称。  在以下示例中， `ondevice-featureflag` 是为体验B定义的位置。或者，您可以添加受众细化(4)以限制活动的资格。

   ![替代图像](assets/asset-location.png)

1. 在 **[!UICONTROL 内容]** 部分，选择 **[!UICONTROL 创建JSON选件]** (1)中进行归因、筛选、流程、流失等。

   ![替代图像](assets/asset-offer.png)

1. 在 **[!UICONTROL JSON数据]** 在显示的文本框中，使用有效的JSON对象(2)为每个体验(1)键入功能标志变量。

   输入体验A的功能标志变量。

   ![替代图像](assets/asset-json_a.png)

   **（以上适用于体验A的示例JSON）**

   ```json {line-numbers="true"}
   {
      "enabled" : true,
      "flag" : "expA"
   }
   ```

   输入体验B的功能标志变量。

   ![替代图像](assets/asset-json_b.png)

   **（以上适用于体验B的JSON示例）**

   ```json {line-numbers="true"}
   {
      "enabled" : true,
      "flag" : "expB"
   }
   ```

1. 单击 **[!UICONTROL 下一个]** (1)垫付予本公司股东，作为本 **[!UICONTROL 定位]** 活动创建步骤。

   ![替代图像](assets/asset-next_2_t.png)

1. 在 **[!UICONTROL 定位]** 为了简单起见，如下所示的步骤示例，“受众定位”(2)保留在“所有访客”的默认集中。 这意味着该活动未定位。 但是，请注意Adobe建议您始终将目标定位到生产活动的受众。 单击 **[!UICONTROL 下一个]** (3)垫付予本公司股东，作为本 **[!UICONTROL 目标和设置]** 活动创建步骤。

   ![替代图像](assets/asset-next_2_g.png)

1. 在 **[!UICONTROL 目标和设置]** 步骤，设置 **[!UICONTROL 报表源]** 到 **[!UICONTROL Adobe Target]** (1)。 定义 **[!UICONTROL 目标量度]** 作为 **[!UICONTROL 转化]**，根据网站的转化量度指定详细信息(2)。 单击 **[!UICONTROL 保存并关闭]** (3)保存活动。

   ![替代图像](assets/asset-conv.png)

## 5.在应用程序中实施并渲染功能

在中设置功能标记变量后 [!DNL Target]，修改您的应用程序代码以使用它们。 例如，在应用程序中获取功能标志后，您可以使用该标志启用功能并呈现访客符合条件的体验。

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
//... Code removed for brevity
​
let featureFlags = {};
​
function targetClientReady() {
   tClient.getAttributes(["ondevice-featureflag"]).then(function(response) {
      const featureFlags = response.asObject("ondevice-featureflag");
      if(featureFlags.enabled && featureFlags.flag !== "expA") { //Assuming "expA" is control
         console.log("Render alternate experience" + featureFlags.flag);
      }
      else {
         console.log("Render default experience");
      }
   });
}
```

>[!TAB Java (Maven)]

```javascript {line-numbers="true"}
MboxRequest mbox = new MboxRequest().name("ondevice-featureflag").index(0);
TargetDeliveryRequest request = TargetDeliveryRequest.builder()
   .context(new Context().channel(ChannelType.WEB))
   .execute(new ExecuteRequest().mboxes(Arrays.asList(mbox)))
   .build();
Attributes attributes = targetClient.getAttributes(request, "ondevice-featureflag");
String flag = attributes.getString("ondevice-featureflag", "flag");
```

>[!TAB .NET (C#)]

```csharp {line-numbers="true"}
var mbox = new MboxRequest(index: 0, name: "ondevice-featureflag");
var deliveryRequest = new TargetDeliveryRequest.Builder()
   .SetContext(new Context(ChannelType.Web))
   .SetExecute(new ExecuteRequest(mboxes: new List<MboxRequest> { mbox }))
   .Build();
var attributes = targetClient.GetAttributes(request, "ondevice-featureflag");
var flag = attributes.GetString("ondevice-featureflag", "flag");
```

>[!TAB Python]

```python {line-numbers="true"}
# ... Code removed for brevity

feature_flags = {}

def target_client_ready():
   attribute_provider = target_client.get_attributes(["ondevice-featureflag"])
   feature_flags = attribute_provider.as_object(mbox_name="ondevice-featureflag")
   if feature_flags.get("enabled") and feature_flags.get("flag") != "expA": # Assuming "expA" is control
      print("Render alternate experience {}".format(feature_flags.get("flag")))
   else:
      print("Render default experience")
```

>[!ENDTABS]

## 6.对应用程序中的事件实施其他跟踪

或者，您也可以使用sendNotification()函数发送用于跟踪转换的其他事件。

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
//... Code removed for brevity
​
//When a conversion happens
TargetClient.sendNotifications({
   targetCookie,
   "request" : {
      "notifications" : [
      {
         type: "display",
         timestamp : Date.now(),
         id: "conversion",
         mbox : {
            name : "orderConfirm"
         },
         order : {
            id: "BR9389",
            total : 98.93,
            purchasedProductIds : ["J9393", "3DJJ3"]
         }
      }
      ]
   }
})
```

>[!TAB Java (Maven)]

```javascript {line-numbers="true"}
Notification notification = new Notification();
notification.setId("conversion");
notification.setImpressionId(UUID.randomUUID().toString());
notification.setType(MetricType.DISPLAY);
notification.setTimestamp(System.currentTimeMillis());
Order order = new Order("BR9389");
order.total(98.93);
order.purchasedProductIds(["J9393", "3DJJ3"]);
notification.setOrder(order);

TargetDeliveryRequest notificationRequest =
   TargetDeliveryRequest.builder()
      .context(new Context().channel(ChannelType.WEB))
      .notifications(Collections.singletonList(notification))
      .build();

NotificationDeliveryService notificationDeliveryService = new NotificationDeliveryService();
notificationDeliveryService.sendNotification(notificationRequest);
```

>[!TAB .NET (C#)]

```csharp {line-numbers="true"}
var order = new Order
{
   Id = "BR9389",
   Total = 98.93M,
   PurchasedProductIds = new List<string> { "J9393", "3DJJ3" },
};
​
var notification = new Notification
{
   Id = "conversion",
   ImpressionId = Guid.NewGuid().ToString(),
   Type = MetricType.Display,
   Timestamp = DateTimeOffset.UtcNow.ToUnixTimeMilliseconds(),
   Order = order,
};
​
var notificationRequest = new TargetDeliveryRequest.Builder()
   .SetContext(new Context(ChannelType.Web))
   .SetNotifications(new List<Notification> {notification})
   .Build();
​
targetClient.SendNotifications(notificationRequest);
```

>[!TAB Python]

```python {line-numbers="true"}
# ... Code removed for brevity

# When a conversion happens
notification_mbox = NotificationMbox(name="orderConfirm")
order = Order(id="BR9389, total=98.93, purchased_product_ids=["J9393", "3DJJ3"])
notification = Notification(
   id="conversion",
   type=MetricType.DISPLAY,
   timestamp=1621530726000,  # Epoch time in milliseconds
   mbox=notification_mbox,
   order=order
)
notification_request = DeliveryRequest(notifications=[notification])


target_client.send_notifications({
   "target_cookie": target_cookie,
   "request" : notification_request
})
```

>[!ENDTABS]

## 7.激活您的 [!UICONTROL A/B测试] 活动

1. 单击 **[!UICONTROL 激活]** (1)激活您的 [!UICONTROL A/B测试] 活动。

   >[!NOTE]
   >
   >您必须拥有 **[!UICONTROL 审批者]** 或 **[!UICONTROL 发布者]** [用户角色](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html) 以执行此步骤。

   ![替代图像](assets/asset-activate.png)
