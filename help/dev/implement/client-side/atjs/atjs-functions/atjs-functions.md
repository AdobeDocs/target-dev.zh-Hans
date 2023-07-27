---
keywords: at.js，函数， javascript库
description: 在中查看可与at.js JavaScript库1.x和2.x版本一起使用的函数列表 [!DNL Adobe Target].
title: 我可以对at.js使用哪些函数？
feature: at.js
exl-id: 1efed365-8a74-4c85-bdb1-8daaaf53d642
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 73%

---

# at.js 函数

可以结合使用的函数列表 [!DNL Adobe Target] at.js JavaScript库。 单击“函数”列中的链接以获取更多信息和示例。

| 函数 | 详细信息 |
| --- | --- | 
| [[!UICONTROL adobe.target.getOffer(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffer.md) | 此函数会触发用于获取 [!DNL Target] 选件。 使用 `adobe.target.applyOffer()` 来处理响应或使用您自己的成功处理。 |
| [[!UICONTROL adobe.target.getOffers(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)<P>(at.js 2.x) | 此函数允许您通过传递多个 mbox 来检索多个选件。此外，还可以针对活跃活动中的所有视图检索多个选件。<P>**注意：**&#x200B;此函数已在 at.js 2.x 中引入。但此函数不适用于 at.js 版本 1.*x*。 |
| [[!UICONTROL adobe.target.applyOffer(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffer.md) | 此函数用于应用响应内容。 |
| [[!UICONTROL adobe.target.applyOffers(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)<P>(at.js 2.x) | 此函数允许您应用检索到的多个选件 [!UICONTROL adobe.target.getOffers()].<P>**注意：**&#x200B;此函数已在 at.js 2.x 中引入。但此函数不适用于 at.js 版本 1.*x*。 |
| [[!UICONTROL adobe.target.triggerView (viewName, options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-triggerview-atjs-2.md)<P>(at.js 2.x) | 每当加载新页面或重新渲染页面上的组件时，都可以调用此函数。<P> 应该为单页应用程序(SPA)实施此函数，以便使用 [!UICONTROL 可视化体验编辑器] (VEC)以创建 [!UICONTROL A/B测试] 和 [!UICONTROL 体验定位] (XT)活动。 |
| [[!UICONTROL adobe.target.trackEvent(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md) | 此函数会触发用户操作（例如点击和转化）报告请求。它不会在响应中交付活动。 |
| [[!UICONTROL mboxCreate(mbox,params)]](/help/dev/implement/client-side/atjs/atjs-functions/mboxcreate-atjs.md)<P>(at.js 1.x) | 可使用 mboxDefault 类名称执行请求并将选件应用到最近的 DIV。<P>**注意：**&#x200B;此函数仅可用于 at.js 版本 1.*x*。此函数已在 at.js 2.x 版本中弃用。如果与 at.js 2.x 一起使用，此函数将返回默认内容。 |
| [[!UICONTROL mboxDefine(options)] 和 [!UICONTROL mboxUpdate(options)]](/help/dev/implement/client-side/atjs/atjs-functions/mboxdefine-mboxupdate-atjs-1x.md)<P>(at.js 1.x) | 定义和更新 mbox。<P>**注意：**&#x200B;此函数仅可用于 at.js 版本 1.*x*。此函数已在 at.js 2.x 版本中弃用。如果与 at.js 2.x 一起使用，此函数将返回默认内容。 |
| [[!UICONTROL targetGlobalSettings(options)]](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md) | 您可以使用覆盖at.js库中的设置 `[!UICONTROL targetGlobalSettings()]`，而不是在中配置它们 [!DNL Target Standard/Premium] 用户界面或使用REST API。<ul><li>数据提供程序：通过此设置，客户可以从第三方数据提供程序收集数据，例如 Demandbase、BlueKai 和自定义服务，并将这些数据作为全局 mbox 请求中的 mbox 参数传递给 Target。</li></ul> |
| [[!UICONTROL targetPageParams(options)]](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md) | 此方法允许您从请求代码外部将参数附加到全局 mbox。 |
| [[!UICONTROL targetPageParamsAll(options)]](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparamsall.md) | 此方法允许您从请求代码外部将参数附加到所有 mbox。 |
| [[!UICONTROL registerExtension(options)]](/help/dev/implement/client-side/atjs/atjs-functions/registerextension-atjs-1x.md)<P>(at.js 1.x) | 可提供用于注册特定扩展的标准方法。<P>**注意：**&#x200B;此函数仅可用于 at.js 版本 1.*x*。此函数已在 at.js 2.x 版本中弃用。如果与 at.js 2.x 一起使用，此函数将返回默认内容。 |
| [[!UICONTROL at.js 自定义事件]](/help/dev/implement/client-side/atjs/atjs-functions/atjs-custom-events.md) | 通过 at.js 自定义事件，您可以知道 mbox 请求或选件何时成功或失败。 |
| [[!UICONTROL adobe.target.sendNotifications(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21.md)<P>(at.js 2.1.0) | 此函数将通知发送至 [!DNL Target] 在不使用的情况下呈现体验时呈现边缘 `[!UICONTROL adobe.target.applyOffer()]` 或 `[!UICONTROL adobe.target.applyOffers()]`.<P>**注意**：此函数已在 at.js 2.1.0 中引入，可用于 2.1.0 以上的任何版本。 |
