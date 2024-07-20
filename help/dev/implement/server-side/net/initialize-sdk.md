---
title: 使用create方法初始化.NET SDK
description: 了解如何使用create方法初始化Java SDK并实例化[!UICONTROL TargetClient]以调用 [!DNL Adobe Target] 进行实验和个性化体验。
feature: APIs/SDKs
exl-id: 501010c3-22f4-49a8-b2ac-c7307232d180
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 16%

---

# 初始化.NET SDK

## 描述

使用`Create`方法初始化.NET SDK并实例化[!UICONTROL Target Client]以调用[!DNL Adobe Target]进行实验和个性化体验。

使用.NET依赖项注入时，只需在服务配置步骤中通过调用`services.AddTargetLibrary()`添加SDK；然后在应用程序的构造函数中插入`ITargetClient targetClient`。

之后，使用SDK的`Initialize`方法配置SDK，从而完成初始化步骤。

## 方法

`TargetClient`是使用`TargetClient.Create`创建的。

## C\
#

```csharp {line-numbers="true"}
TargetClient TargetClient.Create(TargetClientConfig clientConfig)
```

`ClientConfig`是使用ClientConfig.Builder创建的。

## C\
#

```csharp {line-numbers="true"}
TargetClientConfig.Builder TargetClientConfig.Builder()
```

## 参数

`TargetClientConfig.Builder`具有以下结构：

| 名称 | 类型 | 必需 | 默认 | 描述 |
| --- | --- | --- | --- | --- |
| 客户 | 字符串 | 是 | 无 | [!UICONTROL Target Client Id] |
| OrganizationId | 字符串 | 是 | 无 | [!UICONTROL Experience Cloud Organization ID] |
| 超时 | int | 否 | 10000 | 所有请求的超时（以毫秒为单位） |
| 代理 |  | WebProxy | 否 | null | 所有[!DNL Target]请求的代理 |
| RetryPolicy | 策略 | 否 | null | 重试所有[!DNL Target]请求的策略 |
| AsyncRetryPolicy | AsyncPolicy | 否 | null | 所有[!DNL Target]请求的异步重试策略 |
| Logger | ILogger | 否 | null | 用于[!DNL Target]请求和响应的调试日志记录 |
| ServerDomain | 字符串 | 否 | `client.tt.omtrdc.net` | 覆盖默认主机名 |
| 安全 | 布尔 | 否 | true | 取消设置以强制HTTP方案 |
| DefaultPropertyToken | 字符串 | 否 | null | 为每个`getOffers`调用设置默认属性令牌 |
| TelemetryEnabled | 布尔 | 否 | true | 发送遥测数据以改善SDK使用体验 |
| 决策方法 | DecisioningMethod枚举 | 否 | 服务器端 | 必须设置为OnDevice或Hybrid才能启用设备上决策 |
| OndeviceDecisioningReady | 操作 | 否 | null | 委派设备上决策就绪事件（当设备上决策就绪时调用一次） |
| ArtifactDownloadSucceeded | 操作 | 否 | null | 委派设备上决策构件下载成功（在每次成功下载构件时调用） |
| ArtifactDownloadFailed | 操作 | 否 | null | 委派设备上决策工件下载失败（在每次失败的工件下载时调用） |
| OnDeviceEnvironment | 字符串 | 否 | 生产 | 可用于指定其他设备上环境，如暂存 |
| OnDeviceConfigHost | 字符串 | 否 | `assets.adobetarget.com` | 可以指定其他主机来下载设备上决策构件文件 |
| OnDeviceDecisioningPollingIntSecs | int | 否 | 300（5分钟） | 从设备端决策工件文件两次获取之间的秒数 |
| OnDeviceArtifactPayload | 字符串 | 否 | null | 为设备上决策提供本地工件有效负载以允许立即执行 |

## 示例

## C\
#

```csharp {line-numbers="true"}
var targetClientConfig = new TargetClientConfig.Builder("acmeclient", "ABCDEF012345677890ABCDEF0@AdobeOrg")
    .Build();

targetClient = TargetClient.Create(targetClientConfig);

// make calls to Adobe Target
```
