---
keywords: adobe.target.triggerView， triggerView， triggerview， trigger view， at.js，函数，函数， viewName， viewname，视图名称， adobe.target.triggerView1
description: 将adobe.target.triggerView()函数用于 [!DNL Adobe Target] at.js JavaScript库，用于单页应用程序(SPA)。 (at.js 2.x)
title: 如何使用adobe.target.triggerView()函数？
feature: at.js
exl-id: d6130c56-4e77-4668-ad21-a5b335f8b234
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 37%

---

# adobe.target.triggerView (viewName, options) - at.js 2.x

每当加载新页面或重新渲染页面上的组件时，都可以调用此函数。`adobe.target.triggerView()` 应为单页应用程序(SPA)实施，以使用 [!UICONTROL 可视化体验编辑器] (VEC)以创建 [!UICONTROL A/B测试] 和 [!UICONTROL 体验定位] (XT)活动。 如果 `[!UICONTROL adobe.target.triggerView()]` 未在网站上实施，VEC无法用于SPA。 有关更多信息，请参阅[单页应用程序实施](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md)。

>[!NOTE]
>
>此函数已在at.js 2.*x*.此函数不适用于at.js版本1.*x*。

| 参数 | 类型 | 必需？ | 描述 |
| --- | --- | --- | --- |
| viewName | 字符串 | 是 | 将任何名称作为要显示视图的字符串类型传递。此视图名称显示在 [!UICONTROL 修改] 供营销人员创建操作并运行其的VEC面板 [!UICONTROL A/B测试] 和 [!UICONTROL 体验定位] XT活动。 |
| options | 对象 | 否 |  |
| options > page | 布尔值 | 否 | **TRUE：** page 的默认值为 true。当 page=true 时，将向 [!DNL Target] 后端发送增加展示次数计数的通知。<P>默认情况下，当 `[!UICONTROL triggerView]` 调用，但options > page设置为false时除外。<P>**FALSE：**&#x200B;当 page=false 时，将不会发送增加展示次数计数的通知。当您只想在具有选件的页面上重新呈现组件时，才应该使用此方法。<P>**注意**：在以下情况下，不会重新呈现VEC中的自定义代码选件： `[!UICONTROL triggerView()]` 调用方法 `{page: false}` 作为选项。 |

## 示例：True

`[!UICONTROL triggerView()]`[!DNL Target] 调用向 后端发送增加活动展示次数和其他量度的通知。

```javascript {line-numbers="true"}
adobe.target.triggerView("homeView")
```

## 示例：False

`[!UICONTROL triggerView()]`[!DNL Target] 调用不会向 后端发送增加展示次数计数的通知。

```javascript {line-numbers="true"}
adobe.target.triggerView("homeView", {page: false})
```

## 示例：Promise链接方式 `getoffers()` 和 `applyOffers()`

要执行 `triggerView()` 当 `getOffers()` promise得以解决，执行 `triggerView()` 在最后一个块上，如下面的示例所示。 这是VEC检测所必需的 `Views` 在创作模式下。

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
