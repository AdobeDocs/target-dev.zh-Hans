---
keywords: 实施、设置、设置、批量配置文件更新api
description: 使用[!UICONTROL Bulk Profile Update API]将数据导入 [!DNL Target] 。
title: 如何使用[!UICONTROL Bulk Profile Update API]将数据导入 [!DNL Target] ？
feature: Implementation
exl-id: 654b13b7-1683-4c44-80e6-7557b9d29f66
source-git-commit: 946e9431e6bde30f564b4ba1a4cf0a78d8c5c6bf
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 7%

---

# 批量配置文件更新API

[!DNL Adobe Target] [!UICONTROL Bulk Profile Update API]允许您使用批处理文件批量更新网站多个访客的用户配置文件。

使用[!UICONTROL Bulk Profile Update API]，您可以方便地将许多用户的详细访客配置文件数据以配置文件参数的形式从任何外部源发送到[!DNL Target]。 外部来源可能包括客户关系管理(CRM)或销售点(POS)系统，这些系统通常无法在网页上使用。

将[!UICONTROL Bulk Profile Update API]与[[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)进行对比。

## [!UICONTROL Customer attributes]与[!UICONTROL Bulk Profile Update API]

此选项与[[!UICONTROL customer attributes]](/help/dev/before-implement/methods-to-get-data-into-target/customer-attributes.md)相似，但有一些区别：

* [!UICONTROL Customer attributes]使用FTP上传。 [!UICONTROL Target Bulk Profile Update API]使用HTTPPOSTAPI。
* [!UICONTROL Customer attribute]数据可以与[!DNL Analytics]共享。 [!UICONTROL Bulk Profile Update]只能在[!DNL Target]中使用。
* [!UICONTROL Customer attributes]支持为用户[!DNL Target]创建配置文件，但该支持尚未显示。
   * [!UICONTROL Bulk Profile Update API] v2：无需为每个`pcId`指定所有参数值。 已为[!DNL Target]中未找到的任何`pcId`或`mbox3rdPartyId`创建配置文件。
   * [!UICONTROL Bulk Profile Update API] v1： [!UICONTROL Bulk Profile Update API]仅更新现有[!DNL Target]配置文件。 如果您使用的是v1，则不会为缺失的`pcIds`或`mbox3rdPartyIds`创建配置文件。
* [!UICONTROL Customer attributes]要求使用[!UICONTROL Experience Cloud ID] (ECID)和源ID，如CRM ID或忠诚度ID。
* [!UICONTROL Bulk Profile Update API]需要TNT ID或`mbox3rdPartyId`。
* 不能在 `mbox3rdPartyID` 中发送下列字符：加号 (+) 和正斜线 (/)。

## 资源

有关更多信息，请参阅：

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)