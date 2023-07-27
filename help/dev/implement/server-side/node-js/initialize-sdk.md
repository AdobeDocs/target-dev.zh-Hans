---
title: 使用create方法初始化Node.js SDK
description: 了解如何使用create方法初始化Node.js SDK并实例化 [!DNL Target] 要调用到的客户端 [!DNL Adobe Target] 用于实验和个性化体验。
feature: APIs/SDKs
exl-id: 71516e44-508a-4d8d-9f2b-7c54243e9c60
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 18%

---

# 初始化Node.js SDK

## 描述

使用 `create` 方法，以便初始化Node.js SDK并实例化 [!UICONTROL Target] 要调用到的客户端 [!DNL Adobe Target] 用于实验和个性化体验。

## 方法

**创建**

```js {line-numbers="true"}
TargetClient.create(options: Object): TargetClient
```

## 参数

`options` 具有以下结构：

| 名称 | 类型 | 必需 | 默认 | 描述 |
| --- | --- | --- | --- | --- |
| 客户端 | 字符串 | 是 | 无 | [!UICONTROL Adobe Target客户端ID] |
| organizationId | 字符串 | 是 | 无 | [!UICONTROL Experience Cloud组织ID] |
| environment（环境） | 字符串 | 否 | 生产 | 目标环境名称。 在 [!DNL Target] UI、 [!UICONTROL 管理] > [!UICONTROL 环境]. |
| timeout | 数值 | 否 | 3000 | 超时时间（以毫秒为单位） |
| serverDomain | 字符串 | 否 | `*client*.tt.omtrdc.net` | 覆盖默认主机名 |
| secure | 布尔值 | 否 | true | 取消设置以强制HTTP方案 |
| logger | 对象 | 否 | NOOP记录器 | 替换默认的NOOP记录器 |
| targetLocationHint | 字符串 | 否 | 无 | Target位置提示 |
| fetchApi | 函数 | 否 | global.fetch或window.fetch | [fetch](https://fetch.spec.whatwg.org/) sdk用于http请求。 默认情况下，会使用节点获取或浏览器实现的获取。 但是，可以使用提供替代实施 `fetchApi` |
| propertyToken | 字符串 | 否 | 无 | **目标资产令牌**. 如果在此指定，则所有 `getOffers` 调用将使用此值。 **用于设备上决策**&#x200B;时，SDK将仅下载包含在中设置的属性令牌的符合条件的活动的项目 `propertyToken` |
| 决策方法 | 字符串 | 否 | 服务器端 | 确定要使用的决策方法([设备端](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md)，服务器端，混合) |
| pollingInterval | 数值 | 否 | 300000（5分钟） | 的轮询间隔 [设备上决策规则构件](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md) （以毫秒为单位） |
| artifectlocation | 字符串 | 否 | 无 | 指向的完全限定URL [设备上决策规则构件](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md). 覆盖内部确定的位置。 |
| artifactPayload | 对象 | 否 | 无 | 的JSON有效负荷 [设备上决策规则构件](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md). 如果指定，将使用该值，而不是从URL请求值。 |
| [events](sdk-events.md) | 对象&lt;string function=&quot;&quot;> | 否 | 无 | 具有事件名称键和回调函数值的可选对象 |
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
