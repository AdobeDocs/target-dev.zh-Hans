---
keywords: at.js，函数， javascript库
description: 查看可用于 [!DNL Adobe Target]中at.js JavaScript库的1.x和2.x版本的函数的列表。
title: 我可以对at.js使用哪些函数？
feature: at.js
exl-id: 1efed365-8a74-4c85-bdb1-8daaaf53d642
TQID: https://experienceleague.adobe.com/7uABK1rDaMpA7a0skEo3g1KxTnoc-gif-uHMkMnE8QE
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 557
ht-degree: 38%

---

# at.js 函数

可与[!DNL Adobe Target] at.js JavaScript库一起使用的函数列表。 单击“函数”列中的链接以获取更多信息和示例。

| 函数 | 详细信息 |
| --- | --- |
| [[!UICONTROL adobe.target.getOffer(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffer.md) | 此函数会触发用于获取[!DNL Target]选件的请求。 使用 `adobe.target.applyOffer()` 来处理响应或使用您自己的成功处理。 |
| [[!UICONTROL adobe.target.getOffers(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)<P>(at.js 2.x) | 此函数允许您通过传递多个 mbox 来检索多个产品建议。 此外，还可以针对活跃活动中的所有视图检索多个产品建议。<P>**注意：**&#x200B;此函数已在at.js 2.x中引入。 此函数不适用于at.js版本1.*x*。 |
| [[!UICONTROL adobe.target.applyOffer(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffer.md) | 此函数用于应用响应内容。 |
| [[!UICONTROL adobe.target.applyOffers(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)<P>(at.js 2.x) | 此函数允许您应用[!UICONTROL adobe.target.getOffers()]检索到的多个选件。<P>**注意：**&#x200B;此函数已在at.js 2.x中引入。 此函数不适用于at.js版本1.*x*。 |
| [[!UICONTROL adobe.target.triggerView (viewName， options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-triggerview-atjs-2.md)<P>(at.js 2.x) | 每当加载新页面或重新渲染页面上的组件时，都可以调用此函数。<P> 应该为单页应用程序(SPA)实施此函数，以便使用[!UICONTROL 可视化体验编辑器] (VEC)创建[!UICONTROL A/B测试]和[!UICONTROL 体验定位] (XT)活动。 |
| [[!UICONTROL adobe.target.trackEvent(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md) | 此函数会触发用户操作（例如点击和转化）报告请求。 它不会在响应中交付活动。 |
| [[!UICONTROL mboxCreate(mbox，params)]](/help/dev/implement/client-side/atjs/atjs-functions/mboxcreate-atjs.md)<P>(at.js 1.x) | 可使用 mboxDefault 类名称执行请求并将产品建议应用到最近的 DIV。<P>**注意：**&#x200B;此函数仅适用于at.js版本1.*x*。 此函数已在at.js 2.x版本中弃用。 如果与at.js 2.x一起使用，此函数将返回默认内容。 |
| [[!UICONTROL mboxDefine(options)]和[!UICONTROL mboxUpdate(options)]](/help/dev/implement/client-side/atjs/atjs-functions/mboxdefine-mboxupdate-atjs-1x.md)<P>(at.js 1.x) | 定义和更新 mbox。<P>**注意：**&#x200B;此函数仅适用于at.js版本1.*x*。 此函数已在at.js 2.x版本中弃用。 如果与at.js 2.x一起使用，此函数将返回默认内容。 |
| [[!UICONTROL targetGlobalSettings(options)]](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md) | 您可以使用`[!UICONTROL targetGlobalSettings()]`覆盖at.js库中的设置，而不是在[!DNL Target Standard/Premium] UI中或通过使用REST API来配置它们。<ul><li>数据提供程序：通过此设置，客户可以从第三方数据提供程序收集数据，例如 Demandbase、BlueKai 和自定义服务，并将这些数据作为全局 mbox 请求中的 mbox 参数传递给 Target。</li></ul> |
| [[!UICONTROL targetPageParams(options)]](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md) | 此方法允许您从请求代码外部将参数附加到全局 mbox。 |
| [[!UICONTROL targetPageParamsAll(options)]](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparamsall.md) | 此方法允许您从请求代码外部将参数附加到所有 mbox。 |
| [[!UICONTROL 注册扩展（选项）]](/help/dev/implement/client-side/atjs/atjs-functions/registerextension-atjs-1x.md)<P>(at.js 1.x) | 可提供用于注册特定扩展的标准方法。<P>**注意：**&#x200B;此函数仅适用于at.js版本1.*x*。 此函数已在at.js 2.x版本中弃用。 如果与at.js 2.x一起使用，此函数将返回默认内容。 |
| [[!UICONTROL at.js自定义事件]](/help/dev/implement/client-side/atjs/atjs-functions/atjs-custom-events.md) | 通过 at.js 自定义事件，您可以知道 mbox 请求或产品建议何时成功或失败。 |
| [[!UICONTROL adobe.target.sendNotifications(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21.md)<P>(at.js 2.1.0) | 在不使用`[!UICONTROL adobe.target.applyOffer()]`或`[!UICONTROL adobe.target.applyOffers()]`呈现体验时，此函数会向[!DNL Target]边缘发送通知。<P>**注意**：此函数已在at.js 2.1.0中引入，可用于2.1.0以上的任何版本。 |
