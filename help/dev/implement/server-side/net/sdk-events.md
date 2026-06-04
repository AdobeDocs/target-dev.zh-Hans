---
title: 订阅 [!DNL Adobe Target] .NET SDK中的事件
description: 了解如何使用[!UICONTROL OnDeviceDecisioningHandler]对象订阅在.NET SDK中发生的各种事件。
feature: APIs/SDKs
exl-id: 7578033f-3de5-4d13-9739-46ad1269ec5f
TQID: https://experienceleague.adobe.com/oeGknU-pW1-XjVrxn8JNEPoFBF8Gntt-vaVnqjdyTC8
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 133
ht-degree: 5%

---

# SDK事件(.NET)

## 描述

在[初始化SDK](initialize-sdk.md)时，可在`TargetClientConfig`对象中提供可选的`OnDeviceDecisioningReady`委派，当SDK准备好进行设备上方法调用时，将调用该委派。 还有几个其他代理人可用于处理[!UICONTROL 设备上决策]工件下载。

## 事件

可以为某些事件配置以下委派：

| 名称 | 参数 | 描述 |
| --- | --- | --- |
| OndeviceDecisioningReady | 无 | 在客户端首次准备[!UICONTROL 设备上决策]时只调用一次 |
| ArtifactDownloadSucceeded | 工件文件的字符串内容 | 每次下载[!UICONTROL 设备上决策]工件时调用 |
| ArtifactDownloadFailed | 例外 | 每次未能下载[!UICONTROL 设备上决策]工件时调用 |

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
