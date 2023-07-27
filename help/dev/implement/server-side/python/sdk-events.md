---
title: 订阅中的事件 [!DNL Adobe Target] Python SDK
description: 了解如何使用订阅Python SDK中发生的各种事件 [!UICONTROL OnDeviceDecisioningHandler] 对象。
feature: APIs/SDKs
exl-id: 4e32e3b5-6072-4703-b09d-abb467aa1304
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 3%

---

# SDK事件(Python)

## 描述

时间 [初始化SDK](initialize-sdk.md)， `options["events"]` dict是一个可选对象，具有事件名称键和回调函数值。 它可用于订阅SDK内发生的各种事件。 例如， `client_ready` 事件可与回调函数一起使用，在SDK准备好进行方法调用时，将调用该回调函数。

当 `callback` 调用函数，传入一个事件对象。 每个事件都有一个 `type` 和事件名称相对应，并且某些事件包含附加属性以及相关信息。

## 事件

| 事件名称（类型） | 描述 | 其他事件属性 |
| --- | --- | --- |
| client_ready | 在下载工件并且SDK准备好进行get_offers调用时发出。 建议在使用时 | 设备上决策方法。 | 无 |
| artifact_download_succeeded | 每次下载新工件时发出。 | artifact_payload， artifact_location |
| artifact_download_failed | 每次未能下载工件时发出。 | artifact_location，错误 |

## 示例

### Python

```python {line-numbers="true"}
def client_ready_callback():
    # make get_offers requests

def artifact_download_succeeded(event):
    print("The artifact was successfully downloaded from {}".format(event.artifact_location))
    # optionally do something with event.artifact_payload, like persist it

def artifact_download_failed(event):
    print("The artifact failed to download from {} with the following error: {}"
          .format(event.artifact_location, str(event.error)))

client_options = {
    "client": "acmeclient",
    "organization_id": "1234567890@AdobeOrg",
    "events": {
        "client_ready": client_ready_callback,
        "artifact_download_succeeded": artifact_download_succeeded,
        "artifact_download_failed": artifact_download_failed
    }
}
target_client = target_client.create(client_options)
```
