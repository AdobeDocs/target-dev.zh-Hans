---
title: 使用create方法初始化Python SDK
description: 了解如何使用create方法初始化Python SDK并实例化[!UICONTROL TargetClient]以调用 [!DNL Adobe Target] 进行实验及个性化体验。
feature: APIs/SDKs
exl-id: 3e231e8e-696d-45c7-b733-79bf99da5bec
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 17%

---

# 初始化Python SDK

描述
使用`create`方法初始化Python SDK并实例化[!UICONTROL Target Client]以调用[!DNL Adobe Target]进行实验和个性化体验。

## 方法

### 创建

```python {line-numbers="true"}
TargetClient.create(options)
```

## 参数

`options`具有以下结构：

| 名称 | 类型 | 必需 | 默认 | 描述 |
| --- | --- | --- | --- | --- |
| 客户端 | str | 是 | 无 | [!UICONTROL Adobe Target client ID] |
| organization_id | str | 是 | 无 | [!UICONTROL Experience Cloud Organization ID] |
| timeout | int | 否 | 3000 | 超时时间（以毫秒为单位） |
| server_domain | str | 否 | `client.tt.omtrdc.net` | 覆盖默认主机名 |
| secure | 布尔 | 否 | true | 取消设置以强制HTTP方案 |
| logger | 对象 | 否 | INFO记录器 | 替换默认信息记录器 |
| target_location_hint | str | 否 | 无 | [!DNL Target]位置提示 |
| property_token | str | 否 | 无 | [!DNL Target]属性令牌。 如果在此处指定，则所有get_offers调用都将使用此值。 |
| decisioning_method | str | 否 | 服务器端 | 确定要使用的决策方法（[设备上](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md)，服务器端，混合） |
| polling_interval | int | 否 | 300000（5分钟） | [设备上决策规则构件](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md)的轮询间隔（以毫秒为单位） |
| artifact_location | str | 否 | 无 | [设备上决策规则项目](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md)的完全限定URL。 覆盖内部确定的位置。 |
| artifact_payload | 对象 | 否 | 无 | [设备上决策规则项目](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md)的JSON有效负荷。 如果指定，将使用该值，而不是从URL请求值。 |
| [events](sdk-events.md) | dict &lt;str， callable> | 否 | 无 | 具有事件名称键和回调函数值的可选对象 |
| environment_id | int | 否 | 生产 | [!DNL Target]环境标识 |
| 环境 | str | 否 | 生产 | [!DNL Target]环境名称 |
| cdn_environment | str | 否 | 生产 | CDN环境名称 |
| telemetry_enable | 布尔 | 否 | true | 如果设置为False，则遥测数据将不会发送到[!DNL Adobe] |
| version | str | 否 | 无 | 此SDK的版本号 |

## 示例

### Python

```python {line-numbers="true"}
from target_python_sdk import TargetClient

def client_ready_callback(ready_event):
    # make calls to Adobe Target

client_options = {
    "client": "acmeclient",
    "organization_id": "1234567890@AdobeOrg",
    "events": {
        "client_ready": client_ready_callback
    }
}
target_client = TargetClient.create(client_options)
```
