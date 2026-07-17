---
title: Adobe Target投放API快速入门
description: 如何使用[!UICONTROL Adobe Target投放API]？
keywords: 投放api
exl-id: 142ec3be-b017-4cdc-9079-b1cc173a710a
feature: APIs/SDKs
TQID: https://experienceleague.adobe.com/DC-YVq6VfAaqMU1utmIMw73gzp4PIJgQjaS0a8FQEO4
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: b6b447ccb88925a8efb6ff6a80ae475c8780dbc8
workflow-type: tm+mt
source-wordcount: 180
ht-degree: 0%

---

# 开始使用[!UICONTROL Adobe Target投放API]

>[!IMPORTANT]
>
>本指南适用于直接调用[!UICONTROL Target投放API]的[!DNL at.js]和直接服务器端实施。 如果您使用[!UICONTROL Adobe Experience Platform Web SDK]实现[!DNL Target]，请改用Interact API （[!UICONTROL Experience Platform Edge Network]上的`sendEvent`命令）。 有关详细信息，请参阅[Adobe Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md)。

[!UICONTROL Target交付API]调用如下所示：

```
curl -X POST \
  'https://`clientCode`.tt.omtrdc.net/rest/v1/delivery?client=`clientCode`&sessionId=d359234570e04f14e1faeeba02d6ab9914e' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{
      "context": {
        "channel": "web",
        "browser" : {
          "host" : "demo"
        },
        "address" : {
          "url" : "http://demo.dev.tt-demo.com/demo/store/index.html"
        },
        "screen" : {
          "width" : 1200,
          "height": 1400
        }
      },
        "execute": {
        "mboxes" : [
          {
            "name" : "homepage",
            "index" : 1
          }
        ]
      }
    }'
```

通过导航到&#x200B;**[!UICONTROL 管理]** > **[!UICONTROL 实现]**，可以从[!DNL Target] UI检索`clientCode`。

在进行[!UICONTROL Target投放API]调用之前，请按照以下步骤操作，以确保响应包含向最终用户显示的相关体验：

1. 使用基于表单的编辑器[&#128279;](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=en)或[可视化体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)创建[!DNL Target]活动（A/B、XT、AP或推荐）。
1. 使用投放API获取在步骤2中创建的[!DNL Target]活动中使用的mbox的响应。
1. 向访客展示体验。
