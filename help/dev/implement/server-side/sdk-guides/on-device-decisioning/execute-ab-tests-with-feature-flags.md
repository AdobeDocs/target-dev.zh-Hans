---
title: 使用功能标志和设备上决策执行A/B测试
description: 使用设备上决策通过功能标志执行A/B测试。
feature: APIs/SDKs
exl-id: abf66e00-742d-4d40-9b6e-9bd71638c31a
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 0%

---

# 使用功能标志执行A/B测试

## 步骤摘要

1. 为您的组织启用[!UICONTROL on-device decisioning]
1. 创建[!UICONTROL A/B Test]活动
1. 定义A和B
1. 添加受众
1. 设置流量分配
1. 将流量分配设置为变量
1. 设置报表
1. 添加用于跟踪KPI的量度
1. 实施代码以使用功能标记执行A/B测试
1. 使用功能标记激活A/B测试

>[!NOTE]
>
>假设您想确定您的主页的秋季主题重新设计能否被用户接受。 您决定通过在[!DNL Adobe Target]中运行A/B试验来测试它。 此外，您还需要确保交付试验时性能良好，以免负面或缓慢的用户体验扭曲结果。

## 1.为您的组织启用[!UICONTROL on-device decisioning]

启用设备上决策可确保在几乎零延迟的情况下执行A/B活动。 要启用此功能，请在[!DNL Adobe Target]中导航到&#x200B;**[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]**，并启用&#x200B;**[!UICONTROL On-Device Decisioning]**&#x200B;切换开关。

&lt;！ — 插入image-odd4.png —>
![替代图像](assets/asset-odd-toggle.png)

>[!NOTE]
>
>您必须具有管理员或审批者[用户角色](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html?lang=zh-Hans)才能启用或禁用“设备端决策”切换开关。

启用&#x200B;**[!UICONTROL On-Device Decisioning]**&#x200B;切换后，[!DNL Adobe Target]开始为您的客户端生成规则工件。

## 2.创建[!UICONTROL A/B Test]活动

在[!DNL Adobe Target]中，导航到&#x200B;**[!UICONTROL Activities]**&#x200B;页面，然后选择&#x200B;**[!UICONTROL Create Activity]** > **[!UICONTROL A/B test]**。

![替代图像](assets/asset-ab.png)

在&#x200B;**[!UICONTROL Create A/B Test Activity]**&#x200B;模式中，保留默认的&#x200B;**[!UICONTROL Web]**&#x200B;选项(1)，选择&#x200B;**[!UICONTROL Form]**&#x200B;作为体验编辑器(2)，选择没有&#x200B;**[!UICONTROL Property Restrictions]**&#x200B;的&#x200B;**[!UICONTROL Default Workspace]** (3)，然后单击&#x200B;**[!UICONTROL Next]** (4)。

![替代图像](assets/asset-form.png)

## 3.定义A和B

1. 在活动创建&#x200B;**[!UICONTROL Experiences]**&#x200B;步骤中，提供活动(1)的名称，然后单击&#x200B;**[!UICONTROL Add Experience]** (2)按钮以添加第二个体验，即体验B。 输入应用程序中要执行A/B测试的位置(3)的名称。 在下面显示的示例中，主页是为体验A定义的位置（也是为体验B定义的位置）。

   体验A定义控制，这是当前的主页设计。

   ![替代图像](assets/asset-exp-a.png)

   体验B定义了挑战者，即重新设计的主页。 单击以更改默认内容(1)。

   ![替代图像](assets/asset-exp-b.png)

1. 在体验B中，通过选择&#x200B;**[!UICONTROL Create JSON Offer]**&#x200B;将内容从&#x200B;**[!UICONTROL Default Content]**&#x200B;更改为重新设计的内容，如下所示(1)。

   ![替代图像](assets/asset-offer.png)

1. 使用将用作标志的属性来定义JSON，以使您的业务逻辑能够呈现重新设计的主页，而不是生产环境中的当前主页。


   >[!NOTE]
   >
   >当[!DNL Adobe Target]存储用户以查看体验B（重新设计的主页）时，将返回具有示例中定义的属性的JSON。 在您的代码中，您将需要检查属性值以确定是否执行业务逻辑以呈现重新设计的主页。 您可以定义此JSON响应中的名称、值和属性数。

   ![替代图像](assets/asset-homepage.png)

## 4.添加受众

假设您要首先针对忠诚客户测试重新设计，可以根据他们是否已登录来识别这些客户。

1. 在&#x200B;**[!UICONTROL Targeting]**&#x200B;步骤中，单击以替换&#x200B;**[!UICONTROL All Visitors]**&#x200B;受众，如所示。

   ![替代图像](assets/asset-all-audiences.png)

1. 在&#x200B;**[!UICONTROL Create Audience]**&#x200B;模式中，定义`logged-in = true`的自定义规则。 这会定义已登录的用户组。 在活动中使用此受众。

   ![替代图像](assets/asset-audience.png)

## 5.设置流量分配

定义登录用户的百分比，您要针对该百分比来测试新主页重新设计。 换言之，您希望将此测试转出到用户中的哪个百分比？ 在本例中，要将此测试部署到所有登录用户，请将流量分配保持在100%。

![替代图像](assets/asset-allocation.png)

## 6.将流量分配设置为变体

定义您的登录用户中将会看到主页当前设计或全新重新设计的百分比。 在此示例中，将流量分配保持为体验A和B之间的50/50比例。

![替代图像](assets/asset-traffic-distribution.png)

## 7.设置报表

在&#x200B;**[!UICONTROL Goals & Settings]**&#x200B;步骤中，选择&#x200B;**[!UICONTROL Adobe Target]**&#x200B;作为&#x200B;**[!UICONTROL Reporting Source]**&#x200B;以在[!DNL Adobe Target] UI中查看活动结果，或选择&#x200B;**[!UICONTROL Adobe Analytics]**&#x200B;以在Adobe Analytics UI中查看这些结果。

![替代图像](assets/asset-reporting.png)

## 8.添加用于跟踪KPI的量度

选择&#x200B;**[!UICONTROL Goal Metric]**&#x200B;以测量A/B测试。 在本例中，成功的转化取决于用户是否到达页面底部，指示参与度。 因此，将根据用户是否查看了名为bottom-of-the-page的位置来确定&#x200B;**[!UICONTROL Conversion]**。

## 9.实施代码以在应用程序中执行带有功能标记的A/B测试

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const options = {
  client: "testClient",
  organizationId: "ABCDEF012345677890ABCDEF0@AdobeOrg",
  decisioningMethod: "on-device",
  events: {
    clientReady: targetClientReady
  }
};
const targetClient = TargetClient.create(options);

function targetClientReady() {
  return targetClient.getAttributes(["homepage"]).then(function(attributes) {
    const flag = attributes.getValue("homepage", "feature-flag");
    // ...
  });
}
```

>[!TAB Java]

```java {line-numbers="true"}
import com.adobe.target.edge.client.ClientConfig;
import com.adobe.target.edge.client.TargetClient;
import com.adobe.target.delivery.v1.model.ChannelType;
import com.adobe.target.delivery.v1.model.Context;
import com.adobe.target.delivery.v1.model.ExecuteRequest;
import com.adobe.target.delivery.v1.model.MboxRequest;
import com.adobe.target.edge.client.entities.TargetDeliveryRequest;
import com.adobe.target.edge.client.model.TargetDeliveryResponse;

ClientConfig config = ClientConfig.builder()
    .client("testClient")
    .organizationId("ABCDEF012345677890ABCDEF0@AdobeOrg")
    .build();
TargetClient targetClient = TargetClient.create(config);
MboxRequest mbox = new MboxRequest().name("homepage").index(0);
TargetDeliveryRequest request = TargetDeliveryRequest.builder()
    .context(new Context().channel(ChannelType.WEB))
    .execute(new ExecuteRequest().mboxes(Arrays.asList(mbox)))
    .build();
Attributes attributes = targetClient.getAttributes(request, "homepage");
String flag = attributes.getString("homepage", "feature-flag");
```

>[!ENDTABS]

## 10.使用功能标记激活A/B测试

![替代图像](assets/asset-activate.png)
