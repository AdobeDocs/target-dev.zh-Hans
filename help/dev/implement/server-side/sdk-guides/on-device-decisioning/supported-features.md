---
title: 设备上决策支持哪些功能？
description: 了解如何使用实时服务器调用，通过机器学习提供最相关且最引人入胜的个性化内容。
feature: APIs/SDKs
exl-id: 15d9870f-6c58-4da0-bfe5-ef23daf7d273
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 13%

---

# 支持的功能概述

[!DNL Adobe Target]的服务器端SDK使开发人员能够灵活地在数据的性能和新鲜度之间进行选择，以便做出决策。 换言之，如果通过机器学习提供最相关且最引人入胜的个性化内容对您来说最重要，则应进行实时服务器调用。 但是，当性能更为关键时，则应该做出设备上决策。 要使[!UICONTROL on-device decisioning]正常工作，请参阅以下支持的功能列表：

* 活动类型
* 受众定位
* 分配方法

## 活动类型

下表指明了[!UICONTROL on-device decisioning]支持或不支持使用基于[表单的体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?)创建的[活动类型](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html)。

| 活动类型 | 受支持 |
| --- | --- |
| [A/B 测试](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html) | 是 |
| [自动分配](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | 否 |
| [Auto-Target（自动定位）](https://experienceleague.adobe.com/docs/target/using/activities/auto-target/auto-target-to-optimize.html) | 否 |
| [Analytics for Target](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html) (A4T) | 是 |
| [多变量测试](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html) (MVT) | 否 |
| [体验定位](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html) (XT) | 是 |
| [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html) (AP) | 否 |
| [推荐](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html) | 否 |


## 受众定位

下表指示哪些受众规则受[!UICONTROL on-device decisioning]支持或不受支持。

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
| [时间范围](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html) | 是 |
| [Experience Cloud受众](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html)(来自Adobe Audience Manager、Adobe Analytics和Adobe Experience Manager的受众) | 否 |

### [!UICONTROL on-device decisioning]的地理定位

为了对具有基于地理位置的Adobe的[!UICONTROL on-device decisioning]活动保持近零延迟，Audience建议您在对`getOffers`的调用中自己提供地理值。 为此，请在请求的`Context`中设置`Geo`对象。 这意味着您的服务器将需要一种方法来确定每个最终用户的位置。 例如，您的服务器可能会使用您配置的服务执行IP到地理位置的查找。 某些托管提供商(如Google Cloud)通过每个`HttpServletRequest`中的自定义标头提供此功能。

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

但是，如果您无法在服务器上执行IP到地理位置的查找，但仍希望对包含基于地理位置的受众的`getOffers`请求执行[!UICONTROL on-device decisioning]，则也支持此操作。 此方法的缺点是，它将使用远程IP到地理位置的查找，这将为每个`getOffers`调用添加延迟。 此延迟应低于远程`getOffers`调用，因为它点击了位于服务器附近的CDN。 您必须在请求的`Context`的`Geo`对象中仅提供`ipAddress`字段，以便SDK检索用户IP地址的地理位置。 如果除了`ipAddress`之外还提供了任何其他字段，则[!DNL Target] SDK将不会获取地理位置元数据以进行解析。


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

下表指示[!UICONTROL on-device decisioning]支持或不支持哪些分配方法。

| 分配方法 | 受支持 |
| --- | --- |
| 手动 | 是 |
| [自动分配到最佳体验](https://experienceleague.adobe.com/docs/target/using/activities/auto-allocate/automated-traffic-allocation.html) | 否 |
| [自动定位以提供个性化体验](https://experienceleague.adobe.com/docs/target/using/activities/auto-target-to-optimize.html) | 否 |
