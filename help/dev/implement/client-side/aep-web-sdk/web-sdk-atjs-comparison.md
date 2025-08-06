---
title: 将at.js与Experience Platform Web SDK进行比较
description: 了解at.js功能与 [!DNL Experience Platform Web SDK]的比较。
keywords: target；adobe target；activity.id；experience.id；renderDecisions；decisionScopes；预隐藏代码片段；vec；基于表单的体验编辑器；xdm；受众；决策；范围；架构；系统图；图
feature: AEP Web SDK
source-git-commit: d6b93537692a1efbc2650a015f5a44d4fd1fd422
workflow-type: tm+mt
source-wordcount: '2006'
ht-degree: 5%

---

# 将at.js库与[!DNL Adobe Experience Platform Web SDK]进行比较

## 概述

本文概述了`at.js`库与Experience Platform Web SDK之间的差异。

## 安装库

### 安装at.js

[!DNL Adobe]允许客户直接从[!DNL Adobe Experience Cloud] [!UICONTROL Implementation]选项卡下载库。 使用客户拥有的如下设置自定义at.js库： clientCode、imsOrgId等

### 安装Web SDK

预建版本在CDN上可用。 您可以在页面上直接在CDN上引用库，也可以将其下载并托管在您自己的基础架构上。 它以缩小和未缩小的格式提供。 未缩小的版本有助于进行调试。

有关详细信息，请参阅[使用JavaScript库安装Web SDK](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/web-sdk/install/library)。

## 配置库

### 配置at.js

在每个at.js文件末尾，您会看到一个部分，其中[!DNL Adobe]实例化并传递设置对象。 它可自定义，在下载时，Adobe会使用当前客户设置填充该部分。

```javascript
window.adobe.target.init(window, document, {
  "clientCode": "demo",
  "imsOrgId": "",
  "serverDomain": "localhost:5000",
  "timeout": 2000,
  "globalMboxName": "target-global-mbox",
  "version": "2.0.0",
  "defaultContentHiddenStyle": "visibility: hidden;",
  "defaultContentVisibleStyle": "visibility: visible;",
  "bodyHiddenStyle": "body {opacity: 0 !important}",
  "bodyHidingEnabled": true,
  "deviceIdLifetime": 63244800000,
  "sessionIdLifetime": 1860000,
  "selectorsPollingTimeout": 5000,
  "visitorApiTimeout": 2000,
  "overrideMboxEdgeServer": false,
  "overrideMboxEdgeServerTimeout": 1860000,
  "optoutEnabled": false,
  "optinEnabled": false,
  "secureOnly": false,
  "supplementalDataIdParamTimeout": 30,
  "authoringScriptUrl": "//cdn.tt.omtrdc.net/cdn/target-vec.js",
  "urlSizeLimit": 2048,
  "endpoint": "/rest/v1/delivery",
  "pageLoadEnabled": true,
  "viewsEnabled": true,
  "analyticsLogging": "server_side",
  "serverState": {},
  "decisioningMethod": "server-side",
  "legacyBrowserSupport":  false
});
```

[了解详情](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md)

### 配置平台Web SDK

使用[`configure`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/web-sdk/commands/configure/overview)命令完成SDK的配置。 `configure`命令是首先调用的&#x200B;*始终*。

## 如何请求和自动渲染页面加载[!DNL Target]选件

### 使用at.js

使用at.js 2.x时，如果启用设置`pageLoadEnabled,`，则库将通过[!DNL Target]触发对`execute -> pageLoad` Edge的调用。 如果所有设置都设置为默认值，则无需自定义编码。 将at.js添加到页面并由浏览器加载后，将执行[!DNL Target] Edge调用。

### 使用[!DNL PLatform Web SDK]

SDK可以自动检索和渲染[!DNL Target] [可视化体验编辑器](https://experienceleague.adobe.com/zh-hans/docs/target/using/experiences/vec/visual-experience-composer)中创建的内容。

要请求并自动呈现[!DNL Target]优惠，请使用`sendEvent`命令并将`renderDecisions`选项设置为`true.`。这样做会强制SDK自动呈现任何有资格自动呈现的个性化内容。

示例：

```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "commerce": {
      "order": {
        "purchaseID": "a8g784hjq1mnp3",
        "purchaseOrderNumber": "VAU3123",
        "currencyCode": "USD",
        "priceTotal": 999.98
      }
    }
  }
});
```

[!DNL Experience Platform Web SDK]自动发送包含[!DNL Platform WEB SDK]执行的选件的通知。 以下示例展示了通知请求有效负载的外观：

```json
{
  "events": [{
      "xdm": {
        "_experience": {
          "decisioning": {
            "propositions": [
              {
                "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI3MDE5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
                "scope": "cart",
                "scopeDetails": {
                  "decisionProvider": "TGT",
                  "activity": {
                    "id": "127019"
                  },
                  "experience": {
                    "id": "0"
                  },
                  "strategies": [
                    {
                      "step": "entry",
                      "algorithmID": "0",
                      "trafficType": "0"
                    },
                    {
                      "step": "display",
                      "algorithmID": "0",
                      "trafficType": "0"
                    }
                  ],
                  "characteristics": {
                    "eventToken": "bKMxJ8dCR1XlPfDCx+2vSGqipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q=="
                  }
                }
              }
            ]
          }
        },
        "eventType": "display",
        "web": {
          "webPageDetails": {
            "viewName": "cart",
            "URL": "https://alloyio.com/personalizationSpa/cart"
          },
          "webReferrer": {
            "URL": ""
          }
        },
        "device": {
          "screenHeight": 800,
          "screenWidth": 1280,
          "screenOrientation": "landscape"
        },
        "environment": {
          "type": "browser",
          "browserDetails": {
            "viewportWidth": 1280,
            "viewportHeight": 284
          }
        },
        "placeContext": {
          "localTime": "2021-12-10T15:50:34.467+02:00",
          "localTimezoneOffset": -120
        },
        "timestamp": "2021-12-10T13:50:34.467Z",
        "implementationDetails": {
          "name": "https://ns.adobe.com/experience/alloy",
          "version": "2.6.2",
          "environment": "browser"
        }
      }
    }
  ]
}
```

[了解详情](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/web-sdk/personalization/rendering-personalization-content)

## 如何请求和&#x200B;*NOT*&#x200B;自动渲染页面加载目标选件

### 使用at.js

有两种方法可触发对[!DNL Target]个Edge的调用，该调用会获取用于页面加载的选件。

示例1：

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox", 
   success: console.log,
   error: console.error
});
```

示例2：

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {}
    }
  }
})
.then(console.log)
.catch(console.error);
```

[了解详情](https://experienceleague.adobe.com/zh-hans/docs/target-dev/developer/client-side/at-js-implementation/functions-overview/atjs-functions)

### 使用[!DNL Platform Web SDK]

在`sendEvent`下执行具有特殊作用域的`decisionScopes`命令： `__view__`。 [!DNL Adobe]使用此作用域作为信号，从[!DNL Target]获取所有页面加载活动并预取所有视图。 [!DNL Platform Web SDK]还会尝试评估所有基于VEC视图的活动。 [!DNL Platform Web SDK]当前不支持禁用视图预取。

要访问任何个性化内容，您可以提供回调函数，在SDK收到来自服务器的成功响应后，将调用该函数。 您的回调提供了一个结果对象，该对象可能包含包含包含任何返回的个性化内容的建议属性。

示例：

```javascript
alloy("sendEvent", {
    xdm: {...},
    decisionScopes: ["__view__"]
  }).then(function(result) {
    if (result.propositions) {
      result.propositions.forEach(proposition => {
        proposition.items.forEach(item => {
          if (item.schema === HTML_SCHEMA) {
            // manually apply offer
            document.getElementById("form-based-offer-container").innerHTML =
              item.data.content;
            const executedPropositions = [
              {
                id: proposition.id,
                scope: proposition.scope,
                scopeDetails: proposition.scopeDetails
              }
            ];
          // manually send the display notification event, so that Target/Analytics impressions aare increased
            alloy("sendEvent",{
              "xdm": {
                "eventType": "decisioning.propositionDisplay",
                "_experience": {
                  "decisioning": {
                    "propositions": executedPropositions
                  }
                }
              }
            });
          }
        });
      });
    }
  });
```

[了解详情](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/web-sdk/personalization/rendering-personalization-content)

## 如何请求特定的基于表单的Target mbox

### 使用at.js

您可以使用`getOffer`函数获取活动：

示例1：

```javascript
adobe.target.getOffer({
   mbox: "hero-banner", 
   success: console.log,
   error: console.error
});
```

示例2：

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        mboxes: [
        {
          index: 0,
          name: "hero-banner"
        }]
    }
  }
})
.then(console.log)
.catch(console.error);
```

[了解详情](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/functions-overview/atjs-functions.html?lang=zh-Hans)

### 使用[!DNL Platform Web SDK]

您可以使用[!UICONTROL Form-Based Composer]命令并在`sendEvent`选项下传递mbox名称来获取基于`decisionScopes`的活动。 `sendEvent`命令返回一个承诺，该承诺会使用包含所请求的活动/建议的对象来解析：

此代码片段是`propositions`数组的外观：

```javascript
[
  {
    "id": "AT:eyJhY3Rpdml0eUlkIjoiNDM0Njg5IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
    "scope": "hero-banner",
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
        "eventToken": "2lTS5KA6gj4JuSjOdhqUhGqipfsIHvVzTQxHolz2IpTMromRrB5ztP5VMxjHbs7c6qPG9UF4rvQTJZniWgqbOw=="
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
    "scope": "hero-banner",
    "scopeDetails": {
      "decisionProvider": "TGT",
      "activity": {
        "id": "434689"
      },
      "characteristics": {
        "eventToken": "E0gb6q1+WyFW3FMbbQJmrg=="
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
]
```

示例：

```javascript
alloy("sendEvent", {
  xdm: { ...},
  decisionScopes: ["hero-banner"]
}).then(function (result) {
  var propositions = result.propositions;

  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      for (var j = 0; j < proposition.items; j++) {
        var item = proposition.items[j];
        if (item.schema === HTML_SCHEMA) {
          // apply offer
          document.getElementById("form-based-offer-container").innerHTML =
            item.data.content;
          const executedPropositions = [
            {
              id: proposition.id,
              scope: proposition.scope,
              scopeDetails: proposition.scopeDetails
            }
          ];

          alloy("sendEvent", {
            "xdm": {
              "eventType": "decisioning.propositionDisplay",
              "_experience": {
                "decisioning": {
                  "propositions": executedPropositions
                }
              }
            }
          });
        }
      }
    }
  }
});
```

[了解详情](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/web-sdk/personalization/rendering-personalization-content)

## 如何应用[!DNL Target]活动

### 使用at.js

您可以使用[!DNL Target]函数来应用`applyOffers`活动： `adobe.target.applyOffer(options).`

示例：

```javascript
adobe.target.getOffers({...})
  .then(response => adobe.target.applyOffers({ response: response }))
  .then(() => console.log("Success"))
  .catch(error => console.log("Error", error));
```

从`applyOffers`专用文档[了解有关](https://experienceleague.adobe.com/zh-hans/docs/target-dev/developer/client-side/at-js-implementation/functions-overview/adobe-target-applyoffers-atjs-2)命令的更多信息。

### 使用[!DNL Platform Web SDK]

您可以使用[!DNL Target]命令应用`applyPropositions`活动。

示例：

```javascript
alloy("applyPropositions", {
    propositions: [...]
});
```

从`applyPropositions`专用文档[了解有关](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/web-sdk/personalization/rendering-personalization-content)命令的更多信息。

## 如何跟踪事件

### 使用at.js

您可以使用`trackEvent`函数或使用`sendNotifications.`跟踪事件

此函数会触发用户操作（例如点击和转化）报告请求。此函数不会在响应中投放活动。

**示例 1**

```javascript
adobe.target.trackEvent({ 
    "type": "click",
    "mbox": "some-mbox"
});
```

**示例 2**

```javascript
adobe.target.sendNotifications({ 
    request: {
       notifications: [{
          ...,
          mbox: {
            name: "some-mbox"
          },
          type: "click",
          ...
       }]
    }
});
```

[了解详情](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-trackevent.html?lang=zh-Hans)

### 使用[!DNL Platform Web SDK]

您可以通过调用`sendEvent`命令、填充`_experience.decisioning.propositions` XDM `fieldgroup`并将`eventType`设置为两个值之一来跟踪事件和用户操作：

* `decisioning.propositionDisplay`：表示[!DNL Target]活动的呈现。
* `decisioning.propositionInteract`：表示用户与活动的交互，如鼠标单击。

`_experience.decisioning.propositions` XDM `fieldgroup`是一个对象数组。 每个对象的属性派生自`result.propositions`命令中返回的`sendEvent`： `{ id, scope, scopeDetails }.`

**示例1 — 呈现活动后跟踪`decisioning.propositionDisplay`事件**

```javascript
alloy("sendEvent", {
  xdm: {},
  decisionScopes: ['discount']
}).then(function(result) {
  var propositions = result.propositions;

  var discountProposition;
  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      if (proposition.scope === "discount") {
        discountProposition = proposition;
        break;
      }
    }
  }

  if (discountProposition) {
    // Find the item from proposition that should be rendered.
    // Rather than assuming there a single item that has HTML
    // content, find the first item whose schema indicates
    // it contains HTML content.
    for (var j = 0; j < discountProposition.items.length; j++) {
      var discountPropositionItem = discountProposition.items[i];
      if (discountPropositionItem.schema === "https://ns.adobe.com/personalization/html-content-item") {
        var discountHtml = discountPropositionItem.data.content;
        // Render the content
        var dailySpecialElement = document.getElementById("daily-special");
        dailySpecialElement.innerHTML = discountHtml;
        
        // For this example, we assume there is only a single place to update in the HTML.
        break;  
      }
    }
    // Send a "decisioning.propositionDisplay" event signaling that the proposition has been rendered.
    alloy("sendEvent", {
      "xdm": {
        "eventType": "decisioning.propositionDisplay",
        "_experience": {
          "decisioning": {
            "propositions": [{
              "id": id,
              "scope": scope,
              "scopeDetails": scopeDetails
            }],
            "propositionEventType": {
              "display": 1
            }
          }
        }
      }
    });
  }
});
```

**示例2 — 发生点击量度后跟踪`decisioning.propositionInteract`事件**

```javascript
alloy("sendEvent", {
  xdm: { ...},
  decisionScopes: ["hero-banner"]
}).then(function (result) {
  var propositions = result.propositions;

  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      for (var j = 0; j < proposition.items.length; j++) {
        var item = proposition.items[j];

        if (item.schema === "https://ns.adobe.com/personalization/measurement") {
          // add metric to the DOM element
          const button = document.getElementById("form-based-click-metric");

          button.addEventListener("click", event => {
            const executedPropositions = [
              {
                id: proposition.id,
                scope: proposition.scope,
                scopeDetails: proposition.scopeDetails
              }
            ];
            // send the click track event
            alloy("sendEvent", {
              "xdm": {
                "eventType": "decisioning.propositionInteract",
                "_experience": {
                  "decisioning": {
                    "propositions": executedPropositions
                  }
                }
              }
            });
          });
        }
      }
    }
  }
});
```

[了解详情](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/web-sdk/personalization/rendering-personalization-content#manual)

**示例3 — 跟踪执行操作后触发的事件**

此示例跟踪在执行特定操作（如单击按钮）后触发的事件。
您可以通过`__adobe.target`数据对象添加任何其他自定义参数。

您还可以添加`commerce` XDM对象。

```js
alloy("sendEvent", {
    "xdm": {
        "_experience": {
            "decisioning": {
                "propositions": [
                    {
                        "scope": "orderConfirm" //example scope name
                    }
                ],
                "propositionEventType": {
                    "display": 1
                }
            }
        },
        "eventType": "decisioning.propositionDisplay"
    },
    "commerce": {
        "order": {
            "purchaseID": "a8g784hjq1mnp3",
            "purchaseOrderNumber": "VAU3123",
            "currencyCode": "USD",
            "priceTotal": 999.98
        }
    },
    "data": {
        "__adobe": {
            "target": {
                "pageType": "Order Confirmation",
                "user.categoryId": "Insurance"
            }
        }
    }
})
```

## 如何在单页应用程序中触发视图更改

### 使用at.js

使用`adobe.target.triggerView`函数。 每当加载新页面或重新渲染页面上的组件时，都可以调用此函数。应该为单页应用程序(SPA)实施`adobe.target.triggerView()`函数以使用[!UICONTROL Visual Experience Composer] (VEC)创建[!UICONTROL A/B Test]和[!UICONTROL Experience Targeting] (XT)活动。 如果未在网站上实施`adobe.target.triggerView()`，则VEC无法用于SPA。

**示例**

```javascript
adobe.target.triggerView("homeView")
```

[了解详情](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-triggerview-atjs-2.md)

### 使用[!DNL Platform Web SDK]

要触发或指示单页应用程序[!UICONTROL View Change]，请在`web.webPageDetails.viewName`命令的`xdm`选项下设置`sendEvent`属性。 如果[!DNL Platform Web SDK]中指定的`viewName`有选件，`sendEvent`将检查视图缓存，然后执行选件并发送显示通知事件。

**示例**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  xdm:{
    web:{
      webPageDetails:{
        viewName: "homeView"
      }
    }
  }
});
```

[了解详情](/help/dev/implement/client-side/aep-web-sdk/spa-implementation.md)

## 如何利用[!UICONTROL Response Tokens]

从[!DNL Target]返回的Personalization内容包含[响应令牌](https://experienceleague.adobe.com/zh-hans/docs/target/using/administer/response-tokens)。 响应令牌包含有关活动、选件、体验、用户配置文件、地理信息等的详细信息。 这些详细信息可与第三方工具共享或用于调试。 可在[!DNL Target]用户界面中配置响应令牌。

### 使用at.js

使用at.js自定义事件监听[!DNL Target]响应并读取响应令牌。

**示例**

```javascript
document.addEventListener(adobe.target.event.REQUEST_SUCCEEDED, function(e) { 
  console.log("Request succeeded", e.detail); 
}); 
```

[了解详情](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?lang=zh-Hans)

### 使用[!DNL Platform Web SDK]

>[!IMPORTANT]
>
>确保您使用的是[!DNL Experience Platform Web SDK]版本2.6.0或更高版本。

响应令牌作为`propositions`的一部分返回，在`sendEvent`命令的结果中公开。 每个建议包含一个由`items,`组成的数组，并且每个项目都有一个使用响应令牌填充的`meta`对象（如果在[!DNL Target]管理UI中启用了响应令牌）。 [了解详情](https://experienceleague.adobe.com/zh-hans/docs/target/using/administer/response-tokens)

**示例**

```javascript
alloy("sendEvent", {
    renderDecisions: true,
    xdm: {}
  }).then(function(result) {
    if (result.propositions) {
      // Format of result.propositions:
      /*
        [
            {
                "id": "",
                "scope": "",
                "items": [
                    {
                        "id": "",
                        "schema": "",
                        "data": {},
                        "meta": { // RESPONSE TOKENS
                            "activity.name": ...,
                            "offer.id": ...,
                            "profile.activeActivities": ...
                        }
                    }
                ],
                "scopeDetails": {}
                "renderAttempted": false
            }
        ]
      */
    }
  });
```

[了解详情](/help/dev/implement/client-side/aep-web-sdk/accessing-response-tokens.md)

## 如何管理闪烁

### 使用at.js

使用at.js，您可以通过设置`bodyHidingEnabled: true`来管理闪烁，以便at.js可以解决此问题
在提取和应用DOM更改之前预隐藏个性化容器。

通过覆盖at.js `bodyHiddenStyle.`，可以预先隐藏包含个性化内容的页面部分

默认情况下，`bodyHiddenStyle`会隐藏整个HTML `body.`

可使用`window.targetGlobalSettings.`覆盖这两个设置`window.targetGlobalSettings`应放在加载at.js之前。

### 使用[!DNL Platform Web SDK]

使用[!DNL Platform Web SDK]，客户可以在configure命令中设置其预隐藏样式，如以下示例所示：

```javascript
alloy("configure", {
  datastreamId: "configurationId",
  orgId: "orgId@AdobeOrg",
  debugEnabled: true,
  prehidingStyle: "body { opacity: 0 !important }"
});
```

加载[!DNL Platform Web SDK]异步时，[!DNL Adobe]建议在插入[!DNL Platform Web SDK]之前在页面中插入以下代码片段：

```html
<script>
  !function(e,a,n,t){
  if (a) return;
  var i=e.head;if(i){
  var o=e.createElement("style");
  o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),
  setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
  (document, document.location.href.indexOf("adobe_authoring_enabled") !== -1, "body { opacity: 0 !important }", 3000);
</script>
```

## 如何处理A4T

### 使用at.js

使用at.js支持以下两种类型的A4T日志记录：

* Analytics客户端日志记录
* Analytics服务器端日志记录

#### Analytics客户端日志记录

**示例1：使用[!DNL Target]全局设置**

可以通过在at.js设置中设置`analyticsLogging: client_side`或覆盖`window.targetglobalSettings`对象来启用Analytics客户端日志记录。

设置此选项后，返回的有效负载格式如下所示：

```json
{
  "analytics": {
    "payload": {
      "pe": "tnt",
      "tnta": "167169:0:0|0|100,167169:0:0|2|100,167169:0:0|1|100"
    }
  }
}
```

然后，可以通过[!DNL Analytics]将该有效负载转发到[!DNL &#x200B; Data Insertion API]。

示例2：在每个`getOffers`函数中对其进行配置：

```javascript
adobe.target.getOffers({
      request: {
        experienceCloud: {
          analytics: {
            logging: "client_side"
          }
        },
        prefetch: {
          mboxes: [{
            index: 0,
            name: "a1-serverside-xt"
          }]
        }
      }
    })
    .then(console.log)
```

此代码片段展示了响应有效负载的外观：

```json
{
  "prefetch": {
    "mboxes": [{
      "index": 0,
      "name": "a1-serverside-xt",
      "options": [{
        "content": "<img src=\"http://s7d2.scene7.com/is/image/TargetAdobeTargetMobile/L4242-xt-usa?tm=1490025518668&fit=constrain&hei=491&wid=980&fmt=png-alpha\"/>",
        "type": "html",
        "eventToken": "n/K05qdH0MxsiyH4gX05/2qipfsIHvVzTQxHolz2IpSCnQ9Y9OaLL2gsdrWQTvE54PwSz67rmXWmSnkXpSSS2Q==",
        "responseTokens": {
          "profile.memberlevel": "0",
          "geo.city": "bucharest",
          "activity.id": "167169",
          "experience.name": "USA Experience",
          "geo.country": "romania"
        }
      }],
      "analytics": {
        "payload": {
          "pe": "tnt",
          "tnta": "167169:0:0|0|100,167169:0:0|2|100,167169:0:0|1|100"
        }
      }
    }]
  }
}
```

[!DNL Analytics]有效负载（`tnta`令牌）应包含在使用[!DNL Analytics]数据插入API[的](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md)点击中。

#### [!DNL Analytics]服务器端日志记录

可以通过在at.js设置中设置[!DNL Analytics]或覆盖`analyticsLogging: server_side`对象来启用`window.targetglobalSettings`服务器端日志记录。

然后，数据将按如下方式流动：

![显示Analytics服务器端日志记录工作流的图表](/help/dev/implement/client-side/aep-web-sdk/assets/a4t-server-side-atjs.png)

[了解更多](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4timplementation.html?lang=zh-Hans)

### 使用[!DNL Platform Web SDK]

Web SDK还支持：

* Analytics客户端日志记录
* Analytics服务器端日志记录

#### [!DNL Analytics]客户端日志记录

当针对该DataStream配置禁用[!DNL Analytics]时，[!DNL Adobe Analytics]客户端日志记录已启用。

![显示Analytics客户端日志记录工作流的图表](/help/dev/implement/client-side/aep-web-sdk/assets/analytics-disabled-datastream-config.png)

客户有权访问需要使用[!DNL Analytics]数据插入API`tnta`与[!DNL Analytics]共享的[令牌(](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md))，方法是链接`sendEvent`命令并迭代结果建议数组。

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
    var proposition = results.propositions[i];
    var renderAttempted = proposition.renderAttempted;

    if (renderAttempted === true) {
      var analyticsPayload = getAnalyticsPayload(proposition);
      if (analyticsPayload !== undefined) {
        analyticsPayloads.add(analyticsPayload);
      }
    }
  }
  var analyticsPayloadsToken = concatenateAnalyticsPayloads(analyticsPayloads);
  // send the page view Analytics hit with collected Analytics payload using Data Insertion API
});
```

下图显示了启用[!DNL Analytics]客户端时数据如何流动：

Analytics客户端日志记录中的![数据流图](/help/dev/implement/client-side/aep-web-sdk/assets/analytics-client-side-logging.png)

#### [!DNL Analytics]服务器端日志记录

为该DataStream配置启用了[!DNL Analytics]时，将启用[!DNL Analytics]服务器端日志记录。

![显示Analytics设置的数据流UI。](/help/dev/implement/client-side/aep-web-sdk/assets/analytics-enabled-datastream-config.png)

启用服务器端[!DNL Analytics]日志记录后，A4T有效负载需要与[!DNL Analytics]共享，以便[!DNL Analytics]报表显示正确的展示次数并在Edge Network级别共享转化，这样客户就无需执行任何附加处理。

下面是启用服务器端Analytics日志记录时数据如何流入系统：

![显示服务器端Analytics日志记录中数据流的图表](/help/dev/implement/client-side/aep-web-sdk/assets/analytics-server-side-logging.png)

## 如何设置[!DNL Target]全局设置

### 使用at.js

您可以使用`window.targetGlobalSettings,`覆盖at.js库中的设置，而不是在[!DNL Target]用户界面中或通过使用REST API来配置设置。

应在加载at.js之前或在“管理”>“实施”>“编辑at.js设置”>“代码设置”>“库标题”中定义覆盖。

示例：

```javascript
window.targetGlobalSettings = {  
   timeout: 200, // using custom timeout  
   visitorApiTimeout: 500, // using custom API timeout  
   enabled: document.location.href.indexOf('https://www.adobe.com') >= 0 // enabled ONLY on adobe.com  
};
```

[了解详情](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetgobalsettings.html?lang=zh-Hans)

### 使用[!DNL Platform Web SDK]

Web SDK不支持此功能。

## 如何更新[!DNL Target]配置文件属性

### 使用at.js

**示例 1**

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox",
   params: {
     "profile.name": "test",
     "profile.gender": "female"
   },
   success: console.log,
   error: console.error
});
```

**示例 2**

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {
          profileParameters: {
            name: "test",
            gender: "female"
          }
        }
    }
  }
})
.then(console.log)
.catch(console.error);
```

### 使用[!DNL Platform Web SDK]

要更新[!DNL Target]配置文件，请使用`sendEvent`命令并设置`data.__adobe.target`属性，并使用`profile.`为键名添加前缀

**示例**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "profile.gender": "female",
        "profile.age": 30
      }
    }
  }
});
```

## 如何使用[!DNL Target Recommendations]

### 使用at.js

**示例 1**

```javascript
adobe.target.getOffer({
   mbox: "target-global-mbox",
   params: {
     "entity.name": "T-shirt",
     "entity.id": "1234"
   },
   success: console.log,
   error: console.error
});
```

**示例 2**

```javascript
adobe.target.getOffers({
    request: {
      execute: {
        pageLoad: {
          parameters: {
            "entity.name": "T-shirt",
            "entity.id": "1234"
          }
        }
    }
  }
})
.then(console.log)
.catch(console.error);
```

[了解详情](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/adobe-target-getoffers-atjs-2.html?lang=zh-Hans)

### 使用[!DNL Platform Web SDK]

要发送[!DNL Recommendations]数据，请使用`sendEvent`命令并设置`data.__adobe.target`属性，并使用`entity.`为键名添加前缀

**示例**

```javascript
alloy("sendEvent", {
  renderDecisions: true,
  data: {
    __adobe: {
      target: {
        "entity.name": "T-shirt",
        "entity.id": "1234"
      }
    }
  }
});
```

## 如何使用第三方ID

### 使用at.js

使用at.js可通过多种方式使用`mbox3rdPartyId`或`getOffer,`发送`getOffers`：

**示例 1**

```javascript
adobe.target.getOffer({
  mbox:"test",
  params:{
    "mbox3rdPartyId": "1234"
  },
  success: console.log,
  error: console.error
});
```

**示例 2**

```javascript
adobe.target.getOffers({
    request: {
      id:{
        thirdPartyId: "1234"
      },
      execute: {
        pageLoad: {}
    }
  }
})
.then(console.log)
.catch(console.error);
```

或者可以在`mbox3rdPartyId`或`targetPageParams`中设置`targetPageParamsAll.`

设置`targetPageParams`时，它会发送对`target-global-mbox`的请求，也称为`pag-lLoad`。

推荐将使用`targetPageParamsAll`进行设置，因为它将在每[!DNL Target]个请求中发送。 使用`targetPageParamsAll`的优点是，您可以在页面上定义一次`mbox3rdPartyId`以确保所有[!DNL Target]请求都有正确的`mbox3rdPartyId.`

```javascript
window.targetPageParamsAll = function() {
      return {
        "mbox3rdPartyId": "1234"
      };
    };
```

```javascript
window.targetPageParams = function() {
  return {
    "mbox3rdPartyId": "1234"
  };
};
```

[了解详情](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/functions-overview/targetpageparams.html?lang=zh-Hans)

### 使用[!DNL Platform Web SDK]

[!DNL Platform Web SDK]支持[!DNL Target]第三方ID 但是，还需要执行几个步骤。

标识映射允许客户发送多个标识。 所有身份都处于命名空间中。 每个命名空间可以具有一个或多个标识。 可以将特定标识标记为主要标识。 有了这些知识，您可以了解为[!DNL Platform Web SDK]设置使用[!DNL Target]第三方ID所需的步骤。

1. 在数据流配置页面中设置包含[!DNL Target]第三方ID的命名空间：

![数据流UI显示Target第三方ID命名空间字段](/help/dev/implement/client-side/aep-web-sdk/assets/mbox3rdpartyid.png)

1. 在每个`sendEvent`命令中发送该身份命名空间，如下所示：

```javascript
alloy("sendEvent", {
  "renderDecisions": true,
  "xdm": {
    "identityMap": {
      "TGT3PID": [
        {
          "id": "1234",
          "primary": true
        }
      ]
    }
  }
});
```

## 如何设置属性令牌

### 使用at.js

使用at.js有两种设置属性令牌的方法，即使用`targetPageParams`或`targetPageParamsAll.`使用`targetPageParams`将属性令牌添加到`target-global-mbox`调用中，但使用`targetPageParamsAll`会将该令牌添加到所有[!DNL Target]调用中：

**示例 1**

```javascript
   window.targetPageParamsAll = function() {
      return {
        "at_property": "1234"
      };
    };
```

**示例 2**

```javascript
window.targetPageParams = function() {
      return {
        "at_property": "1234"
      };
    };
```

### 使用[!DNL Platform Web SDK]

使用[!DNL Platform Web SDK]，客户在设置[!DNL Adobe Target]命名空间下的数据流配置时，能够在更高级别设置属性：

![显示Adobe Target设置的数据流UI。](/help/dev/implement/client-side/aep-web-sdk/assets/at-property-setup.png)

这意味着该特定数据流配置的每[!DNL Target]调用都包含该属性令牌。

## 如何预取mbox

### 使用at.js

此功能仅在at.js 2.x中可用。at.js 2.x具有一个名为`getOffers`的新函数。 `getOffers`函数允许客户预取一个或多个mbox的内容。 示例如下：

```javascript
adobe.target.getOffers({
    request: {
      prefetch: {
        mboxes: [{
          index: 0,
          name: "test-mbox",
          parameters: {
            ...
          },
          profileParameters: {
            ...
          }
        }]
    }
  }
})
.then(console.log)
.catch(console.error);
```

>[!NOTE]
>
>Adobe建议确保`mbox`数组中的每个`mboxes`都有自己的索引。 通常，第一个mbox具有`index=0`以及下一个`index=1,`，依此类推。

### 使用[!DNL Platform Web SDK]

[!DNL Platform Web SDK]当前不支持此功能。

## 如何调试[!DNL Target]实施

### 使用at.js

at.js库会显示以下调试功能：

* Mbox禁用 — 禁止提取和渲染[!DNL Target]以检查页面是否损坏，且没有[!DNL Target]交互
* Mbox调试 — at.js记录每个操作
* 目标跟踪 — 跟踪对象中生成的mbox跟踪令牌包含参与决策过程的详细信息，该跟踪对象可在`window.___target_trace`对象下使用。

>[!NOTE]
>
>所有这些调试功能都可以在[Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)的增强功能中使用。

### 使用[!DNL Platform Web SDK]

使用[!DNL Platform Web SDK]时，您拥有多种调试功能：

* 使用[Assurance](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/assurance/home)
* [已启用Web SDK调试](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/assurance/home)
* 使用[Web SDK监视挂接](https://github.com/adobe/alloy/wiki/Monitoring-Hooks)
* 使用[Adobe Experience Platform Debugger](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/debugger/home)
* 目标跟踪