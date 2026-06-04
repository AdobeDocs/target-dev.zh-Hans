---
title: 管理功能测试的转出
description: 了解如何使用[!UICONTROL 设备上决策]管理功能测试的转出。
feature: APIs/SDKs
exl-id: caa91728-6ac0-4583-a594-0c8fe616342d
TQID: https://experienceleague.adobe.com/soG8leVV3R4Y4FSns5oIJ43oziIhtOb2zJ5bkFYxeo0
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 596
ht-degree: 1%

---

# 管理功能测试的转出

## 步骤摘要

1. 为您的组织启用[!UICONTROL 设备上决策]
1. 创建[!UICONTROL A/B测试]活动
1. 定义您的功能和转出设置
1. 在应用程序中实施和渲染功能
1. 对应用程序中的事件实施跟踪
1. 激活A/B活动
1. 根据需要调整转出和流量分配

## &#x200B;1. 为您的组织启用[!UICONTROL 设备上决策]

启用设备上决策可确保在几乎零延迟的情况下执行A/B活动。 要启用此功能，请在[!DNL Adobe Target]中导航到&#x200B;**[!UICONTROL 管理]** > **[!UICONTROL 实施]** > **[!UICONTROL 帐户详细信息]**，并启用&#x200B;**[!UICONTROL 设备上决策]**&#x200B;切换开关。

![替代图像](assets/asset-odd-toggle.png)

>[!NOTE]
>
>您必须具有管理员或审批者[用户角色](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/user-management.html?lang=zh-Hans)才能启用或禁用[!UICONTROL 设备上决策]切换开关。

启用[!UICONTROL 设备上决策]切换后，[!DNL Adobe Target]开始为您的客户端生成&#x200B;*规则工件*。

## &#x200B;2. 创建[!UICONTROL A/B测试]活动

1. 在[!DNL Adobe Target]中，导航到&#x200B;**[!UICONTROL 活动]**&#x200B;页面，然后选择&#x200B;**[!UICONTROL 创建活动]** > **[!UICONTROL A/B测试]**。

   ![替代图像](assets/asset-ab.png)

1. 在&#x200B;**[!UICONTROL 创建A/B测试活动]**&#x200B;模式中，保留默认的&#x200B;**[!UICONTROL Web]**&#x200B;选项(1)，选择&#x200B;**[!UICONTROL 表单]**&#x200B;作为体验编辑器(2)，选择具有&#x200B;**[!UICONTROL 无属性限制]**&#x200B;的&#x200B;**[!UICONTROL 默认Workspace]**，然后单击&#x200B;**[!UICONTROL 下一步]** (4)。

   ![替代图像](assets/asset-form.png)

## &#x200B;3. 定义您的功能和转出设置

在活动创建的&#x200B;**[!UICONTROL 体验]**&#x200B;步骤中，为您的活动(1)提供一个名称。 输入应用程序中要管理功能转出的位置(2)的名称。 例如，`ondevice-rollout`或`homepage-addtocart-rollout`是位置名称，指示管理功能转出的目标。 在下面显示的示例中，`ondevice-rollout`是为体验A定义的位置。您可以选择添加受众细化(4)以限制活动的资格。

![替代图像](assets/asset-location-rollout.png)

1. 在同一页面的&#x200B;**[!UICONTROL Content]**&#x200B;部分中，从下拉列表(1)中选择&#x200B;**[!UICONTROL 创建JSON选件]**，如下所示。

   ![替代图像](assets/asset-offer.png)

1. 在出现的&#x200B;**[!UICONTROL JSON数据]**&#x200B;文本框中，为您打算在体验A (1)中与此活动一起推出的功能输入功能标志变量，并使用有效的JSON对象(2)。

   ![替代图像](assets/asset-json-a-rollout.png)

1. 单击&#x200B;**[!UICONTROL 下一步]** (1)进入活动创建的&#x200B;**[!UICONTROL 定位]**&#x200B;步骤。

   ![替代图像](assets/asset-next-2-t-rollout.png)

1. 为简单起见，在&#x200B;**[!UICONTROL 定位]**&#x200B;步骤中，保留&#x200B;**[!UICONTROL 所有访客]**&#x200B;受众(1)。 但是将流量分配(2)调整为10%。 这将限制此功能仅访问您网站访客的10%。 单击下一步(3)以前进到&#x200B;**[!UICONTROL 目标和设置]**&#x200B;步骤。

   ![替代图像](assets/asset-next-2-g-rollout.png)

1. 在&#x200B;**[!UICONTROL 目标和设置]**&#x200B;步骤中，选择&#x200B;**[!UICONTROL Adobe Target]** (1)作为&#x200B;**[!UICONTROL 报告Source]**，以便在[!DNL Adobe Target] UI中查看活动结果。

1. 选择一个&#x200B;**[!UICONTROL 目标量度]**&#x200B;以度量该活动。 在此示例中，成功的转换基于用户是否购买商品，如用户是否到达orderConfirm(2)位置所示。

1. 单击&#x200B;**[!UICONTROL 保存并关闭]** (3)以保存活动。

   ![替代图像](assets/asset-conv-rollout.png)

## &#x200B;4. 在应用程序中实施和渲染功能

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
targetClient.getAttributes(["ondevice-rollout"]).then(function(attributes) {
      const featureFlags = attributes.asObject("ondevice-rollout");

      // Your flag variables are now available in the featureFlags object variable.
      //If you failed to qualify for the Activity, you will have an empty object.
      console.log(featureFlags);
    });
```

>[!TAB Java]

```java {line-numbers="true"}
    Attributes attrs = targetJavaClient.getAttributes(targetDeliveryRequest, "ondevice-rollout");
    Map<String, Object> featureFlags = attrs.toMboxMap("ondevice-rollout");
​
    // Your flag variables are now available in the featureFlags object variable.
    //If you failed to qualify for the Activity, you will have an empty object.
    System.out.println(featureFlags);
```

>[!ENDTABS]

## &#x200B;5. 对应用程序中的事件实施跟踪

在使功能标志变量在应用程序中可用之后，您可以使用该变量来启用已属于应用程序的任何功能。 如果访客不符合活动资格，则意味着他们未包含在定义为受众的10%存储段中。

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
//... Code removed for brevity

if(featureFlags.enable == "yes") { //Fell within 10% traffic
    console.log("Render Feature");
}
else {
    console.log("Disable Feature");
}

// alternatively, the getValue method could be used on the Attributes object.

if(attributes.getValue("ondevice-rollout", "enable") === "yes") { //Fell within 10% traffic
    console.log("Render Feature");
}
else {
    console.log("Disable Feature");
}
```

>[!TAB Java]

```java {line-numbers="true"}
//... Code removed for brevity
​
if("yes".equals(String.valueOf(featureFlags.get("enable")))) { //Fell within 10% traffic
    System.out.println("Render Feature");
}
else {
    System.out.println("Disable Feature");
}
​
// alternatively, the getString method could be used on the Attributes object.
​
if("yes".equals(attrs.getString("ondevice-rollout", "enable"))) { //Fell within 10% traffic
    System.out.println("Render Feature");
}
else {
    System.out.println("Disable Feature");
}
```

>[!ENDTABS]

## &#x200B;6. 激活您的转出活动

![替代图像](assets/asset-activate-rollout.png)

## &#x200B;7. 根据需要调整转出和流量分配

激活活动后，可随时编辑它以根据需要增加或减少流量分配。

由于初始转出成功，流量分配从10%增加到50%。

![替代图像](assets/asset-adjust-rollout.png)
