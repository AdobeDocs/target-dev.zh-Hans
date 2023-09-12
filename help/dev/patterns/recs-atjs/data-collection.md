---
title: 配置数据收集
description: 请确保数据收集的所有必要任务都按正确顺序执行。
feature: APIs/SDKs
level: Experienced
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 6cd78f8e3cbdd97a09b0cb6ca3af55994e85f819
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 3%

---

# 配置数据收集

请按照 *数据收集* 图可确保数据收集所需的所有必要任务按正确顺序执行。

>[!TIP]
>
>单击本主题中的图像以展开到全屏。

数据层在页面加载期间准备就绪，或者数据层在页面加载后发生更改。

如果您已在以下期间映射数据 [初始化SDK阶段](/help/dev/patterns/recs-atjs/initialize-sdk.md)时，您必须执行以下图表中的步骤：

* 您的数据层将在同一页面上以任何方式增加，并且您要将附加数据发送至 [!DNL Target]
* 要将产品目录数据发送到 [!DNL Target Recommendations]

## 收集数据图表 {#diagram}

下图中的步骤编号与以下部分相对应。

![数据收集图表](/help/dev/patterns/recs-atjs/assets/data-collection-diagram.png){width="600" zoomable="yes"}

单击以下链接以导航到所需的部分：

* [2.1：配置数据映射](#configure)
* [2.2链接到实体属性](#entity-attributes)
* [2.3触发Adobe Target跟踪API](#fire-api)

## 2.1：配置数据映射 {#configure}

此步骤有助于确保必须发送到的所有 [!DNL Adobe Target] 设置。

+++查看详细信息

![配置数据映射图](/help/dev/patterns/recs-atjs/assets/cofigure-data-mapping.png){width="400" zoomable="yes"}

**先决条件**

* 数据层应准备好所有必须发送到的数据 [!DNL Target].

**读数**

[targetPageParams函数](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)

**操作**

使用 `targetPageParams()` 函数，用于设置必须发送到的全部必需数据 [!DNL Target].

+++

[返回此页面顶部的图表。](#diagram)

## 2.2：链接到实体属性 {#entity-attributes}

链接到实体属性以更新产品目录 [!DNL Target Recommendations].

+++查看详细信息

**读数**

* [实体属性](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html){target=_blank}

**注意事项**

* 传递实体属性的另一种方法是更新以下文件中的产品目录： [!DNL Target] 要使用的UI [Recommendations产品信息源](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/feeds.html){target=_blank}.
* 传递实体属性仅适用于数据层中有产品目录数据的页面。
* 传递 `entity.event.detailsOnly=true` 任何调用中的参数优先。

+++

[返回此页面顶部的图表。](#diagram)

## 2.3触发Adobe Target跟踪API {#fire-api}

此步骤有助于确保必须发送到的所有 [!DNL Target] 已发送。

+++查看详细信息

![Fire Adobe Target跟踪API图](/help/dev/patterns/recs-atjs/assets/fire-track-api.png){width="400" zoomable="yes"}

**先决条件**

* 必须使用完成所有数据映射 [targetPageParams函数](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md).

**读数**

* [adobe.target.trackEvent()方法](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)

**操作**

使用 [adobe.target.trackEvent()方法](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md) 以发送所有必须发送到的数据 [!DNL Target].

+++

[返回此页面顶部的图表。](#diagram)

