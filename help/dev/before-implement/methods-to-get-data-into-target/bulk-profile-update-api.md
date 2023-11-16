---
keywords: 实施、实施、设置、设置、批量配置文件更新
description: 将数据导入 [!DNL Target] 使用批量配置文件更新API。
title: 如何将数据导入 [!DNL Target] 是否使用批量配置文件更新API？
feature: Implementation
exl-id: 654b13b7-1683-4c44-80e6-7557b9d29f66
source-git-commit: 773f8a2f22cfbf740a5ce68809b38b33b621f3b5
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 57%

---

# 批量配置文件更新 API

通过API，将.csv文件发送到 [!DNL Adobe Target] 包含许多访客的访客配置文件更新。 每个访客配置文件均可以在一次调用中通过多个页面内配置文件属性进行更新。

此选项与客户属性类似，但有一些区别：

* 客户属性使用FTP上传，而 [!UICONTROL Target批量配置文件更新API] 使用HTTPPOSTAPI。
* 客户属性数据可与共享 [!DNL Analytics]. [!UICONTROL 批量配置文件更新只能在 Target 中使用。]
* 客户属性支持为用户创建配置文件 [!DNL Target] 还没看见。 存在批量配置文件更新API更新 [!DNL Target] 仅配置文件。
* 客户属性要求使用Experience CloudID (ECID)和源ID，例如CRM ID或忠诚度ID。
* 批量配置文件更新 API 需要 TNT ID 或 `mbox3rdPartyId`。
* 不能在 `mbox3rdPartyID` 中发送下列字符：加号 (+) 和正斜线 (/)。

## 格式

.csv文件必须通过访客引用每个访客 [!DNL Target] PCID或 `mbox3rdPartyId`. 不支持 Experience Cloud ID (ECID)。所有配置文件属性/值都可通过 API 创建和更新。格式详细信息可在 API 文档中找到。

## 示例用例

您在 CRM 或其他内部系统中存储那些要持续更新到 Target 的有关访客的宝贵数据，从而无需在您的页面实施中暴露配置文件数据。

## 方法的优势

配置文件属性的数量没有限制。

通过该站点发送的配置文件属性可以通过 API 进行更新，反之亦然。

## 注意事项

批处理文件必须小于 50 MB。另外，每次上传的总行数不应超过 500,000 行。

更新通常在一小时内发生，但可能需要长达24小时的时间才能反映出来。

在后续的批处理中，您在 24 小时内上传的数量或行数不受限制。但是，为了确保其他进程能够高效运行，这些数据的吸收过程在工作时间可能会受到节流限制。

对于相同 thirdPartyId，如果连续的 [V2 批量更新调用](https://developers.adobetarget.com/api/#updating-profiles)之间没有 mbox 调用，则会覆盖在第一次批量更新调用中更新的属性。

## 代码示例

请参阅[更新配置文件](https://developers.adobetarget.com/api/#updating-profiles)。

### 相关信息的链接

[更新配置文件](https://developers.adobetarget.com/api/#updating-profiles)
