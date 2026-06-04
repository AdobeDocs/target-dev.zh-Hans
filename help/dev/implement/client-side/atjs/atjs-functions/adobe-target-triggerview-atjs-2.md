---
keywords: adobe.target.triggerView， triggerView， triggerview， trigger view， at.js，函数，函数， viewName， viewname，视图名称， adobe.target.triggerView1
description: 对 [!DNL Adobe Target] at.js JavaScript库使用adobe.target.triggerView()函数，以便在单页应用程序(SPA)中使用。 (at.js 2.x)
title: 如何使用adobe.target.triggerView()函数？
feature: at.js
exl-id: d6130c56-4e77-4668-ad21-a5b335f8b234
TQID: https://experienceleague.adobe.com/pBC1GRKG0mxeaZ1hfaByKv2tu-XScrSJfm7lUw-3yKw
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 446
ht-degree: 19%

---

# adobe.target.triggerView (viewName, options) - at.js 2.x

每当加载新页面或重新渲染页面上的组件时，都可以调用此函数。 应为单页应用程序(SPA)实施`adobe.target.triggerView()`以使用[!UICONTROL 可视化体验编辑器] (VEC)创建[!UICONTROL A/B测试]和[!UICONTROL 体验定位] (XT)活动。 如果未在网站上实施`[!UICONTROL adobe.target.triggerView()]`，则VEC无法用于SPA。 有关更多信息，请参阅[单页应用程序实施](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md)。

>[!NOTE]
>
>此函数已在at.js 2.*x*&#x200B;中引入。 此函数不适用于at.js版本1.*x*。

| 参数 | 类型 | 必需？ | 描述 |
| --- | --- | --- | --- |
| viewName | 字符串 | 是 | 将任何名称作为要显示视图的字符串类型传递。 此视图名称显示在VEC的[!UICONTROL 修改]面板中，供营销人员创建操作并运行其[!UICONTROL A/B测试]和[!UICONTROL 体验定位] XT活动。 |
| options | 对象 | 否 |  |
| options > page | 布尔值 | 否 | **TRUE：** page 的默认值为 true。 当 page=true 时，将向 [!DNL Target] 后端发送增加展示次数计数的通知。<P>调用`[!UICONTROL triggerView]`时，默认情况下始终会发送通知，但options > page设置为false时除外。<P>**FALSE：**&#x200B;当page=false时，将不会发送增加展示次数计数的通知。 当您只想在具有选件的页面上重新呈现组件时，才应该使用此方法。<P>**注意**：在将`{page: false}`作为选项调用`[!UICONTROL triggerView()]`时，不会重新呈现VEC中的自定义代码选件。 |

## 示例：True

`[!UICONTROL triggerView()]`调用以向[!DNL Target]后端发送增加活动展示次数和其他量度的通知。

```javascript {line-numbers="true"}
adobe.target.triggerView("homeView")
```

## 示例：False

`[!UICONTROL triggerView()]`调用不会向[!DNL Target]后端发送增加展示次数计数的通知。

```javascript {line-numbers="true"}
adobe.target.triggerView("homeView", {page: false})
```

## 示例：与`getoffers()`和`applyOffers()`链接的Promise

要在解析`getOffers()` promise时执行`triggerView()`，必须在最终块上执行`triggerView()`，如以下示例所示。 这是VEC在创作模式下检测`Views`所必需的。

```javascript {line-numbers="true"}
adobe.target.getOffers({
    'request': {
        'prefetch': {
            'views': [{
                'parameters': {}
            }]
        }
    }
}).then(function(response) {
    // Apply Offers
    adobe.target.applyOffers({
        response: response
    });
}).catch(function(error) {
    console.log("AT: getOffers failed - Error", error);
}).finally(() => {
    // Trigger View call, assuming pageView is defined elsewhere
    adobe.target.triggerView(pageView, {
        page: true
    });
    console.log('AT: View triggered on : ' + pageView);
});
```

## 示例： `triggerView()`与[!UICONTROL Adobe可视化编辑帮助程序扩展的最佳兼容性]

使用[Adobe可视化编辑帮助程序扩展](https://experienceleague.adobe.com/en/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension){target=_blank}时，请考虑以下事项：

由于[!DNL Googl]e为[!DNL Chrome]扩展添加了新的V3清单策略，[!UICONTROL 可视化编辑帮助程序扩展]必须等待`DOMContentLoaded`事件才能在VEC中加载[!DNL Target]库。 此延迟可能会导致网页在创作库准备就绪之前触发`triggerView()`调用，从而导致在加载时未填充视图。

要缓解此问题，请为页面`load`事件使用侦听器。

以下是实施示例：

```javascript
function triggerViewIfLoaded() {
    adobe.target.triggerView("homeView");
}

if (document.readyState === "complete") {
    // If the page is already loaded
    triggerViewIfLoaded();
} else {
    // If the page is not yet loaded, set up an event listener
    window.addEventListener("load", triggerViewIfLoaded);
}
```


