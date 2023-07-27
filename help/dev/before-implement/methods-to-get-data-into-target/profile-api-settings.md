---
keywords: 实施， api，配置文件，配置文件api设置，身份验证令牌
description: 了解如何通过为批量更新配置身份验证 [!DNL Adobe Target] API并生成配置文件身份验证令牌。
title: 如何使用配置文件API设置启用或禁用批量更新？
feature: APIs/SDKs
exl-id: 968f33d0-296b-4248-8c9a-8e6f3077bdfa
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 42%

---

# 配置文件 API 设置

启用或禁用批量更新的身份验证 [!DNL Adobe Target] API并生成配置文件身份验证令牌。

[!DNL Adobe Target] 会为每一个用户创建并维护一个配置文件。此配置文件存储在 [!DNL Target] 边缘群集，并在每次访问后实时更新。 您还可以单独或通过API批量更新用户档案。

为了提高安全性，您可以要求批量更新 API 调用必须在请求的标头中传递有效的访问令牌。

**[!DNL Target]使用 UI 设置身份验证要求并生成访问令牌：**

1. 单击&#x200B;**[!UICONTROL “管理”]**>**[!UICONTROL “实现”]**。
1. 下 **[!UICONTROL 配置文件API]** 滑动 **[!UICONTROL 需要身份验证]** 切换到启用或禁用位置。

   ![替代图像](assets/profile_api_settings.png)

1. （视情况而定）如果启用了身份验证要求，请单击 **[!UICONTROL 生成新的配置文件身份验证令牌]**.

   ![替代图像](assets/profile_api_settings_2.png)

   令牌将根据“到期时间”框中所列的时间到期。

   您必须具有以下用户权限之一才能生成身份验证令牌：

   * 管理员角色或至少具有审批者权限

     有关Target Standard客户的详细信息，请参阅 [指定角色和权限](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/users/user-management.html#roles-permissions) 在 *用户*. 有关 [!DNL Target Premium] 客户的详细信息，请参阅[配置企业权限](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html)。

   * 工作区/产品配置文件级别的管理员角色

     工作区仅对 [!DNL Target Premium] 客户可用。有关更多信息，请参阅[配置企业权限](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html)。

   * [!DNL Adobe Target] 产品级别的管理员权限（系统管理员权限）

您也可以通过 API 生成配置文件身份验证令牌。有关详细信息，请参阅 [Adobe Target管理和配置文件API指南](../../administer/admin-api/admin-api-overview-new.md).

1. 复制令牌并将其包含在请求的标头中，格式为：“授权”：“持有者”。

1. 单击 **[!UICONTROL 生成新的配置文件身份验证令牌]** 以根据需要重新生成令牌。

>[!WARNING]
>
>重置此令牌会导致使用当前令牌的 API 调用失败。这将需要更新使用此令牌的任何脚本或应用程序。
