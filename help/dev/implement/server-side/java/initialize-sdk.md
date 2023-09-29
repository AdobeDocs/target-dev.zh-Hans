---
title: 使用create方法初始化Java SDK
description: 了解如何使用create方法初始化Java SDK并实例化 [!UICONTROL TargetClient] 以调用 [!DNL Adobe Target] 用于实验和个性化体验。
feature: APIs/SDKs
exl-id: 0e0ddead-7de8-4549-b81c-e72598558e4b
source-git-commit: 1d080b5e402e5d55039bf06611b44678cc6c36de
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 17%

---

# 初始化 Java SDK

## 描述

使用 `create` 方法，以初始化Java SDK并实例化 [!UICONTROL Target客户端] 以调用 [!DNL Adobe Target] 用于实验和个性化体验。

## 方法

[!UICONTROL TargetClient] 创建工具 `TargetClient.create`.

### 创建

```javascript {line-numbers="true"}
TargetClient TargetClient.create(ClientConfig clientConfig)
```

创建ClientConfig时使用 `ClientConfig.builder`.

```javascript {line-numbers="true"}
ClientConfigBuilder ClientConfig.builder()
```

## 参数

`ClientConfigBuilder` 具有以下结构：

| 名称 | 类型 | 必需 | 默认 | 描述 |
| --- | --- | --- | --- | --- |
| 客户端 | 字符串 | 是 | 无 | [!UICONTROL Target客户端Id] |
| organizationId | 字符串 | 是 | 无 | [!UICONTROL Experience Cloud组织ID] |
| connectTimeout | 数值 | 否 | 10000 | 所有请求的连接超时（以毫秒为单位） |
| sockettimeout | 数值 | 否 | 10000 | 所有请求的套接字超时（以毫秒为单位） |
| maxConnectionsPerHost | 数值 | 否 | 100 | 最大连接数，每 [!DNL Target] 主机 |
| maxConnectionsTotal | 数值 | 否 | 200 | 最大连接数（包括全部） [!DNL Target] 主机 |
| connectionTtlMs | 数值 | 否 | -1 | 总生存时间(TTL)定义持久连接的最大生存时间（以毫秒为单位）。 默认情况下，连接将无限期地保持活动状态 |
| idleConnectionValidationMs | 数值 | 否 | 1000 | 非活动时间段（以毫秒为单位），在此段时间后，将重新验证永久连接后再重新使用 |
| evictIdleConnectionsAfterSecs | 数值 | 否 | 20 | 从连接池中收回空闲连接的时间（以秒为单位） |
| enableRetries | 布尔值 | 否 | true | 套接字超时自动重试（最多4次） |
| logRequests | 布尔值 | 否 | false | 日志 [!DNL Target] debug中的请求和响应 |
| Logrequestatus | 布尔值 | 否 | false | 日志 [!DNL Target] 响应时间、状态和URL |
| serverDomain | 字符串 | 否 | `*client*.tt.omtrdc.net` | 覆盖默认主机名 |
| secure | 布尔值 | 否 | true | 取消设置以强制HTTP方案 |
| requestInterceptor | HttpRequestInterceptor | 否 | 空 | 添加自定义请求侦听器 |
| defaultPropertyToken | 字符串 | 否 | 无 | 设置默认属性令牌的间隔 `getOffers` 呼叫。 **用于设备上决策**&#x200B;时，SDK将仅下载包含在中设置的属性令牌的符合条件的活动的项目 `defaultPropertyToken` |
| defaultDecisioningMethod | DecisioningMethod枚举 | 否 | 服务器端 | 必须设置为ON_DEVICE或HYBRID才能启用设备上决策 |
| telemetryEnable | 布尔值 | 否 | true | 允许客户在请求期间选择退出其他数据收集 [!DNL Target] 服务器 |
| proxyConfig | ClientProxyConfig | 否 | 无 | 允许客户端提供自己的代理详细信息 |
| exceptionHandler | TargetExceptionHandler | 否 | 无 | 可用于在规则处理期间实施自定义例外处理 |
| httpClient | HttpClient | 否 | 无 | 允许用户替换 [!DNL Target] 带有自定义HTTP客户端的HTTP客户端 |
| onDeviceEnvironment | 字符串 | 否 | 生产 | 可用于指定其他设备上环境，如暂存 |
| onDeviceConfigHost | 字符串 | 否 | `assets.adobetarget.com` | 可以指定其他主机来下载设备上决策构件文件 |
| onDeviceDecisioningPollingIntSecs | int | 否 | 300（5分钟） | 从设备端决策工件文件两次获取之间的秒数 |
| onDeviceArtifactPayload | 字节[] | 否 | 无 | 通过先前的工件有效负载提供设备上决策，以允许立即执行 |
| onDeviceDecisioningHandler | OnDeviceDecisioningHandler | 否 | 无 | 注册设备上决策事件的回调 |
| onDeviceAllMatchingRulesMboxes | 列表\&lt;string> | 否 | 无 | 允许用户指定在设备上决策期间将返回其所有匹配规则内容的mbox |

## 示例

### Java

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .build();

TargetClient.create(clientConfig);

// make calls to Adobe Target
```
