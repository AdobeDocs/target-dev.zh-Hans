---
keywords: 实施、实施、设置、设置、客户属性
description: 使用客户属性将数据导入 [!DNL Target] 。
title: 如何使用客户属性将数据导入 [!DNL Target] ？
feature: Implementation
exl-id: d05cdd38-ba7c-4f29-a0ef-ae68619e7617
TQID: https://experienceleague.adobe.com/bzK915y7fvjfZjTkSK2QWHDzmIN9SdAQiEguiUlc-r8
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 216
ht-degree: 13%

---

# 客户属性

客户属性允许您通过FTP将访客配置文件数据上传到[!DNL Adobe Experience Cloud]。 上传后，使用[!DNL Adobe Analytics]和[!DNL Adobe Target]中的数据。

Target Standard客户可以应用五个属性，[!DNL Target Premium]客户可以应用200个属性。

## 格式

通过FTP或在Experience Cloud UI中手动上传具有[!DNL Experience Cloud] ID (ECID)和属性名称/值对的.csv文件。

## 示例用例

您的CRM或其他内部系统存储了要与[!DNL Adobe Experience Cloud]共享的宝贵信息，包括[!DNL Target]和[!DNL Analytics]。

## 方法的优势

上传客户数据会在Target中为该访客创建一个配置文件条目，即使[!DNL Target]尚未看到该访客。

[!DNL Target]和[!DNL Analytics]中自动提供了相同数据。

与 API 相比，FTP 的实施方法可能更简单。

## 注意事项

Target Standard客户可以应用五个属性，[!DNL Target Premium]客户可以应用200个属性

只能通过客户属性而不是在页面上来更新值。

需要 Experience Cloud ID (ECID) 实施。

## 代码示例

详细信息可在[创建客户属性来源并上传数据文件](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/t-crs-usecase.html?lang=zh-Hans)中找到。

### 相关信息的链接

[创建客户属性源并上传数据文件](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/t-crs-usecase.html?lang=zh-Hans)。
