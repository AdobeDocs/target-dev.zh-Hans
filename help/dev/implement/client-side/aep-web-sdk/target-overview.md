---
title: 使用 [!DNL Adobe Target] 与 [!DNL Web SDK] 进行个性化。
description: 了解如何使用 [!DNL Experience Platform Web SDK] 使用 [!DNL Adobe Target]呈现个性化内容。
feature: AEP Web SDK
source-git-commit: 1fe6adc25604612ed9fa090f1f68c18b9c0bdf63
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 5%

---

# 使用[!DNL Adobe Target]和[!DNL Web SDK]进行个性化

[!DNL Adobe Experience Platform] [!DNL Web SDK]可以将在[!DNL Adobe Target]中管理的个性化体验交付并渲染到Web渠道。 您可以使用名为[可视化体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=zh-Hans) (VEC)的WYSIWYG编辑器，或使用非可视化界面[基于表单的体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html?lang=zh-Hans)创建、激活并交付活动和个性化体验。

>[!IMPORTANT]
>
>了解如何使用[!DNL Target]将Target从at.js 2.x迁移到Experience Platform Web SDK[!DNL Experience Platform Web SDK]教程将[实施迁移到](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html?lang=zh-Hans)。
>
>了解如何使用[!DNL Target]使用Web SDK实施Adobe Experience Cloud[教程首次实施](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=zh-Hans)。 有关[!DNL Target]的特定信息，请参阅标题为[使用Experience Platform Web SDK设置Target](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html?lang=zh-Hans)的教程部分。

以下功能已经过测试，当前在[!DNL Target]中受支持：

* [A/B 测试](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html?lang=zh-Hans)
* [A4T展示和转化报告](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html?lang=zh-Hans)
* [Automated Personalization活动](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html?lang=zh-Hans)
* [体验定位活动](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html?lang=zh-Hans)
* [多变量测试 (MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html?lang=zh-Hans)
* [推荐活动](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations.html?lang=zh-Hans)
* [本机目标展示和转化报告](https://experienceleague.adobe.com/docs/target/using/reports/reports.html?lang=zh-Hans)
* [VEC支持](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=zh-Hans)

## [!DNL Web SDK]系统图

下图可帮助您了解[!DNL Target]和[!DNL Web SDK]边缘决策的工作流。

![使用Experience Platform Web SDK的Adobe Target Edge Decisioning图表](/help/dev/implement/client-side/aep-web-sdk/assets/target-platform-web-sdk-new.png)

| 调用 | 详细信息 |
| --- | --- |
| 1 | 设备加载[!DNL Web SDK]。 [!DNL Web SDK]向Edge Network发送请求，其中包含XDM数据、数据流环境ID、传入参数和客户ID（可选）。 页面（或容器）已预先隐藏。 |
| 2 | Edge Network将请求发送到边缘服务，以使用访客ID、同意和其他访客上下文信息（如地理位置和设备友好名称）对其进行扩充。 |
| 3 | Edge Network使用访客ID和传入的参数将扩充的个性化请求发送给[!DNL Target]边缘。 |
| 4 | 配置文件脚本在执行后进入[!DNL Target]配置文件存储。 配置文件存储从[!UICONTROL Audience Library]获取区段（例如，从[!DNL Adobe Analytics]、[!DNL Adobe Audience Manager]、[!DNL Adobe Experience Platform]共享的区段）。 |
| 5 | 根据URL请求参数和配置文件数据，[!DNL Target]确定将为访客显示的当前页面视图和未来预取视图的活动和体验。 [!DNL Target]然后将此数据发送回Edge Network。 |
| 6 | a. Edge Network将个性化响应发送回页面，其中可能包含其他个性化的配置文件值。 当前页面上的个性化内容会在默认内容不发生闪烁的情况下尽快显示。<br>b。作为用户在单页应用程序(SPA)中操作结果而显示的视图的个性化内容将缓存，这样便可在触发视图时即时应用而无需额外的服务器调用。 <br>c。Edge Network会发送访客ID以及Cookie中的其他值，例如同意、会话ID、身份、Cookie检查和个性化。 |
| 7 | Web SDK将通知从设备发送到Edge Network。 |
| 8 | Edge Network将[!UICONTROL Analytics for Target] (A4T)详细信息（活动、体验和转化元数据）转发到[!DNL Analytics]边缘。 |

## 正在启用[!DNL Adobe Target]

要启用[!DNL Target]，请执行以下操作：

1. 使用适当的客户端代码启用[!DNL Target]数据流[中的](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/datastreams/overview)。
1. 将`renderDecisions`选项添加到您的事件。

然后，您还可以选择添加以下选项：

* **`decisionScopes`**：通过将此选项添加到您的事件中，检索特定活动（对于使用基于表单的编辑器创建的活动很有用）。
* **[预隐藏代码片段](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/web-sdk/personalization/manage-flicker)**：仅隐藏页面的某些部分。

## 使用[!UICONTROL Adobe Target] VEC

要将VEC与[!DNL Web SDK]实现结合使用，请安装并激活[Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/)或[Chrome](https://experienceleague.adobe.com/zh-hans/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension) VEC Helper扩展。

有关详细信息，请参阅[Adobe Target指南](https://experienceleague.adobe.com/docs/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html?lang=zh-Hans)中的&#x200B;*可视化体验编辑器助手扩展*。

## 呈现个性化内容

有关详细信息，请参阅[呈现个性化内容](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/web-sdk/personalization/rendering-personalization-content)。

## XDM中的受众

在为通过[!DNL Target]交付的[!DNL Web SDK]活动定义受众时，必须定义和使用[XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=zh-Hans)。 定义XDM架构、类和架构字段组后，可创建由XDM数据定义的[!DNL Target]受众规则以进行定位。 在[!DNL Target]内，XDM数据在[!UICONTROL Audience Builder]中显示为自定义参数。 XDM使用点表示法序列化（例如，`web.webPageDetails.name`）。

如果您的[!DNL Target]活动包含使用自定义参数或用户配置文件的预定义受众，则无法通过SDK正确交付这些受众。 您必须改用XDM，而不是使用自定义参数或用户配置文件。 但是，有一些通过[!DNL Web SDK]支持的现成受众定向字段不需要XDM。 这些字段在[!DNL Target] UI中可用，不需要XDM：

* 锁定库
* 地域
* 网络
* 操作系统
* 网站页面
* 浏览器
* 流量源
* 时间范围

有关详细信息，请参阅[Adobe Target指南](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/target-rules.html?lang=zh-Hans)中的&#x200B;*受众类别*。

### 响应令牌

响应令牌用于将元数据发送到Google或Facebook等第三方。 返回响应令牌
在`meta` > `propositions`内的`items`字段中。

以下是示例：

```json
{
  "id": "AT:eyJhY3Rpdml0eUlkIjoiMTI2NzM2IiwiZXhwZXJpZW5jZUlkIjoiMCJ9",
  "scope": "__view__",
  "scopeDetails": ...,
  "renderAttempted": true,
  "items": [
    {
      "id": "0",
      "schema": "https://ns.adobe.com/personalization/dom-action",
      "meta": {
        "experience.id": "0",
        "activity.id": "126736",
        "offer.name": "Default Content",
        "offer.id": "0"
      }
    }
  ]
}
```

要收集响应令牌，您必须订阅`alloy.sendEvent` promise，通过`propositions`进行迭代，并从`items` -> `meta`中提取详细信息。

每个`proposition`都有一个`renderAttempted`布尔字段，用于指示`proposition`是否已呈现。 请参阅下面的示例：

```js
alloy("sendEvent",
  {
    "renderDecisions": true,
    "decisionScopes": [
      "hero-container"
    ]
  }).then(result => {
    const { propositions } = result;

    // filter rendered propositions
    const renderedPropositions = propositions.filter(proposition => proposition.renderAttempted === true);

    // collect the item metadata that represents the response tokens
    const collectMetaData = (items) => {
      return items.filter(item => item.meta !== undefined).map(item => item.meta);
    }

    const pageLoadResponseTokens = renderedPropositions
      .map(proposition => collectMetaData(proposition.items))
      .filter(e => e.length > 0)
      .flatMap(e => e);
  });
  
```

启用自动渲染时，建议数组包含：

#### 在页面加载时：

* 基于表单的编辑器`propositions`，其中`renderAttempted`标志设置为`false`
* 基于Visual Experience Composer的建议，`renderAttempted`标志设置为`true`
* 对于标志设置为`renderAttempted`的`true`的单页应用程序视图，基于可视化体验编辑器的建议

#### 查看时 — 更改（对于缓存的视图）：

* 对于标志设置为`renderAttempted`的`true`的单页应用程序视图，基于可视化体验编辑器的建议

禁用自动渲染时，建议数组包含：

#### 在页面加载时：

* 基于[!DNL Form-based Composer]的`propositions`，其中`renderAttempted`标志设置为`false`
* 基于[!DNL Visual Experience Composer]的建议，其中`renderAttempted`标志设置为`false`
* 基于[!DNL Visual Experience Composer]的单页应用程序视图建议，且标志设置为`renderAttempted` `false`

#### 查看时 — 更改（对于缓存的视图）：

* 针对标志设置为`renderAttempted`的`false`的单页应用程序视图，基于可视化体验编辑器的建议

### 单个配置文件更新

通过[!DNL Web SDK]，您可以将个人资料更新到[!DNL Target]个人资料和[!DNL Web SDK]以作为体验事件。

要更新[!DNL Target]配置文件，请确保通过以下方式传递配置文件数据：

* 在`"data {"`下
* 在`"__adobe.target"`下
* 前缀`"profile."`

| 键 | 类型 | 描述 |
| --- | --- | --- |
| `renderDecisions` | 布尔值 | 指示个性化组件是否应解释DOM操作 |
| `decisionScopes` | 数组`<String>` | 要检索决策的作用域列表 |
| `xdm` | 对象 | 以XDM格式显示的数据，作为Web SDK中的体验事件登陆 |
| `data` | 对象 | 发送到target类下[!DNL Target]解决方案的任意键/值对。 |

<!--Typical [!DNL Web SDK] code using this command looks like the following:-->

**延迟保存配置文件或实体参数，直到内容显示给最终用户**

要在显示内容之前延迟在配置文件中记录属性，请在请求中设置`data.adobe.target._save=false`。

例如，您的网站包含三个决策范围，分别对应于网站上的三个类别链接（“男性”、“女性”和“儿童”），并且您希望跟踪用户最终访问的类别。 发送这些请求，并将`__save`标志设置为`false`，以避免在请求内容时保留类别。 内容可视化后，为要记录的相应属性发送适当的负载（包括`eventToken`和`stateToken`）。

以下示例发送trackEvent样式消息，执行配置文件脚本，保存属性，并立即记录事件。

```js
alloy("sendEvent", {
    "renderDecisions": true,
    "xdm": { /* Experience Event XDM data */ },
    "data": {
        "__adobe": {
            "target": {
                " __save": true|false,
                //defaults to true if omitted
                "profile.gender": "female",
                "profile.age": 30,
                "entity.name": "T-shirt",
                "entity.id": "1234"
            }
        }
    }
})
```

>[!NOTE]
>
>如果忽略`__save`指令，将立即保存配置文件和实体属性。 `__save`指令仅与配置文件属性和实体详细信息相关。

## 请求建议

下表列出了[!DNL Recommendations]属性以及是否通过[!DNL Web SDK]支持每个属性：

| 类别 | 属性 | 支持状态 |
| --- | --- | --- |
| 推荐 — 默认实体属性 | entity.id | 受支持 |
|  | entity.name | 受支持 |
|  | entity.categoryId | 受支持 |
|  | entity.pageUrl | 受支持 |
|  | entity.thumbnailUrl | 受支持 |
|  | entity.message | 受支持 |
|  | entity.value | 受支持 |
|  | entity.inventory | 受支持 |
|  | entity.brand | 受支持 |
|  | entity.margin | 受支持 |
|  | entity.event.detailsOnly | 受支持 |
| 推荐 — 自定义实体属性 | entity.yourCustomAttributeName | 受支持 |
| Recommendations — 保留的mbox/页面参数 | excludedIds | 受支持 |
|  | cartIds | 受支持 |
|  | productPurchasedId | 受支持 |
| 类别亲和度的页面或物料类别 | user.categoryId | 受支持 |

**如何将Recommendations属性发送到[!DNL Target]：**

```js
alloy("sendEvent", {
  "renderDecisions": true,
  "data": {
    "__adobe": {
      "target": {
        "entity.id": "123",
        "entity.genre": "Drama"
      }
    }
  }
});
```

## 显示mbox转化量度 {#display-mbox-conversion-metrics}

以下示例显示如何跟踪显示mbox转化并将配置文件参数发送到[!DNL Target]，而无需符合任何内容或活动的条件。

```js
alloy("sendEvent", {
    "xdm": {
        "_experience": {
            "decisioning": {
                "propositions": [{
                    "scope": "conversion-step-1" //example scope name
                }],
                "propositionEventType": {
                    "display": 1
                }
            }
        },
        "eventType": "decisioning.propositionDisplay"
    }
});
```


| 属性 | 描述 |
|---------|----------|
| `xdm._experience.decisioning.propositions[x].scope` | 将成功量度与关联的范围（该范围会将其归因于Target端的特定活动）。 |
| `xdm._experience.decisioning.propositions[x].eventType` | 描述预期事件类型的字符串。 将此用例设置为`"decisioning.propositionDisplay"`。 |

## 调试

已弃用mboxTrace和mboxDebug。 请改用[Web SDK调试](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/web-sdk/use-cases/debugging)的方法。

## 术语

**建议**：在[!DNL Target]中，建议与从活动中选择的体验相关联。

**架构**：决策的架构是[!DNL Target]中的优惠类型。

**范围**：决定的范围。 在[!DNL Target]中，范围是mbox。 全局mbox是`__view__`作用域。

**XDM**： XDM被序列化为点表示法，然后作为mbox参数放入[!DNL Target]中。
