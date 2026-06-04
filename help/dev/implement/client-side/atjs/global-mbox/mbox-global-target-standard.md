---
keywords: 全局 mbox, Target Classic, 使用来自 Target Classic 的全局 mbox
description: 了解如何在您的页面上为旧版实施创建全局mbox时，为 [!DNL Adobe Target] 活动使用旧版全局mbox。
title: 我是否可以使用旧版实施中的全局mbox？
feature: at.js
exl-id: fe608b5e-ff66-4ba2-a622-d4f7307a9ca9
TQID: https://experienceleague.adobe.com/BCubNDwB8gxZ9bpuCNhxcnFnjB1xQK8ZRkLveinPj4w
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c1579802-ddd4-4214-8a91-97b2066abe11id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 304
ht-degree: 19%

---

# 使用旧版实施中的全局mbox

默认情况下，[!DNL Target]会创建一个名为target-global-mbox的全局mbox，用于运行在[!DNL Target]中创建的活动。 但是，如果您已在您的页面上为旧版实施创建了全局mbox，则可以将该mbox用于[!DNL Target]活动。

>[!NOTE]
>
>您的每一个帐户只能有一个全局 mbox。

要将现有的全局 mbox 用于 [!DNL Target] 和旧版实施，您必须设置一些参数。

1. 转到[!DNL Target]，然后单击&#x200B;**[!UICONTROL 管理]** > **[!UICONTROL 实现]**。

   默认情况下，**[!UICONTROL 页面加载已启用(自动创建全局mbox]**&#x200B;已启用，自定义全局mbox名为`target-global-mbox`。

1. 如果要使用现有mbox，请禁用&#x200B;**[!UICONTROL 启用页面加载(自动创建全局mbox]**，并在&#x200B;**[!UICONTROL 全局mbox]**&#x200B;字段中指定之前创建的全局mbox的名称。

   全局mbox下拉列表列出了您帐户中的所有mbox。 如果要使用尚不存在的mbox，请创建该mbox。

1. 单击&#x200B;**[!UICONTROL 保存]**。

   您的帐户设置已更新。

1. 下载新的at.js文件并在您的网站上引用它。

   所有现有的活动均已更新为使用指定的全局 mbox，包括之前已创建和实施的活动。

## 全局mbox实施疑难解答

以下常见问题解答可用于对全局mbox实施进行故障诊断：

### 为何全局mbox未加载？或为何页面加载时全局mbox的加载有所延迟？

确保at.js引用是页面上的第一个JavaScript调用。 有关此问题的其他解决方案，请参阅[全局mbox常见问题解答](/help/dev/implement/client-side/atjs/global-mbox/global-mbox-faq.md)。
