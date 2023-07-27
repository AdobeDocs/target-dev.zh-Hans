---
keywords: 选件，预取， iOS， android， sdk，移动， mobile sdk， 8美元
description: 使用 [!DNL Adobe Target] iOS和Android Mobile SDK中的预取功能，用于通过缓存服务器响应来尽量减少获取选件内容的次数。
title: 我能否预取移动设备应用程序的选件内容？
feature: Implement Mobile
exl-id: 6f8e8298-f1e9-46f0-828f-717c7d632077
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 39%

---

# 预取选件内容

[!DNL Target] 预取功能使用 iOS 和 Android Mobile SDK 获取选件内容，并通过缓存服务器响应来尽量减少获取次数。

>[!IMPORTANT]
>
>支持 [!DNL Adobe Mobile] 版本4。*x* SDK已于2021年8月31日结束，不再建议用于 [!DNL Adobe Target] 移动用户。
>
>此 [适用于移动应用程序的Adobe Experience Platform SDK](https://developer.adobe.com/client-sdks/documentation/){target=_blank} 是推荐的电源解决方案 [!DNL Adobe Experience Cloud] 解决方案和服务。

此过程可缩短加载时间，阻止多个网络调用，并允许 [!DNL Target] 接收有关移动设备应用程序用户访问了哪个 mbox 的通知。在预取调用期间将检索和缓存所有内容，对于以后所有包含指定 mbox 名称的缓存内容的调用，都将从缓存中检索该内容。

在iOS和Android Mobile SDK中使用预取方法时，请考虑以下限制：

* 在启动时，预取内容不会持久保留。只要应用程序处于活动状态，或者在调用 `clearPrefetchCache()` 方法之前，都会一直缓存预取内容。
* 不支持预取功能 [!UICONTROL 自动分配] 和 [!UICONTROL 自动定位] 流量分配方法，用于 [!UICONTROL Automated Personalization] 或 [!UICONTROL Recommendations] 活动类型，或 [A/B或XT活动中的推荐选件](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-as-an-offer.html).

有关更多信息（包括预取方法、公共类和代码示例），请参阅：

* **iOS：**  [在iOS中预取选件内容](https://experienceleague.adobe.com/docs/mobile-services/ios/target-ios/c-mob-target-prefetch-ios.html) 在 *Mobile Services iOS SDK帮助*.
* **Android：**  [在Android中预取选件内容](https://experienceleague.adobe.com/docs/mobile-services/android/target-android/c-mob-target-prefetch-android.html) 在 *Mobile Services Android SDK帮助*.
