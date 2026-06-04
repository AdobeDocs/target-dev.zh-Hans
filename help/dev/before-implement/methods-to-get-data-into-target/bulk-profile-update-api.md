---
keywords: 实施、设置、设置、批量配置文件更新api
description: 使用[!UICONTROL 批量配置文件更新API]将数据导入 [!DNL Target] 。
title: 如何使用[!UICONTROL 批量配置文件更新API]将数据导入 [!DNL Target] ？
feature: Implementation
exl-id: 654b13b7-1683-4c44-80e6-7557b9d29f66
TQID: https://experienceleague.adobe.com/vBcIsBR6wwYr7MbRh7UJvt71ULDEq6iXVZ5spZlif-0
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 284
ht-degree: 5%

---

# 批量配置文件更新API

[!DNL Adobe Target] [!UICONTROL 批量配置文件更新API]允许您使用批处理文件批量更新网站多个访客的用户配置文件。

使用[!UICONTROL 批量配置文件更新API]，您可以方便地以配置文件参数的形式将许多用户的详细访客配置文件数据从任何外部源发送到[!DNL Target]。 外部来源可能包括客户关系管理(CRM)或销售点(POS)系统，这些系统通常无法在网页上使用。

将[!UICONTROL 批量配置文件更新API]与[[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)进行对比。

## [!UICONTROL 客户属性]与[!UICONTROL 批量配置文件更新API]

此选项类似于[[!UICONTROL 客户属性]](/help/dev/before-implement/methods-to-get-data-into-target/customer-attributes.md)，但有一些区别：

* [!UICONTROL 客户属性]使用FTP上传。 [!UICONTROL Target批量配置文件更新API]使用HTTP POST API。
* [!UICONTROL 客户属性]数据可以与[!DNL Analytics]共享。 [!UICONTROL 批量配置文件更新]只能在[!DNL Target]中使用。
* 尚未看到[!UICONTROL 客户属性]支持为用户[!DNL Target]创建配置文件。
   * [!UICONTROL 批量配置文件更新API] v2：无需为每个`pcId`指定所有参数值。 已为[!DNL Target]中未找到的任何`pcId`或`mbox3rdPartyId`创建配置文件。
   * [!UICONTROL 批量配置文件更新API] v1： [!UICONTROL 批量配置文件更新API]仅更新现有[!DNL Target]配置文件。 如果您使用的是v1，则不会为缺失的`pcIds`或`mbox3rdPartyIds`创建配置文件。
* [!UICONTROL 客户属性]要求使用[!UICONTROL Experience Cloud ID] (ECID)和使用源ID，如CRM ID或忠诚度ID。
* [!UICONTROL 批量配置文件更新API]需要TNT ID或`mbox3rdPartyId`。
* 不能在 `mbox3rdPartyID` 中发送下列字符：加号 (+) 和正斜线 (/)。

## 资源

有关更多信息，请参阅：

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)