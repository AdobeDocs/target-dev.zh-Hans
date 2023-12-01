---
keywords: 实施、实施、设置、设置、单个配置文件更新
description: 将数据导入 [!DNL Target] 使用单个配置文件更新API。
title: 如何将数据导入 [!DNL Target] 是否使用单个配置文件更新API？
feature: Implementation
exl-id: e6c394cb-74a3-4991-b656-5ae601f2d5e2
source-git-commit: af9db32d59bdf32f2b9fade267922803250377dd
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 13%

---

# 单个配置文件更新API

几乎与 [!UICONTROL 批量配置文件更新API] 在 [!DNL Adobe Target]，但一次更新一个访客资料，在API调用中排队，而不是使用.csv文件。

## 格式

必须通过来识别访客 [!DNL Target] `mboxPC` 值或 `mbox3rdPartyId` 值。 此 [!UICONTROL EXPERIENCE CLOUDID] 不支持(ECID)。

## 示例用例

您要更新执行某些离线操作的单个访客的配置文件。 操作包括联系呼叫中心、资助贷款、在商店中使用会员卡、访问自助服务亭等。

## 方法的优势

* 配置文件属性的数量没有限制。*
* 通过网站发送的用户档案属性可以通过API更新，反之亦然。

## 注意事项

* 每 24 小时限制 1,000,000（100 万）次 API 调用.
* 仅限配置文件更新。无法为潜在用户创建配置文件 [!DNL Target] 尚未看到。
* 更新通常在一小时内发生，但可能需要24小时才能反映出来。

## 代码示例

支持 GET 和 POST。

```
https://CLIENT.tt.omtrdc.net/m2/client/profile/update?mboxPC=1368007744041-575948.01_00&profile.attr1=0&profile.attr2=1...
```

## 资源

* [[!DNL Adobe Target Profile APIs overview]](/help/dev/administer/profile-api/profile-api-overview.md)
* [[!DNL Adobe Target Single Profile Update API]](/help/dev/administer/profile-api/profile-single-api.md)
* [[!DNL Adobe Target Bulk Profile Update API]](/help/dev/administer/profile-api/profile-bulk-api.md)
