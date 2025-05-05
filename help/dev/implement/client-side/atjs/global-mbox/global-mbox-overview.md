---
keywords: 全局mbox，实施at.js
description: 了解 [!DNL Adobe Target], a name used to refer to the single server call made at the top of each web page in your [!DNL Target] 实施中的全局mbox。
title: 什么是全局mbox？
feature: at.js
exl-id: 572c1dc6-5cdd-427a-9458-e5ec49990cf8
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 62%

---

# 了解全局 mbox

有关全局mbox的信息，该名称用于引用[!DNL Adobe Target]实施中每个网页顶部发出的单个服务器调用。

默认情况下，全局 mbox 将名为 `target-global-mbox`。如有必要，可以为您的帐户重命名全局 mbox。

常规 mbox（非全局 mbox）和全局 mbox 之间存在以下几点差异：

| 常规 mbox | 全局 mbox |
|--- |--- |
| 常规 mbox 通常使用 `<DIV>` 标记来封装内容。 | 全局 mbox 是“空的”，并未封装任何内容。 |
| 一个常规 mbox 只能交付一个活动中的内容。 | 对全局 mbox 的一个响应可以交付多个活动中的内容。 |

如果通过全局mbox或多个常规mbox交付多个活动，则Target [确定将活动（或多个活动）交付到网页的优先级](https://experienceleague.adobe.com/docs/target/using/activities/priority.html?lang=zh-Hans)。

使用 [!DNL Target] 函数，可以将其他页面级别数据与全局 mbox 一起发送到 `[!UICONTROL targetPageParams]`。这类似于 mbox 参数功能。有关更多信息，请参阅[将参数传递到全局 Mbox](/help/dev/implement/client-side/atjs/global-mbox/pass-parameters-to-global-mbox.md)。
