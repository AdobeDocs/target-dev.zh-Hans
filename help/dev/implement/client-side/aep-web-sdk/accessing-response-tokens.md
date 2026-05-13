---
title: 使用Adobe Experience Platform Web SDK访问响应令牌
description: 了解如何使用 [!DNL Adobe Experience Platform Web SDK]访问响应令牌。
keywords: 个性化；target；adobe target；renderDecisions；sendEvent；decisionScopes；result.decisions，响应令牌；
feature: AEP Web SDK
exl-id: b125017c-c257-4f2f-a479-dd0f20e76a9a
TQID: https://experienceleague.adobe.com/kqa-HY5-dOvNq-yGqthunYDdyTKkiiFdsHquyN34ERg
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 273
ht-degree: 0%

---

# 访问响应令牌

从[!DNL Adobe Target]返回的Personalization内容包括[响应令牌](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=zh-Hans)，这些令牌包含有关活动、选件、体验、用户配置文件、地理信息等的详细信息。 这些详细信息可与第三方工具共享或用于调试。 可在[!DNL Target]用户界面中配置响应令牌。

要访问任何个性化内容，请在发送事件时提供回调函数。 SDK收到来自服务器的成功响应后，将调用此回调。 为您的回调提供了`result`对象，该对象可能包含包含包含任何返回的个性化内容的`propositions`属性。 以下是提供回调函数的示例。

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Manually render propositions
    }
  });
```

在此示例中，`result.propositions`（如果存在）是一个数组，其中包含与事件相关的个性化建议。 有关`result.propositions.`内容的更多信息，请参阅[渲染个性化内容](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/web-sdk/personalization/rendering-personalization-content)

假设您要从Web SDK自动渲染的所有建议中收集所有活动名称，并将它们推入单个数组中。 然后，您可以将单个阵列发送给第三方。 在本例中：

1. 从`result`对象提取建议。
1. 循环访问每个建议。
1. 确定SDK是否呈现了建议。
1. 如果是，则循环遍历建议中的每个项目。
1. 从`meta`属性中检索活动名称，该属性是包含响应令牌的对象。
1. 将活动名称推入数组。
1. 将活动名称发送给第三方。

您的代码将如下所示：

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    var activityNames = [];
    propositions.forEach(function(proposition) {
      if (proposition.renderAttempted) {
        proposition.items.forEach(function(item) {
          if (item.meta) {
            // item.meta contains the response tokens.
            var activityName = item.meta["activity.name"];
            // Ignore duplicates
            if (activityNames.indexOf(activityName) === -1) {
              activityNames.push(activityName);
            }
          }
        });
      }
    });
    // Now that activity names are in an array,
    // you can send them to a third party or use
    // them in some other way.
  });
```
