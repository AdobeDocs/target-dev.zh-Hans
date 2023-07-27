---
keywords: 实施， javascript库， js， atjs，设备上决策，设备上决策，支持的功能， $8
description: 了解支持哪些功能 [!UICONTROL 设备上决策].
title: 设备上决策支持哪些功能
feature: at.js
exl-id: bdd65658-6c4a-41ae-a222-59c00a11bdac
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 9%

---

# 支持的功能 [!UICONTROL 设备上决策]

此 [!DNL Adobe Target] JS SDK使客户能够灵活地在数据的性能和新鲜度之间进行选择，以便做出决策。 换言之，如果通过机器学习提供最相关且最引人入胜的个性化内容对您来说最重要，则应进行实时服务器调用。 但是，当性能更加关键时，应该做出设备上决策和内存决策。 对象 [!UICONTROL 设备上决策] 要使其正常工作，请参阅以下列出所支持功能的章节。

## 支持的活动类型

下表指明了 [活动类型](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) 创建者 [基于表单的体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html) 或 [可视化体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html) (VEC)支持或不支持 [!UICONTROL 设备上决策].

| 活动类型 | 受支持? |
| --- | --- |
| [A/B 测试](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html) | 是 |
| [自动分配](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | 否 |
| [Auto-Target（自动定位）](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) ![Premium](../../../assets/premium.png) | 否 |
| [多变量测试](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html) (MVT) | 否 |
| [体验定位](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html) (XT) | 是 |
| [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html) ![Premium](../../../assets/premium.png) | 否 |
| [推荐](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html) ![Premium](../../../assets/premium.png) | 否 |
| [使用Analytics for Target的活动](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?) (A4T) | 是 |

## 受众定位

下表指明了支持或不支持哪些受众规则 [!UICONTROL 设备上决策].

| 受众规则 | 受支持? |
| --- | --- |
| [地域](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html) | 是 |
| [网络](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html) | 否 |
| [移动设备](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html) | 否 |
| [自定义参数](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html) | 是 |
| [操作系统](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html) | 是 |
| [网页](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html) | 是 |
| [浏览器](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html) | 是 |
| [访客资料](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html) | 否 |
| [流量源](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html) | 否 |
| [期限](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html) | 是 |
| Adobe Experience Cloud受众<P>([!DNL Audiences from Adobe Analytics], [!DNL Adobe Audience Manager], 和 [!DNL Adobe Experience Manager]) | 否 |

### 的地理定位 [!UICONTROL 设备上决策]

保持最低延迟 [!UICONTROL 设备上决策] 具有基于地理位置的受众的活动，Adobe建议您在调用中自己提供地理值， [getOffers](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md). 在请求的上下文中设置地理对象。 这意味着通过浏览器来确定每个访客的位置。 例如，您可以使用配置的服务执行IP到地理位置的查找。 某些托管提供商(如Google Cloud)通过每个提供商中的自定义标头提供此功能 `HttpServletRequest`.

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

但是，如果您无法在服务器上执行IP到地理位置的查找，但仍希望执行 [!UICONTROL 设备上决策] 对象 [getOffers](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md) 包含基于地理位置的受众的请求也支持此功能。 此方法的缺点是，它使用远程IP到地理位置的查找，这会为每个查询添加延迟 `getOffers` 呼叫。 滞后时间应小于 `getOffers` 通过服务器端决策调用，因为它会点击位于您服务器附近的CDN。 在请求SDK检索访客IP地址的地理位置的上下文中，在地理对象中仅提供“ipAddress”字段。 如果除了“ipAddress”之外还提供了任何其他字段， [!DNL Target] SDK将不会获取地理位置元数据以进行解析。

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

下表指明了支持或不支持哪些分配方法 [!UICONTROL 设备上决策].

| 分配方法 | 受支持? |
| --- | --- |
| 手动 | 是 |
| [自动分配到最佳体验](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | 否 |
| [自动定位以提供个性化体验](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) | 否 |
