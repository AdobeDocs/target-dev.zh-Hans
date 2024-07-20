---
keywords: 实施、实施、设置、设置、单个配置文件更新
description: 使用单个配置文件更新API将数据导入 [!DNL Target] 。
title: 如何使用[!UICONTROL Single Profile Update API]将数据导入 [!DNL Target] ？
feature: Implementation
exl-id: e6c394cb-74a3-4991-b656-5ae601f2d5e2
source-git-commit: 946e9431e6bde30f564b4ba1a4cf0a78d8c5c6bf
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 3%

---

# [!UICONTROL Single Profile Update API]

[!DNL Adobe Target] [!UICONTROL Single Profile Update API]允许您为单个用户发送配置文件更新。 [!UICONTROL Single Profile Update API]几乎与[!UICONTROL Bulk Profile Update API]相同，但一次更新一个访客资料，与API调用内联，而不是.cvs文件。

[!UICONTROL Single Profile Update API]和通常用于必须发生与未实现[!DNL Target]的渠道中发生的事务相关的更新时。 例如，要更新执行某些离线操作的单个访客的配置文件。 操作包括联系呼叫中心、资助贷款、在商店中使用会员卡、访问自助服务亭等。

将[!UICONTROL Single Profile Update API]与[[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)进行对比。

## 资源

有关更多信息，请参阅：

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)
