---
title: 在 [!DNL Adobe Target] Java SDK中实施代理配置
description: 了解如何在 [!DNL Adobe Target] Java SDK中配置TargetClient代理配置。
feature: APIs/SDKs
exl-id: 32e8277d-3bba-4621-b9c7-3a49ac48a466
source-git-commit: 59ab3f53e2efcbb9f7b1b2073060bbd6a173e380
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 1%

---

# 代理配置(Java)

## 基本代理

如果运行SDK的应用程序需要代理来访问Internet，则需要为`TargetClient`配置代理配置，如下所示。

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

如果需要进行代理身份验证，则可以将凭据作为参数传递到`ClientProxyConfig`构造函数，如下例所示。 请注意，这仅适用于简单用户名/密码代理身份验证。

### 基本代理身份验证

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .proxyConfig(new ClientProxyConfig(host,port,username,password))
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```

## 设备上决策

对于提取规则工件的请求，应将代理配置为不缓存响应。 但是，如果无法为该请求配置代理的缓存机制，请使用配置选项作为绕过代理级别缓存的解决方法。 此解决方法会将带有空字符串值的`Authorization`标头添加到规则请求中，这应该向代理指示不应缓存响应。

要启用此解决方法，请设置以下内容：

```java {line-numbers="true"}
ClientConfig.builder()
    .shouldArtifactRequestBypassProxyCache(true)
    .build();
```


