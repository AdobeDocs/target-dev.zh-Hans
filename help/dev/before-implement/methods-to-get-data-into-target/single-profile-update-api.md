---
keywords: 实施、实施、设置、设置、单个配置文件更新
description: 使用单个配置文件更新API将数据导入 [!DNL Target] 。
title: 如何使用[!UICONTROL 单个配置文件更新API]将数据导入 [!DNL Target] ？
feature: Implementation
exl-id: e6c394cb-74a3-4991-b656-5ae601f2d5e2
TQID: https://experienceleague.adobe.com/tkh7YEJ9Vr5eMynNYYxYKZZDOXZTVJNxwUSCxiwPfzI
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 160
ht-degree: 3%

---

# [!UICONTROL 单个配置文件更新API]

[!DNL Adobe Target] [!UICONTROL 单个配置文件更新API]允许您为单个用户发送配置文件更新。 [!UICONTROL 单个配置文件更新API]几乎与[!UICONTROL 批量配置文件更新API]相同，但一次更新一个访客配置文件，与API调用内联，而不是.cvs文件。

[!UICONTROL 单个配置文件更新API]，通常用于必须发生与未实现[!DNL Target]的渠道中发生的事务相关的更新时。 例如，要更新执行某些离线操作的单个访客的配置文件。 操作包括联系呼叫中心、资助贷款、在商店中使用会员卡、访问自助服务亭等。

将[!UICONTROL 单个配置文件更新API]与[[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)进行对比。

## 资源

有关更多信息，请参阅：

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)
