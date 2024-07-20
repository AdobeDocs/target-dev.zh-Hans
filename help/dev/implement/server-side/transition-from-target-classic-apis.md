---
keywords: api， adobe i/o， classic， adobe developer console
description: 了解如何从 [!DNL Adobe Target Classic] API转换到 [!DNL Adobe Developer Console]上的 [!DNL Target] API。
title: 如何从 [!DNL Adobe Developer Console]上的 [!DNL Target Classic] API转换到 [!DNL Target] API？
feature: APIs/SDKs
exl-id: b84e3767-89ad-4e2d-9bb4-7e31bffbc285
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 38%

---

# 从[!DNL Adobe Developer Console]上的[!DNL Target Classic] API过渡到[!DNL Target] API

此信息可帮助您从[!DNL Target Classic] API过渡到[[!DNL Adobe Developer Console]](https://developer.adobe.com/console/home)上的[!DNL Target] API。

随着[!DNL Adobe Target Classic]的停用，连接到您的[!DNL Target Classic]帐户的API也变得不可用。 本文可帮助您将基于[!DNL Target Classic]的API集成转换为由[[!DNL Adobe Developer Console]](https://developer.adobe.com/console/home)提供支持的[!DNL Target] API。

有关[!DNL Target] API的详细信息，请参阅[[!DNL Target] API](/help/dev/before-administer/target-api-overview.md)。 有关[!DNL Target] SDK的详细信息，请参阅[[!DNL Target] 服务器端实施](/help/dev/implement/server-side/server-side-overview.md)

## 术语

| 术语 | 描述 |
|--- |--- |
| 经典API | 链接到您的[!DNL Target Classic]帐户的API。 这些 API 调用以基于用户名和密码的身份验证为基础，且使用主机名 `testandtarget.omniture.com`。如果API调用在请求URL中包含用户名和密码，则必须转换到[!DNL Adobe Developer Console] API。 |
| [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/home) | [!DNL Adobe Developer Console]是[!DNL Target] API的网关。 这些API已连接到您的[!DNL Target Standard/Premium]帐户。 [!DNL Adobe Developer Console]上的[!DNL Target] API使用基于[JWT的身份验证](../../before-administer/configure-authentication.md)，这是安全企业API的行业标准。 |

## 时间表

[!DNL Target Classic]停用时，以下API被停用：

| 日期 | 详细信息 |
|--- |--- |
| 2017 年 10 月 17 日 | 所有执行写入操作的 API 方法（`saveCampaign`、`copyCampaign`、`saveHTMLOfferContent` 和 `setCampaignState`）都已停用。<P>在这一天，所有[!DNL Target Classic]用户帐户都设置为只读状态。 |
| 2017 年 11 月 14 日 | 其余 API 都停用。这是停用[!DNL Target Classic]用户界面的日期 |

[!DNL Recommendations Classic] API不受此时间线影响。

## 等效方法

下表列出了经典API方法的等效的[!DNL Adobe Developer Console] API方法。 [!DNL Adobe Developer Console] API返回JSON，而经典API返回XML。

[!DNL Adobe Developer Console] API方法链接到API文档网站中的相应部分。 每个 API 方法都提供有相关示例。您还可以使用[!DNL Target]管理员API Postman集合，该集合包含[!DNL Adobe Developer Console]上所有AdobeAPI方法的示例API调用。

| 分组 | 经典API方法 | [!DNL Adobe Developer Console] API方法 | 注释 |
|--- |--- |--- |--- |
| 营销活动/活动 | 营销活动创建 | [创建 AB 活动](https://developers.adobetarget.com/api/#create-ab-activity)<P>[创建 XT 活动](https://developers.adobetarget.com/api/#create-xt-activity) | 新版 API 为 AB 活动和 XT 活动提供了不同的创建方法。 |
|  | 营销活动更新 | [更新 AB 活动](https://developers.adobetarget.com/api/#update-ab-activity)<P>[更新 XT 活动](https://developers.adobetarget.com/api/#update-xt-activity) |  |
|  | 复制营销活动 | 不适用 | 使用活动创建 API。 |
|  | 营销活动列表 | [列出活动](https://developers.adobetarget.com/api/#list-activities) |  |
|  | 营销活动状态 | [更新活动状态](https://developers.adobetarget.com/api/#update-activity-state) |  |
|  | 营销活动查看 | [按 ID 获取 AB 活动](https://developers.adobetarget.com/api/#get-ab-activity-by-id)<P>[按 ID 获取 XT 活动](https://developers.adobetarget.com/api/#get-xt-activity-by-id) |  |
|  | 第三方营销活动 ID | 不适用 | 如果您使用的是 thirdpartyID，则可以使用相关的活动方法。 |
| 选件 | 选件创建 | [创建选件](https://developers.adobetarget.com/api/#create-offer) |  |
|  | 选件获取 | [按 ID 获取选件](https://developers.adobetarget.com/api/#get-offer-by-id) |  |
|  | 选件列表 | [列出选件](https://developers.adobetarget.com/api/#list-offers) |  |
|  | 文件夹列表 | 不适用 | [!DNL Target Standard/Premium]不支持文件夹 |
| 报表 | 营销活动性能报表 | [获取 AB 性能报表](https://developers.adobetarget.com/api/#get-ab-performance-report)<P>[获取 XT 性能报表](https://developers.adobetarget.com/api/#get-xt-performance-report) |  |
|  | 审计报表 | [获取审核报告](https://developers.adobetarget.com/api/#get-audit-report) |  |
|  | 1-1 内容报表 | [获取 AP 性能报表](https://developers.adobetarget.com/api/#get-ap-activity-performance-report) |  |
| 帐户设置 | 获取主机组 | [列出环境](https://developers.adobetarget.com/api/#list-environments) |  |

## 例外

如果您需要设置例外，请联系您的客户成功经理。

## 帮助

如果您有任何问题，或者需要帮助从[!DNL Adobe Developer Console]上的经典API迁移到[!DNL Target] API，请联系[!DNL Adobe Target Client Care] (tt-support@adobe.com)。
