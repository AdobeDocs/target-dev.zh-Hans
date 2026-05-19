---
title: 配置数据收集
description: 请确保数据收集的所有必要任务都按正确顺序执行。
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: 66e0f18d-c78c-463b-8c47-132ef6332927
TQID: https://experienceleague.adobe.com/fg3xJnwYAVyz-N-xzT5Piu35Ajd2UMEvuTvTQs2wj3c
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 401
ht-degree: 1%

---

# 配置数据收集

请按照&#x200B;*数据收集*&#x200B;图中的步骤操作，以确保数据收集所需的所有必要任务都按正确的顺序执行。

>[!TIP]
>
>单击本主题中的图像以展开到全屏。

数据层在页面加载期间准备就绪，或者数据层在页面加载后发生更改。

如果在[初始化SDK阶段](/help/dev/patterns/recs-atjs/initialize-sdk.md)期间已映射数据，则在下列情况下必须执行此图中的步骤：

* 您的数据层在同一页面上以任何方式增加，并且您想要将该附加数据发送到[!DNL Target]
* 要将产品目录数据发送到[!DNL Target Recommendations]

## 收集数据图表 {#diagram}

下图中的步骤编号与以下部分相对应。

![数据收集图表](/help/dev/patterns/recs-atjs/assets/data-collection-diagram.png){width="600" zoomable="yes"}

单击以下链接以导航到所需的部分：

* [2.1：配置数据映射](#configure)
* [2.2链接到实体属性](#entity-attributes)
* [2.3触发Adobe Target跟踪API](#fire-api)

## 2.1：配置数据映射 {#configure}

此步骤有助于确保设置必须发送到[!DNL Adobe Target]的所有数据。

+++查看详细信息

![配置数据映射关系图](/help/dev/patterns/recs-atjs/assets/configure-data-mapping-combined.png){width="400" zoomable="yes"}

**先决条件**

* 数据层应准备好所有必须发送到[!DNL Target]的数据。

**读数**

[targetPageParams函数](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)

**操作**

使用`targetPageParams()`函数设置必须发送到[!DNL Target]的所有必需数据。

+++

[返回此页面顶部的图表。](#diagram)

## 2.2：链接到实体属性 {#entity-attributes}

链接到实体属性以更新[!DNL Target Recommendations]的产品目录。

+++查看详细信息

**读数**

* [实体属性](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html?lang=zh-Hans){target=_blank}

**注意事项**

* 传递实体属性的另一种方法是更新[!DNL Target] UI中的产品目录以使用[Recommendations产品馈送](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/feeds.html?lang=zh-Hans){target=_blank}。
* 传递实体属性仅适用于数据层中有产品目录数据的页面。
* 在任何调用中传递`entity.event.detailsOnly=true`参数具有优先权。

+++

[返回此页面顶部的图表。](#diagram)

## 2.3触发Adobe Target跟踪API {#fire-api}

此步骤有助于确保必须发送到[!DNL Target]的所有数据均已发送。

+++查看详细信息

![触发Adobe Target跟踪API关系图](/help/dev/patterns/recs-atjs/assets/fire-track-api-combined.png){width="400" zoomable="yes"}

**先决条件**

* 必须已使用[targetPageParams函数](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)完成所有数据映射。

**读数**

* [adobe.target.trackEvent()方法](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)

**操作**

使用[adobe.target.trackEvent()方法](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)发送必须发送到[!DNL Target]的所有数据。

+++

[返回此页面顶部的图表。](#diagram)

继续步骤3：[渲染体验](/help/dev/patterns/recs-atjs/render-experiences.md)
