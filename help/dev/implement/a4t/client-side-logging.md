---
title: Experience Platform Web SDK中的A4T数据的客户端日志记录
description: 了解如何使用Experience Platform Web SDK为Adobe Analytics for Target (A4T)启用客户端日志记录。
seo-title: Client-side logging for A4T data in the Experience Platform Web SDK
seo-description: Learn how to enable client-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: target；a4t；日志记录；Web SDK；体验；平台；
feature: Implementation
source-git-commit: 4d4ca7dcffdbaee5770084bd85c3109df0d6a8d4
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 0%

---

# [!DNL Experience Platform Web SDK]中A4T数据的客户端日志记录

[!DNL Adobe Experience Platform Web SDK]允许您在Web应用程序的客户端收集[Adobe Analytics for Target (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html)数据。

客户端日志记录意味着在客户端返回相关的[!DNL Target]数据，允许您收集数据并与[!DNL Analytics]共享。 如果您打算使用[数据插入API](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html)手动将数据发送到Analytics，则应启用此选项。

>[!NOTE]
>
>使用[AppMeasurement.js](https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html)执行此操作的方法目前正在开发中，将在不久的将来提供。

本文档介绍了为[!DNL Platform Web SDK]设置客户端A4T日志记录的步骤，并提供常见用例的实施示例。

## 先决条件 {#prerequisites}

本教程假设您熟悉与将[!DNL Platform Web SDK]用于个性化目的相关的基本概念和流程。 如果您需要了解简介，请查看以下文档：

* [配置Web SDK](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/configure/overview)
* [正在发送事件](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/sendevent/overview)
* [呈现个性化内容](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/personalization/rendering-personalization-content)

## 设置[!DNL Analytics]客户端日志记录 {#set-up-client-side-logging}

以下子部分概述了如何为您的[!DNL Analytics]实施启用[!DNL Platform Web SDK]客户端日志记录。

### 启用[!DNL Analytics]客户端日志记录 {#enable-analytics-client-side-logging}

若要考虑为您的实施启用[!DNL Analytics]客户端日志记录，您必须在[!DNL Adobe Analytics]数据流[中禁用](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview)配置。

![已禁用Analytics数据流配置](/help/dev/implement/a4t/assets/disable-analytics-datastream.png)

### 从SDK检索[!DNL A4T]数据并将其发送给[!DNL Analytics] {#a4t-to-analytics}

为了使此报告方法正常工作，您必须发送从[!DNL A4T]点击中的[`sendEvent`](https://experienceleague.adobe.com/en/docs/experience-platform/web-sdk/commands/sendevent/overview)命令检索到的[!DNL Analytics]相关数据。

当[!DNL Target] Edge计算建议响应时，它会检查是否启用了[!DNL Analytics]客户端日志记录（例如，数据流中是否禁用了[!DNL Analytics]）。 如果启用了客户端日志记录，则系统会向响应中的每个建议添加[!DNL Analytics]令牌。

该流量与以下内容类似：

![客户端日志记录流程](/help/dev/implement/a4t/assets/analytics-client-side-logging.png)

以下是启用`interact`客户端日志记录时的[!DNL Analytics]响应示例。 如果建议针对具有[!DNL Analytics]报表的活动，则它将具有`scopeDetails.characteristics.analyticsToken`属性。

```json
{
  "requestId": "1234",
  "handle": [
    {
      "payload": [
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
          "scopeDetails": {
            "decisionProvider": "TGT",
            "activity": {
              "id": "434689"
            },
            "experience": {
              "id": "0"
            },
            "strategies": [
              {
                "algorithmID": "0",
                "trafficType": "0"
              }
            ],
            "characteristics": {
              "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
              "analyticsToken": "434689:0:0|2,434689:0:0|1"
            }
          },
          "items": [
            {
              "id": "1184844",
              "schema": "https://ns.adobe.com/personalization/html-content-item",
              "meta": {
                "geo.state": "bucuresti",
                "activity.id": "434689",
                "experience.id": "0",
                "activity.name": "a4t test form based activity",
                "offer.id": "1184844",
                "profile.tntId": "04608610399599289452943468926942466370-pybgfJ"
              },
              "data": {
                "id": "1184844",
                "format": "text/html",
                "content": "<div> analytics impressions </div>"
              }
            }
          ]
        },
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
          "scopeDetails": {
            "decisionProvider": "TGT",
            "activity": {
              "id": "434689"
            },
            "characteristics": {
              "eventToken": "E0gb6q1+WyFW3FMbbQJmrg==",
              "analyticsToken": "434689:0:0|32767"
            }
          },
          "items": [
            {
              "id": "434689",
              "schema": "https://ns.adobe.com/personalization/measurement",
              "data": {
                "type": "click",
                "format": "application/vnd.adobe.target.metric"
              }
            }
          ]
        }
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

[!UICONTROL Form-based Experience Composer]活动的建议可以同时包含相同建议下的内容和点击量度项目。 因此，它们可以相应地在`scopeDetails.characteristics.analyticsToken`和`scopeDetails.characteristics.analyticsDisplayToken`属性中同时指定显示和点击分析令牌，而不是在`scopeDetails.characteristics.analyticsClickToken`属性中只显示一个分析令牌。

```json
{
  "requestId": "1234",
  "handle": [
    {
      "payload": [
        {
          "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
          "scope": "a4t-test",
          "scopeDetails": {
            "decisionProvider": "TGT",
            "activity": {
              "id": "434689"
            },
            "experience": {
              "id": "0"
            },
            "strategies": [
              {
                "algorithmID": "0",
                "trafficType": "0"
              }
            ],
            "characteristics": {
               "displayToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
               "clickToken": "E0gb6q1+WyFW3FMbbQJmrg==",
               "analyticsDisplayToken": "434689:0:0|2,434689:0:0|1", 
               "analyticsClickToken": "434689:0:0|32767"
            }
          },
          "items": [
            {
              "id": "1184844",
              "schema": "https://ns.adobe.com/personalization/html-content-item",
              "meta": {
                "geo.state": "bucuresti",
                "activity.id": "434689",
                "experience.id": "0",
                "activity.name": "a4t test form based activity",
                "offer.id": "1184844",
                "profile.tntId": "04608610399599289452943468926942466370-pybgfJ"
              },
              "data": {
                "id": "1184844",
                "format": "text/html",
                "content": "<div> analytics impressions </div>"
              }
            },
            {
              "id": "434689",
              "schema": "https://ns.adobe.com/personalization/measurement",
              "data": {
                "type": "click",
                "format": "application/vnd.adobe.target.metric"
              }
            }
          ]
        }
      ],
      "type": "personalization:decisions",
      "eventIndex": 0
    }
  ]
}
```

来自`scopeDetails.characteristics.analyticsToken`、`scopeDetails.characteristics.analyticsDisplayToken`（用于显示的内容）和`scopeDetails.characteristics.analyticsClickToken`（用于点击量度）的所有值都是需要收集的A4T负载，并将它们作为`tnta`标记包含在[数据插入API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md)调用中。

>[!IMPORTANT]
>
>`analyticsToken`、`analyticsDisplayToken`、`analyticsClickToken`属性可以包含多个令牌，并作为单个以逗号分隔的字符串连接。
>
>在下一节中提供的实施示例中，正在迭代收集多个[!DNL Analytics]令牌。 要连接[!DNL Analytics]令牌数组，请使用如下所示的函数：
>
>```javascript
>var concatenateAnalyticsPayloads = function concatenateAnalyticsPayloads(analyticsPayloads) {
>   if (analyticsPayloads.size > 1) {
>       return [].concat(analyticsPayloads).join(',');
>   }
>   return [].concat(analyticsPayloads).join();
>};
>```

## 实施示例 {#implementation-examples}

以下子部分演示了如何为常见用例实施[!DNL Analytics]客户端日志记录。

### [!UICONTROL Form-Based Experience Composer]活动 {#form-based-composer}

您可以使用[!DNL Platform Web SDK]来控制从[Adobe Target基于表单的体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html)活动中执行建议。

在为特定决策范围请求建议时，返回的建议包含其相应的[!DNL Analytics]令牌。 最佳实践是链[!DNL Experience Platform Web SDK] `sendEvent`命令并在同时收集[!DNL Analytics]令牌时循环遍历返回的建议以执行它们。

您可以为`sendEvent`活动范围触发[!UICONTROL Form-Based Experience Composer]命令，如下所示：

```javascript
alloy("sendEvent", {
    "decisionScopes": ["a4t-test"],
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function(results) {
  for (var i = 0; i < results.propositions.length; i++) {
    //Execute the propositions and collect the Analytics payload
  }
});
```

从此处，您必须实施代码以执行建议并构建最终发送到[!DNL Analytics]的有效负载。 这是`results.propositions`可能包含的内容的示例：

```json
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "experience": {
        "id": "0"
      },
      "strategies": [
        {
          "algorithmID": "0",
          "trafficType": "0"
        }
      ],
      "characteristics": {
        "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw==",
        "analyticsToken": "434689:0:0|2,434689:0:0|1"
      }
    },
    "items": [
      {
        "id": "1184844",
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "meta": {
          "geo.state": "bucuresti",
          "activity.id": "434689",
          "experience.id": "0",
          "activity.name": "a4t test form based activity",
          "offer.id": "1184844",
          "profile.tntId": "04608610399599289452943468926942466370-pybgfJ"
        },
        "data": {
          "id": "1184844",
          "format": "text/html",
          "content": "<div> analytics impressions </div>"
        }
      }
    ]
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "characteristics": {
        "eventToken": "E0gb6q1+WyFW3FMbbQJmrg==",
        "analyticsToken": "434689:0:0|32767"
      }
    },
    "items": [
      {
        "id": "434689",
        "schema": "https://ns.adobe.com/personalization/measurement",
        "data": {
          "type": "click",
          "format": "application/vnd.adobe.target.metric"
        }
      }
    ]
  },
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "a4t-test",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434688"
      },
      "experience": {
        "id": "0"
      },
      "strategies": [
        {
          "algorithmID": "0",
          "trafficType": "0"
        }
      ],
      "characteristics": {
          "displayToken": "91TS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqgEt==",
          "clickToken": "Tagb6q1+WyFW3FMbbQJrtg==",
          "analyticsDisplayTokens": "434688:0:0|2,434688:0:0|1",
          "analyticsClickTokens": "434688:0:0|32767"
        }
      }
    },
    "items": [
      {
        "id": "1184845",
        "schema": "https://ns.adobe.com/personalization/html-content-item",
        "meta": {
          "geo.state": "bucuresti",
          "activity.id": "434688",
          "experience.id": "0",
          "activity.name": "a4t test form based activity 1",
          "offer.id": "1184845"
        },
        "data": {
          "id": "1184845",
          "format": "text/html",
          "content": "<div> analytics impressions 1</div>"
        }
      },
      {
        "id": "434688",
        "schema": "https://ns.adobe.com/personalization/measurement",
        "data": {
          "type": "click",
          "format": "application/vnd.adobe.target.metric"
        }
      }
    ]
  }
]
```

要从具有内容项的建议中提取[!DNL Analytics]令牌，您可以实现类似于以下内容的函数：

```javascript
function getDisplayAnalyticsPayload(proposition) {
  if (!proposition || !proposition.scopeDetails || !proposition.scopeDetails.characteristics) {
    return;
  }
  var characteristics = proposition.scopeDetails.characteristics;
  if (characteristics.analyticsDisplayToken) {
    return characteristics.analyticsDisplayToken;
  }
  return characteristics.analyticsToken;
}
```

建议可以具有不同类型的项目，如所讨论项目的`schema`属性所指示。 [!UICONTROL Form-Based Experience Composer]活动支持四个建议项目架构：

```javascript
var HTML_SCHEMA = "https://ns.adobe.com/personalization/html-content-item";
var MEASUREMENT_SCHEMA = "https://ns.adobe.com/personalization/measurement";
var JSON_SCHEMA = "https://ns.adobe.com/personalization/json-content-item";
var REDIRECT_SCHEMA = "https://ns.adobe.com/personalization/redirect-item";
```

`HTML_SCHEMA`和`JSON_SCHEMA`是反映选件类型的架构，而`MEASUREMENT_SCHEMA`反映应附加到DOM元素的量度。

当访客实际点击之前显示的内容时，点击量度的[!DNL Analytics]负载应该与内容项一起收集并发送到[!DNL Analytics]。

在这种情况下，以下用于获取点击量度A4T有效负载的帮助程序函数将会非常实用：

```javascript
function getClickAnalyticsPayload(proposition) {
  if (!proposition || !proposition.scopeDetails || !proposition.scopeDetails.characteristics) {
    return;
  }
  var characteristics = proposition.scopeDetails.characteristics;
  if (characteristics.analyticsClickToken) {
    return characteristics.analyticsClickToken;
  }
  return characteristics.analyticsToken;
}
```

#### 实施摘要 {#implementation-summary}

总之，在使用[!UICONTROL Form-Based Experience Composer]应用[!DNL Experience Platform Web SDK]活动时必须执行以下步骤：

1. 发送获取[!UICONTROL Form-Based Experience Composer]活动选件的事件；
1. 将内容更改应用到页面；
1. 发送`decisioning.propositionDisplay`通知事件；
1. 从SDK响应中收集[!DNL Analytics]显示令牌并构建[!DNL Analytics]点击的有效负载；
1. 使用[!DNL Analytics]数据插入API[将有效负载发送到](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md)；
1. 如果投放的建议中包含任何点击量度，则应设置点击侦听器，以便在执行点击时，发送`decisioning.propositionInteract`通知事件。 应配置`onBeforeEventSend`处理程序，以便在拦截`decisioning.propositionInteract`事件时执行以下操作：
   1. 正在从[!DNL Analytics]收集点击`xdm._experience.decisioning.propositions`令牌
   1. 通过[!DNL Analytics]数据插入API[!DNL Analytics]，使用收集的[有效负载发送点击](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md)点击；

```javascript
alloy("sendEvent", {
    "decisionScopes": ["a4t-test"],
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function(results) {
  var analyticsPayload = new Set();
  results.propositions.forEach(function (proposition) {
    proposition.items.forEach(function (item) {
      if (item.schema === HTML_SCHEMA) {
        // 1. Apply offer
        // 2. Collect executed propositions and send the decisioning.propositionDisplay notification event
        // 3. Collect the display Analytics tokens
      }
      if (item.schema === MEASUREMENT_SCHEMA) {
        // Setup click listener, so that when clicked:
        // 1. Collect clicked propositions and send the decisioning.propositionInteract notification event
        // Note: onBeforeEventSend handler should be configured, so that when intercepting decisioning.propositionInteract events:
        //   1. Collect the click Analytics tokens from xdm._experience.decisioning.propositions
        //   2. Send the click Analytics hit with the collected Analytics payload via Data Insertion API
      }
    });
  });
  // Send the page view Analytics hit with the collected display Analytics payload via Data Insertion API
});
```

### [!UICONTROL Visual Experience Composer] (VEC)活动 {#visual-experience-composer-acitivties}

[!DNL Platform Web SDK]允许您处理使用[可视化体验编辑器(VEC)](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html)创作的选件。

>[!NOTE]
>
>实施此用例的步骤与[基于表单的体验编辑器活动](#form-based-composer)的步骤非常相似。 有关更多详细信息，请参阅上一节。

启用自动渲染后，您可以从页面上执行的建议中收集[!DNL Analytics]令牌。 最佳实践是链接[!DNL Experience Platform Web SDK] `sendEvent`命令并循环遍历返回的建议，以筛选Web SDK尝试渲染的建议。

**示例**

```javascript
alloy("sendEvent", {
    "renderDecisions": true,
    "xdm": {
      "web": {
        "webPageDetails": {
          "name": "Home Page"
        }
      }
    }
  }
).then(function (results) {
  var analyticsPayloads = new Set();
  
  for (var i = 0; i < results.propositions.length; i++) {
  
    var proposition = propositions[i];
    var renderAttempted = proposition.renderAttempted;

    if (renderAttempted === true) {
      var analyticsPayload = getDisplayAnalyticsPayload(proposition);
      
      if (analyticsPayload !== undefined) {
        analyticsPayloads.add(analyticsPayload);
      }
    }
  }
  var analyticsPayloadsToken = concatenateAnalyticsPayloads(analyticsPayloads);
  // Send the page view Analytics hit with collected Analytics payload via Data Insertion API
});
```

### 使用`onBeforeEventSend`处理页面量度 {#using-onbeforeeventsend}

使用[!DNL Adobe Target]活动，您可以在页面上设置不同的量度，手动附加到DOM或自动附加到DOM（VEC创作的活动）。 这两种类型都是网页上延迟的最终用户交互。

要解决此问题，最佳实践是使用[!DNL Analytics] `onBeforeEventSend`挂接收集[!DNL Adobe Experience Platform Web SDK]有效负载。 `onBeforeEventSend`挂接应使用`configure`命令进行配置，并反映在通过数据流发送的所有事件中。

以下是如何将`onBeforeEventSent`配置为触发[!DNL Analytics]点击的示例：

```javascript
alloy("configure", {
  datastreamId: "datastream configuration ID",
  orgId: "adobe ORG ID",
  onBeforeEventSend: function(options) {
    const xdm = options.xdm;
    const eventType = xdm.eventType;
    if (eventType === "decisioning.propositionInteract") {
      const analyticsPayloads = new Set();
      const propositions = xdm._experience.decisioning.propositions;

      for (var i = 0; i < propositions.length; i++) {
        var proposition = propositions[i];
        analyticsPayloads.add(getClickAnalyticsPayload(proposition));
      }
      // Trigger the Analytics hit
    }
  }
});
```

## 后续步骤 {#next-steps}

本指南介绍了[!DNL Platform Web SDK]中A4T数据的客户端日志记录。 有关如何在Edge Network上处理A4T数据的更多信息，请参阅[服务器端日志记录](/help/dev/implement/a4t/server-side-a4t.md)指南。