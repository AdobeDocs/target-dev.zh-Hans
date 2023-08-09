---
keywords: qa，预览，预览链接，移动设备，移动设备预览
description: 使用移动设备预览链接对移动设备应用程序活动执行端到端QA。 您无需特殊的测试设备即可注册不同的体验。
title: 如何在中使用移动设备预览链接 [!DNL Target] 手机？
feature: Implement Mobile
exl-id: c0c4237a-de1f-4231-b085-f8f1e96afc13
source-git-commit: cf39b35e208a99114b3f97df2e9ef7eb8a46e153
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 57%

---

# [!DNL Target] 移动设备预览

使用移动预览链接可对移动设备应用程序活动轻松执行端到端 QA，并且无需任何特殊的测试设备即可在您的设备上感受到不同的体验。

## 概述

通过移动设备预览功能，您可以在启动移动设备应用程序活动之前，对其进行全面测试。

## 先决条件

1. **使用受支持的 SDK 版本：**&#x200B;移动设备预览功能要求您在相应的应用程序中下载并安装适当的 Adobe Mobile SDK 4.14（或更高）版本。

   有关下载适当SDK的说明，请参阅 [当前SDK版本](https://developer.adobe.com/client-sdks/documentation/current-sdk-versions/){target=_blank} 在 *[!DNL Adobe Experience Platform Mobile SDK]* 文档。

1. **设置 URL 方案：**&#x200B;预览链接需使用 URL 方案来打开应用程序。您必须为预览指定一个唯一的 URL 方案。

   有关更多信息，请参阅 [可视化预览](https://developer.adobe.com/client-sdks/documentation/adobe-target/#visual-preview){target=_blank} 在 *Adobe Target* 在 *[!DNL Adobe Experience Platform Mobile SDK]* 文档。

   以下链接包含更多信息：

   * **iOs**：有关为iOS设置URL方案的更多信息，请参阅 [为您的应用程序定义自定义URL方案](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app){target=_blank} 在Apple开发人员网站上。
   * **Android**：有关为Android设置URL方案的更多信息，请参阅 [创建指向应用程序内容的深层链接](https://developer.android.com/training/app-links/deep-linking){target=_blank} Android开发人员网站上的。

1. **设置 `collectLaunchInfo` API**

   有关更多信息，请参阅 [可视化预览](https://developer.adobe.com/client-sdks/documentation/adobe-target/#visual-preview){target=_blank} 在 *Adobe Target* 在 *[!DNL Adobe Experience Platform Mobile SDK]* 文档。

## 生成预览链接

1. 在 [!DNL Target] 在UI中，单击 **[!UICONTROL 更多选项]** 图标（垂直省略号），然后选择 **[!UICONTROL 创建移动设备预览]**.

   ![替代图像](assets/mobile-preview-create.png)

1. 选择要预览的活动，然后单击 **[!UICONTROL 生成移动设备预览链接]**.

   >[!NOTE]
   >
   >只能选择基于表单的 AB 活动和 XT 活动。

   ![替代图像](assets/mobile-preview-select-activities.png)

1. 指定应用程序的 URL 方案。

   这需要与您的 iOS 或 Android 应用程序中存在的方案相同。如有需要，请分别对 iOS 和 Android 重复此过程。

   ![替代图像](assets/mobile-preview-enter-url-scheme.png)

1. 单击&#x200B;**[!UICONTROL 生成移动设备预览链接]**，然后复制该链接。

   ![替代图像](assets/mobile-preview-generate-and-copy.png)

## 在设备上预览

在安装了您的应用程序的设备上，使用移动设备浏览器打开链接。此应用程序可以是您从 Apple App Store 或 Google Play 商店下载的生产应用程序。此应用程序不必是某个特殊版本。如果您有一个有效的预览链接，您便能够在设备上查看体验。

1. 在移动设备浏览器中打开链接。

   共享您在上一步中复制的来自的链接 [!DNL Target] 以方便的方式访问移动设备的UI，例如使用文本、电子邮件或Slack。

   |![预览深层链接 1](assets/mobile-preview-open-deeplink.png)|![预览深层链接 2](assets/mobile-preview-open-app.png)|

   您的应用程序随即会打开，并启动 [!DNL Target] 移动设备预览模式。

1. 选择要查看的体验组合，然后单击&#x200B;**[!UICONTROL 启动体验]**。

   |![移动设备预览 1](assets/mobile-preview-experience-selection-1.png)|![移动设备预览 2](assets/mobile-preview-experience-result-1-france.png)|![移动设备预览 3](assets/mobile-preview-experience-result-1-shipfree.png)|
|![移动设备预览 4](assets/mobile-preview-experience-selection-2.png)|![移动设备预览 5](assets/mobile-preview-experience-result-2-aus.png)|![移动设备预览 6](assets/mobile-preview-experience-result-2-10off.png)|

## 限制

* 单击“**[!UICONTROL 启动体验]**”按钮后，必须重新加载视图，才能显示新内容。最简单的方式是先切换到另一个屏幕，然后再返回到您期待发生更改的屏幕。
* 低于 API-19 (KitKat) 的 Android 版本不支持移动设备预览功能。
