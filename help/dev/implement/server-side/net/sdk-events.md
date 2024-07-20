---
title: 订阅 [!DNL Adobe Target] .NET SDK中的事件
description: 了解如何使用[!UICONTROL OnDeviceDecisioningHandler]对象订阅在.NET SDK中发生的各种事件。
feature: APIs/SDKs
exl-id: 7578033f-3de5-4d13-9739-46ad1269ec5f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 5%

---

# SDK事件(.NET)

## 描述

在[初始化SDK](initialize-sdk.md)时，可在`TargetClientConfig`对象中提供可选的`OnDeviceDecisioningReady`委派，当SDK准备好进行设备上方法调用时，将调用该委派。 还有几个其他代理人可用于处理[!UICONTROL on-device decisioning]工件下载。

## 事件

可以为某些事件配置以下委派：

| 名称 | 参数 | 描述 |
| --- | --- | --- |
| OndeviceDecisioningReady | 无 | 在客户端第一次为[!UICONTROL on-device decisioning]准备就绪时只调用一次 |
| ArtifactDownloadSucceeded | 工件文件的字符串内容 | 每次下载[!UICONTROL on-device decisioning]工件时调用 |
| ArtifactDownloadFailed | 例外 | 每次下载[!UICONTROL on-device decisioning]工件失败时调用 |

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
