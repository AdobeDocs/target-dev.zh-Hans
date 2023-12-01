---
keywords: 实施、设置、设置、批量配置文件更新api
description: 将数据导入 [!DNL Target] 使用 [!UICONTROL 批量配置文件更新API].
title: 如何将数据导入 [!DNL Target] 使用 [!UICONTROL 批量配置文件更新API]？
feature: Implementation
exl-id: 654b13b7-1683-4c44-80e6-7557b9d29f66
source-git-commit: af9db32d59bdf32f2b9fade267922803250377dd
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 23%

---

# 批量配置文件更新API

通过API，将.csv文件发送到 [!DNL Adobe Target] 包含许多访客的访客配置文件更新。 每个访客配置文件均可以在一次调用中通过多个页面内配置文件属性进行更新。

此选项类似于 [!UICONTROL 客户属性] 但有一些不同之处：

* [!UICONTROL 客户属性] 使用FTP上传。此 [!UICONTROL Target批量配置文件更新API] 使用HTTPPOSTAPI。
* [!UICONTROL 客户属性] 数据可与共享 [!DNL Analytics]. [!UICONTROL 批量配置文件更新] 只能在 [!DNL Target].
* [!UICONTROL 客户属性] 支持为用户创建配置文件 [!DNL Target] 还没看见。
   * [!UICONTROL 批量配置文件更新API] v2：无需为每个参数指定所有参数值 `pcId`. 已为任何对象创建配置文件 `pcId` 或 `mbox3rdPartyId` 在中未找到的 [!DNL Target].
   * [!UICONTROL 批量配置文件更新API] v1：和 [!UICONTROL 批量配置文件更新API] 更新现有 [!DNL Target] 仅配置文件。 如果您使用的是v1，则不会为缺失创建配置文件 `pcIds` 或 `mbox3rdPartyIds`.
* [!UICONTROL 客户属性] 要求使用 [!UICONTROL EXPERIENCE CLOUDID] (ECID)和源ID的使用，如CRM ID或忠诚度ID。
* 此 [!UICONTROL 批量配置文件更新API] 需要TNT ID或 `mbox3rdPartyId`.
* 不能在 `mbox3rdPartyID` 中发送下列字符：加号 (+) 和正斜线 (/)。

## 格式

.csv文件必须通过每个访客的 [!DNL Target] PCID或 `mbox3rdPartyId`. 此 [!UICONTROL EXPERIENCE CLOUDID] 不支持(ECID)。 所有配置文件属性/值都可通过 API 创建和更新。格式详细信息可在 API 文档中找到。

## 示例用例

您的CRM或其他内部系统会存储有关您想要以一致方式更新的访客的有价值数据 [!DNL Target]，而不会在页面实施中公开用户档案数据。

## 方法的优势

* 配置文件属性的数量没有限制。
* 通过网站发送的用户档案属性可以通过API更新，反之亦然。

## 注意事项

* 批处理文件必须小于 50 MB。另外，每次上传的总行数不应超过 500,000 行。
* 更新通常在一小时内发生，但可能需要24小时才能反映出来。
* 对于在后续批次中可以在24小时内上传的一个或多个行数没有限制。 但是，为了确保其他进程能够高效运行，这些数据的吸收过程在工作时间可能会受到节流限制。
* 对相同的V2进行连续V2批量更新调用，且其中没有mbox调用 `thirdPartyIds` 覆盖在第一次批量更新调用中更新的属性。

## 资源

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)