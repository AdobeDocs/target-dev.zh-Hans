---
keywords: 故障诊断, 常见问题解答, FAQ, 全局, 全局 mbox
description: 阅读有关Adobe [!DNL Target] 全局mbox的常见问题解答(FAQ)和答案。
title: 关于全局mbox的常见问题解答是什么？
feature: at.js
exl-id: 7bcd1b67-809a-466a-b648-6e0e44386157
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 39%

---

# 全局 mbox 常见问题解答

有关全局 mbox 的常见问题解答 (FAQ) 列表。

## 如果我设置了跨多个域的[!DNL Target]帐户，那么我是否可以拥有多个全局mbox？

您的帐户仅支持一个全局 mbox。

您可以通过向活动中添加 URL 规则来限制活动运行的位置。有关详细信息，请参阅[在相似页面上包含相同体验](https://experienceleague.adobe.com/docs/target/using/experiences/vec/temtest.html)。

您还可以在页面上使用[targetPageParams](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)来传递参数，然后在[!UICONTROL Visual Experience Composer] (VEC)的“配置URL”部分选择这些参数，或者通过在[!UICONTROL Form-Based Experience Composer]中将参数添加为“细化”来选择这些参数。

## 如何在[!DNL Target]全局mbox中传递收入数据？

要收集有关target-global-mbox的收入和订单信息，必须将“mbox参数”发送到[!DNL Target]。 这些参数是用于向[!DNL Target]发送更多信息的名称/值对。 [!DNL Target]会自动查找这些参数（保留名称）以填充收入数据。

对于`orderConfirmPage`，您应该传入`orderTotal`、`orderId`和`productPurchasedId`。

必须通过`targetPageParams()`将这些参数发送到target-global-mbox。 有关更多信息，请参阅[将参数传递到全局 Mbox](/help/dev/implement/client-side/atjs/global-mbox/pass-parameters-to-global-mbox.md)。

您还需要将定位添加到转化条目，以便[!DNL Target]仅在查看订单确认页面时计算target-global-mbox上的转化，如下所示：

![替代图像](assets/revenue1.png)

上图所示的“网站页面”部分包含以下几个选项：“当前页面”、“URL”、“包含”及“orderconfirm”。

![替代图像](assets/revenue2.png)

上图中的选项包含以下设置：

* **您希望如何衡量此活动：**&#x200B;收入
* **报表的默认视图：**&#x200B;每位访客带来的收入 (RPV)
* **受众采取的哪项操作可指示您的目标已达到？** 已查看 mbox，target-global-mbox
