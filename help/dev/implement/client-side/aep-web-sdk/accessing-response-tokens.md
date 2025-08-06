---
title: 使用Adobe Experience Platform Web SDK访问响应令牌
description: 了解如何使用 [!DNL Adobe Experience Platform Web SDK]访问响应令牌。
keywords: 个性化；target；adobe target；renderDecisions；sendEvent；decisionScopes；result.decisions，响应令牌；
feature: AEP Web SDK
source-git-commit: f010ca54aac3c2a644a77fb2f88aff1996f6ddfe
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# 访问响应令牌

从[!DNL Adobe Target]返回的Personalization内容包括[响应令牌](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html)，这些令牌包含有关活动、选件、体验、用户配置文件、地理信息等的详细信息。 这些详细信息可与第三方工具共享或用于调试。 可在[!DNL Target]用户界面中配置响应令牌。

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

在此示例中，`result.propositions`（如果存在）是一个数组，其中包含与事件相关的个性化建议。 有关[内容的更多信息，请参阅](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/rendering-personalization-content)渲染个性化内容`result.propositions.`

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
