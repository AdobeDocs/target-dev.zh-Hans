---
title: Adobe Target配置文件API
description: 了解如何使用Adobe Target配置文件API将访客数据发送至 [!DNL Target].
contributors: https://github.com/icaraps
feature: APIs/SDKs
source-git-commit: 289299a52e5611c0da341f313aa4a447fcf3666a
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 1%

---

# [!DNL Adobe Target Profiles API] 概述

[!DNL Adobe Target] 为每个用户创建和维护配置文件。 此配置文件存储在 [!DNL Target] 边缘群集，并在每次访问后实时更新。

## 配置文件 [!DNL Postman] 收藏集

[!DNL Postman] 是一个应用程序，可轻松触发API调用。 此 [!DNL Postman] 收藏集包含所有 [!DNL Profile API] 呼叫。 单击 [在Postman上运行](https://www.getpostman.com/collections/ec7376f9028977ccaa99){target=_blank} 以导入配置文件API集合。

## 旧版配置文件API文档。

旧版配置文件API文档可在以下位置找到： [https://developers.adobetarget.com/api/#profiles](https://developers.adobetarget.com/api/#profiles){target=_blank}

## 的结构 [!DNL Target] 个人资料

Target配置文件包含以下对象：

| 对象 | 详细信息 |
| --- | --- |
| `clientcode` | 此 [!DNL Target] 与配置文件关联的客户端代码。 |
| `visitorId` | 用户档案的标识符。 这可以是 `tntid`， `thirdpartyid`，或 `marketingcloudvisitorid`. |
| `modifiedAt` | 上次更新配置文件的时间戳。 |
| `profileAttributes` | 该单个配置文件上作为键值对存储的所有配置文件属性的列表。 |

### 示例配置文件结构

```
{
    "client": "<your-tenant-name>",
    "visitorId": "a1-mbox3rdPartyId",
    "modifiedAt": "2017-08-18T17:53:39.003-04:00",
    "profileAttributes": {
        "insurance": {
            "value": "false",
            "modifiedAt": "2017-07-31T20:34:55.625-04:00"
        },
        "country": {
            "value": "france",
            "modifiedAt": "2017-07-31T14:26:30.879-04:00"
        },
        "checking": {
            "value": "true",
            "modifiedAt": "2017-07-31T20:34:55.625-04:00"
        },
        "user.memberlevel": {
            "value": "0.0",
            "modifiedAt": "2017-08-09T18:18:04.661-04:00"
        },
        "param1": {
            "value": "value1",
            "modifiedAt": "2017-08-09T18:18:04.659-04:00"
        },
        "param2": {
            "value": "value2",
            "modifiedAt": "2017-08-09T18:18:04.659-04:00"
        },
        "firstSessionStart": {
            "value": "1500648715286",
            "modifiedAt": "2017-07-21T10:51:55.286-04:00"
        },
        "entity.name": {
            "value": "my-entityName",
            "modifiedAt": "2017-08-09T18:18:04.659-04:00"
        },
        "entity.id": {
            "value": "my-entityId",
            "modifiedAt": "2017-08-09T18:18:04.659-04:00"
        }
    }
}
```
