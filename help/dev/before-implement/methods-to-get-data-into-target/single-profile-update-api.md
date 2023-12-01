---
keywords: 实施、实施、设置、设置、单个配置文件更新
description: 将数据导入 [!DNL Target] 使用单个配置文件更新API。
title: 如何将数据导入 [!DNL Target] 使用 [!UICONTROL 单个配置文件更新API]？
feature: Implementation
exl-id: e6c394cb-74a3-4991-b656-5ae601f2d5e2
source-git-commit: 81bff85a9d1fe28ca267c471a470da95568fd06d
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 2%

---

# [!UICONTROL 单个配置文件更新API]

此 [!DNL Adobe Target] [!UICONTROL 单个配置文件更新API] 允许您为单个用户发送配置文件更新。 此 [!UICONTROL 单个配置文件更新API] 几乎与 [!UICONTROL 批量配置文件更新API]，但一次更新一个访客资料，与API调用而不是.cvs文件内联。

此 [!UICONTROL 单个配置文件更新API] 并且通常用于必须针对在尚未实施的渠道中发生的事务进行更新时 [!DNL Target]. 例如，要更新执行某些离线操作的单个访客的配置文件。 操作包括联系呼叫中心、资助贷款、在商店中使用会员卡、访问自助服务亭等。

有关更多信息，请参阅：

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)
