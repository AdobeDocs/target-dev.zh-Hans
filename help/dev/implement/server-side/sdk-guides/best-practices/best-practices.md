---
title: 使用设备上决策时的最佳实践
description: 了解使用时的最佳实践 [!UICONTROL 设备上决策] 在 [!DNL Adobe Target]
feature: Implement Server-side
exl-id: a0ca014d-ad9f-4ecc-961d-cb7ba236507f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 2%

---

# 最佳实践

[!DNL Adobe] 建议在使用时遵循以下最佳实践 [!UICONTROL 设备上决策]：

## 当决策方法为“设备端”时的最佳实践

将“设备端”用作决策方法时，如果访客是首次加载网页，则会下载构件。 只有在完全下载工件后，才会在首次页面加载（无缓存）时需要进行的任何活动鉴别。 您可以遵循某些最佳实践，以确保新的匿名访客能够快速获得活动资格。

* 取消激活不在工件中的支持“设备端”的活动。
* 如果您有Target Premium，则可以使用 [属性/工作区](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=zh-Hans) 为不同的工作区创建不同的工件文件。
* 如果工件文件由于合法原因变得非常大，则可以使用“混合”决策方法。 此方法允许您并行下载工件，所有Target API调用都会通过在线进行，直到下载工件为止。 请阅读下面有关“混合”决策模式的最佳实践部分，了解有关此方法的更多信息。
* 如果您有一个单页应用程序(SPA)， [!DNL Adobe] 建议在首次加载页面期间加载应用程序的主JavaScript文件之前，加载并初始化at.js。 这种方法可以更早地启动工件下载，从而提供更快的体验渲染。

## 当决策方法为“混合”时的最佳实践

使用“混合”作为决策方法时，将并行下载工件。 在下载工件之前，任意 [!DNL Target] 即使“位置”在设备上可用，API调用也会通过线路。 这是所有用户的默认设置 `getOffers()` 调用并在大多数情况下提供最佳性能。 如果更改以下项的默认行为 `getOffers()` 通过设置 `decisioningMethod` 到 `on-device`，请按照这些最佳实践操作，以避免错误并确保获得最佳性能。

* 如果您决定致电 `getOffers()` 替换为 `decisioningMethod` 作为 `on-device` 首次加载页面时，必须在“ARTIFACT_DOWNLOAD_SUCCEEDED”at.js事件处理程序中执行此操作以避免出现错误。 如果您的工件非常大，则任何使用此方法的“位置”仅在工件完全下载后才会渲染，这可能会延迟体验渲染。 [!DNL Adobe] 建议很少使用此方法。 使用此方法时，请按照上面“设备上”最佳实践部分下的最佳实践来减小工件大小。
