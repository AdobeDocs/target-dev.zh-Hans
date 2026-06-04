---
keywords: 全局mbox，自定义全局mbox，编辑at.js， at.js，实施at.js
description: 了解如何在 [!DNL Adobe Target]中的[!UICONTROL 管理]-[!UICONTROL 实现]页面上为at.js自定义全局mbox。
title: 如何自定义全局mbox？
feature: at.js
exl-id: f7809c3d-6e77-4bbe-8da3-4ab0a448c801
TQID: https://experienceleague.adobe.com/MtbjwpKrZ-WmBnE5tBY74oJgQVB-zPLrCuFDrFshkGo
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
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 227
ht-degree: 16%

---

# 自定义全局 mbox

此信息可帮助您为at.js自定义[!DNL Adobe Target]全局mbox。

1. 单击&#x200B;**[!UICONTROL 管理]** > **[!UICONTROL 实现]**。

1. 禁用&#x200B;**[!UICONTROL 启用页面加载（自动创建全局mbox）]**，然后添加要用于从[!DNL Target]交付活动的自定义全局mbox的名称。

>[!WARNING]
>
>当您选择其他全局mbox时，会自动保存更改。

此自定义全局 mbox 还用于点击跟踪。

![custom-global-mbox](../../assets/custom-global-mbox.png)

1. 在您的网站上实施at.js库。

   有关详细信息，请参阅[如何部署at.js](/help/dev/implement/client-side/atjs/how-to-deployatjs/how-to-deployatjs.md)。

1. 在您的版本中安排进行转换。

   当您准备好让[!DNL Target]开始将您的全局mbox用于未来所有活动时，您可以继续此步骤。

   更新自定义全局 mbox 的名称，以使其匹配上面步骤 2 中所使用的名称。


>[!WARNING]
>
>您帐户中的所有活动均与此mbox同步。 确保您的网站上存在全局mbox，以便活动可以继续正常运行。 请务必编辑并重新保存使用与此mbox同步的[!UICONTROL 可视化体验编辑器] (VEC)创建的受影响活动。 无需重新保存在[!UICONTROL 基于表单的体验编辑器]中或通过API创建的活动。
