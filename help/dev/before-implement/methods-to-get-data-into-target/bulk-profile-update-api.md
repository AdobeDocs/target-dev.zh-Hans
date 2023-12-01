---
keywords: 实施、设置、设置、批量配置文件更新api
description: 将数据导入 [!DNL Target] 使用 [!UICONTROL 批量配置文件更新API].
title: 如何将数据导入 [!DNL Target] 使用 [!UICONTROL 批量配置文件更新API]？
feature: Implementation
exl-id: 654b13b7-1683-4c44-80e6-7557b9d29f66
source-git-commit: 946e9431e6bde30f564b4ba1a4cf0a78d8c5c6bf
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 5%

---

# 批量配置文件更新API

此 [!DNL Adobe Target] [!UICONTROL 批量配置文件更新API] 允许您使用批处理文件批量更新网站多个访客的用户配置文件。

使用 [!UICONTROL 批量配置文件更新API]，您可以方便地以多个用户的配置文件参数的形式将详细的访客配置文件数据发送至 [!DNL Target] 来自任何外部源。 外部来源可能包括客户关系管理(CRM)或销售点(POS)系统，这些系统通常无法在网页上使用。

对比 [!UICONTROL 批量配置文件更新API] 使用 [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md).

## [!UICONTROL 客户属性] 对比 [!UICONTROL 批量配置文件更新API]

此选项类似于 [[!UICONTROL 客户属性]](/help/dev/before-implement/methods-to-get-data-into-target/customer-attributes.md) 但有一些不同之处：

* [!UICONTROL 客户属性] 使用FTP上传。此 [!UICONTROL Target批量配置文件更新API] 使用HTTPPOSTAPI。
* [!UICONTROL 客户属性] 数据可与共享 [!DNL Analytics]. 此 [!UICONTROL 批量配置文件更新] 只能在 [!DNL Target].
* [!UICONTROL 客户属性] 支持为用户创建配置文件 [!DNL Target] 还没看见。
   * [!UICONTROL 批量配置文件更新API] v2：无需为每个参数指定所有参数值 `pcId`. 已为任何对象创建配置文件 `pcId` 或 `mbox3rdPartyId` 在中未找到的 [!DNL Target].
   * [!UICONTROL 批量配置文件更新API] v1：和 [!UICONTROL 批量配置文件更新API] 更新现有 [!DNL Target] 仅配置文件。 如果您使用的是v1，则不会为缺失创建配置文件 `pcIds` 或 `mbox3rdPartyIds`.
* [!UICONTROL 客户属性] 要求使用 [!UICONTROL EXPERIENCE CLOUDID] (ECID)和源ID的使用，如CRM ID或忠诚度ID。
* 此 [!UICONTROL 批量配置文件更新API] 需要TNT ID或 `mbox3rdPartyId`.
* 不能在 `mbox3rdPartyID` 中发送下列字符：加号 (+) 和正斜线 (/)。

## 资源

有关更多信息，请参阅：

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)