---
keywords: 实施，实施， adobe launch， launch，竞争，重定向， experience platform launch， platform launch，标记， adobe platform，实施2
description: 了解如何使用首选的Target实施方法 [!DNL Adobe Experience Platform]来实施 [!DNL Adobe Target] at.js库。
title: 如何使用 [!DNL Adobe Experience Platform]实施 [!DNL Target] ？
feature: Implement Server-side
exl-id: 0a325871-194a-479c-a3bf-294e3dde3e9a
TQID: https://experienceleague.adobe.com/5dXJlXYYvlu5sskrNED2j55SNmeggtWTb1jLgXRXAEo
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
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: ca4254966a337a0215d66bd28506128b9751d0e0
workflow-type: tm+mt
source-wordcount: 446
ht-degree: 4%

---

# 使用[!DNL Adobe Experience Platform]实施[!DNL Target]

[!DNL Adobe Experience Platform]中的标记是来自[!DNL Adobe]的下一代标记管理功能。 标记为客户提供了一种简单的方式来部署和管理用来加强相关客户体验的分析、营销和广告标记。

>[!NOTE]
>
>Adobe Experience Platform Launch已更名为[!DNL Adobe Experience Platform]中的一套数据收集技术。 因此，产品文档中的术语有一些改动。 有关术语更改的综合参考，请参阅以下[文档](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html？)。

下表列出了可在其中获取更多信息的各种源：

| 资源 | 详细信息 |
|--- |--- |
| [添加Adobe Target](https://experienceleague.adobe.com/docs/launch-learn/implementing-in-websites-with-launch/implement-solutions/target.html#implement-solutions) | 本教程提供了在网站中通过[!DNL Adobe Experience Platform]中的标记实施[!DNL Target]的分步说明。 主题包括添加 at.js JavaScript 库、触发全局 mbox、添加参数，以及与其他解决方案集成。 本文是一个庞大教程的一部分，该教程向您介绍了如何实施Adobe Experience Platform及其他Adobe Experience Cloud解决方案。 |
| [快速入门指南](https://experienceleague.adobe.com/docs/experience-platform/tags/get-started/quick-start.html) | 有关部署和管理为相关客户体验提供支持所需的分析、营销和广告标记的信息。 |
| [Adobe [!DNL Target] 扩展概述](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/target/overview.html) | 有关使用[!DNL Adobe Experience Platform]实现[!DNL Target]的信息。 |

## 使用[!DNL Target]扩展实施at.js的优势

以下优势仅适用于使用[!DNL Adobe Experience Platform]中的标记实施at.js的情况。 因此，Adobe强烈建议您在[!DNL Adobe Experience Platform]中使用标记，而不是手动实施at.js。

* **解决了[!DNL Adobe Analytics]和[!DNL Target]争用情况：**&#x200B;由于可以在[!DNL Target]调用之前触发[!DNL Analytics]调用，因此[!DNL Target]调用不会与[!DNL Analytics]调用相拼合。 此排序可能会导致数据不正确。 [!DNL Target]扩展可确保[!DNL Analytics]信标调用等待[!DNL Target]调用完成，无论是否成功。 使用[!DNL Adobe Experience Platform]中的标记可解决客户在手动实施时可能遇到的数据不一致问题。

  >[!NOTE]
  >
  >在[!DNL Adobe Analytics]扩展中使用Send Beacon操作，以便[!DNL Analytics]调用等待[!DNL Target]调用。 如果您使用自定义代码直接调用`s.t()`或`s.tl()`，则[!DNL Analytics]调用不会等到[!DNL Target]调用完成。

* **阻止错误的重定向选件处理：**&#x200B;如果您在页面上同时具有[!DNL Target]和[!DNL Analytics]，并且有一个重定向选件由Target执行，则您可能会遇到如下情况：[!DNL Analytics]跟踪器触发了不应触发的请求（因为用户将被重定向到不同的URL）。 如果您通过[!DNL Adobe Experience Platform]中的标记实施[!DNL Target]和[!DNL Analytics]，则不会遇到此问题。 使用[!DNL Adobe Experience Platform]中的标记，[!DNL Target]指示[!DNL Analytics]中止[!DNL Analytics]信标请求。



