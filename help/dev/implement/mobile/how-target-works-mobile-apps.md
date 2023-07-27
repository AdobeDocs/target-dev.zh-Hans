---
description: 了解如何使用 [!DNL Adobe Mobile SDK] 向移动设备应用程序访客显示最佳体验。
title: 如何 [!DNL Target] 在移动设备应用程序中工作？
feature: Implement Mobile
exl-id: 33001f01-fde6-48cb-ac02-d1a632b2150d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 34%

---

# 如何 [!DNL Target] 在移动设备应用程序中工作

此 [!DNL Adobe Mobile SDK] 联系 [!DNL Target] 服务器获取内容以及其他数据点，以便向用户显示正确的体验。

>[!IMPORTANT]
>
>支持 [!DNL Adobe Mobile] 版本4。*x* SDK已于2021年8月31日结束，不再建议用于 [!DNL Adobe Target] 移动用户。
>
>此 [适用于移动应用程序的Adobe Experience Platform SDK](https://developer.adobe.com/client-sdks/documentation/){target=_blank} 是推荐的电源解决方案 [!DNL Adobe Experience Cloud] 解决方案和服务。

## [!DNL Target] 位置和成功量度

*Target 位置*&#x200B;也称为 mbox。将会启用应用程序中的标识位置，以用于测试或个性化（例如，主页屏幕上的欢迎消息）。这些位置是在测试创建过程中标识的。

*[](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html)成功量度*&#x200B;是指用户执行的用于标识特定活动是否成功的操作（例如注册、购买、订票等等）。

![替代图像](assets/mobile-target-location.png)

* **[!DNL Target]位置：** 注册按钮下方显示的内容。

  在下午 6 点之前此特定用户可享受免运费优惠。此位置可在多个位置重复使用 [!DNL Target] 用于运行A/B测试和个性化的活动。

* **成功量度：** 用户点按注册按钮时执行的操作。

**了解如何 [!DNL Target] 在SDK中工作**

![替代图像](assets/how-target-mobile-works.png)
