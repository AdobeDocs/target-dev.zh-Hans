---
title: 初始化SDK
description: 确保加载 [!DNL Adobe Target] at.js JavaScript库以正确的顺序执行。
feature: APIs/SDKs
level: Experienced
role: Developer
source-git-commit: 723bb2f33a011995757009193ee9c48757ae1213
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 8%

---

# 初始化SDK

请按照 *初始化SDK* 确保加载 [!DNL Adobe Target] at.js JavaScript库以正确的顺序执行。

>[!TIP]
>
>单击本主题中的图像以展开到全屏。

## 初始化SDK图 {#diagram}

对于多页面应用程序，每当页面重新加载或访客导航到网站上的新页面时，就会出现此流程。

>[!NOTE]
>
>下图中的步骤编号与以下部分相对应。 步骤编号没有特定顺序，并且不反映中执行的步骤顺序 [!DNL Target] 创建活动时的UI。

![初始化SDK图](/help/dev/patterns/recs-atjs/assets/diagram-initiaze-sdk.png){width="600" zoomable="yes"}

单击以下链接以导航到所需的部分：

* [1.1：加载访客API SDK](#load)
* [1.2：设置客户Id](#set)
* [1.3：配置自动页面加载请求](#automatic)
* [1.4：配置闪烁处理](#flicker)
* [1.5：配置数据映射](#data-mapping)
* [1.6：促销活动](#promotion)
* [1.7：基于购物车的标准](#cart)
* [1.8：基于热门程度的标准](#popularity)
* [1.9：基于项目的标准](#item)
* [1.10：基于用户的标准](#user)
* [1.11：自定义标准](#custom)
* [1.12：提供包含规则中使用的属性](#inclusion)
* [1.13：提供excludedIds](#exclude)
* [1.14：传递entity.event.detailsOnly=true参数](#true)
* [1.15：配置远程数据映射](#remote)
* [1.16：加载at.js](#web)

## 1.1：加载访客API SDK {#load}

此步骤有助于确保 `VisitorAPI.js` 库已正确加载、配置和初始化。

+++查看详细信息

![加载访客API SDK图](/help/dev/patterns/recs-atjs/assets/load-visitor-combined.png){width="400" zoomable="yes"}

**先决条件**

* 要使用访客ID/API服务，您的公司必须启用 [!DNL Adobe Experience Cloud] 并拥有 [!UICONTROL 组织ID]. 有关更多信息，请参阅 [Experience Cloud要求：组织ID](https://experienceleague.adobe.com/docs/id-service/using/reference/requirements.html?){target=_blank} 在 *Identity服务帮助* 指南。
* 您需要 `VisitorAPI.js` 文件。 如果您拥有，则应该已经拥有此文件 [!DNL Adobe Analytics] 已实施。 此文件也可以通过 [[!DNL Adobe Experience Platform] 标记扩展](https://experienceleague.adobe.com/docs/tags.html){target=_blank} or can be downloaded from the [Adobe Analytics Code Manager](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-analytics.html){target=_blank}.

**配置和引用VisitorAPI.js**

有关更多信息，请参阅 [实施适用于Target的Experience Cloud服务](https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-target.html){target=_blank}.

**读数**

* [Experience CloudIdentity Service概述](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html){target=_blank}
* [关于ID服务](https://experienceleague.adobe.com/docs/id-service/using/intro/about-id-service.html){target=_blank}
* [Cookie 和 Experience Cloud 标识服务](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html){target=_blank}
* [Experience CloudIdentity服务如何请求和设置ID](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html){target=_blank}
* [了解ID同步和匹配率](https://experienceleague.adobe.com/docs/id-service/using/intro/match-rates.html){target=_blank}

**操作**

* 嵌入 `VisitorAPI.js` 文件。
* 了解 [访客ID/API服务的可用配置](https://experienceleague.adobe.com/docs/id-service/using/reference/requirements.html){target=_blank}.
* 在 `VisitorAPI.js` 文件已加载，请使用 `Visitor.getInstance` 方法，以使用所需的配置进行初始化。
* 熟悉 [可用方法](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/get-set.html){target=_blank}.

+++

[返回此页面顶部的图表。](#diagram)

## 1.2：设置客户Id {#set}

此步骤可帮助确保将访客的已知ID（CRM ID、用户ID等）与的匿名ID绑定 [!DNL Adobe] 用于跨设备个性化。

+++查看详细信息

![设置客户ID](/help/dev/patterns/recs-atjs/assets/set-customer-id-combined.png){width="400" zoomable="yes"}

**先决条件**

* 访客的已知ID应该可以在Data Layer中使用。

**设置客户ID**
有关更多信息，请参阅 [setCustomerIds](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html){target=_blank}.

**读数**

* [mbox3rdPartyId 的实时配置文件同步](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html){target=_blank}

**操作**

* 使用 `visitor.setCustomerIDs` 设置访客已知ID。

+++

[返回此页面顶部的图表。](#diagram)

## 1.3：配置自动页面加载请求 {#automatic}

此步骤使at.js能够获取在加载at.js JavaScript库文件时必须在页面上渲染的所有体验。

+++查看详细信息

![配置自动页面加载请求](/help/dev/patterns/recs-atjs/assets/configure-automatic-page-request-combined.png){width="400" zoomable="yes"}

**先决条件**

* 并非数据层中的所有数据都必须发送到 [!DNL Target]. 请咨询您的业务团队（数字营销团队），确定哪些数据对于实验、优化和个性化很有价值。 仅应将此数据发送至 [!DNL Target].
* 确保您不会将任何个人身份信息(PII)数据发送至 [!DNL Target].

**配置自动页面加载请求**

有关更多信息，请参阅 [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md)。

**读数**

了解 `pageLoadEnabled` 在中设置 [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**操作**

* 修改 `window.targetGlobalSettings` 对象以启用自动页面加载请求。

+++

[返回此页面顶部的图表。](#diagram)

## 1.4：配置闪烁处理 {#flicker}

此步骤有助于确保在交付体验时不会出现页面闪烁。

+++查看详细信息

![配置闪烁处理图](/help/dev/patterns/recs-atjs/assets/flicker-handling-combined.png){width="400" zoomable="yes"}

**先决条件**

* 与负责网页性能的团队讨论使用at.js使用的默认方法控制闪烁的利弊。 您可以搜索设计模式，以便使用自定义闪烁处理解决方案，如加载器动画。 如果找不到模式，则可以请求一个新模式。

**配置闪烁处理**

有关更多信息，请参阅 [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md)。

设置 `bodyHidingEnabled` 到 `true` 在页面加载请求进行中时隐藏整个页面正文。 如果出于任何原因（例如，数据稍后未准备就绪）未启用自动页面加载请求，则最好将此设置设置为 `false`.

如果您已禁用 `bodyHidingEnabled` 由于您不希望触发APLR并希望稍后触发页面请求，或者您不需要进行闪烁处理，因此必须实施自己的闪烁处理。 您可以通过两种方式处理闪烁：隐藏受测试区域，或在受测试区域上显示引发器。

**读数**

* [at.js 如何管理闪烁](/help/dev/implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md)
* 了解bodyHiddenStyle和bodyHidingEnabled对象 [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

**操作**

* 修改 `window.targetGlobalSettings` 要设置的对象 `bodyHiddenStyle` 和 `bodyHidingEnabled`.

+++

[返回此页面顶部的图表。](#diagram)

## 1.5：配置数据映射 {#data-mapping}

此步骤有助于确保必须发送到的所有 [!DNL Target] 设置。

+++查看详细信息

![数据映射图](/help/dev/patterns/recs-atjs/assets/data-mapping-combined.png){width="400" zoomable="yes"}

**先决条件**

* 数据层应准备好所有必须发送到的数据 [!DNL Target].
* Recommendations：扩充用户档案。
   * 通过 `entity.id` 用于根据基于上次查看产品的标准，捕获最近查看标准和项目的数据。
   * 通过 `entity.id` 用于根据最喜爱的类别捕获热门程度标准的数据。
   * 如果自定义标准基于配置文件属性，或者在任何标准的包含规则筛选中使用配置文件属性，请传递该属性。
* Recommendations：摄取产品数据。
   * 可以传递其他实体参数（保留和自定义）以摄取或更新中的产品目录 [!DNL Recommendations].
   * 产品目录也可以通过使用实体源进行更新。 [!DNL Target] ui或API。

**将数据映射到[!DNL Target]**

有关更多信息，请参阅 [targetPageParams()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md).

**读数**

* [targetPageParams()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)
* [计划和实施推荐](/help/dev/implement/recommendations/recommendations.md)
* [设置您的Recommendations目录](/help/dev/implement/recommendations/recommendations.md)

**操作**

* 使用 `targetPageParams()` 函数，用于设置必须发送到的全部必需数据 [!DNL Target].

+++

[返回此页面顶部的图表。](#diagram)

## 1.6：促销活动 {#promotion}

添加促销项目并控制它们在中的位置 [!DNL Target Recommendations] [设计](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-design/create-design.html){target=_blank}.

+++查看详细信息

**可用选项**

* 按ID提升
* [按收藏集促销](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/collections.html){target=_blank}
* [按属性促销](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**需要实体参数**

* 使用“按属性促销”选项时，必须传递促销中的项目属性。

+++

[返回此页面顶部的图表。](#diagram)

## 1.7：基于购物车的标准 {#cart}

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

## 1.8：基于热门程度的标准 {#popularity}

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

* `entity.categoryId` 或基于热门程度的项目属性（如果标准基于当前项目或项目属性）。
* 对于网站中的“查看次数最多”/“销售最高”页面，无需传递任何内容。

**读数**

* [基于热门程度](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[返回此页面顶部的图表。](#diagram)

## 1.9：基于项目的标准 {#item}

根据查找的用户正在查看或最近查看过的项目的相似项目提供推荐。

+++查看详细信息

**可用标准**

* [!UICONTROL 查看了这个项目，也查看了那个项目的人]
* [!UICONTROL 查看了这个项目，但购买了那个项目的人]
* [!UICONTROL 购买了这个项目，也购买了那个项目的人]
* [!UICONTROL 具有相似属性的项目]

**需要实体参数**

* `entity.id` 或任何用作键的配置文件属性

**读数**

* [基于项目](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[返回此页面顶部的图表。](#diagram)

## 1.10：基于用户的标准 {#user}

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

## 1.11：自定义标准 {#custom}

根据您上传的自定义文件提出推荐。

+++查看详细信息

**可用标准**

* [!UICONTROL 自定义算法]

**需要实体参数**

`entity.id` 或用作自定义算法键的属性

**读数**

* [自定义标准](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/algorithms.html?lang=en#section_885B3BB1B43048A88A8926F6B76FC482){target=_blank}

+++

[返回此页面顶部的图表。](#diagram)

## 1.12：提供包含规则中使用的属性 {#inclusion}

+++查看详细信息

**读数**

* [使用动态和静态包含规则](https://experienceleague.adobe.com/docs/target/using/recommendations/criteria/dynamic-static/use-dynamic-and-static-inclusion-rules.html){target=_blank}

+++

[返回此页面顶部的图表。](#diagram)

## 1.13：提供excludedIds {#exclude}

传递要从推荐中排除的实体ID。 例如，可排除购物车中已有的商品。

+++查看详细信息

**读数**

* [能否动态地排除实体？](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/recommendations-faq.html?lang=en#exclude){target=_blank}

+++

[返回此页面顶部的图表。](#diagram)

## 1.14：通过 `entity.event.detailsOnly=true` 参数 {#true}

可使用实体属性，将产品或内容信息传递到 [!DNL Target Recommendations].

+++查看详细信息

**读数**

* [实体属性](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html?lang=en){target=_blank}

+++

[返回此页面顶部的图表。](#diagram)

## 1.15：配置远程数据映射（远程）

此步骤可确保必须发送到的所有 [!DNL Target] 设置。

+++查看详细信息

![远程数据映射图](/help/dev/patterns/recs-atjs/assets/remote-data-mapping-combined.png){width="400" zoomable="yes"}

**先决条件**

* 数据层应准备好所有必须发送到的数据 [!DNL Target].

**设置数据提供程序**

有关更多信息，请参阅 [数据提供程序](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers).

**读数**

[targetPageParams函数](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)

**操作**

使用 `targetPageParams()` 函数，用于设置必须发送到的全部必需数据 [!DNL Target].

+++

[返回此页面顶部的图表。](#diagram)

## 1.16：加载at.js {#web}

此步骤可确保加载并初始化at.js JavaScript库。

+++查看详细信息

![加载Adobe Target at.js图](/help/dev/patterns/recs-atjs/assets/load-atjs-combined.png){width="400" zoomable="yes"}

**先决条件**

* 下载或请求您的数字营销团队获得 `at.js 2.*x*` javascript库文件。

*读数*

* [Target 的工作方式](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html){target=_blank}
* [at.js 的工作原理](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md)
* [不通过标记管理器实施 Target](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md)

**操作**

在必须进行试验、优化、个性化和数据收集的所有网页上嵌入at.js文件。

+++

[返回此页面顶部的图表。](#diagram)

继续执行步骤2： [配置数据收集](/help/dev/patterns/recs-atjs/data-collection.md).





























