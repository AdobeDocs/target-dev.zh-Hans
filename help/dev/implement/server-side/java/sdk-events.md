---
title: 订阅 [!DNL Adobe Target] Java SDK中的事件
description: 了解如何使用[!UICONTROL OnDeviceDecisioningHandler]对象订阅在Java SDK中发生的各种事件。
feature: APIs/SDKs
exl-id: f2d56762-6bf7-4c6b-9c14-fb20e5cfd60d
TQID: https://experienceleague.adobe.com/x3aig-jM-GXzmLNcUNclZUK9Y49tuSF9-sdkxzJFtiM
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 144
ht-degree: 4%

---

# SDK Events (Java)

## 描述

当[初始化SDK](initialize-sdk.md)时，可在`ClientConfig`对象中提供可选的`OnDeviceDecisioningHandler`对象。 它可用于订阅在SDK内发生的各种事件。 例如，`onDeviceDecisioningReady`事件可与回调函数一起使用，在SDK准备好进行方法调用时将调用该回调函数。

## 事件

`OnDeviceDecisioningHandler`对象包含以下回调，这些回调是为某些事件调用的：

| 名称 | 参数 | 描述 |
| --- | --- | --- |
| DevicedecisioningReady | 无 | 在客户端首次准备[!UICONTROL 设备上决策]时只调用一次 |
| artifactDownloadSucceeded | 工件文件的字节[]内容 | 每次下载[!UICONTROL 设备上决策]工件时调用 |
| artifactDownloadFailed | 例外 | 每次未能下载[!UICONTROL 设备上决策]工件时调用 |

## 示例

### SDK事件

```javascript {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .defaultDecisioningMethod(DecisioningMethod.ON_DEVICE)
        .onDeviceDecisioningHandler(new OnDeviceDecisioningHandler() {
            @Override
            public void onDeviceDecisioningReady() {
                // make getOffers requests
                makeTargetRequests();
            }

            @Override
            public void artifactDownloadSucceeded(byte[] artifactData) {
                System.out.println("The artifact was successfully downloaded.");
            }

            @Override
            public void artifactDownloadFailed(TargetClientException e) {
                System.out.println("The artifact failed to download.");
            }
        }).build();

TargetClient targetJavaClient = TargetClient.create(clientConfig);


void makeTargetRequests() {
    List<MboxRequest> mboxRequests = new ArrayList<>();
    mboxRequests.add((MboxRequest) new MboxRequest().name("a1-serverside-ab").index(1));

    TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
            .context(new Context().channel(ChannelType.WEB))
            .execute(new ExecuteRequest().setMboxes(mboxRequests))
            .build();

    TargetDeliveryResponse targetResponse = targetJavaClient.getOffers(targetDeliveryRequest);
}
```
