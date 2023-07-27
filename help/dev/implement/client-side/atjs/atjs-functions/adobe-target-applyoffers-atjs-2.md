---
keywords: adobe.target.applyOffers， applyOffers， applyoffers，应用选件， at.js，函数，函数，
description: 使用 [!UICONTROL adobe.target.applyOffers()] 函数 [!DNL Adobe Target] at.js JavaScript库以在响应中应用多个选件。 (at.js 2.x)
title: 如何使用 [!UICONTROL adobe.target.applyOffers()] 功能？
feature: at.js
exl-id: c391e3f4-fdf1-4e33-8dcb-6bf46e390538
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '813'
ht-degree: 85%

---

# [!UICONTROL adobe.target.applyOffers(options)] - at.js 2.x

此函数允许您应用 `adobe.target.getOffers()` 检索到的多个选件。

>[!NOTE]
>
>此函数已在at.js 2.*x*.此函数不适用于at.js版本1.*x*。

| 键值 | 类型 | 必需？ | 描述 |
| --- | --- | --- | --- |
| selector | 字符串 | 否 | HTML 元素或 CSS 选择器，用于标识 [!DNL Target] 应将选件内容放置在其中的 HTML 元素。如果未提供选择器， [!DNL Target] 假定要使用的HTML元素为HTMLHEAD。 |
| 响应 | 对象 | 是 | 来自 `getOffers()` 的响应对象。<br />请参阅下文的“请求”表。 |

## 响应

>[!NOTE]
>
>请参阅 [交付API文档](/help/dev/implement/delivery-api/overview.md) 有关下面列出的所有字段的可接受类型的信息。

| 字段名称 | 描述 |
| --- | --- |
| response > prefetch > views > options > content | 请注意，“options”内容的定义不明确，将直接取决于选项类型/模板结构。 |
| response > prefetch > views > options > type | 选项类型。反映“content”字段的类型。受支持的类型是“action”。 |
| response > prefetch > views > state | 应该与视图的显示通知一起转发的不透明视图状态令牌 |
| response > prefetch > views > options > responseTokens | 包含在处理当前选项时收集的 `responseTokens` 映射。 |
| response > prefetch > views > analytics > payload | [!DNL Analytics]用于客户端集成的 有效负荷，应在应用视图后将其发送到 [!DNL Analytics] |
| response > prefetch > views > trace | 包含每个视图预取调用的所有跟踪数据的对象。<br />跟踪对象还将包含跟踪的版本。<br />跟踪对象还将包含当前视图的详细信息。 |
| response > prefetch > views > options > eventToken | 按选项完成事件日志记录。对于已应用的选项，应将相应的事件令牌添加到通知令牌列表。请注意，一个视图由多个选项组成。如果已应用并可看到所有选项，则需要将所有 `eventTokens` 包含在通知中。 |
| response > prefetch > views > name | 可读的视图名称。 |
| response > prefetch > views > metrics | 应监视并通知 [!DNL Target] 的报告量度。目前，仅支持点击量度。如果发生点击该元素的情况，则应收集相应的 `eventTokens` 并发送通知。 |
| response > prefetch > views > key | 可标识视图的键值或指纹。 |
| response > prefetch > views > id | 视图的 ID。 |
| response > notifications > id | 通知 ID。 |
| response > notifications > events > type | 通知、点击或显示的类型。 |
| response > notifications > events > trace | 针对通知事件的跟踪。 |
| response > notifications > events > token | 与通知事件一起发送的令牌。 |
| response > notifications > events > timestamp | 与通知事件一起发送的时间戳。 |
| response > notifications > events > errorCode | 如果通知失败，则代码将指明失败的原因。 |
| response > notifications > events | 为当前通知记录或未能记录的事件。 |
| response > notifications | 指示已记录或已失败的通知。 |
| response > execute > mboxes > mbox > trace | 包含单个 mbox 请求的所有跟踪数据的对象。 |
| response > execute > mboxes > mbox > responseTokens | 包含针对特定 mbox 请求执行的 `responseTokens` 映射。 |
| response > execute > mboxes > mbox > option > content | 请注意，“options”内容的定义不明确，将直接取决于选项类型/模板结构。 |
| response > execute > mboxes > mbox > option > type | 选项类型。反映“content”字段的类型。支持的类型包括：html、重定向、JSON 和动态。 |
| response > execute > mboxes > mbox > options | 响应选项。 |
| response > execute > mboxes > mbox > metrics > eventToken | 点击事件的令牌。 |
| response > execute > mboxes > mbox > metrics > type | &quot;click&quot; |
| response > execute > mboxes > mbox > metrics | 包含 `clickThrough` 量度列表。 |
| response > execute > mboxes > mbox > mbox | mbox 的名称。 |
| response > execute > mboxes > mbox >index | 表示响应用于请求中具有此索引的 mbox。 |
| response > execute > mboxes > mbox > analytics > payload | [!DNL Analytics]用于客户端集成的 有效负荷，应在应用 mbox 后将其发送到 [!DNL Analytics]（请参阅“启用 A4T 的营销活动”部分。） |
| response > execute > mboxes | 已执行的 mbox 列表。 |
| response > execute > pageLoad > options > content | 请注意，“options”内容的定义不明确，将直接取决于选项类型/模板结构。 |
| response > execute > pageLoad > options > type | 选项类型。反映“content”字段的类型。支持的类型包括：html、重定向、JSON、动态和操作。 |
| response > execute > pageLoad > options | 未按视图进行分组的选项（target-global-mbox + 活动中的选项，这些活动包含未按视图进行分组的视图）。 |
| response > execute > pageLoad > metrics | 未设置为属于特定视图的点击量度。 |
| response > execute > pageLoad > trace | 包含 pageLoad 请求的所有跟踪数据的对象。 |
| response > execute > pageLoad > analytics > payload | [!DNL Analytics]用于客户端集成的 有效负荷，应在应用页面加载内容后将其发送到 [!DNL Analytics]（请参阅“启用 A4T 的营销活动”部分。） |

## 示例 [!UICONTROL applyOffers()] 调用

```javascript {line-numbers="true"}
adobe.target.applyOffers({response:{
  "execute": {
    "pageLoad": {
      "options": [{
        "type": "html",
        "content": "page-load"
      },
      {
        "type": "actions",
        "content": [{
          "type": "setHtml",
          "content": "<h1>Container 1</h1>",
          "selector": "#container1",
          "cssSelector": "#container1"
        },
        {
          "type": "setHtml",
          "content": "<h3>Container 3</h3>",
          "selector": "#container3",
          "cssSelector": "#container3"
        }]
      }],
 
 
      "metrics": [{
        "type": "click",
        "selector": "#container1",
        "eventToken": "page-load-click-metric" 
      }]
    }
  }
}});
```

## 与链接的Promise调用示例 `[!UICONTROL getOffers()]` 和 `[!UICONTROL applyOffers()]`，因为这些函数基于Promise

```javascript {line-numbers="true"}
adobe.target.getOffers({...})
.then(response => adobe.target.applyOffers({ response: response }))
.then(() => console.log("Success"))
.catch(error => console.log("Error", error));
```

有关如何使用getOffers()的更多示例，请参阅getOffers [文档](adobe-target-getoffers-atjs-2.md)

### 页面加载请求示例


```javascript {line-numbers="true"}
adobe.target.getOffers({
    request: {
        execute: {
            pageLoad: {}
        }
    }
}).
then(response => adobe.target.applyOffers({ response: response }))
.then(() => console.log("Success"))
.catch(error => console.log("Error", error));
```
