---
keywords: adobe.target.trackEvent， trackEvent， trackevent，跟踪事件， at.js，函数，函数， preventDefault， preventdefault，阻止默认值， adobe.target.trackEvent
description: 对 [!DNL Adobe Target] at.js JavaScript库使用[!UICONTROL adobe.target.trackEvent()]函数以触发报告用户操作（如网站上的点击次数和转化次数）的请求。
title: 如何使用[!UICONTROL adobe.target.trackEvent()]函数？
feature: at.js
exl-id: 9a55e4f1-d7f9-47c1-867c-2ce06fb26f9f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 62%

---

# [!UICONTROL adobe.target.trackEvent(options)]

此函数会触发用户操作（例如点击和转化）报告请求。它不会在响应中交付活动。

这些事件跟踪 mbox 调用可以用来定义活动中的量度。有关更多信息，请参阅[成功量度](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html?lang=zh-Hans)和[跟踪转化](../how-to-deployatjs/implement-target-without-a-tag-manager.md#track-conversions)。

以下是该 API 的详细信息：

| 键 | 类型 | 必需 | 描述 |
|--- |--- |--- |--- |
| mbox | 字符串 | 是 | Mbox 名称<P>**注意**：如果通过页面上已触发的mbox名称触发[!UICONTROL trackEvent()]调用，则[!UICONTROL trackEvent()]的SDID将重置，并且将与页面上的[!DNL Target]调用不同。 但是，使用不同的mbox名称触发[!UICONTROL trackEvent()]调用可使[!UICONTROL trackEvent()]调用的SDID与页面上的[!UICONTROL Page Load Request]/[!UICONTROL triggerView()]调用一致。 |
| selector | 字符串 | 否 | 用于查找 HTML 元素的 CSS 选择器。事件监听程序将附加到找到的元素。 |
| type | 字符串 | 否 | 表示已注册的事件类型。它既可以是 HTML 已知的事件，如：click、mousedown 等，也可以是自定义 HTML 事件。 |
| preventDefault | 布尔值 | 否 | 表示是否在事件监听程序回调中使用 `[!UICONTROL event.preventDefault()]`。默认为 false。<P>**注释**：仅支持`[!UICONTROL form[submit]]`和`a[click]`。 由于复杂性和要支持的方案数量太多，因此其他方案不受支持。 |
| 参数 | 对象 | 否 | Mbox 参数。键值对这一对象具有以下结构：<P>`{ "param1": "value1", "param2": "value2"}` |
| timeout | 数值 | 否 | 以毫秒为单位的超时时间。<P>如果未指定，则使用默认值：<P>`...timeoutInSeconds: 0.15...}` |
| success | 函数 | 否 | 用于表示该事件已报告的回调函数。 |
| error | 函数 | 否 | 用于表示该事件无法报告的回调函数。 |

## 示例

```javascript {line-numbers="true"}
<a href="https://asite.com">click me!</a> 
```

加上用于分配 `trackEvent` 的 javaScript 代码：

```javascript {line-numbers="true"}
<script> 
$('a').click(function(event){ 
  adobe.target.trackEvent({'mbox':'homePageHero'}) 
}); 
</script> 
```

或：

```javascript {line-numbers="true"}
adobe.target.trackEvent({ 
    "mbox": "clicked-cta", 
    "params": { 
        "param1": "value1" 
    } 
});
```

>[!WARNING]
>
>如果未设置必填字段，则不会执行请求，并会引发错误。
