---
title: mbox3rdPartyId 的实时轮廓同步
description: 了解如何将mbox3rdPartyId与 [!DNL Adobe Experience Platform Web SDK]结合使用。
keywords: 个性化；target；adobe target；renderDecisions；sendEvent；mbox3rdPartyId；
feature: AEP Web SDK
exl-id: 1c5067ef-38b3-4bf1-bd39-ea0f2cbd1074
TQID: https://experienceleague.adobe.com/Ej2sYVnBD9orRTlsMQG85JJV7dvn-9gnABDa0b8uBlM
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 170
ht-degree: 24%

---

# 使用mbox3rdPartyId

[!DNL Adobe Target]中的`mbox3rdPartyId`是您公司的访客ID，例如您公司的忠诚度计划的会员ID。

访客登录到某个公司的网站后，该公司通常会创建一个 ID，并将其绑定到访客的帐户、会员卡、会员编号，以及该公司的其他适用标识符。 [了解详情](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html?lang=zh-Hans)

## 如何将`mbox3rdPartyId`与[!DNL Platform Web SDK]一起使用

### 步骤1：配置`Target Third Party ID Namespace`

使用要用作mbox第三方ID的ID命名空间，在[数据流](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/datastreams/overview)中配置`Target Third Party ID Namespace`。 [了解有关ID命名空间的更多信息](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=zh-Hans)

![Experience Platform UI显示Target第三方ID命名空间字段。](/help/dev/implement/client-side/aep-web-sdk/assets/mbox3rdpartyid.png)

### 步骤2：将`mbox3rdpartyId`发送至[!DNL Target]

使用您在步骤1中配置的ID命名空间，在`sendEvent`命令中将`mbox3rdpartyId`发送到[!DNL Target]。
[了解有关发送ID的详细信息](/help/dev/implement/client-side/aep-web-sdk/using-mbox-3rdpartyid.md)

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Replace `ID_NAMESPACE` with the namespace you have configured in Step 1.
        {
          "id": "1234",
          "authenticatedState": "authenticated"
        }
      ]
    }
  }
});
```
