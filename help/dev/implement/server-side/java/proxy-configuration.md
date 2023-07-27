---
title: 在中实施代理配置 [!DNL Adobe Target] Java SDK
description: 了解如何在中配置TargetClient代理配置 [!DNL Adobe Target] Java SDK。
feature: APIs/SDKs
exl-id: 32e8277d-3bba-4621-b9c7-3a49ac48a466
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 1%

---

# 代理配置(Java)

## 基本代理

如果运行SDK的应用程序需要代理来访问Internet，则 `TargetClient` 需要使用代理配置进行配置，如下所示。

### 基本代理配置

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .proxyConfig(new ClientProxyConfig(host,port))
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```

## 身份验证

如果需要进行代理身份验证，可以将凭据作为参数传递到 `ClientProxyConfig` 构造函数，如下例所示。 请注意，这仅适用于简单用户名/密码代理身份验证。

### 基本代理身份验证

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .proxyConfig(new ClientProxyConfig(host,port,username,password))
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```
