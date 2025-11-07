---
title: 订阅 [!DNL Adobe Target] Node.js SDK中的事件
description: 了解如何使用[!UICONTROL OnDeviceDecisioningHandler]对象订阅在Node.js SDK中发生的各种事件。
feature: APIs/SDKs
exl-id: 40c53840-a560-4819-ae04-f527c36b22fe
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 2%

---

# SDK事件(Node.js)

## 描述

在[初始化SDK](initialize-sdk.md)时，`options.events`对象是可选对象，具有事件名称键和回调函数值。 它可用于订阅在SDK内发生的各种事件。 例如，`clientReady`事件可与回调函数一起使用，在SDK准备好进行方法调用时将调用该回调函数。

调用回调函数时，将传入一个事件对象。 每个事件都有一个与事件名称对应的`type`。 某些事件包含其他属性及相关信息。

## 事件

| 事件名称（类型） | 描述 | 其他事件属性 |
| --- | --- | --- |
| clientready | 在下载工件且SDK已准备好进行`getOffers`调用时发出。 建议在使用设备上决策方法时使用该选项。 |  |
| artifactDownloadSucceeded | 每次下载新工件时发出。 | artifactPayload， artifactLocation |
| artifactDownloadFailed | 每次未能下载工件时发出。 | artifactLocation，错误 |

## 示例

### Node.js

```js {line-numbers="true"}
const targetClient = TargetClient.create({
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
    decisioningMethod: "on-device",
    events: {
        clientReady: onTargetClientReady,
        artifactDownloadSucceeded: onArtifactDownloadSucceeded,
        artifactDownloadFailed: onArtifactDownloadFailed
    }
});

function onTargetClientReady() {
    // make getOffers requests
    targetClient.getOffers({...})            
}

function onArtifactDownloadSucceeded(event) {
    console.log(`The artifact was successfully downloaded from '${event.artifactLocation}'`);
    // optionally do something with event.artifactPayload, like persist it
}

function onArtifactDownloadFailed(event) {
    console.log(`The artifact failed to download from '${event.artifactLocation}' with the following error message: ${event.error.message}`);
}
```
