---
keywords: 全局mbox，自定义全局mbox，编辑at.js， at.js，实施at.js
description: 了解如何在上为at.js自定义全局mbox [!UICONTROL 管理]-[!UICONTROL 实现] 页面位置 [!DNL Adobe Target].
title: 如何自定义全局mbox？
feature: at.js
exl-id: f7809c3d-6e77-4bbe-8da3-4ab0a448c801
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 17%

---

# 自定义全局 mbox

帮助您自定义的信息 [!DNL Adobe Target] 适用于at.js的全局mbox。

1. 单击&#x200B;**[!UICONTROL “管理”]**>**[!UICONTROL “实现”]**。

1. 禁用 **[!UICONTROL 已启用页面加载（自动创建全局mbox）]**，然后添加要从中交付活动的自定义全局mbox的名称 [!DNL Target].

>[!WARNING]
>
>当您选择其他全局mbox时，会自动保存更改。

此自定义全局 mbox 还用于点击跟踪。

![custom-global-mbox](../../assets/custom-global-mbox.png)

1. 在您的网站上实施at.js库。

   请参阅 [如何部署at.js](/help/dev/implement/client-side/atjs/how-to-deployatjs/how-to-deployatjs.md) 以了解更多信息。

1. 在您的版本中安排进行转换。

   当您准备好时 [!DNL Target] 要在以后开始将全局mbox用于所有活动，您可以继续此步骤。

   更新自定义全局 mbox 的名称，以使其匹配上面步骤 2 中所使用的名称。


>[!WARNING]
>
>您帐户中的所有活动均与此mbox同步。 确保您的网站上存在全局mbox，以便活动可以继续正常运行。 请务必编辑并重新保存使用创建的受影响活动。 [!UICONTROL 可视化体验编辑器] (VEC)与此mbox同步。 无需重新保存在中创建的活动 [!UICONTROL 基于表单的体验编辑器] 或通过API。
