---
title: 渲染体验
description: 请确保按照正确的顺序执行渲染体验的所有必要步骤。
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 5321ce43be26e8f0776da49e597ecb5f8dfb5984
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 5%

---

# 渲染体验

请按照 *渲染体验* 图，可确保呈现体验所需的所有必要任务均以正确顺序执行。

>[!TIP]
>
>单击本主题中的图像以展开到全屏。

## 渲染体验图 {#diagram}

at.js提供的现成自动闪烁处理功能仅在您具备以下条件时才有意义 [!UICONTROL 自动页面加载请求] 已启用。 此选项在从提取HTML时隐藏整个体验正文 [!DNL Target]. 在这种情况下，您有责任处理闪烁。 搜索可用于闪烁处理的实施模式以获取指导。

下图中的步骤编号与以下部分相对应。

![渲染体验图](/help/dev/patterns/assets/render-experiences-diagram.png){width="600" zoomable="yes"}

单击以下链接以导航到所需的部分：

* [3.1：促销活动](#promotion)
* [3.2：基于购物车的标准](#cart)
* [3.3：基于热门程度的标准](#popularity)
* [3.4：基于项目的标准](#item)
* [3.5：基于用户的标准](#user)
* [3.6：自定义标准](#custom)
* [3.7：提供包含规则中使用的属性](#inclusion)
* [3.8：提供excludedIds](#exclude)
* [3.9：提供实体属性以更新Recommendations的产品目录](#entity-attributes)
* [3.10：提供用作包含规则键的配置文件属性](#keys)
* [3.11：触发页面加载请求](#fire)
* [3.12：消防区域定位请求](#location)

## 3.1：促销活动 {#promotion}

添加促销项目并控制它们在Target Recommendations中的放置位置 [设计](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-design/create-design.html){target=_blank}.

+++查看详细信息

**可用选项**

* 按ID提升
* [按收藏集促销](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/collections.html){target=_blank}
* [按属性促销](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**需要实体参数**

* 使用“按属性促销”选项时，必须传递促销活动中的项目属性。

+++

[返回此页面顶部的图表。](#diagram)

## 3.2：基于购物车的标准 {#cart}

根据用户的购物车内容提供推荐。

+++查看详细信息

**可用标准**

* [!UICONTROL 查看了这些项目，也查看了这些项目的人]
* [!UICONTROL 查看了这些商品的人们购买了那些商品]
* [!UICONTROL 购买了这些商品的人们也购买了这些商品]

**需要实体参数**

* cartIds

**读数**

* [基于购物车](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[返回此页面顶部的图表。](#diagram)

## 3.3：基于热门程度的标准 {#popularity}

根据项目在整个网站中的整体受欢迎程度或用户最喜爱或查看次数最多的类别、品牌、流派等中的项目受欢迎程度提供推荐。

+++查看详细信息

**可用标准**

* [!UICONTROL 全网站查看的次数最多]
* [!UICONTROL 同类中查看次数最多]
* [!UICONTROL 按项目属性查看的次数最多]
* [!UICONTROL 全网站最畅销商品]
* [!UICONTROL 按类别划分的畅销商品排名]
* [!UICONTROL 按项目属性排名的最畅销商品]
* [!UICONTROL 按Analytics量度排名]

**需要实体参数**

* `entity.categoryId` 或基于热门程度的项目属性（如果标准基于当前或项目属性）。
* 对于网站中的“查看次数最多”/“销售最高”页面，无需传递任何内容。

**读数**

* [基于热门程度](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[返回此页面顶部的图表。](#diagram)

## 3.4：基于项目的标准 {#item}

根据查找的用户正在查看或最近查看过的项目的相似项目提供推荐。

+++查看详细信息

**可用标准**

* [!UICONTROL 查看了这个项目，也查看了那个项目的人]
* [!UICONTROL 查看了这个项目，但购买了那个项目的人]
* [!UICONTROL 购买了这个项目，也购买了那个项目的人]
* [!UICONTROL 具有相似属性的项目]

**需要实体参数**

* `entity.id`
* 如果有任何配置文件属性用作键

**读数**

* [基于项目](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[返回此页面顶部的图表。](#diagram)

## 3.5：基于用户的标准 {#user}

根据用户的行为提供推荐。

+++查看详细信息

**可用标准**

* [!UICONTROL 最近查看的项目]
* [!UICONTROL 为您推荐]

**需要实体参数**

* `entity.id`

**读数**

* [基于用户](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[返回此页面顶部的图表。](#diagram)

## 3.6：自定义标准 {#custom}

根据您上传的自定义文件提出推荐

+++查看详细信息

**可用标准**

* [!UICONTROL 自定义算法]

**需要实体参数**

`entity.id` 或用作自定义算法键的属性

**读数**

* [自定义标准](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[返回此页面顶部的图表。](#diagram)

## 3.7：提供包含规则中使用的属性 {#inclusion}

+++查看详细信息

**读数**

* [使用动态和静态包含规则](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/dynamic-static/use-dynamic-and-static-inclusion-rules.html){target=_blank}

+++

[返回此页面顶部的图表。](#diagram)

## 3.8：提供excludedIds {#exclude}

传递要从推荐中排除的实体ID。 例如，可排除购物车中已有的商品。

+++查看详细信息

**读数**

* [能否动态地排除实体？](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/recommendations-faq.html?lang=en#exclude){target=_blank}

+++

[返回此页面顶部的图表。](#diagram)

## 3.9：提供实体属性以更新产品目录 [!DNL Recommendations] {#entity-attributes}

+++查看详细信息

**读数**

* [实体属性](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

您还可以通过使用创建产品馈送来完成此步骤。 [!DNL Target] 用于更新产品目录的UI [!DNL Recommendations].

+++

[返回此页面顶部的图表。](#diagram)

## 3.10：提供用作包含规则键的配置文件属性 {#keys}

提供用作上述任何Recommendations标准中包含规则的键的配置文件属性。

+++ 查看详细信息

**读数**

* [配置文件属性](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html){target=_blank}

+++

[返回此页面顶部的图表。](#diagram)

## 3.11：触发页面加载请求 {#fire}

此步骤会触发 [!DNL Delivery API] 调用 `execute` > `pageLoad` 请求中的有效负荷。 此 `getOffers()` 方法可获取经验和 `applyOffers()` 呈现页面上的体验。 呈现在中创作的体验需要pageLoad请求 [可视化体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html){target=_blank} (VEC)。

+++查看详细信息

![触发页面加载请求图表](/help/dev/patterns/assets/fire-page-load-request.png){width="100" zoomable="yes"}

**先决条件**

* 必须使用完成所有数据映射 `targetPageParams` 函数。

**读数**

* [adobe.target.getOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)
* [adobe.target.applyOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)

**操作**

* 使用 `getOffers` 和 `applyOffers` 使用页面加载请求API调用获取体验的方法。

+++

[返回此页面顶部的图表。](#diagram)

## 3.12：消防区域定位请求(#location)

此步骤会触发 [!DNL Delivery API] 调用 `execute` > `mboxes` 有效负荷的更改情况。 此 `getOffers` 方法可获取经验和 `applyOffers` 将体验呈现到页面。 您可以在 `execute` > `mboxes` 有效负荷。

+++查看详细信息

![触发区域位置请求图表](/help/dev/patterns/assets/fire-regional-location-request.png){width="100" zoomable="yes"}

**先决条件**

* 必须使用完成所有数据映射 `targetPageParams` 函数。

**读数**

* [adobe.target.getOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)
* [adobe.target.applyOffers()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)

**操作**

* 使用 `getOffers` 和 `applyOffers` 使用页面加载请求API调用获取体验的方法。

+++

[返回此页面顶部的图表。](#diagram)