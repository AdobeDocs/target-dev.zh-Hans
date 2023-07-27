---
title: 设备上决策支持哪些功能？
description: 了解如何使用实时服务器调用，通过机器学习提供最相关且最引人入胜的个性化内容。
feature: APIs/SDKs
exl-id: 15d9870f-6c58-4da0-bfe5-ef23daf7d273
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 10%

---

# 支持的功能概述

[!DNL Adobe Target]的服务器端SDK使开发人员能够灵活地在数据的性能和新鲜度之间进行选择，以便做出决策。 换言之，如果通过机器学习提供最相关且最引人入胜的个性化内容对您来说最重要，则应进行实时服务器调用。 但是，当性能更为关键时，则应该做出设备上决策。 对象 [!UICONTROL 设备上决策] 要正常工作，请参阅以下支持的功能列表：

* 活动类型
* 受众定位
* 分配方法

## 活动类型

下表指明了 [活动类型](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) 使用创建 [基于表单的体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?) 支持或不支持 [!UICONTROL 设备上决策].

| 活动类型 | 受支持 |
| --- | --- |
| [A/B 测试](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html) | 是 |
| [自动分配](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | 否 |
| [Auto-Target（自动定位）](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) | 否 |
| [Analytics for Target](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) (A4T) | 是 |
| [多变量测试](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html) (MVT) | 否 |
| [体验定位](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html) (XT) | 是 |
| [自当个性化](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html) (AP) | 否 |
| [推荐](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html) | 否 |


## 受众定位

下表指明了支持或不支持哪些受众规则 [!UICONTROL 设备上决策].

| 受众规则 | 设备上决策 |
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
| [Experience Cloud受众](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html) (Adobe Audience Manager、Adobe Analytics和Adobe Experience Manager的受众 | 否 |

### 的地理定位 [!UICONTROL 设备上决策]

为了保持几乎零延迟 [!UICONTROL 设备上决策] 具有基于地理位置的受众的活动，Adobe建议您在调用中自己提供地理值， `getOffers`. 为此，请设置 `Geo` 中的对象 `Context` 请求的。 这意味着您的服务器将需要一种方法来确定每个最终用户的位置。 例如，您的服务器可能会使用您配置的服务执行IP到地理位置的查找。 某些托管提供商(如Google Cloud)通过每个提供商中的自定义标头提供此功能 `HttpServletRequest`.

>[!BEGINTABS]

>[!TAB Node.js]

```csharp {line-numbers="true"}
const CONFIG = {
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
    decisioningMethod: "on-device"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
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

>[!TAB Java]

```javascript {line-numbers="true"}
public class TargetRequestUtils {

    public static Context getContext(HttpServletRequest request) {
        Context context = new Context()
            .geo(ipToGeoLookup(request.getRemoteAddr()))
            .channel(ChannelType.WEB)
            .timeOffsetInMinutes(330.0)
            .address(getAddress(request));
        return context;
    }

    public static Geo ipToGeoLookup(String ip) {
        GeoResult geoResult = geoLookupService.lookup(ip);
        return new Geo()
            .city(geoResult.getCity())
            .stateCode(geoResult.getStateCode())
            .countryCode(geoResult.getCountryCode());
    }

}
```

>[!ENDTABS]

但是，如果您无法在服务器上执行IP到地理位置的查找，但仍希望执行 [!UICONTROL 设备上决策] 对象 `getOffers` 包含基于地理位置的受众的请求也支持此功能。 此方法的不利之处在于，它将使用远程IP到地理位置的查找，这会为每个查询添加延迟 `getOffers` 呼叫。 此延迟应低于远程延迟 `getOffers` 调用，因为它点击了位于服务器附近的CDN。 您必须仅提供 `ipAddress` 中的字段 `Geo` 中的对象 `Context` ，以便SDK检索用户IP地址的地理位置。 如果除了 `ipAddress` 提供， [!DNL Target] SDK将不会获取地理位置元数据以进行解析。


>[!BEGINTABS]

>[!TAB Node.js]

```csharp {line-numbers="true"}
const CONFIG = {
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
    decisioningMethod: "on-device"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
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

>[!TAB Java]

```javascript {line-numbers="true"}
public class TargetRequestUtils {

    public static Context getContext(HttpServletRequest request) {
        Context context = new Context()
            .geo(new Geo().ipAddress(request.getRemoteAddr()))
            .channel(ChannelType.WEB)
            .timeOffsetInMinutes(330.0)
            .address(getAddress(request));
        return context;
    }

}
```

>[!ENDTABS]

## 分配方法

下表指明了支持或不支持哪些分配方法 [!UICONTROL 设备上决策].

| 分配方法 | 受支持 |
| --- | --- |
| 手动 | 是 |
| [自动分配到最佳体验](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | 否 |
| [自动定位以提供个性化体验](https://experienceleague.adobe.com/docs/target/using/activities/auto-target-to-optimize.html) | 否 |
