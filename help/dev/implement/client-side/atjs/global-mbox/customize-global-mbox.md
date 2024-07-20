---
keywords: 全局mbox，自定义全局mbox，编辑at.js， at.js，实施at.js
description: 了解如何在 [!DNL Adobe Target]中的[!UICONTROL Administration]-[!UICONTROL Implementation]页面上为at.js自定义全局mbox。
title: 如何自定义全局mbox？
feature: at.js
exl-id: f7809c3d-6e77-4bbe-8da3-4ab0a448c801
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 18%

---

# 自定义全局 mbox

此信息可帮助您为at.js自定义[!DNL Adobe Target]全局mbox。

1. 单击&#x200B;**[!UICONTROL Administration]** > **[!UICONTROL Implementation]**。

1. 禁用&#x200B;**[!UICONTROL Page load enabled (Auto create global mbox)]**，然后添加从[!DNL Target]交付活动时要使用的自定义全局mbox的名称。

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
>您帐户中的所有活动均与此mbox同步。 确保您的网站上存在全局mbox，以便活动可以继续正常运行。 请务必编辑并重新保存使用与此mbox同步的[!UICONTROL Visual Experience Composer] (VEC)创建的受影响活动。 无需重新保存在[!UICONTROL Form-Based Experience Composer]中或通过API创建的活动。
