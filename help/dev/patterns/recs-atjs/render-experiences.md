---
title: 渲染体验
description: 请确保按照正确的顺序执行渲染体验的所有必要步骤。
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: 7cf0c70b-a4bc-46f4-9b33-099bdb7dd9a9
TQID: https://experienceleague.adobe.com/uHFbc8JEhjjGYIulJUvhkH7cXXht6Rht9rY43HjuNqg
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 1060
ht-degree: 3%

---

# 渲染体验

请按照&#x200B;*渲染体验*&#x200B;图中的步骤操作，以确保渲染体验所需的所有必要任务都按正确顺序执行。

>[!NOTE]
>
>如果您在&#x200B;*初始化SDK*&#x200B;中的[配置自动页面加载请求步骤](/help/dev/patterns/recs-atjs/initialize-sdk.md#automatic)期间启用了自动页面加载请求，则可以跳过此活动，除非您想要调用Adobe Target SDK以使用区域位置请求呈现其他体验。

>[!TIP]
>
>单击本主题中的图像以展开到全屏。

## 渲染体验图 {#diagram}

只有当您启用了[!UICONTROL Automatic Page Load Request]时，at.js提供的现成自动闪烁处理才有意义。 此选项在从[!DNL Target]获取体验时隐藏整个HTML正文。 在这种情况下，您有责任处理闪烁。 搜索可用于闪烁处理的实施模式以获取指导。

>[!NOTE]
>
>下图中的步骤编号与以下部分相对应。 步骤编号没有特定顺序，也不反映创建活动时在[!DNL Target] UI中执行的步骤顺序。

![渲染体验图表](/help/dev/patterns/recs-atjs/assets/diagram-render-experiences-new.png){width="600" zoomable="yes"}

单击以下链接以导航到所需的部分：

* [3.1：促销活动](#promotion)
* [3.2：基于购物车的标准](#cart)
* [3.3：基于热门程度的标准](#popularity)
* [3.4：基于项目的标准](#item)
* [3.5：基于用户的标准](#user)
* [3.6：自定义标准](#custom)
* [3.7：提供包含规则中使用的属性](#inclusion)
* [3.8：提供excludedIds](#exclude)
* [3.9：提供实体属性以更新“推荐”的产品目录](#entity-attributes)
* [3.10：提供用作包含规则键的配置文件属性](#keys)
* [3.11：触发页面加载请求](#fire)
* [3.12：消防区域定位请求](#location)

## 3.1：促销活动 {#promotion}

创建活动时，通过在[!DNL Target] UI中选择“前面”或“后面”促销活动，添加促销项目并控制它们在推荐设计中的放置位置。

+++查看详细信息

**可用选项**

* 按ID提升
* [按收藏集促销](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/collections.html?lang=zh-Hans){target=_blank}
* [按属性促销](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html?lang=zh-Hans){target=_blank}

**需要实体参数**

* 使用“按属性促销”选项时，必须传递促销活动中的项目属性。

**读数**

* [添加促销活动](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-activity/adding-promotions.html?lang=zh-Hans){target=_blank}

+++

[返回此页面顶部的图表。](#diagram)

## 3.2：基于购物车的标准 {#cart}

根据用户的购物车内容提供推荐。

+++查看详细信息

**可用标准**

* [!UICONTROL People Who Viewed These, Viewed Those]
* [!UICONTROL People Who Viewed These, Bought Those]
* [!UICONTROL People Who Bought These, Bought Those]

**需要实体参数**

* cartIds

**读数**

* [基于购物车](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=zh-Hans#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[返回此页面顶部的图表。](#diagram)

## 3.3：基于热门程度的标准 {#popularity}

根据项目在整个网站中的整体受欢迎程度或访客最喜爱或查看次数最多的类别、品牌、流派等中的项目受欢迎程度提供推荐。

+++查看详细信息

**可用标准**

* [!UICONTROL Most Viewed Across the Site]
* [!UICONTROL Most Viewed by Category]
* [!UICONTROL Most Viewed by Item Attribute]
* [!UICONTROL Top Sellers Across the Site]
* [!UICONTROL Top Sellers by Category]
* [!UICONTROL Top Sellers by Item Attribute]
* [!UICONTROL Top by Analytics Metric]

**需要实体参数**

* `entity.categoryId`或基于热门程度的项属性（如果条件基于当前或项属性）。
* 对于网站中的“查看次数最多”/“销售最高”页面，无需传递任何内容。

**读数**

* [基于热门程度](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=zh-Hans#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[返回此页面顶部的图表。](#diagram)

## 3.4：基于项目的标准 {#item}

根据查找的用户正在查看或最近查看过的项目的相似项目提供推荐。

+++查看详细信息

**可用标准**

* [!UICONTROL People Who Viewed This, Viewed That]
* [!UICONTROL People Who Viewed This, Bought That]
* [!UICONTROL People Who Bought This, Bought That]
* [!UICONTROL Items with Similar Attributes]

**需要实体参数**

* `entity.id`
* 如果有任何配置文件属性用作键

**读数**

* [基于项目](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=zh-Hans#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[返回此页面顶部的图表。](#diagram)

## 3.5：基于用户的标准 {#user}

根据用户的行为提供推荐。

+++查看详细信息

**可用标准**

* [!UICONTROL Recently Viewed Items]
* [!UICONTROL Recommended for You]

**需要实体参数**

* `entity.id`

**读数**

* [基于用户](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=zh-Hans#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[返回此页面顶部的图表。](#diagram)

## 3.6：自定义标准 {#custom}

根据您上传的自定义文件提出推荐。

+++查看详细信息

**可用标准**

* [!UICONTROL Custom algorithm]

**需要实体参数**

`entity.id`或用作自定义算法键的属性

**读数**

* [自定义标准](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=zh-Hans#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[返回此页面顶部的图表。](#diagram)

## 3.7：提供包含规则中使用的属性 {#inclusion}

+++查看详细信息

**读数**

* [使用动态和静态包含规则](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/dynamic-static/use-dynamic-and-static-inclusion-rules.html?lang=zh-Hans){target=_blank}

+++

[返回此页面顶部的图表。](#diagram)

## 3.8：提供excludedIds {#exclude}

传递要从推荐中排除的实体ID。 例如，可排除购物车中已有的商品。

+++查看详细信息

**读数**

* [我可以动态排除实体吗？](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/recommendations-faq.html?lang=zh-Hans#exclude){target=_blank}

+++

[返回此页面顶部的图表。](#diagram)

## 3.9：提供实体属性以更新[!DNL Recommendations]的产品目录 {#entity-attributes}

+++查看详细信息

**读数**

* [实体属性](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html?lang=zh-Hans){target=_blank}

您还可以通过使用[!DNL Target] UI创建[产品馈送](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/feeds.html?lang=zh-Hans){target=_blank}来更新[!DNL Recommendations]的产品目录，从而完成此步骤。

+++

[返回此页面顶部的图表。](#diagram)

## 3.10：提供用作包含规则键的配置文件属性 {#keys}

提供用作上述任何推荐标准中包含规则的键的配置文件属性。

+++ 查看详细信息

**读数**

* [轮廓属性](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html?lang=zh-Hans){target=_blank}

+++

[返回此页面顶部的图表。](#diagram)

## 3.11：触发页面加载请求 {#fire}

此步骤在请求中触发具有`execute` > `pageLoad`有效负载的[!DNL Delivery API]调用。 `getOffers()`方法提取体验，`applyOffers()`渲染页面上的体验。 在[可视化体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=zh-Hans){target=_blank} (VEC)中创作的呈现体验需要`pageLoad`请求。

+++查看详细信息

![触发页面加载请求图表](/help/dev/patterns/recs-atjs/assets/fire-page-load-request-combined.png){width="400" zoomable="yes"}

**先决条件**

* 必须使用`targetPageParams`函数完成所有数据映射。

**读数**

* [adobe.target.getOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)
* [adobe.target.applyOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)

**操作**

* 使用`getOffers`和`applyOffers`方法通过页面加载请求API调用获取体验。

+++

[返回此页面顶部的图表。](#diagram)

## 3.12：消防区域定位请求(#location)

此步骤在其请求中触发具有`execute` > `mboxes`有效负载的[!DNL Delivery API]调用。 `getOffers`方法提取体验，然后`applyOffers`将体验渲染到页面。 您可以在`execute` > `mboxes`有效负载下发送多个mbox。

+++查看详细信息

![触发区域位置请求图表](/help/dev/patterns/recs-atjs/assets/fire-regional-location-request-combined.png){width="400" zoomable="yes"}

**先决条件**

* 必须使用`targetPageParams`函数完成所有数据映射。

**读数**

* [adobe.target.getOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)
* [adobe.target.applyOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)

**操作**

* 使用`getOffers`和`applyOffers`方法通过页面加载请求API调用获取体验。

+++

[返回此页面顶部的图表。](#diagram)

继续执行步骤4： [通知Target](/help/dev/patterns/recs-atjs/notify-target.md)。
