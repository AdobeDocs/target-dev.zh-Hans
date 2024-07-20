---
keywords: 全局 mbox, Target Classic, 使用来自 Target Classic 的全局 mbox
description: 了解如何在您的页面上为旧版实施创建全局mbox时，为 [!DNL Adobe Target] 活动使用旧版全局mbox。
title: 我是否可以使用旧版实施中的全局mbox？
feature: at.js
exl-id: fe608b5e-ff66-4ba2-a622-d4f7307a9ca9
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 20%

---

# 使用旧版实施中的全局mbox

默认情况下，[!DNL Target]会创建一个名为target-global-mbox的全局mbox，用于运行在[!DNL Target]中创建的活动。 但是，如果您已在您的页面上为旧版实施创建了全局mbox，则可以将该mbox用于[!DNL Target]活动。

>[!NOTE]
>
>您的每一个帐户只能有一个全局 mbox。

要将现有的全局 mbox 用于 [!DNL Target] 和旧版实施，您必须设置一些参数。

1. 转到[!DNL Target]，然后单击&#x200B;**[!UICONTROL Administration]** > **[!UICONTROL Implementation]**。

   默认情况下，**[!UICONTROL Page load enabled (Auto-create global mbox]**&#x200B;已启用，自定义全局mbox名为`target-global-mbox`。

1. 如果要使用现有的mbox，请禁用&#x200B;**[!UICONTROL Page load enabled (Auto-create global mbox]**，然后在&#x200B;**[!UICONTROL Global Mbox]**&#x200B;字段中指定之前创建的全局mbox的名称。

   全局mbox下拉列表列出了您帐户中的所有mbox。 如果要使用尚不存在的mbox，请创建该mbox。

1. 单击 **[!UICONTROL Save]**。

   您的帐户设置已更新。

1. 下载新的at.js文件并在您的网站上引用它。

   所有现有的活动均已更新为使用指定的全局 mbox，包括之前已创建和实施的活动。

## 全局mbox实施疑难解答

以下常见问题解答可用于对全局mbox实施进行故障诊断：

### 为何全局mbox未加载？或为何页面加载时全局mbox的加载有所延迟？

确保at.js引用是页面上的第一个JavaScript调用。 有关此问题的其他解决方案，请参阅[全局mbox常见问题解答](/help/dev/implement/client-side/atjs/global-mbox/global-mbox-faq.md)。
