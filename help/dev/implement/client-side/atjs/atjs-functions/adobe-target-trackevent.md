---
keywords: adobe.target.trackEvent， trackEvent， trackevent，跟踪事件， at.js，函数，函数， preventDefault， preventdefault，阻止默认值， adobe.target.trackEvent
description: 对 [!DNL Adobe Target] at.js JavaScript库使用[!UICONTROL adobe.target.trackEvent()]函数以触发报告用户操作（如网站上的点击次数和转化次数）的请求。
title: 如何使用[!UICONTROL adobe.target.trackEvent()]函数？
feature: at.js
exl-id: 9a55e4f1-d7f9-47c1-867c-2ce06fb26f9f
TQID: https://experienceleague.adobe.com/Jib9C5FvmsgIF6CA-0UbdMdnMiXxQCkU2-O3Zys3vrY
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
source-git-commit: 07d851e2344279caeae25e4823ca86b9c17efd63
workflow-type: tm+mt
source-wordcount: 336
ht-degree: 59%

---

# [!UICONTROL adobe.target.trackEvent(options)]

此函数会触发用户操作（例如点击和转化）报告请求。 它不会在响应中交付活动。

这些事件跟踪 mbox 调用可以用来定义活动中的量度。 有关更多信息，请参阅[成功量度](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html?lang=zh-Hans)和[跟踪转化](../how-to-deployatjs/implement-target-without-a-tag-manager.md#track-conversions)。

以下是该 API 的详细信息：

| 键 | 类型 | 必需 | 描述 |
|--- |--- |--- |--- |
| mbox | 字符串 | 是 | Mbox 名称<P>**注意**：如果[!UICONTROL trackEvent()]调用是使用页面上已触发的mbox名称触发的，则[!UICONTROL trackEvent()]的SDID将被重置，并且将与页面上的[!DNL Target]调用不同。 但是，使用不同的mbox名称触发[!UICONTROL trackEvent()]调用会使[!UICONTROL trackEvent()]调用的SDID与页面上的[!UICONTROL 页面加载请求]/[!UICONTROL triggerView()]调用一致。 |
| selector | 字符串 | 否 | 用于查找 HTML 元素的 CSS 选择器。 事件监听程序将附加到找到的元素。 |
| type | 字符串 | 否 | 表示已注册的事件类型。 它既可以是 HTML 已知的事件，如：click、mousedown 等，也可以是自定义 HTML 事件。 |
| preventDefault | 布尔值 | 否 | 表示是否在事件监听程序回调中使用 `[!UICONTROL event.preventDefault()]`。 默认为 false。<P>**注释**：仅支持`[!UICONTROL form[submit]]`和`a[click]`。 由于复杂性和要支持的方案数量太多，因此其他方案不受支持。 |
| 参数 | 对象 | 否 | Mbox 参数。 键值对这一对象具有以下结构：<P>`{ "param1": "value1", "param2": "value2"}` |
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


