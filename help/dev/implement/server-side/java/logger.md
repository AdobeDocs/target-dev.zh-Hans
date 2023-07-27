---
title: 初始化 [!DNL Adobe Target] 用于记录请求的Java SDK
description: 了解如何在中记录请求 [!DNL Adobe Target] Java SDK。
feature: APIs/SDKs
exl-id: 85d1a6ef-0b08-4948-8133-740b7d6141dd
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 4%

---

# Logger (Java)

## 描述

时间 [初始化SDK](initialize-sdk.md)，上提供了多个选项 `ClientConfig` 对象，可设置为记录请求。

| 选项 | 描述 |
| --- | --- |
| `logRequests` | 记录整个请求正文以及响应正文。 |
| `logRequestStatus` | 记录请求的URL、状态以及响应时间。 |

[!DNL Target] Java SDK使用 `slf4j` 日志记录。 您需要提供记录器的实施，例如 `java.util.logging`， `logback`、和 `log4j`. 请参阅 [http://www.slf4j.org/manual.html](http://www.slf4j.org/manual.html) 以了解更多信息。 所有日志将打印在 `debug`.

## 示例

添加 `slf4j` 依赖关系。

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

启用 `DEBUG` 日志，并标记请求日志标记符。

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
