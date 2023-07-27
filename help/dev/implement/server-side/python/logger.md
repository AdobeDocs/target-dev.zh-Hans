---
title: 初始化 [!DNL Adobe Target] 用于记录请求的Python SDK
description: 了解如何在中记录请求 [!DNL Adobe Target] Python SDK.
feature: APIs/SDKs
exl-id: 0b3792a5-a9a7-4768-a429-598b49f1fd93
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 3%

---

# Logger (Python)

## 描述

时间 [初始化SDK](initialize-sdk.md)， `options["logger"]` 对象是可选对象。 默认情况下，将在下创建INFO级别记录器 `adobe.target` 命名空间。 但是，为了在发生问题时自定义日志级别或有效调试， `logger` 初始化SDK时可以提供对象。

此 `logger` 对象应具有 `debug()` 和 `error()` 方法。 当提供合适的记录器时， [!DNL Target] 将记录请求和响应。

## 示例

### Python

```python {line-numbers="true"}
logger = logging.getLogger("org.logger")
logger.setLevel(logging.DEBUG)

client_options = {
  "client": "acmeclient",
  "organization_id": "1234567890@AdobeOrg",
  "logger": logger
}
target_client = TargetClient.create(client_options)
```

您应该会看到控制台中正在打印的请求和响应。
