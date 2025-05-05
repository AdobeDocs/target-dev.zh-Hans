---
keywords: 实施，非javascript， mbox， adbox
description: 使用AdBox在 [!DNL Adobe Target]的站外实施中传递图像。 AdBox与mbox类似，但由URL而不是JavaScript控制。
title: 如何为图像创建Adbox？
feature: Implement Email
exl-id: ad1eb6c4-7a16-4054-ae76-57971261e931
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 71%

---

# 为图像创建 Adbox

使用AdBox在站点外实施中使用[!DNL Adobe Target]传递图像。

AdBox 与 mbox 类似，但它由 URL 控制而非 JavaScript。创建的 AdBox 具有特殊的 AdBox URL，此 URL 会将“广告”mbox（或 AdBox）加载到您的 Adobe 帐户中。在活动中可使用此 AdBox 替代 mbox。在电子邮件或其他非 JavaScript 实施中可使用 AdBox URL，而不使用直接图像引用。

有关选择正确设置的帮助，请参阅[不基于JavaScript的实施](/help/dev/implement/email/overview.md)。

1. 创建 AdBox URL：

   ```
   https://myClientCode.tt.omtrdc.net/m2/myClientCode/ubox/
   image?mbox=emailHeroImage123_320x200&
   mboxDefault=http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2Fimg%2Flogo%2Egif
   ```

   * 其中，`myClientCode` 是您公司的客户端代码。您公司的客户端代码全部为小写字母，且不含任何特殊字符。

     您的客户端代码位于[!DNL Target]界面的&#x200B;**[!UICONTROL Administation]** > **[!UICONTROL Implementation]**&#x200B;页面顶部。

   * 其中，`image` 是调用类型。在此例中为图像。

   * 其中，`emailHeroImage123_320x200` 是 AdBox 的名称。

   * 其中，`http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2Fimg%2Flogo%2Egif` 是 mbox 的默认内容。该内容必须是图像。

     这必须是进行了编码的 URL，且必须是绝对引用。您可以使用[HTMLURL编码引用](https://www.w3schools.com/tags/ref_urlencode.asp)来快速对您的URL进行编码。

1. 为每个替代图像创建[重定向选件](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=zh-Hans)。

   >[!NOTE]
   >
   >AdBox 必须和重定向选件或默认内容选件共同加载。不接受其他的选件类型。由于 AdBox 是 URL，它只能显示自身接收到的 URL，因此只有重定向选件才适用。

1. 创建活动。

   请参阅[不基于 JavaScript 的实施](/help/dev/implement/email/overview.md)，以了解如何正确设置来实现您的目标。

1. 完成活动 QA。

   最佳做法是，创建一个虚拟页面，并确认在所有环境中，所有体验、默认内容和报表在所有类型的浏览器上的行为均符合预期。

1. 启动活动。
