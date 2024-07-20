---
title: Adobe Target投放API快速入门
description: 如何使用[!UICONTROL Adobe Target Delivery API]？
keywords: 投放api
exl-id: 142ec3be-b017-4cdc-9079-b1cc173a710a
feature: APIs/SDKs
source-git-commit: e5a1c38d448cb7446b7b26cd0dc882976ba94dd3
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# 开始使用[!UICONTROL Adobe Target Delivery API]

[!UICONTROL Target Delivery API]调用如下所示：

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

通过导航到&#x200B;**[!UICONTROL Administration]** > **[!UICONTROL Implementation]**，可以从[!DNL Target] UI检索`clientCode`。

在进行[!UICONTROL Target Delivery API]调用之前，请按照以下步骤操作，以确保响应包含向最终用户显示的相关体验：

1. 使用基于表单的编辑器[或[可视化体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)创建[!DNL Target]活动(A/B、XT、AP或Recommendations)。](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=en)
1. 使用投放API获取在步骤2中创建的[!DNL Target]活动中使用的mbox的响应。
1. 向访客展示体验。
