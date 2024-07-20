---
title: 初始化 [!DNL Adobe Target] Python SDK以记录请求
description: 了解如何在 [!DNL Adobe Target] Python SDK中记录请求。
feature: APIs/SDKs
exl-id: 0b3792a5-a9a7-4768-a429-598b49f1fd93
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 3%

---

# Logger (Python)

## 描述

当[初始化SDK](initialize-sdk.md)时，`options["logger"]`对象是可选对象。 默认情况下，将在`adobe.target`命名空间下创建INFO级别日志记录器。 但是，为了在发生问题时有效地自定义日志级别或调试，可以在初始化SDK时提供`logger`对象。

`logger`对象应具有`debug()`和`error()`方法。 提供适当的记录器后，将记录[!DNL Target]个请求和响应。

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
