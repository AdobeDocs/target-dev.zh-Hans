---
keywords: Recommendations，设置，首选项，垂直行业，筛选不兼容的标准，默认主机组，缩览图基本url，推荐api令牌，
description: 了解如何实施 [!UICONTROL Recommendations] 中的活动 [!DNL Adobe Target].
title: 如何实施 [!UICONTROL Recommendations] 活动？
feature: Recommendations
hidefromtoc: true
hide: true
source-git-commit: 8d04fe249aafb5ee064dc614ae72f68b8f8459f2
workflow-type: tm+mt
source-wordcount: '1550'
ht-degree: 20%

---

# 计划和实施 [!UICONTROL Recommendations]

帮助您计划和实施的信息 [!DNL Adobe Target Recommendations].

>[!NOTE]
>
>除了本文之外， [Adobe Target商业从业者指南](https://experienceleague.adobe.com/en/docs/target/using/target-home){target=_blank} 包含有关以下内容的深入信息 [定位Recommendations](https://experienceleague.adobe.com/en/docs/target/using/recommendations/recommendations){target=_blank}.

在设置您的第一个之前 [!UICONTROL Recommendations] 中的活动 [!DNL Adobe Target]，请完成以下步骤：

1. [实施 [!UICONTROL Target]](#implement-target) ，以用于捕获用户行为和提供推荐。
1. [设置您的 [!UICONTROL Recommendations] 目录](#set-up-your-recommendations-catalog) 要推荐给用户的产品或内容。
1. [传递行为信息和上下文](#pass-behavioral-information-and-context) 到 [!DNL Target Recommendations] 以使其能够提供个性化推荐。
1. [配置全局排除项](#configure-global-exclusions).
1. [配置 [!UICONTROL Recommendations] 设置](#configure-recommendations-settings).
1. （可选） [管理员 [!UICONTROL Recommendations] 使用管理员API](#administer-recommendations-using-admin-apis).

## 1.实施 [!UICONTROL Target]

[!DNL Target Recommendations] 要求您实施 [!DNL Adobe Experience Platform Web SDK] 或at.js 0.9.2（或更高版本）。 请参阅 [[!UICONTROL Target] 客户端实施指南](../client-side/overview.md) 以了解更多信息。

## 2.设置您的 [!UICONTROL Recommendations] 目录

要提供高质量的推荐， [!UICONTROL Target] 必须了解您要推荐的产品或内容。 目录通常包括有关推荐项目的三种类型的信息。 假设您正在推荐电影。 包括以下内容：

1. 要向收到推荐的用户显示的数据。例如，您可以显示电影的名称以及电影海报的缩略图图像的URL。
1. 用于应用营销和销售控制的数据。例如，您可以显示电影的分级，这样就不会推荐评级为NC-17的电影。
1. 用于确定项目与其他项目段相似度的数据。 例如，您可以显示电影的流派和电影的导演。

[!UICONTROL Target] 提供了多个集成选项来填充您的目录。 这些选项可以组合使用，以更新目录中的不同项目或更新不同频率上的不同项目属性。

| 方法 | 内容 | 何时使用 | 其他信息 |
| --- | --- | --- | --- |
| 目录信息源 | 计划信息源(CSV， [!DNL Google] 产品XML，或 [!UICONTROL Analytics Product Classifications])每天上传和摄取。 | 用于一次发送有关多个项目的信息。 用于发送不经常更改的信息。 | 请参阅 [信息源](https://experienceleague.adobe.com/en/docs/target/using/recommendations/entities/feeds). |
| 实体API | 调用API以发送单个项目的最新更新。 | 用于在更新发生时一次发送一个项目的更新。 用于发送经常更改的信息（例如价格、库存/库存水平）。 | 请参阅 [实体API开发人员文档](https://developer.adobe.com/target/administer/recommendations-api/#tag/Entities). |
| 在页面上传递更新 | 在页面上使用JavaScript或使用投放API发送单个项目的即时更新。 | 用于在更新发生时一次发送一个项目的更新。 用于发送经常更改的信息（例如价格、库存/库存水平）。 | 请参阅 [项目查看次数/产品页面](#item-views-or-product-pages) 下。 |

大多数客户应至少实施一个信息源。 然后，您可以选择使用实体API或页面上的方法通过经常更改属性或项目的更新来补充馈送。

## 3.传递行为信息和上下文

您应该传递到的行为信息和上下文 [!UICONTROL Target] 取决于访客正在执行的操作，该操作通常与访客与之交互的页面类型有关。

### 项目视图或产品页面

在访客正在查看单个项目的页面（如产品详细信息页面）上，您应该传递访客正在查看项目的标识。 此外，还要传递访客正在查看的项目的最细粒度类别，以允许将推荐过滤到当前类别。

您还可以在产品页面本身上传递某些快速更改的属性。 例如，您可以传递价格(`value`)和库存/库存水平。

#### 传递价格和库存

```js {line-numbers="true"}
<script type="text/javascript">
function targetPageParams() { 
   return { 
      "entity": { 
         "id": "32323", 
         "categoryId": "running-shoes", 
         "value": 119.99, 
         "inventory": 329 
      } 
   } 
}
</script>
```

### 类别视图/类别页面

在类别页面上，您可能希望将推荐限制为该类别中的产品或内容。 为此，请确保传递当前查看的类别的身份。

#### 传递当前类别

```js {line-numbers="true"}
function targetPageParams() { 
   return { 
      "entity": { 
         "categoryId": "running-shoes" 
      } 
   } 
}
```

### 购物车添加/购物车视图/结账页面

在购物车页面上，您可以根据访客当前购物车的内容推荐项目。 为此，请使用特殊参数传递访客当前购物车中所有项目的ID `cartIds`.

#### 传递购物车中的当前项目

```js {line-numbers="true"}
function targetPageParams() {
   return {
      "cartIds": "352,223,23432,432,553"
      }
}
```

有关基于购物车的推荐的更多信息，请参阅 [基于购物车](https://experienceleague.adobe.com/en/docs/target/using/recommendations/criteria/base-the-recommendation-on-a-recommendation-key#cart-based) 在 *[!DNL Adobe Target]商业从业者指南*.

### 排除访客购物车中已有的项目

在整个网站的页面上，您可以从推荐中排除某些项目。 例如，您可能不希望推荐访客当前购物车中已有的项目。 要实现此目的，请使用特殊参数传递要排除的所有项目的ID `excludedIds`.

#### 传递要排除的项目

```js {line-numbers="true"}
function targetPageParams() {
   return {
      "excludedIds": "352,223,23432,432,553"
      }
}
```

### 购买/订单确认页面

发生购买事件时，传递购买项目的身份。 请参阅 [跟踪转化](../client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md#track-conversions) 在 [如何部署at.js >实施 [!UICONTROL Target] 没有标签管理器](../client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md) 文章。

## 4.配置全局排除项

排除全局级别上您绝不希望向访客推荐的任何项目。 请参阅 [排除项](https://experienceleague.adobe.com/en/docs/target/using/recommendations/entities/exclusions) 在 *[!DNL Adobe Target]商业从业者指南*.

## 5.配置 [!UICONTROL Recommendations] 设置

可使用一些设置来管理 [!UICONTROL Recommendations] 实施。

要访问 **[!UICONTROL Recommendations Settings]** 选项，打开 [!DNL Target] 在 [!DNL Adobe Experience Cloud]，然后单击 **[!UICONTROL Administration]** > **[!UICONTROL Recommendations]**.

![“Recommendations设置”页面](/help/dev/implement/recommendations/assets/recs-settings-new.png)

配置以下选项：

### [!UICONTROL Recommendations API Token]

以下选项位于 [!UICONTROL Recommendations API Token] 部分：

#### [!UICONTROL Client code]

此 [!DNL Target] [!UICONTROL client code].

如果你不了解 [!UICONTROL client code]，在 [!DNL Target] 用户界面，单击 **[!UICONTROL Administration]** > **[!UICONTROL Implementation]**. 此 [!UICONTROL client code] 在中显示 [!UICONTROL Account Details] 部分。

#### 身份验证令牌

此 [!DNL Adobe Target] 管理员API，包括 [!DNL Recommendations Admin] API通过身份验证进行保护，以确保只有授权用户才能使用它们进行访问 [!DNL Adobe Target]. 使用 [Adobe Developer控制台](https://developer.adobe.com/console/home) 以管理所有用户的此身份验证 [!DNL Adobe Experience Cloud solutions]，包括 [!DNL Adobe Target].

有关更多信息，请参阅 [为Adobe Target API配置身份验证](/help/dev/before-administer/configure-authentication.md).

>[!WARNING]
>
>生成新的身份验证令牌时请务必小心。 生成新令牌会导致使用当前令牌的API调用失败。 使用新生成的身份验证令牌更新任何脚本或应用程序。

### 标准

了解您网站的垂直行业有助于Target为您的推荐选择标准。

中的标准 [!DNL Recommendations] 是一些规则，可根据预先确定的一组访客行为来确定要推荐的产品或内容。 标准可以基于流行趋势、访客当前和过去的行为或类似产品和内容。 您可以添加多个标准，以便对多个推荐类型进行相互测试。

有关更多信息，请参阅 [标准](https://experienceleague.adobe.com/en/docs/target/using/recommendations/criteria/algorithms){target=_blank} 在 *Adobe Target商业从业者指南。*

以下设置位于 [!UICONTROL Criteria] 部分：

#### [!UICONTROL Industry/Vertical]

垂直行业用来帮助对您的推荐标准进行分类。此信息可帮助您的团队成员找到适合特定页面的标准，例如最适合购物车页面或媒体页面的标准。

下拉列表中提供以下类别：

* 无个性化
* 零售/电子商务
* 潜在客户拓展/B2B/金融服务
* 媒体/出版

#### [!UICONTROL Filter Incompatible Criteria]

启用此选项，可仅显示要求选定页面传递所需数据的标准。并非每个标准都在每个页面上正确运行。 必须传入页面或mbox `entity.id` 或 `entity.categoryId` 以使当前项目/当前类别推荐兼容。

一般来说，最好只显示兼容的标准。但是，如果您希望不兼容的标准也可用于活动，请不要启用此选项。

如果使用标签管理解决方案，Adobe建议您禁用此选项。

有关此选项的详细信息，请参阅 [[!UICONTROL Recommendations] 常见问题解答](https://experienceleague.adobe.com/en/docs/target/using/recommendations/recommendations-faq/recommendations-faq){target=_blank} 在 *[!DNL Adobe Target]商业从业者指南*.

### [!UICONTROL Product Catalog]

以下选项位于 [!UICONTROL Product Catalog] 部分：

#### [!UICONTROL Default Host Group]

选择默认主机组。

主机组可用于为不同用途而分隔目录中的可用项。例如，您可以将主机组用于“开发和生产”环境、不同的品牌或不同的地理位置。默认情况下，“目录搜索”、“收藏集”和“排除项”中的预览结果均基于默认的主机组。（也可以使用“环境”筛选器来选择要预览结果的不同主机组。）默认情况下，新添加的项目在所有主机组中都可用，除非在创建或更新项目时指定了环境 ID。交付的“推荐”取决于请求中指定的主机组。

如果您看不到产品，请确保您使用的是正确的主机组。例如，如果您将推荐设置为使用测试环境并将您的主机组设置为“测试”，则您可能需要在测试环境中重新创建收藏集，之后才会显示产品。要查看每个环境中提供了哪些产品，请在每个环境中使用“目录搜索”。您还可以预览 [!UICONTROL Recommendations] 选定环境（主机组）的收藏集和排除项。

>[!NOTE]
>
>更改选定的环境后，必须单击 **[!UICONTROL Search]** 以更新返回的结果。

此 **[!UICONTROL Environment]** 筛选器可从Target UI中的以下位置访问：

* 目录搜索(**[!UICONTROL Recommendations]** > **[!UICONTROL Catalog Search]**)
* 收藏集(**[!UICONTROL Recommendations]** > **[!UICONTROL Collections]**)
* “创建收藏集”对话框(**[!UICONTROL Recommendations]** > **[!UICONTROL Collections]** > **[!UICONTROL Create collection]**)
* “更新收藏集”对话框(**[!UICONTROL Recommendations]** > **[!UICONTROL Collections]** > **[!UICONTROL Edit]**)
* “创建排除项”对话框(**[!UICONTROL Recommendations]** > **[!UICONTROL Exclusions]** > **[!UICONTROL Create exclusion]**)
* “更新排除项”对话框(**[!UICONTROL Recommendations]** > **[!UICONTROL Exclusions]** > **[!UICONTROL Edit]**)

有关更多信息，请参阅 [主机](https://experienceleague.adobe.com/en/docs/target/using/administer/hosts){target=_blank} 在 *[!DNL Adobe Target]商业从业者指南*.

#### [!UICONTROL Thumbnail Base]

为您的产品目录设置基本 URL 后，可以在指定产品缩览图以及传递缩览图 URL 时使用相对 URL。

例如：

`"entity.thumbnailURL=/Images/Homepage/product1.jpg"`

设置的便是相对于缩览图基本 URL 的 URL。

### [!UICONTROL Custom Attribute Key Configuration]

根据访客配置文件中存储的项目提供推荐。 例如，“上一个添加到购物车的项目”或“上一个观看了90%或更多内容的视频”。

单击 **[!UICONTROL Add]** 要创建新配置，请指定配置名称，选择所需的配置文件属性，然后单击 **[!UICONTROL Save]**.

## 6. （可选）管理 [!UICONTROL Recommendations] 使用管理员API

请参阅 [使用 [!UICONTROL Recommendations] API](../../before-administer/recs-api/overview.md) 实践指南，以了解如何配置和使用 [!UICONTROL Target] 的管理和交付API [!UICONTROL Recommendations].