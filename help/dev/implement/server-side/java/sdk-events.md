---
title: 订阅 [!DNL Adobe Target] Java SDK中的事件
description: 了解如何使用[!UICONTROL OnDeviceDecisioningHandler]对象订阅在Java SDK中发生的各种事件。
feature: APIs/SDKs
exl-id: f2d56762-6bf7-4c6b-9c14-fb20e5cfd60d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 5%

---

# SDK事件(Java)

## 描述

当[初始化SDK](initialize-sdk.md)时，可以在`ClientConfig`对象中提供可选的`OnDeviceDecisioningHandler`对象。 它可用于订阅SDK内发生的各种事件。 例如，`onDeviceDecisioningReady`事件可与回调函数一起使用，在SDK准备好进行方法调用时，将调用该回调函数。

## 事件

`OnDeviceDecisioningHandler`对象包含以下回调，这些回调是为某些事件调用的：

| 名称 | 参数 | 描述 |
| --- | --- | --- |
| DevicedecisioningReady | 无 | 在客户端第一次为[!UICONTROL on-device decisioning]准备就绪时只调用一次 |
| artifactDownloadSucceeded | 工件文件的字节[]内容 | 每次下载[!UICONTROL on-device decisioning]工件时调用 |
| artifactDownloadFailed | 例外 | 每次下载[!UICONTROL on-device decisioning]工件失败时调用 |

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
