---
title: 使用create方法初始化Node.js SDK
description: 了解如何使用create方法初始化Node.js SDK并实例化 [!DNL Target] 客户端以调用 [!DNL Adobe Target] 进行实验及个性化体验。
feature: APIs/SDKs
exl-id: 71516e44-508a-4d8d-9f2b-7c54243e9c60
TQID: https://experienceleague.adobe.com/uawle0-l5bcv-FuXMLkPc8kIf8DvbkRqAYelr-ehNLk
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 321
ht-degree: 18%

---

# 初始化Node.js SDK

## 描述

使用`create`方法初始化Node.js SDK并实例化[!UICONTROL Target]客户端以调用[!DNL Adobe Target]进行实验和个性化体验。

## 方法

**创建**

```js {line-numbers="true"}
TargetClient.create(options: Object): TargetClient
```

## 参数

`options`具有以下结构：

| 名称 | 类型 | 必需 | 默认 | 描述 |
| --- | --- | --- | --- | --- |
| 客户端 | 字符串 | 是 | 无 | [!UICONTROL Adobe Target Client ID] |
| organizationId | 字符串 | 是 | 无 | [!UICONTROL Experience Cloud Organization ID] |
| 环境 | 字符串 | 否 | 生产 | 目标环境名称。 在[!DNL Target]用户界面中，[!UICONTROL Administration] > [!UICONTROL Environments]。 |
| timeout | 数值 | 否 | 3000 | 超时时间（以毫秒为单位） |
| serverDomain | 字符串 | 否 | `*client*.tt.omtrdc.net` | 覆盖默认主机名 |
| secure | 布尔值 | 否 | true | 取消设置以强制HTTP方案 |
| logger | 对象 | 否 | NOOP记录器 | 替换默认的NOOP记录器 |
| targetLocationHint | 字符串 | 否 | 无 | Target位置提示 |
| fetchApi | 函数 | 否 | global.fetch或window.fetch | SDK已将[fetch](https://fetch.spec.whatwg.org/)用于http请求。 默认情况下，会使用节点获取或浏览器实现的获取。 但可以使用`fetchApi`提供替代实现 |
| propertyToken | 字符串 | 否 | 无 | **目标属性令牌**。 如果在此处指定，则所有`getOffers`调用都将使用此值。 **对于设备上决策**，SDK将仅下载包含在`propertyToken`中设置的属性令牌的合格活动的项目 |
| 决策方法 | 字符串 | 否 | 服务器端 | 确定要使用的决策方法（[设备上](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md)，服务器端，混合） |
| pollingInterval | 数值 | 否 | 300000（5分钟） | [设备上决策规则构件](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md)的轮询间隔（以毫秒为单位） |
| artifectlocation | 字符串 | 否 | 无 | [设备上决策规则项目](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md)的完全限定URL。 覆盖内部确定的位置。 |
| artifactPayload | 对象 | 否 | 无 | [设备上决策规则项目](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md)的JSON有效负荷。 如果指定，将使用该值，而不是从URL请求值。 |
| [events](sdk-events.md) | 对象&lt;字符串，函数> | 否 | 无 | 具有事件名称键和回调函数值的可选对象 |
| telemetryEnable | 布尔值 | 否 | true | 启用后，Adobe将收集SDK功能使用情况和性能遥测数据。 不收集个人数据。 |

## 示例

### Node.js

```js {line-numbers="true"}
const CONFIG = {
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
    events: {clientReady: targetClientReady }
};

const targetClient = TargetClient.create(CONFIG);

function targetClientReady() {
    // make calls to Adobe Target
}
```
