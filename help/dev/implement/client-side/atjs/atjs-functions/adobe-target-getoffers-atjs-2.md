---
keywords: adobe.target.getOffers， getOffers， getoffers， get offers， at.js，函数，函数， $8
description: 使用 [!UICONTROL adobe.target.getOffers()] 函数及其选项 [!DNL Adobe Target] at.js库触发获取多个 [!DNL Target] 选件。 (at.js 2.x)
title: 如何使用 [!UICONTROL adobe.target.getOffers()] 功能？
feature: at.js
exl-id: b96a3018-93eb-49e7-9aed-b27bd9ae073a
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1306'
ht-degree: 64%

---

# [!UICONTROL adobe.target.getOffers()] - at.js 2.x

此函数允许您通过传递多个 mbox 来检索多个选件。此外，还可以针对活跃活动中的所有视图检索多个选件。

>[!NOTE]
>
>此函数已在 at.js 2.x 中引入。但此函数不适用于 at.js 版本 1.*x*。

| 键值 | 类型 | 必需？ | 描述 |
| --- | --- | --- | --- |
| `consumerId` | 字符串 | 否 | 如果未提供，则默认值为客户端的全局 mbox。可使用此键值生成用于A4T集成的补充数据ID (SDID)。<P>使用时 `getOffers()`，则每个调用均会生成一个新的SDID。 如果您在同一页面上有多个mbox请求，并且希望保留SDID(以便它与target-global-mbox中的SDID以及 [!DNL Adobe Analytics] SDID)，使用 `consumerId` 参数。<P>如果 `getOffers()` 包含三个mbox（名为“mbox1”、“mbox2”和“mbox3”），包括： `consumerId: "mbox1, mbox2, mbox3"` 在 `getOffers()` 呼叫。 |
| `decisioningMethod` | 字符串 | 否 | &quot;server-side&quot;、&quot;on-device&quot;、&quot;hybrid&quot; |
| `request` | 对象 | 是 | 请参阅下文的“请求”表。 |
| `timeout` | 数值 | 否 | 请求超时. 如果未指定，将使用默认的 at.js 超时值。 |

## 请求

>[!NOTE]
>
>请参阅 [交付API文档](/help/dev/implement/delivery-api/overview.md) 有关下面列出的所有字段的可接受类型的信息。

| 字段名称 | 必需？ | 限制 | 描述 |
| --- | --- | --- | --- |
| request > id | 否 |  | 需要使用 `tntId`、`thirdPartyId` 或 `marketingCloudVisitorId` 中的一个。 |
| request > id > thirdPartyId | 否 | 最大大小 = 128. |  |  |
| Request > experienceCloud | 否 |  |  |
| Request > experienceCloud > analytics | 否 |  | Adobe Analytics 集成 |
| Request > experienceCloud > analytics > logging | 否 | 必须在页面上实施以下内容：<ul><li>访客 ID 服务</li><li>Appmeasurement.js</li></ul> | 支持以下值：<P>**client_side**：指定后，将向调用方返回分析有效负载，该有效负载应该用于发送至 [!UICONTROL Adobe Analytics] 通过 [!UICONTROL 数据插入API].<P>**server_side**[!DNL Target][!DNL Analytics]：这是默认值， 和 后端会使用 SDID 将调用拼合在一起进行报告。 |
| request > prefetch | 否 |  |  |
| request > prefetch > views | 否 | 最大计数50。<P>名称不为空。<P>名称长度 `<=` 128.<P>值长度 `<=` 5000<P>名称不应以“profile”开头。<P>不允许的名称： “orderId”、“orderTotal”、“productPurchasedId”。 | 传递用于检索活跃活动中相关视图的参数。 |
| request > prefetch > views > profileParameters | 否 | 最大计数50。<P>名称不为空。<P>名称长度 `<=` 128.<P>值长度 `<=` 5000<P>仅接受字符串值。<P>名称不应以“profile”开头。 | 传递用于检索活跃活动中相关视图的配置文件参数。 |
| request > prefetch > views > product | 否 |  |  |
| request > prefetch > views > product -> id | 否 | 不为空。<P>最大大小= 128。 | 传递用于检索活跃活动中相关视图的产品 ID。 |
| request > prefetch > views > product > categoryId | 否 | 不为空。<P>最大大小= 128。 | 传递用于检索活跃活动中相关视图的产品类别 ID。 |
| request > prefetch > views > order | 否 |  |  |
| request > prefetch > views > order > id | 否 | 最大长度 = 250. | 传递用于检索活跃活动中相关视图的订单 ID。 |
| request > prefetch > views > order > total | 否 | 总额 `>=` 0. | 传递用于检索活跃活动中相关视图的订单总额。 |
| request > prefetch > views > order > purchasedProductIds | 否 | 无空白值。<P>每个值的最大长度为50。<P>连接并以逗号分隔。<P>产品ID总长度 `<=` 250。 | 传递用于检索活跃活动中相关视图的已购买产品 ID。 |
| request > execute | 否 |  |  |
| request > execute > pageLoad | 否 |  |  |
| request > execute > pageLoad > parameters | 否 | 最大计数50。<P>名称不为空。<P>名称长度 `<=` 128.<P>值长度 `<=` 5000<P>仅接受字符串值。<P>名称不应以“profile”开头。<P>不允许的名称： “orderId”、“orderTotal”、“productPurchasedId”。 | 页面加载时使用指定的参数检索选件。 |
| request > execute > pageLoad > profileParameters | 否 | 最大计数50。<P>名称不为空。<P>名称长度 `<=` 128.<P>值长度 `<=`256。<P>名称不应以“profile”开头。<P>仅接受字符串值。 | 页面加载时使用指定的配置文件参数检索选件。 |
| request > execute > pageLoad > product | 否 |  |  |
| request > execute > pageLoad > product -> id | 否 | 不为空。<P>最大大小 = 128. | 页面加载时使用指定的产品 ID 检索选件。 |
| request > execute > pageLoad > product > categoryId | 否 | 不为空。<P>最大大小 = 128. | 页面加载时使用指定的产品类别 ID 检索选件。 |
| request > execute > pageLoad > order | 否 |  |  |
| request > execute > pageLoad > order > id | 否 | 最大长度 = 250. | 页面加载时使用指定的订单 ID 检索选件。 |
| request > execute > pageLoad > order > total | 否 | `>=` 0. | 页面加载时使用指定的订单总额检索选件。 |
| request > execute > pageLoad > order > purchasedProductIds | 否 | 无空白值。<P>每个值的最大长度为50。<P>连接并以逗号分隔。<P>产品ID总长度 `<=` 250。 | 页面加载时使用指定的已购产品 ID 检索选件。 |
| request > execute > mboxes | 否 | 最大大小 = 50.<P>无null元素。 |  |
| request > execute > mboxes > mbox | 是 | 不为空。<P>无“ — clicked”后缀。<P>最大大小 = 250.<P>允许的字符： `'-, ._\/=:;&!@#$%^&*()_+|?~[]{}'` | mbox 的名称。 |
| request > execute > mboxes > mbox > index | 是 | 不为null。<P>独特.<P>`>=` 0. | 请注意，index 并不表示 mbox 的处理顺序。与具有多个区域 mbox 的网页相同，无法指定这些 mbox 的处理顺序。 |
| request > execute > mboxes > mbox > parameters | 否 | 最大计数= 50。<P>名称不为空。<P>名称长度 `<=` 128.<P>仅接受字符串值。<P>值长度 `<=` 5000<P>名称不应以“profile”开头。<P>不允许的名称： “orderId”、“orderTotal”、“productPurchasedId”。 | 使用指定的参数针对给定 mbox 检索选件。 |
| request > execute > mboxes > mbox > profileParameters | 否 | 最大计数= 50。<P>名称不为空。<P>名称长度 `<=` 128.<P>仅接受字符串值。<P>值长度 `<=`256。<P>名称不应以“profile”开头。 | 使用指定的配置文件参数检索给定 mbox 的选件。 |
| request > execute > mboxes > mbox > product | 否 |  |  |
| request > execute > mboxes > mbox > product > id | 否 | 不为空。<P>最大大小 = 128. | 使用指定的产品 ID 检索给定 mbox 的选件。 |
| request > execute > mboxes > mbox > product > categoryId | 否 | 不为空。<P>最大大小 = 128. | 使用指定的产品类别 ID 检索给定 mbox 的选件。 |
| request > execute > mboxes > mbox > order | 否 |  |  |
| request > execute > mboxes > mbox > order > id | 否 | 最大长度 = 250. | 使用指定的订单 ID 检索给定 mbox 的选件。 |
| request > execute > mboxes > mbox > order > total | 否 | `>=` 0. | 使用指定的订单总额检索给定 mbox 的选件。 |
| request > execute > mboxes > mbox > order > purchasedProductIds | 否 | 无空白值。<P>每个值的最大长度= 50。<P>连接并以逗号分隔。<P>产品ID总长度 `<=` 250。 | 使用指定的订单已购产品 ID 检索给定 mbox 的选件。 |

## 调用 [!UICONTROL getOffers()] （所有视图）

```javascript {line-numbers="true"}
adobe.target.getOffers({
    request: {
      prefetch: {
        views: [{}]
    }
  }
});
```

## 调用 [!UICONTROL getOffers()] 进行设备上决策

```javascript {line-numbers="true"}
adobe.target.getOffers({ 

  decisioningMethod:"on-device", 
  request: { 
    execute: { 
      mboxes: [ 
        { 
          index: 0, 
          name: "homepage" 
        } 
      ] 
    } 
 } 
}); 
```

## 调用 [!UICONTROL getOffers()] 使用传递的参数和配置文件参数检索最新的视图

```javascript {line-numbers="true"}
adobe.target.getOffers({
  request: {
    "prefetch": {
      "views": [
        {
          "parameters": {
            "ad": "1"
          },
          "profileParameters": {
            "age": 23
          }
        }
      ]
    }
  }
});
```

## 调用 [!UICONTROL getOffers()] 以使用传递的参数和配置文件参数检索mbox。

```javascript {line-numbers="true"}
adobe.target.getOffers({
  request: {
    execute: {
      mboxes: [
        {
          index: 0,
          name: "first-mbox"
        },
        {
          index: 1,
          name: "second-mbox",
          parameters: {
            a: 1
          },
          profileParameters: {
            b: 2
          }
        }
      ]
    }
  }
});
```

## 调用 [!UICONTROL getOffers()] 从客户端检索分析有效负载

```javascript {line-numbers="true"}
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

**响应**：

```javascript {line-numbers="true"}
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

然后，可以将有效负载转发到 [!DNL Adobe Analytics] 通过 [数据插入API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md).

## 通过获取并渲染多个mbox的数据 [!UICONTROL getOffers()] 和 [!UICONTROL applyOffers()]

at.js 2.x 允许您通过 `[!UICONTROL getOffers()]` API 获取多个 mbox。您还可以获取多个 mbox 的数据，然后使用 `[!UICONTROL applyOffers()]` 在 CSS 选择器标识的不同位置渲染数据。

以下示例展示了实施了 at.js 2.x 的简单 HTML 页面：

```html {line-numbers="true"}
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>at.js 2.x, multiple selectors and multiple mboxes</title>
  <script src="at.js"></script>
</head>
<body>
  <div id="container1">Default content 1</div>
  
  <div id="container2">Default content 2</div>

  <div id="container3">Default content 3</div>
</body>
</html>
```

假设您有三个容器，并且想要通过从 [!DNL Target] 收到的内容对其进行修改。您可以为三个 mbox 构建一个请求，其中每个 mbox 都有一些内容要渲染到相应的容器中。

请求和渲染代码可能类似于以下示例：

```javascript {line-numbers="true"}
adobe.target.getOffers({
  request: {
    prefetch: {
      mboxes: [
        {
          index: 0,
          name: "mbox1"
        },
        {
          index: 1,
          name: "mbox2"
        },
        {
          index: 2,
          name: "mbox3"
        }
      ]
    }
  }
})
.then(response => {
  // get all mboxes from response
  const mboxes = response.prefetch.mboxes;
  let count = 1;

  mboxes.forEach(el => {
    adobe.target.applyOffers({
      selector: "#container" + count,
      response: {
        prefetch: {
          mboxes: [el]
        }
      }
    });

    count += 1;
  });
});
```

在 `request > prefetch > mboxes` 部分中，有三个不同的 mbox。如果请求成功完成，您将从 `response > prefetch > mboxes` 中收到每个 mbox 的响应。获得响应和要用于渲染的位置后，可以调用 `applyOffers()` 以渲染从 [!DNL Target] 中检索的内容。在本示例中，我们有以下映射：

* mbox1 > CSS 选择器 #container1
* mbox2 > CSS 选择器 #container2
* mbox3 > CSS 选择器 #container3

此示例使用 count 变量来构建 CSS 选择器。在现实场景中，您可以使用 CSS 选择器和 mbox 之间的不同映射。

请注意，此示例使用了 `prefetch > mboxes`，但您也可以使用 `execute > mboxes`。请确保，如果在 `getOffers()` 中使用 prefetch，则在 `applyOffers()` 调用中也应使用 prefetch。

## 调用 [!UICONTROL getOffers()] 执行页面加载

以下示例说明如何使用执行pageLoad [!UICONTROL getOffers()] 使用at.js 2.*x*

```javascript {line-numbers="true"}
adobe.target.getOffers({
    request: {
        execute: {
            pageLoad: {
                parameters: {}
            }
        }
    }
});
```
