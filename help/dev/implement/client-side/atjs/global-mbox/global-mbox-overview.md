---
keywords: 全局mbox，实施at.js
description: 了解 [!DNL Adobe Target], a name used to refer to the single server call made at the top of each web page in your [!DNL Target] 实施中的全局mbox。
title: 什么是全局mbox？
feature: at.js
exl-id: 572c1dc6-5cdd-427a-9458-e5ec49990cf8
TQID: https://experienceleague.adobe.com/MXEGvHHY8tFMfS6bMHcZYaG9mZtOWEkuODKH24JifZI
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 201
ht-degree: 61%

---

# 了解全局 mbox

有关全局mbox的信息，该名称用于引用[!DNL Adobe Target]实施中每个网页顶部发出的单个服务器调用。

默认情况下，全局 mbox 将名为 `target-global-mbox`。 如有必要，可以为您的帐户重命名全局 mbox。

常规 mbox（非全局 mbox）和全局 mbox 之间存在以下几点差异：

| 常规 mbox | 全局 mbox |
|--- |--- |
| 常规 mbox 通常使用 `<DIV>` 标记来封装内容。 | 全局 mbox 是“空的”，并未封装任何内容。 |
| 一个常规 mbox 只能交付一个活动中的内容。 | 对全局 mbox 的一个响应可以交付多个活动中的内容。 |

如果通过全局mbox或多个常规mbox交付多个活动，则Target [确定将活动（或多个活动）交付到网页的优先级](https://experienceleague.adobe.com/docs/target/using/activities/priority.html)。

使用 [!DNL Target] 函数，可以将其他页面级别数据与全局 mbox 一起发送到 `[!UICONTROL targetPageParams]`。 这类似于 mbox 参数功能。 有关更多信息，请参阅[将参数传递到全局 Mbox](/help/dev/implement/client-side/atjs/global-mbox/pass-parameters-to-global-mbox.md)。
