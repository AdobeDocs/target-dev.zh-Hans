---
title: 通知Target
description: 确保使用trackEvent方法发送所有需要由 [!DNL Target] 跟踪的事件。
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: efccadab-d139-4423-8613-c2743d87b3a0
source-git-commit: 50ee7e66e30c0f8367763a63b6fde5977d30cfe7
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 1%

---

# 通知[!DNL Target]

完成此步骤可确保使用`trackEvent`方法发送所有必须发送到[!DNL Adobe Target]的事件。

任何需要在[!DNL Target]中跟踪的事件都可以是主要转化事件或成功量度。

>[!TIP]
>
>单击本主题中的图像以展开到全屏。

## 通知[!DNL Target]关系图 {#diagram}

下图中的步骤编号与以下部分相对应。

![通知目标关系图](/help/dev/patterns/recs-atjs/assets/diagram-notify-target.png){width="600" zoomable="yes"}

## 4.1：触发[!DNL Adobe Target]跟踪API

此步骤可帮助您确保必须发送到[!DNL Target]的所有事件均使用`trackEvent`方法发送。

+++查看详细信息

![触发Adobe Target跟踪API关系图](/help/dev/patterns/recs-atjs/assets/fire-adobe-target-track-api-diagram-combined.png){width="400" zoomable="yes"}

您发送以下&#x200B;*先决条件*&#x200B;部分中提到的订单转换属性。 mbox的名称无关紧要，但转换是使用`orderConfirmPage`。

您无需在此调用中包含订单转化属性。 这些调用最好记录一些成功量度，这些量度可以被视为主转化事件之前的小型转化事件。 `CardIds`必须包含在基于`Add to Cart`事件的基于购物车的推荐中。

**先决条件**

* 与您的业务团队会面，以确定可被视为转化或成功量度的所有事件。 您还必须确定生成收入的转化事件，以便将这些详细信息与事件数据一起发送到[!DNL Target]。
* 确保以下属性在数据层中可用，以便您可以在发送转换事件的同时发送这些属性。 转化事件可生成收入，如产品购买或添加到购物车事件。

   * `productPurchaseId`：作为订单的一部分购买的产品ID。 使用逗号分隔多个产品。
   * `orderTotal`：购买的订单总计。
   * `orderId`：购买的订单ID。

  下图显示了 [!DNL Experience Platform]](https://experienceleague.adobe.com/docs/tags.html){target=_blank}中 [!DNL tags] 的[规则，该规则应仅在[!UICONTROL Confirmation]页面上触发。

  ![操作配置页面](/help/dev/patterns/recs-atjs/assets/action-configuration.png){width="400" zoomable="yes"}

* 如果您正在跟踪购物车添加事件，请发送`cartIds`作为参数。 可以为`cardIds`传递产品ID的逗号分隔列表。

**读数**

* [adobe.target.trackEvent()方法](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)
* 基于购物车的标准的[cartIds](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/base-the-recommendation-on-a-recommendation-key.html?lang=en#cart-based){target=_blank}

**操作**

* 使用`adobe.target-trackEvent()`方法发送必须发送到[!DNL Target]的所有数据。
