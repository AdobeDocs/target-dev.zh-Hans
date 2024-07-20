---
title: 了解如何配置自定义HTTP客户端
description: 了解如何使用ClientConfig.builder()。httpClient()配置TargetClient。
feature: APIs/SDKs
exl-id: 7615029c-b62d-4ed1-aadb-32e364c4c654
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# 自定义HTTP客户端配置(Java)

如果运行SDK的应用程序需要自定义HTTP客户端，要启用配置SSL或向请求添加默认标头等功能，则需要使用`ClientConfig.builder().httpClient()`配置`TargetClient`：

## 基本自定义HTTP客户端配置

SDK当前支持实施`org.apache.http.client.HttpClient`接口的HTTP客户端。

### 基本实施

```java {line-numbers="true"}
CloseableHttpClient httpClient = HttpClients.custom().build();
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .httpClient(httpClient)
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```

## 使用SSL配置进行自定义HTTP客户端配置

以下是如何通过自定义传递到`ClientConfig`的`HttpClient`在`TargetClient`中配置SSL的示例。 以下代码片段使用`org.apache.http.conn.ssl`包中的类进行SSL配置。

### SSL实施

```java {line-numbers="true"}
SSLContext context = SSLContextBuilder.create().build();
SSLConnectionSocketFactory sslSocketFactory = new SSLConnectionSocketFactory(context);
CloseableHttpClient httpClient = HttpClients.custom().setSSLSocketFactory(sslSocketFactory).build();
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .httpClient(httpClient)
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```
