---
title: 使用属性执行功能测试
description: 使用属性执行功能测试
feature: APIs/SDKs
exl-id: c89d337c-20a9-454c-930c-79d9217e23b6
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 0%

---

# 使用属性执行功能测试

## 步骤摘要

1. 为您的组织启用[!UICONTROL on-device decisioning]
1. 创建[!UICONTROL A/B Test]活动
1. 定义A和B
1. 添加受众
1. 设置流量分配
1. 将流量分配设置为变量
1. 设置报表
1. 添加用于跟踪KPI的量度
1. 实施代码以使用属性执行功能测试
1. 实施代码以跟踪转化事件
1. 使用属性激活功能测试

>[!NOTE]
>
>假设您是一家零售电子商务公司。 当客户浏览您的产品目录并进行排序时，您希望提高转化率。 您有一个假设，即某些排序算法和分页策略产生比其他算法更好的结果。 为了测试此理论，您决定运行一个功能测试，该测试涉及使用最终用户不同的排序选项重新设计排序小组件。 您希望确保此功能测试在近乎零延迟的情况下执行，以便它不会对用户体验产生负面影响并扭曲结果。

## 1.为您的组织启用[!UICONTROL on-device decisioning]

启用设备上决策可确保在几乎零延迟的情况下执行A/B活动。 要启用此功能，请在[!DNL Adobe Target]中导航到&#x200B;**[!UICONTROL Administration]** > **[!UICONTROL Implementation]** > **[!UICONTROL Account details]**，并启用&#x200B;**[!UICONTROL On-Device Decisioning]**&#x200B;切换开关。

![替代图像](assets/asset-odd-toggle.png)

>[!NOTE]
>
>您必须具有管理员或审批者[用户角色](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html?lang=zh-Hans)才能启用或禁用&#x200B;**[!UICONTROL On-Device Decisioning]**&#x200B;切换开关。

启用&#x200B;**[!UICONTROL On-Device Decisioning]**&#x200B;切换后，[!DNL Adobe Target]开始为您的客户端生成&#x200B;*规则工件*。

## 2.创建[!UICONTROL A/B Test]活动

1. 在[!DNL Adobe Target]中，导航到&#x200B;**[!UICONTROL Activities]**&#x200B;页面，然后选择&#x200B;**[!UICONTROL Create Activity]** > **[!UICONTROL A/B test]**。

   ![替代图像](assets/asset-ab.png)

1. 在&#x200B;**[!UICONTROL Create A/B Test Activity]**&#x200B;模式中，保留默认的&#x200B;**[!UICONTROL Web]**&#x200B;选项(1)，选择&#x200B;**[!UICONTROL Form]**&#x200B;作为体验编辑器(2)，选择带有&#x200B;**[!UICONTROL No Property Restrictions]** (3)的&#x200B;**[!UICONTROL Default Workspace]**，然后单击&#x200B;**[!UICONTROL Next]** (4)。

   ![替代图像](assets/asset-form.png)

## 3.定义A和B

1. 在活动创建&#x200B;**[!UICONTROL Experiences]**&#x200B;步骤中，提供活动(1)的名称，然后单击&#x200B;**[!UICONTROL Add Experience]** (2)按钮以添加第二个体验，即体验B。 输入应用程序内要使用属性执行功能测试的位置(3)的名称。 在以下示例中，`product-results-page`是为体验A定义的位置。（它也是为体验B定义的位置。）

   ![替代图像](assets/asset-location.png)

   **[!UICONTROL Experience A]**&#x200B;将包含指示您的业务逻辑执行以下操作的JSON：

   * 通过`test_sorting`功能标志启动排序算法功能
   * 执行`sorting_algorithm _**_attribute`中定义的推荐排序算法
   * 按照`pagination_limit`中定义的分页策略定义，每页返回50个产品

1. 在体验A中，通过选择&#x200B;**[!UICONTROL Create JSON Offer]**&#x200B;将内容从&#x200B;**[!UICONTROL Default Content]**&#x200B;更改为JSON，如下所示(1)。

   ![替代图像](assets/asset-offer.png)

1. 使用`test_sorting`、`sorting_algorithm`和`pagination_limit`标志和属性定义JSON，这些标志和属性将用于启动推荐的排序算法，分页限制为50个产品。

   >[!NOTE]
   >
   >当[!DNL Adobe Target]存储用户以查看体验A时，将返回具有示例中定义的属性的JSON。 在您的代码中，您需要检查功能标志`test_sorting`的值以查看是否应打开排序功能。 如果是这样，您将使用`sorting_algorithm`属性的推荐值在产品列表视图中显示推荐的产品。 为您的应用程序显示的产品限制将为50，因为这是`pagination_limit`属性的值。

   ![替代图像](assets/asset-sorting.png)

   **[!UICONTROL Experience B]**&#x200B;将定义指示您的业务逻辑执行以下操作的JSON：

   * 通过test_sorting功能标志启动排序算法功能
   * 执行`sorting_algorithm _**_attribute`中定义的`best_sellers`排序算法
   * 按照`pagination_limit`中定义的分页策略定义，每页返回50个产品

   >[!NOTE]
   >
   >当[!DNL Adobe Target]存储用户以查看体验B时，将返回具有示例中定义的属性的JSON。 在您的代码中，您需要检查功能标志`test_sorting`的值以查看是否应打开排序功能。 如果是这样，您将使用`sorting_algorithm`属性的`best_sellers`值在产品列表视图中显示最畅销的产品。 为您的应用程序显示的产品限制将为50，因为这是`pagination_limit`属性的值。

   ![替代图像](assets/asset-sorting-b.png)

## 4.添加受众

在&#x200B;**[!UICONTROL Targeting]**&#x200B;步骤中，保留&#x200B;**[!UICONTROL All Visitors]**&#x200B;受众。 这使您能够了解排序功能的影响，以及哪个算法和项目数最能影响结果。

![替代图像](assets/asset-audience-b.png)

## 5.设置流量分配

定义访客所占的百分比，您要根据此百分比来测试排序算法和分页策略。 换言之，您希望将此测试转出到用户中的哪个百分比？ 在本例中，要将此测试部署到所有登录用户，请将流量分配保持在100%。

![替代图像](assets/asset-allocation-100.png)

## 6.将流量分配设置为变体

定义将看到推荐的与最畅销商品排序算法的访客百分比，每个页面最多可查看50个产品。 在此示例中，将流量分配保持为体验A和B之间的50/50比例。

![替代图像](assets/asset-variations-50.png)

## 7.设置报表

在&#x200B;**[!UICONTROL Goals & Settings]**&#x200B;步骤中，选择&#x200B;**[!UICONTROL Adobe Target]**&#x200B;作为&#x200B;**[!UICONTROL Reporting Source]**，以便在[!DNL Adobe Target] UI中查看A/B测试结果；或者选择&#x200B;**[!UICONTROL Adobe Analytics]**，以便在Adobe Analytics UI中查看这些结果。

![替代图像](assets/asset-reporting-b.png)

## 8.添加用于跟踪KPI的量度

选择&#x200B;**[!UICONTROL Goal Metric]**&#x200B;以使用属性测量功能测试。 在本例中，成功取决于用户是否购买产品，具体取决于显示它们的排序算法和分页策略。

## 9.在应用程序中实施具有属性的功能测试

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
  return targetClient.getAttributes(["product-results-page"]).then(function(attributes) {
    const test_sorting = attributes.getValue("product-results-page", "test-sorting");
    const sorting_algorithm = attributes.getValue("product-results-page", "sorting_algorithm");
    const pagination_limit = attributes.getValue("product-results-page", "pagination_limit");
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
MboxRequest mbox = new MboxRequest().name("product-results-page").index(0);
TargetDeliveryRequest request = TargetDeliveryRequest.builder()
    .context(new Context().channel(ChannelType.WEB))
    .execute(new ExecuteRequest().mboxes(Arrays.asList(mbox)))
    .build();
Attributes attributes = targetClient.getAttributes(request, "product-results-page");
String testSorting = attributes.getString("product-results-page", "test-sorting");
String sortingAlgorithm = attributes.getString("product-results-page", "sorting_algorithm");
String paginationLimit = attributes.getString("product-results-page", "pagination_limit");
```

>[!ENDTABS]

## 10.实施代码以跟踪转化事件

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
            name : "product-results-page"
          }
        }
      ]
    }
})
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

Attributes attributes = targetClient.getAttributes(request, "product-results-page");
String testSorting = attributes.getString("product-results-page", "test-sorting");
String sortingAlgorithm = attributes.getString("product-results-page", "sorting_algorithm");
String paginationLimit = attributes.getString("product-results-page", "pagination_limit");
```

>[!ENDTABS]

## 11.使用属性激活功能测试

![替代图像](assets/asset-activate.png)
