---
keywords: 实施、实施、设置、设置、客户属性
description: 将数据导入 [!DNL Target] 使用客户属性。
title: 如何将数据导入 [!DNL Target] 使用客户属性？
feature: Implementation
exl-id: d05cdd38-ba7c-4f29-a0ef-ae68619e7617
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 24%

---

# 客户属性

客户属性可让您通过 FTP 将访客配置文件数据上传到 [!DNL Adobe Experience Cloud]. 上传后，使用中的数据 [!DNL Adobe Analytics] 和 [!DNL Adobe Target].

Target Standard客户可以应用五个属性： [!DNL Target Premium] 客户可以应用200个属性。

## 格式

包含的.csv文件 [!DNL Experience Cloud] ID (ECID)和属性名称/值对可通过FTP上传，或在Experience CloudUI中手动上传。

## 示例用例

您的CRM或其他内部系统存储了您想要与分享的重要信息 [!DNL Adobe Experience Cloud]，包括 [!DNL Target] 和 [!DNL Analytics].

## 方法的优势

上传客户数据会在Target中为该访客创建一个配置文件条目，即使 [!DNL Target] 尚未看到访客。

相同的数据自动在以下位置提供： [!DNL Target] 和 [!DNL Analytics].

与 API 相比，FTP 的实施方法可能更简单。

## 注意事项

Target Standard客户可以应用五个属性： [!DNL Target Premium] 客户可以应用200个属性

只能通过客户属性而不是在页面上来更新值。

需要 Experience Cloud ID (ECID) 实施。

## 代码示例

详情请见 [创建客户属性来源并上传数据文件](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/t-crs-usecase.html).

### 相关信息的链接

[创建客户属性来源并上传数据文件](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/t-crs-usecase.html).
