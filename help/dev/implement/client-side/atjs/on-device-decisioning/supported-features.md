---
keywords: 实施， javascript库， js， atjs，设备上决策，设备上决策，支持的功能， $8
description: 了解[!UICONTROL on-device decisioning]支持哪些功能。
title: 设备上决策支持哪些功能
feature: at.js
exl-id: bdd65658-6c4a-41ae-a222-59c00a11bdac
source-git-commit: 79ffa3f58d780f587fe1202b82d3860395504dfe
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 12%

---

# [!UICONTROL on-device decisioning]支持的功能

[!DNL Adobe Target] JS SDK使客户能够灵活地选择数据的性能和新鲜度以供决策。 换言之，如果通过机器学习提供最相关且最引人入胜的个性化内容对您来说最重要，则应进行实时服务器调用。 但是，当性能更加关键时，应该做出设备上决策和内存决策。 要使[!UICONTROL on-device decisioning]正常工作，请参阅以下部分，其中列出了支持的功能。

## 支持的活动类型

下表指明了[!UICONTROL on-device decisioning]支持或不支持由基于[表单的体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html)或[可视化体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC)创建的[活动类型](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html)。

| 活动类型 | 受支持? |
| --- | --- |
| [A/B 测试](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html) | 是 |
| [自动分配](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | 否 |
| [自动定位](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) ![高级版](../../../assets/premium.png) | 否 |
| [多变量测试](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html) (MVT) | 否 |
| [体验定位](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html) (XT) | 是 |
| [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html) ![高级版](../../../assets/premium.png) | 否 |
| [Recommendations](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html) ![高级版](../../../assets/premium.png) | 否 |
| 使用Analytics for Target [&#128279;](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?) (A4T)的活动 | 是 |

## 受众定位

下表指示哪些受众规则受[!UICONTROL on-device decisioning]支持或不受支持。

| 受众规则 | 受支持? |
| --- | --- |
| [地域](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html) | 是<P>使用设备上决策时，支持以下地理属性：<ul><li>国家/地区</li><li>城市</li><li>纬度</li><li>经度</li></ul> |
| [网络](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html) | 否 |
| [移动设备](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html) | 否 |
| [自定义参数](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html) | 是 |
| [操作系统](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html) | 是 |
| [网页](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html) | 是 |
| [浏览器](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html) | 是 |
| [访客资料](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html) | 否 |
| [流量源](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html) | 否 |
| [时间范围](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html) | 是 |
| Adobe Experience Cloud受众<P>（[!DNL Audiences from Adobe Analytics]、[!DNL Adobe Audience Manager]和[!DNL Adobe Experience Manager]） | 否 |

### [!UICONTROL on-device decisioning]的地理定位

为了保持对基于地理位置的Adobe的[!UICONTROL on-device decisioning]活动延迟最短，建议您在调用[getOffers](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)时自行提供地理位置值。 在请求的上下文中设置地理对象。 这意味着通过浏览器来确定每个访客的位置。 例如，您可以使用配置的服务执行IP到地理位置的查找。 某些托管提供商(如Google Cloud)通过每个`HttpServletRequest`中的自定义标头提供此功能。

```javascript {line-numbers="true"}
window.adobe.target.getOffers({ 
    decisioningMethod: "on-device", 
    request: { 
        context: { 
            geo: { 
                city: "SAN FRANCISCO", 
                countryCode: "US", 
                stateCode: "CA", 
                latitude: 37.75, 
                longitude: -122.4 
            } 
        }, 
        execute: { 
            pageLoad: {} 
        } 
    } 
})
```

但是，如果您无法在服务器上执行IP到地理位置的查找，但仍希望对包含基于地理位置的受众的[getOffers](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)请求执行[!UICONTROL on-device decisioning]，则也支持此操作。 此方法的缺点是，它使用远程IP到地理位置的查找，这会增加每个`getOffers`调用的延迟。 此延迟应低于具有服务器端决策的`getOffers`调用，因为它点击了位于服务器附近的CDN。 在请求SDK检索访客IP地址的地理位置的上下文中，在地理对象中仅提供“ipAddress”字段。 如果除了“ipAddress”之外还提供了任何其他字段，[!DNL Target] SDK将不会获取地理位置元数据以进行解析。

```javascript {line-numbers="true"}
window.adobe.target.getOffers({ 
    decisioningMethod: "on-device", 
    request: { 
        context: { 
            geo: { 
                ipAddress: "127.0.0.1" 
            } 
        }, 
        execute: { 
            pageLoad: {} 
        } 
    } 
})
```

### 分配方法

下表指示[!UICONTROL on-device decisioning]支持或不支持哪些分配方法。

| 分配方法 | 受支持? |
| --- | --- |
| 手动 | 是 |
| [自动分配到最佳体验](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | 否 |
| [自动定位以提供个性化体验](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) | 否 |
