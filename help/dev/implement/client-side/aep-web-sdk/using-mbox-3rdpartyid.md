---
title: mbox3rdPartyId 的实时轮廓同步
description: 了解如何将mbox3rdPartyId与 [!DNL Adobe Experience Platform Web SDK]结合使用。
keywords: 个性化；target；adobe target；renderDecisions；sendEvent；mbox3rdPartyId；
feature: AEP Web SDK
source-git-commit: 03b02fb87873d89c917c7a2d7e7f775b724ea083
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 4%

---

# mbox3rdPartyId是什么

`mbox3rdPartyId`中的[!DNL Adobe Target]是您公司的访客ID，例如您公司的忠诚度计划的会员ID。

当访客登录到某个公司的网站时，该公司通常会创建一个ID，并将其绑定到访客的帐户、会员卡、会员编号或该公司的其他适用标识符。 [了解详情](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html)

## 如何将`mbox3rdPartyId`与[!DNL Platform Web SDK]一起使用

### 步骤1：配置`Target Third Party ID Namespace`

使用要用作mbox第三方ID的ID命名空间，在`Target Third Party ID Namespace`数据流[中配置](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview)。 [了解有关ID命名空间的更多信息](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html)

![Experience Platform UI显示Target第三方ID命名空间字段。](/help/dev/implement/client-side/aep-web-sdk/assets/mbox3rdpartyid.png)

### 步骤2：将`mbox3rdpartyId`发送至[!DNL Target]

使用您在步骤1中配置的ID命名空间，在`mbox3rdpartyId`命令中将[!DNL Target]发送到`sendEvent`。
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
