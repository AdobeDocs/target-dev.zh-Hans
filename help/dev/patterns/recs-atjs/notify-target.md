---
title: 通知Target
description: 确保需要跟踪的所有事件 [!DNL Target] 使用trackEvent方法发送。
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 8fae7e18f555e6b549e0b9c486be73e3483dac86
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 1%

---

# 通知 [!DNL Target]

完成此步骤可确保必须发送给的所有事件 [!DNL Adobe Target] 使用发送 `trackEvent` 方法。

需要在中跟踪的任何事件 [!DNL Target] 可以是主要转化事件或成功量度。

>[!TIP]
>
>单击本主题中的图像以展开到全屏。

## 通知 [!DNL Target] 图 {#diagram}

下图中的步骤编号与以下部分相对应。

![通知Target](/help/dev/patterns/recs-atjs/assets/diagram-notify-target.png){width="600" zoomable="yes"}

## 4.1：火灾 [!DNL Adobe Target] 跟踪API

此步骤可帮助您确保必须发送给的所有事件 [!DNL Target] 使用发送 `trackEvent` 方法。

+++查看详细信息

![Fire Adobe Target跟踪API图](/help/dev/patterns/recs-atjs/assets/fire-adobe-target-track-api-diagram-combined.png){width="400" zoomable="yes"}

您可以发送订单转化属性，如以下文档中所述： *先决条件* 部分。 mbox的名称无关紧要，但需进行转换 `orderConfirmPage`.

您无需在此调用中包含订单转化属性。 这些调用最好记录一些成功量度，这些量度可以被视为主转化事件之前的小型转化事件。 `CardIds` 必须包含在基于以下内容的基于购物车的推荐中： `Add to Cart` 事件。

**先决条件**

* 与您的业务团队会面，以确定可被视为转化或成功量度的所有事件。 您还必须确定产生收入的转化事件，以便将这些详细信息发送到 [!DNL Target] 以及事件数据。
* 确保以下属性在数据层中可用，以便您可以在发送转换事件的同时发送这些属性。 转化事件可生成收入，如产品购买或添加到购物车事件。

   * `productPurchaseId`：作为订单的一部分购买的产品ID。 使用逗号分隔多个产品。
   * `orderTotal`：采购的订单总计。
   * `orderId`：购买的订单ID。

* 如果您正在跟踪购物车添加事件，请发送 `cartIds` 作为参数。 可以传递产品ID的逗号分隔列表 `cardIds`.

**读数**

* [adobe.target.trackEvent()方法](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)
* [基于购物车的标准的cartIds](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/base-the-recommendation-on-a-recommendation-key.html?lang=en#cart-based){target=_blank}

**操作**

* 使用 `adobe.target-trackEvent()` 用于发送所有必须发送到的数据的方法 [!DNL Target].







