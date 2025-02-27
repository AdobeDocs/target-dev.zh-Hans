---
title: 初始化 [!DNL Adobe Target] Java SDK以记录请求
description: 了解如何在 [!DNL Adobe Target] Java SDK中记录请求。
feature: APIs/SDKs
exl-id: 85d1a6ef-0b08-4948-8133-740b7d6141dd
source-git-commit: 526445fccee9b778b7ac0d7245338f235f11d333
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 4%

---

# Logger (Java)

## 描述

当[初始化SDK](initialize-sdk.md)时，`ClientConfig`对象上有多个选项，这些选项可以设置为记录请求。

| 选项 | 描述 |
| --- | --- |
| `logRequests` | 记录整个请求正文以及响应正文。 |
| `logRequestStatus` | 记录请求的URL、状态以及响应时间。 |

[!DNL Target] Java SDK使用`slf4j`日志记录。 您需要提供记录器的实现，如`java.util.logging`、`logback`和`log4j`。 有关详细信息，请参阅[https://www.slf4j.org/manual.html](https://www.slf4j.org/manual.html)。 所有日志都将在`debug`中打印。

## 示例

添加`slf4j`依赖项。

>[!BEGINTABS]

>[!TAB Gradle]

### Gradle

```javascript {line-numbers="true"}
compile 'org.slf4j:slf4j-simple:2.0.0-alpha0'
```

>[!TAB Maven]

```javascript {line-numbers="true"}
<dependency>
    <groupId>org.slf4j</groupId>
    <artifactId>slf4j-simple</artifactId>
    <version>2.0.0-alpha0</version>
</dependency>
```

>[!ENDTABS]

基于您的实施启用`DEBUG`日志，并标记请求日志记录标志。

### 调试

```javascript {line-numbers="true"}
System.setProperty(SimpleLogger.DEFAULT_LOG_LEVEL_KEY, "DEBUG");
ClientConfig config = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .logRequests(true)
        .logRequestStatus(true)
        .build();

TargetClient targetClient = TargetClient.create(config);
```

您应该会看到控制台中正在打印的请求、响应和响应时间。
