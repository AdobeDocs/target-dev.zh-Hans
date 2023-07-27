---
keywords: 实施，实施， adobe launch， launch，竞争，重定向，体验platform launch，platform launch，标记， adobe platform，实施2
description: 了解如何实施 [!DNL Adobe Target] at.js库使用 [!DNL Adobe Experience Platform]，实施Target的首选方法。
title: 如何实施 [!DNL Target] 使用 [!DNL Adobe Experience Platform]？
feature: Implement Server-side
exl-id: 0a325871-194a-479c-a3bf-294e3dde3e9a
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 8%

---

# 使用 [!DNL Target] 实施 [!DNL Adobe Experience Platform]

中的标记 [!DNL Adobe Experience Platform] 是推出的新一代标签管理功能 [!DNL Adobe]. 标记为客户提供了一种简单的方式来部署和管理用来加强相关客户体验的分析、营销和广告标记。

>[!NOTE]
>
>Adobe Experience Platform Launch已更名为 [!DNL Adobe Experience Platform]. 因此，产品文档中的术语有一些改动。请参阅以下内容 [文档](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?) 以获取术语更改的综合参考。

下表列出了可在其中获取更多信息的各种源：

| 资源 | 详细信息 |
|--- |--- |
| [添加Adobe Target](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/implement-solutions/target.html#implement-solutions) | 本教程提供了实施的分步说明 [!DNL Target] 带有标记的网站中的 [!DNL Adobe Experience Platform]. 主题包括添加 at.js JavaScript 库、触发全局 mbox、添加参数，以及与其他解决方案集成。本文是一个庞大教程的一部分，该教程向您介绍了如何实施Adobe Experience Platform及其他Adobe Experience Cloud解决方案。 |
| [快速入门指南](https://experienceleague.adobe.com/docs/experience-platform/tags/get-started/quick-start.html) | 有关部署和管理为相关客户体验提供支持所需的分析、营销和广告标记的信息。 |
| [Adobe [!DNL Target] 扩展概述](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/target/overview.html) | 关于实施的信息 [!DNL Target] 使用 [!DNL Adobe Experience Platform]. |

## 使用实施at.js的优势 [!DNL Target] 扩展

以下优点仅适用于您在中使用标记的情况 [!DNL Adobe Experience Platform] 以实施at.js。 因此，Adobe强烈建议您在 [!DNL Adobe Experience Platform] 而不是手动实施at.js。

* **解决 [!DNL Adobe Analytics] 和 [!DNL Target] 竞争条件：** 因为 [!DNL Analytics] 调用可以在以下日期之前触发： [!DNL Target] 调用，该 [!DNL Target] 调用未拼合到 [!DNL Analytics] 呼叫。 此排序可能会导致数据不正确。 此 [!DNL Target] 扩展可确保 [!DNL Analytics] 信标调用将等待 [!DNL Target] 调用完成，无论成功与否。 使用中的标记 [!DNL Adobe Experience Platform] 解决了客户在手动实施时可能遇到的数据不一致问题。

  >[!NOTE]
  >
  >在中使用“发送信标”操作 [!DNL Adobe Analytics] 扩展以便 [!DNL Analytics] 呼叫等待 [!DNL Target] 呼叫。 如果您直接调用 `s.t()` 或 `s.tl()` 使用自定义代码， [!DNL Analytics] 呼叫不会等待 [!DNL Target] 调用完成。

* **阻止错误的重定向选件处理：** 如果您拥有 [!DNL Target] 和 [!DNL Analytics] 如果页面上存在Target执行的重定向选件，则您可能会遇到以下情况 [!DNL Analytics] 跟踪器触发不应触发的请求（因为用户将被重定向到其他URL）。 如果您实施 [!DNL Target] 和 [!DNL Analytics] 通过中的标记 [!DNL Adobe Experience Platform]，您将不会遇到此问题。 使用中的标记 [!DNL Adobe Experience Platform]， [!DNL Target] 指示 [!DNL Analytics] 中止 [!DNL Analytics] 信标请求。
