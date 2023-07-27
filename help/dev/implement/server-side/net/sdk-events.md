---
title: 订阅中的事件 [!DNL Adobe Target] .NET SDK
description: 了解如何使用订阅在.NET SDK中发生的各种事件 [!UICONTROL OnDeviceDecisioningHandler] 对象。
feature: APIs/SDKs
exl-id: 7578033f-3de5-4d13-9739-46ad1269ec5f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 5%

---

# SDK事件(.NET)

## 描述

时间 [初始化SDK](initialize-sdk.md)，可选 `OnDeviceDecisioningReady` 可在以下位置提供委托： `TargetClientConfig` 对象，在SDK准备好进行设备上方法调用时将调用该对象。 还有几个其他代表可处理 [!UICONTROL 设备上决策] 工件下载。

## 事件

可以为某些事件配置以下委派：

| 名称 | 参数 | 描述 |
| --- | --- | --- |
| OndeviceDecisioningReady | 无 | 在客户端第一次准备就绪时只调用一次 [!UICONTROL 设备上决策] |
| ArtifactDownloadSucceeded | 工件文件的字符串内容 | 每次调用 [!UICONTROL 设备上决策] 工件已下载 |
| ArtifactDownloadFailed | 例外 | 每次下载失败时调用 [!UICONTROL 设备上决策] 工件 |

## 示例

### \.NET

```dotnet {line-numbers="true"}
var clientConfig = new TargetClientConfig.Builder("acmeclient", "1234567890@AdobeOrg")
    .SetDecisioningMethod(DecisioningMethod.OnDevice)
    .SetOnDeviceDecisioningReady(DecisioningReady)
    .SetArtifactDownloadSucceeded(artifact => Console.WriteLine("The artifact was successfully downloaded. Contents: " + artifact))
    .SetArtifactDownloadFailed(exception => Console.WriteLine("The artifact failed to download. Exception: " + exception.Message))
    .Build();

var targetClient = TargetClient.Create(clientConfig);

// ...

static void DecisioningReady()
{
    var mboxRequests = new List<MboxRequest> { new (index: 1, name: "a1-serverside-ab") };

    var targetDeliveryRequest = new TargetDeliveryRequest.Builder()
        .SetExecute(new ExecuteRequest(mboxes: mboxRequests))
        .Build();

    var targetResponse = targetClient.GetOffers(targetDeliveryRequest);
}
```
