---
keywords: 移动设备应用程序, 移动设备应用程序 SDK, Target 移动设备应用程序, Mobile Target SDK, 在 SDK 中启用 Target
description: 了解如何将Adobe Mobile Services SDK添加到您的移动应用程序。
title: 如何在 [!DNL Adobe Mobile SDK]中启用 [!DNL Target] ？
feature: Implement Mobile
exl-id: 4263b96a-23c8-4513-8302-00080122181d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 38%

---

# 在SDK中启用[!DNL Target]

将[!UICONTROL Adobe Mobile Services SDK]添加到您的应用程序。

>[!IMPORTANT]
>
>对[!DNL Adobe Mobile]版本4.*x* SDK的支持已于2021年8月31日终止，不再建议向[!DNL Adobe Target]移动用户提供。
>
>适用于移动设备应用程序的[Adobe Experience Platform SDK](https://developer.adobe.com/client-sdks/documentation/){target=_blank}是推荐的解决方案，旨在为移动设备应用程序中的[!DNL Adobe Experience Cloud]解决方案和服务提供支持。

1. 如果您尚未在应用程序中安装Adobe Mobile Services SDK，请使用您的Analytics或Experience Cloud凭据从[Adobe Mobile Services](https://mobilemarketing.adobe.com/)网站下载SDK。

1. 将[!DNL Adobe Mobile Services SDK]添加到您的应用程序。

   您可以在[核心实施和生命周期](https://experienceleague.adobe.com/docs/mobile-services/ios/getting-started-ios/dev-qs.html)下找到相关说明。

1. 添加客户端代码和超时，并启用 SSL。

   在 Experience Cloud 中，打开 Mobile Services，然后转到&#x200B;**[!UICONTROL 管理应用程序设置]** > **[!UICONTROL SDK Target 选项]**。

   添加您的[!DNL Target]客户端代码和超时。 客户端代码是您的帐户或公司的唯一代码。 超时是指[!DNL Target]在显示默认内容之前等待响应的时间（以秒为单位）。 请确保在 Adobe Mobile Services 的“管理应用程序设置”页面上选中&#x200B;**[!UICONTROL 使用 HTTPS]** 选项。 如果未启用HTTPS，则iOS9+中的所有调用都将被阻止，除非您列入允许列表[!DNL Target]服务器。

   ![替代图像](assets/mobile-clientcode.png)

1. 创建/找到您的应用程序后，查找应用程序设置并下载所需的SDK。

   ![替代图像](assets/download-sdk.png)

>[!WARNING]
>
> 如果您无权访问移动设备营销界面，则可以直接在配置文件的应用程序代码中进行更改；不过，所做更改不会与用户界面中的设置页面同步。
