---
title: 受众定位
description: 受众可用于定向您的试验性和个性化活动。 [!DNL Adobe Target] 支持多种现成的强大受众定位功能。
exl-id: df1bd856-e848-452c-90a0-abf29e7a2313
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 22%

---

# 受众定位

## 概述

受众可用于定向您的试验性和个性化活动。 [!DNL Adobe Target]支持多种现成的强大受众定位功能。 以下属性可用于[受众定位](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/create-audience.html?lang=zh-Hans)：

### [!DNL Target]库

有关详细信息，请参阅[[!DNL Target] 库](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-library.html?lang=zh-Hans)。
&#x200B;AEM
* 反向链接来自Bing
* Chrome Browser
* Firefox浏览器
* 反向链接来自Google
* Internet Explorer
* Linux操作系统
* Mac操作系统操作系统
* 新访客
* 旧访客
* Safari浏览器
* 平板电脑设备
* Windows操作系统
* 反向链接来自Yahoo

### 地域

有关详细信息，请参阅[地域](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html?lang=zh-Hans)。
&#x200B;&#x200B;
* 国家/地区
* 省/自治区/直辖市
* 城市
* 邮政编码
* 纬度
* 经度
* DMA
* 移动设备运营商

### 网络

有关详细信息，请参阅[网络](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html?lang=zh-Hans)。

* ISP
* 域名
* 连接速度

### 移动设备

有关更多信息，请参阅[移动设备](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html?lang=zh-Hans)。

* 设备营销名称
* 设备型号
* 设备供应商
* 是移动设备
* 是移动电话
* 是平板电脑
* 操作系统
* 屏幕高度（像素）
* 屏幕宽度（像素）

### 自定义

有关详细信息，请参阅[自定义参数](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html?lang=zh-Hans)。

* 任意键/值对

### 操作系统

有关详细信息，请参阅[操作系统](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html?lang=zh-Hans)。

* Linux
* Macintosh
* Windows

### 网站页面

有关详细信息，请参阅[网站页面](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html?lang=zh-Hans)。

* 当前页面
* 上一页面
* 登录页面
* HTTP 头

### 浏览器

有关详细信息，请参阅[浏览器](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html?lang=zh-Hans)。

* 类型
* 语言
* 版本

### 访客个人资料

有关详细信息，请参阅[访客资料](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html?lang=zh-Hans)。

* 任何键/值对，将保留

### 流量源

有关详细信息，请参阅[流量源](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html?lang=zh-Hans)。

* 来自 Baidu
* 来自 Bing
* 来自 Google
* 来自 Yahoo
* 引荐登陆页面: URL
* 引荐登陆页面: 域
* 引荐登陆页面: 查询

### 时间范围

有关更多信息，请参阅[期限](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html?lang=zh-Hans)。

* 开始日期/结束日期

## 客户端提示

[!DNL Adobe Target]需要客户端提示才能正确划分浏览器、操作系统和移动设备受众属性，以及某些配置文件脚本实例。 有关更多背景信息，请参阅[用户代理和客户端提示](../../../client-side/atjs/user-agent-and-client-hints.md)。

### 如何将客户端提示传递给[!DNL Adobe Target]

从Node.js SDK v2.4.0和Java SDK v2.3.0开始，可以通过`getOffers()`调用将客户端提示发送到[!DNL Target]。 `request.context`对象上应包含客户端提示以及用户代理。

>[!BEGINTABS]

>[!TAB Node.js SDK]

```js {line-numbers="true"}
targetClient.getOffers({ 
    request: { 
        context: { 
            channel: "mobile" 
            userAgent: "Mozilla/5.0 (Linux; Android 12; Pixel 4a) AppleWebKit/537.36 (KHTML, like Gecko) Mobile Safari/537.36", 
            clientHints: { 
                mobile: "true", 
                platform: "Linux", 
                platformVersion: "12.1", 
                model: "Pixel 4a", 
                browserUAWithMajorVersion: "\"Not A;Brand\";v=\"98\", \"Chromium\";v=\"98\", \"Google Chrome\";v=\"98\"", 
                browserUAWithFullVersion: "\" Not A;Brand\";v=\"98.0.0.0\", \"Chromium\";v=\"98.0.4844.83\", \"Google Chrome\";v=\"98.0.4758.101\"", 
                bitness: "64", 
                architecture: "x86" 
            } 
        }, 
        execute: { 
            mboxes: [{ 
                name: "home", 
                index: 1 
            }] 
        } 
    } 
});
```

>[!TAB Java SDK]

```javascript {line-numbers="true"}
import com.adobe.target.delivery.v1.model.ClientHints; 
import com.adobe.target.delivery.v1.model.Context; 
import com.adobe.target.delivery.v1.model.ExecuteRequest; 
import com.adobe.target.edge.client.model.TargetDeliveryRequest; 

 
ClientHints clientHints = new ClientHints(); 
clientHints.setMobile(true); 
clientHints.setPlatform("macOS"); 
clientHints.setArchitecture("x86"); 
clientHints.setPlatformVersion("11.3.1"); 
clientHints.setBrowserUAWithMajorVersion( 
  "\" Not A;Brand\";v=\"99\", \"Chromium\";v=\"99\", \"Google Chrome\";v=\"99\""); 
String userAgent = 
  "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Safari/537.36"; 

 
TargetDeliveryRequest request = TargetDeliveryRequest.builder() 
        .execute(new ExecuteRequest().pageLoad(pageLoad)) 
        .context(new Context().clientHints(clientHints).userAgent(userAgent)) 
        .build(); 
```

>[!ENDTABS]

## 设备上决策

下表指明了设备上决策支持或不支持哪些受众规则。

| 受众规则 | 设备上决策 |
| --- | --- |
| [地域](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html?lang=zh-Hans) | 是 |
| [网络](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html?lang=zh-Hans) | 否 |
| [移动设备](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html?lang=zh-Hans) | 否 |
| [自定义参数](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html?lang=zh-Hans) | 是 |
| [操作系统](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html?lang=zh-Hans) | 是 |
| [网页](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html?lang=zh-Hans) | 是 |
| [浏览器](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html?lang=zh-Hans) | 是 |
| [访客资料](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html?lang=zh-Hans) | 否 |
| [流量源](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html?lang=zh-Hans) | 否 |
| [时间范围](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html?lang=zh-Hans) | 是 |
| [Experience Cloud受众](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html?lang=zh-Hans)(来自Adobe Audience Manager、Adobe Analytics和Adobe Experience Manager的受众) | 否 |

### 针对设备上决策的地理定位

为了保持基于地理位置的受众的设备上决策活动的几乎零延迟，Adobe建议您在对`getOffers`的调用中自己提供地理值。 为此，请在请求的`Context`中设置`Geo`对象。 这意味着您的服务器将需要一种方法来确定每个最终用户的位置。 例如，您的服务器可能会使用您配置的服务执行IP到地理位置的查找。 某些托管提供商(如Google Cloud)通过每个`HttpServletRequest`中的自定义标头提供此功能。

>[!BEGINTABS]

>[!TAB Node.js SDK]

```js {line-numbers="true"}
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

>[!TAB Java SDK]

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

但是，如果您无法在服务器上执行IP到地理位置的查找，但仍希望对包含基于地理位置的受众的`getOffers`请求执行设备端决策，则也支持此操作。 此方法的缺点是，它将使用远程IP到地理位置的查找，这将为每个`getOffers`调用添加延迟。 此延迟应低于远程`getOffers`调用，因为它点击了位于服务器附近的CDN。 您必须&#x200B;**仅**&#x200B;在请求`Context`的`Geo`对象中提供`ipAddress`字段，SDK才能检索用户IP地址的地理位置。 如果除了`ipAddress`之外还提供了任何其他字段，则[!DNL Target] SDK将不会获取地理位置元数据以进行解析。

>[!BEGINTABS]

>[!TAB Node.js SDK]

```js {line-numbers="true"}
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

>[!TAB Java SDK]

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

## 服务器端决策

下表指明了服务器端决策支持或不支持哪些受众规则。

| 受众规则 | 服务器端决策 |
| --- | --- |
| [地域](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/geo.html?lang=zh-Hans) | 是 |
| [网络](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/network.html?lang=zh-Hans) | 是 |
| [移动设备](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/mobile.html?lang=zh-Hans) | 是 |
| [自定义参数](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html?lang=zh-Hans) | 是 |
| [操作系统](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/operating-system.html?lang=zh-Hans) | 是 |
| [网页](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/site-pages.html?lang=zh-Hans) | 是 |
| [浏览器](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/browser.html?lang=zh-Hans) | 是 |
| [访客资料](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html?lang=zh-Hans) | 是 |
| [流量源](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html?lang=zh-Hans) | 是 |
| [时间范围](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/time-frame.html?lang=zh-Hans) | 是 |
| [Experience Cloud受众](https://experienceleague.adobe.com/docs/target/using/integrate/mmp.html?lang=zh-Hans)(来自Adobe Audience Manager、Adobe Analytics和Adobe Experience Manager的受众) | 是 |
