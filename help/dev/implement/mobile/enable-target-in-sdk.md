---
keywords: 移动设备应用程序, 移动设备应用程序 SDK, Target 移动设备应用程序, Mobile Target SDK, 在 SDK 中启用 Target
description: 了解如何将AdobeMobile Services SDK添加到您的移动应用程序。
title: 如何在 [!DNL Adobe Mobile SDK]中启用 [!DNL Target] ？
feature: Implement Mobile
exl-id: 4263b96a-23c8-4513-8302-00080122181d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 29%

---

# 在SDK中启用[!DNL Target]

将[!UICONTROL Adobe Mobile Services SDK]添加到您的应用程序。

>[!IMPORTANT]
>
>支持[!DNL Adobe Mobile]版本4。*x* SDK已于2021年8月31日结束，不再推荐用于[!DNL Adobe Target]移动用户。
>
>适用于移动设备应用程序的[Adobe Experience Platform SDK](https://developer.adobe.com/client-sdks/documentation/){target=_blank}是推荐的解决方案，旨在为您的移动设备应用程序中的[!DNL Adobe Experience Cloud]解决方案和服务提供支持。

1. 如果您尚未在应用程序中安装AdobeMobile Services SDK，请使用您的Analytics或Experience Cloud凭据从[AdobeMobile Services](https://mobilemarketing.adobe.com/)网站下载此SDK。

1. 将[!DNL Adobe Mobile Services SDK]添加到您的应用程序。

   您可以在[核心实施和生命周期](https://experienceleague.adobe.com/docs/mobile-services/ios/getting-started-ios/dev-qs.html)下找到相关说明。

1. 添加客户端代码和超时，并启用 SSL。

   在Experience Cloud中，打开Mobile Services，然后转到&#x200B;**[!UICONTROL Manage App Settings]** > **[!UICONTROL SDK Target Options]**。

   添加您的[!DNL Target]客户端代码和超时。 客户端代码是您的帐户或公司的唯一代码。超时是指[!DNL Target]在显示默认内容之前等待响应的时间（以秒为单位）。 确保在AdobeMobile Services的“管理应用程序设置”页面中选中&#x200B;**[!UICONTROL Use HTTPS]**&#x200B;选项。 如果未启用HTTPS，则iOS9+中的所有调用都将被阻止，除非您列入允许列表[!DNL Target]服务器。

   ![替代图像](assets/mobile-clientcode.png)

1. 创建/找到您的应用程序后，查找应用程序设置并下载所需的SDK。

   ![替代图像](assets/download-sdk.png)

>[!WARNING]
>
> 如果您无权访问移动设备营销界面，则可以直接在配置文件的应用程序代码中进行更改；不过，所做更改不会与用户界面中的设置页面同步。
