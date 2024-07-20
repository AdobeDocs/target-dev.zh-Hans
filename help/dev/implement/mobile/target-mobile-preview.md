---
keywords: qa，预览，预览链接，移动设备，移动设备预览
description: 使用移动设备预览链接对移动设备应用程序活动执行端到端QA。
title: 如何在 [!DNL Adobe Target] 移动设备中使用移动设备预览链接？
feature: Implement Mobile
exl-id: c0c4237a-de1f-4231-b085-f8f1e96afc13
source-git-commit: 15e42d0fb049f9243ff5468ff5f22a8e79c55c79
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 23%

---

# [!DNL Target]移动设备预览

使用移动设备预览链接可对移动设备应用程序活动轻松执行端到端QA，并且无需任何特殊的测试设备即可在使用您的设备的不同体验中注册。

通过移动设备预览功能，您可以在启动移动设备应用程序活动之前，对其进行全面测试。

## 先决条件

1. **使用支持的SDK版本：**&#x200B;移动设备预览功能要求您下载相应的[!DNL Adobe Mobile SDK]版本并在相应的应用程序中安装。

   有关下载适当SDK的说明，请参阅&#x200B;*[!DNL Adobe Experience Platform Mobile SDK]*&#x200B;文档中的[当前SDK版本](https://developer.adobe.com/client-sdks/documentation/current-sdk-versions/){target=_blank}。

1. **设置 URL 方案：**&#x200B;预览链接需使用 URL 方案来打开应用程序。为预览指定唯一的URL方案。

   有关详细信息，请参阅&#x200B;*[!DNL Mobile SDK]*&#x200B;文档中的&#x200B;*在数据连接UI*&#x200B;中配置Target扩展中的[可视化预览](https://developer.adobe.com/client-sdks/documentation/adobe-target/#visual-preview){target=_blank}。

   以下链接包含更多信息：

   * **iOs**：有关为iOS设置URL方案的详细信息，请参阅&#x200B;*Apple Developer*&#x200B;网站上的[为您的应用程序定义自定义URL方案](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app){target=_blank}。
   * **Android**：有关为Android设置URL方案的详细信息，请参阅&#x200B;*Android开发人员*&#x200B;网站上的[创建指向应用程序内容的深层链接](https://developer.android.com/training/app-links/deep-linking){target=_blank}。

1. **设置`collectLaunchInfo` API（仅限i0S）**

   有关详细信息，请参阅&#x200B;*[!DNL Mobile SDK]*&#x200B;文档中的&#x200B;*在数据连接UI*&#x200B;中配置Target扩展中的[可视化预览](https://developer.adobe.com/client-sdks/documentation/adobe-target/#visual-preview){target=_blank}。

## 生成预览链接

1. 在[!DNL Target]用户界面中，单击&#x200B;**[!UICONTROL More Options]**&#x200B;图标（垂直省略号），然后选择&#x200B;**[!UICONTROL Create Mobile Preview Link]**。

   ![替代图像](assets/mobile-preview-create.png)

1. 选择要预览的活动，然后单击&#x200B;**[!UICONTROL Generate Mobile Preview Link]**。

   >[!NOTE]
   >
   >您只能选择基于表单的[!UICONTROL A/B Test]和[!UICONTROL Experience Targeting] (XT)活动。

   ![替代图像](assets/mobile-preview-select-activities.png)

1. 指定应用程序的 URL 方案。

   URL方案必须与iOS或Android应用程序中提供的方案相同。 如有必要，请分别对iOS和Android重复此过程。

   ![替代图像](assets/mobile-preview-enter-url-scheme.png)

1. 单击&#x200B;**[!UICONTROL Generate Mobile Preview Link]**，然后复制链接。

   ![替代图像](assets/mobile-preview-generate-and-copy.png)

## 在设备上预览

在安装了您的应用程序的设备上，使用移动设备浏览器打开链接。此应用可以是您从[!DNL Apple App Store]或[!DNL Google Play Store]下载的生产应用。 该应用程序不需要是一个特殊的内部版本。 如果您有一个活动的预览链接，则可以查看设备上的体验。

1. 在移动设备浏览器中打开链接。

   以方便的方式将您在上一部分中从[!DNL Target] UI复制的链接共享到移动设备，例如使用文本、电子邮件或[!DNL Slack]。

   |![预览深层链接 1](assets/mobile-preview-open-deeplink.png)|![预览深层链接 2](assets/mobile-preview-open-app.png)|

   您的应用程序将打开并启动[!DNL Target] [!UICONTROL Mobile Preview Mode]。

1. 选择要查看的体验组合，然后单击&#x200B;**[!UICONTROL Launch Experiences]**。

   |![移动设备预览 1](assets/mobile-preview-experience-selection-1.png)|![移动设备预览 2](assets/mobile-preview-experience-result-1-france.png)|![移动设备预览 3](assets/mobile-preview-experience-result-1-shipfree.png)|
|![移动设备预览 4](assets/mobile-preview-experience-selection-2.png)|![移动设备预览 5](assets/mobile-preview-experience-result-2-aus.png)|![移动设备预览 6](assets/mobile-preview-experience-result-2-10off.png)|

## 限制

* 单击&#x200B;**[!UICONTROL Launch Experiences]**&#x200B;按钮后，必须再次加载视图才能显示新内容。 最简单的方式是先切换到另一个屏幕，然后再返回到您期待发生更改的屏幕。
* 低于 API-19 (KitKat) 的 Android 版本不支持移动设备预览功能。
