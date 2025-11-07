---
keywords: at.js，函数， javascript库
description: 查看可用于 [!DNL Adobe Target]中at.js JavaScript库的1.x和2.x版本的函数的列表。
title: 我可以对at.js使用哪些函数？
feature: at.js
exl-id: 1efed365-8a74-4c85-bdb1-8daaaf53d642
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 58%

---

# at.js 函数

可与[!DNL Adobe Target] at.js JavaScript库一起使用的函数列表。 单击“函数”列中的链接以获取更多信息和示例。

| 函数 | 详细信息 |
| --- | --- |
| [[!UICONTROL adobe.target.getOffer(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffer.md) | 此函数会触发用于获取[!DNL Target]选件的请求。 使用 `adobe.target.applyOffer()` 来处理响应或使用您自己的成功处理。 |
| [[!UICONTROL adobe.target.getOffers(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)<P>(at.js 2.x) | 此函数允许您通过传递多个 mbox 来检索多个产品建议。此外，还可以针对活跃活动中的所有视图检索多个产品建议。<P>**注意：**&#x200B;此函数已在at.js 2.x中引入。此函数不适用于at.js版本1.*x*。 |
| [[!UICONTROL adobe.target.applyOffer(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffer.md) | 此函数用于应用响应内容。 |
| [[!UICONTROL adobe.target.applyOffers(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)<P>(at.js 2.x) | 此函数允许您应用 [!UICONTROL adobe.target.getOffers()] 检索到的多个产品建议。<P>**注意：**&#x200B;此函数已在at.js 2.x中引入。此函数不适用于at.js版本1.*x*。 |
| [[!UICONTROL adobe.target.triggerView (viewName, options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-triggerview-atjs-2.md)<P>(at.js 2.x) | 每当加载新页面或重新渲染页面上的组件时，都可以调用此函数。<P> 应该为单页应用程序(SPA)实施此函数，以便使用[!UICONTROL Visual Experience Composer] (VEC)创建[!UICONTROL A/B Test]和[!UICONTROL Experience Targeting] (XT)活动。 |
| [[!UICONTROL adobe.target.trackEvent(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md) | 此函数会触发用户操作（例如点击和转化）报告请求。它不会在响应中交付活动。 |
| [[!UICONTROL mboxCreate(mbox,params)]](/help/dev/implement/client-side/atjs/atjs-functions/mboxcreate-atjs.md)<P>(at.js 1.x) | 可使用 mboxDefault 类名称执行请求并将产品建议应用到最近的 DIV。<P>**注意：**&#x200B;此函数可用于at.js版本1.*x*。此函数已在 at.js 2.x 版本中弃用。如果与 at.js 2.x 一起使用，此函数将返回默认内容。 |
| [[!UICONTROL mboxDefine(options)] 和 [!UICONTROL mboxUpdate(options)]](/help/dev/implement/client-side/atjs/atjs-functions/mboxdefine-mboxupdate-atjs-1x.md)<P>(at.js 1.x) | 定义和更新 mbox。<P>**注意：**&#x200B;此函数可用于at.js版本1.*x*。此函数已在 at.js 2.x 版本中弃用。如果与 at.js 2.x 一起使用，此函数将返回默认内容。 |
| [[!UICONTROL targetGlobalSettings(options)]](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md) | 您可以使用`[!UICONTROL targetGlobalSettings()]`覆盖at.js库中的设置，而不是在[!DNL Target Standard/Premium] UI中或通过使用REST API来配置它们。<ul><li>数据提供程序：通过此设置，客户可以从第三方数据提供程序收集数据，例如 Demandbase、BlueKai 和自定义服务，并将这些数据作为全局 mbox 请求中的 mbox 参数传递给 Target。</li></ul> |
| [[!UICONTROL targetPageParams(options)]](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md) | 此方法允许您从请求代码外部将参数附加到全局 mbox。 |
| [[!UICONTROL targetPageParamsAll(options)]](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparamsall.md) | 此方法允许您从请求代码外部将参数附加到所有 mbox。 |
| [[!UICONTROL registerExtension(options)]](/help/dev/implement/client-side/atjs/atjs-functions/registerextension-atjs-1x.md)<P>(at.js 1.x) | 可提供用于注册特定扩展的标准方法。<P>**注意：**&#x200B;此函数可用于at.js版本1.*x*。此函数已在 at.js 2.x 版本中弃用。如果与 at.js 2.x 一起使用，此函数将返回默认内容。 |
| [[!UICONTROL at.js custom events]](/help/dev/implement/client-side/atjs/atjs-functions/atjs-custom-events.md) | 通过 at.js 自定义事件，您可以知道 mbox 请求或产品建议何时成功或失败。 |
| [[!UICONTROL adobe.target.sendNotifications(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21.md)<P>(at.js 2.1.0) | 在不使用[!DNL Target]或`[!UICONTROL adobe.target.applyOffer()]`呈现体验时，此函数会向`[!UICONTROL adobe.target.applyOffers()]`边缘发送通知。<P>**注意**：此函数已在at.js 2.1.0中引入，可用于2.1.0以上的任何版本。 |
