---
title: Adobe Target投放API快速入门
description: 如何使用 [!UICONTROL Adobe Target交付API]？
keywords: 投放api
exl-id: 142ec3be-b017-4cdc-9079-b1cc173a710a
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---

# 入门 [!UICONTROL Adobe Target交付API]

A [!UICONTROL Target投放API] 调用如下所示：

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

此 `clientCode` 可从以下位置检索： [!DNL Target] UI，导航到 **[!UICONTROL 管理]** > **[!UICONTROL 实现]**.

创建之前 [!UICONTROL Target投放API] 调用，请按照以下步骤操作，以确保响应包含向最终用户显示的相关体验：

1. 创建 [!DNL Target] 活动(A/B、XT、AP或Recommendations) [基于表单的编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=en) 或 [可视化体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html).
1. 使用投放API获取 [!DNL Target] 在步骤2中创建的活动。
1. 向访客展示体验。

## Postman收藏集 {#postman}

Postman是一款能够轻松触发API调用的应用程序。 [此Postman收藏集](https://run.pstmn.io/button.svg) 包含示例投放API调用。
