---
keywords: at.js发行版、at.js版本、单页应用程序、spa、跨域、跨域
description: 了解如何从 [!DNL Adobe Target] at.js 1.x升级到at.js 2.x。 检查系统流程图，了解新函数和已弃用的函数等。
title: 如何从at.js版本1.x升级到版本2.x？
feature: at.js
exl-id: fbfa5743-0fa5-44c6-89b3-fdee9b50e126
TQID: https://experienceleague.adobe.com/JGsuogzhCvThr4QGHJ5g4d8ZqGVZ8ClAf7hXuoh7X0Q
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: adee20bd-51f4-461d-b9db-d215f8756eebid: c93393a4-e558-47e1-992e-c91ed4d480ceid: f7c7de77-382f-4f48-8b36-61a170f06d3d
subfeature_v2: id: df62f171-ac37-440f-8f0f-f41a72ebdd34id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: d3cdead0-685a-4489-9250-4bb709942f66id: e0eb8757-182f-49f3-94a4-1587d16f5094id: eddd9b14-83bd-4ff4-9072-54a4a484abb7id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 4d0e7f9f2887db71229061fa64b2633a84c6d054
workflow-type: tm+mt
source-wordcount: 3100
ht-degree: 47%

---

# 从at.js 1.*x*&#x200B;升级到at.js 2.*x*

[!DNL Adobe Target] 中最新版本的 at.js 提供了丰富的功能集，使您的企业能够在下一代客户端技术上实现个性化。 这个新版本着重升级了 at.js 以与单页应用程序 (SPA) 进行良性的交互。

以下是使用at.js 2.*x*&#x200B;的一些好处，这些好处在以前的版本中未提供：

* 能够在页面加载时缓存所有产品建议，将多次服务器调用减少至一次服务器调用。
* 由于产品建议是通过缓存立即显示的，不存在传统服务器调用引入的任何时间延迟，因此极大地提升了最终用户在您网站上的体验。
* 通过简单的单行代码和一次性开发人员设置，您的营销人员能够通过VEC在SPA上创建和运行[!UICONTROL A/B测试]和[!UICONTROL 体验定位] (XT)活动。

## at.js 2.*x*&#x200B;系统图

下图可帮助您了解含有视图的at.js 2.*x*&#x200B;工作流程以及其如何增强SPA集成。 要更好地了解at.js 2.*x*&#x200B;中使用的概念，请参阅[单页应用程序实施](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md)。

（单击图像可展开至全宽。）

![使用at.js 2.x](/help/dev/implement/client-side/assets/system-diagram-atjs-20.png "使用at.js 2.x"){zoomable="yes"}的Target流程

| 调用 | 详细信息 |
| --- | --- |
| 1 | 如果用户通过了身份验证，则调用会返回[!UICONTROL Experience Cloud ID]；另一调用会同步客户ID。 |
| 2 | at.js 库会同步加载，并隐藏文档正文。<P>也可以选择预先隐藏页面上实施的代码段，以异步方式加载at.js。 |
| 3 | 将会发出页面加载请求，其中包括已配置的所有参数（例如，MCID、SDID 和客户 ID）。 |
| 4 | 轮廓脚本在执行后进入轮廓存储区。 存储区向受众库请求符合条件的受众（例如，从[!DNL Adobe Analytics]、[!DNL Audience Manager]等共享的受众）。<P>客户属性会以批量过程发送到配置文件存储区。 |
| 5 | 根据 URL 请求参数和轮廓数据，[!DNL Target] 可决定将哪些活动和体验返回给查看当前页面和未来视图的访客。 |
| 6 | 目标内容会发送回页面，其中可能包含其他个性化的轮廓值。<P>当前页面上的目标内容会在默认内容不发生闪烁的情况下尽快显示。<P>视图中作为用户在SPA中的操作结果而显示的视图的目标内容会缓存在浏览器中，因此当通过`triggerView()`触发视图时，可以立即应用它而无需额外的服务器调用。 |
| 7 | [!UICONTROL Analytics] 数据会发送到数据收集服务器。 |
| 8 | 目标数据通过SDID与[!UICONTROL Analytics]数据匹配，并且已处理到[!UICONTROL Analytics]报表存储中。<P>然后可以通过[!UICONTROL Analytics for Target] (A4T)报表在[!UICONTROL Analytics]和[!DNL Target]中查看[!UICONTROL Analytics]数据。 |

现在，无论在 SPA 上的什么位置实施 `triggerView()`，都会从缓存中检索查看次数和操作，并在没有服务器调用的情况下显示给用户。 `triggerView()` 还会向 [!DNL Target] 后端发出通知请求，以增加和记录展示次数计数。

（单击图像可展开至全宽。）

![Target流程at.js 2.*x* triggerView](/help/dev/implement/client-side/assets/atjs-20-triggerview.png "Target流程at.js 2.*x* triggerView"){zoomable="yes"}

| 调用 | 详细信息 |
| --- | --- |
| 1 | 在 SPA 中调用 `triggerView()` 以渲染视图并应用操作来修改可视化元素。 |
| 2 | 从缓存中读取视图的目标内容。 |
| 3 | 目标内容会在默认内容不发生闪烁的情况下尽快显示。 |
| 4 | 通知请求将发送到 [!DNL Target] 轮廓存储区，以计算活动中的访客和递增量度。 |
| 5 | [!UICONTROL Analytics]数据已发送到数据收集服务器。 |
| 6 | [!DNL Target]数据通过SDID与[!UICONTROL Analytics]数据匹配，并且已处理到[!UICONTROL Analytics]报表存储中。 然后，便可以在[!UICONTROL Analytics]和[!DNL Target]中通过A4T报表查看[!UICONTROL Analytics]数据。 |

## 部署at.js 2.*x*

通过[Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md)扩展中的标记部署at.js 2.*x*。

>[!NOTE]
>
>首选方法是使用[!DNL Adobe Experience Platform]中的标记部署at.js。
>
>或
>
>使用[!DNL Target] UI手动下载at.js 2.*x*，并使用您选择的[方法](/help/dev/implement/client-side/atjs/how-to-deployatjs/how-to-deployatjs.md)进行部署。

## 已弃用的 at.js 函数

at.js 2.*x*&#x200B;中有几个函数已被弃用。

>[!WARNING]
>
>在部署at.js 2.*x*&#x200B;时，如果在您的网站上仍使用这些已弃用的函数，则将会看到控制台警告。 升级时，建议在暂存环境中测试at.js 2.*x*&#x200B;的部署，并确保查看控制台中已记录的每个警告，然后将已弃用的函数转换为at.js 2.*x*&#x200B;中引入的新函数。

您可以在下面找到已弃用的函数及其对应的等效函数。 有关函数的完整列表，请参阅 [at.js 函数](/help/dev/implement/client-side/atjs/atjs-functions/atjs-functions.md)。

>[!NOTE]
>
>at.js 2.*x*&#x200B;不再自动预隐藏`mboxDefault`标记的元素。 因此，客户必须在网站上手动或通过标签管理器容纳预隐藏逻辑。

### mboxCreate(mbox,params)

**描述**：

可使用 `mboxDefault` 类名称执行请求并将产品建议应用到最近的 DIV。

**示例**：

```html {line-numbers="true"}
<div class="mboxDefault">
  default content to replace by offer
</div>
<script>
  mboxCreate('mboxName','param1=value1','param2=value2');
</script>
```

**at.js 2.*x*等效项**

`mboxCreate(mbox, params)` 的替代函数是 `getOffer()` 和 `applyOffer()`。

**示例**：

```html {line-numbers="true"}
<div class="mboxDefault"> 
  default content to replace by offer 
</div> 
<script> 
  var el = document.currentScript.previousElementSibling;
  adobe.target.getOffer({
    mbox: "mboxName",
    params: {
      param1: "value1",
      param2: "value2"
    },
    success: function(offer) {
      adobe.target.applyOffer({
        mbox: "mboxName",
        selector: el,
        offer: offer
      });
    },
    error: function(error) {
      console.error(error);
      el.style.visibility = "visible";
    }
  });
</script> 
```

### mboxDefine() 和 mboxUpdate()

**描述**：

创建元素和 mbox 名称之间的内部映射，但不执行请求。 与 `mboxUpdate()` 结合使用，后者执行请求并将产品建议应用于 `mboxDefine()` 中 nodeId 标识的元素。 也可以用来更新由 `mboxCreate` 发起的 mbox。

**示例**：

```html {line-numbers="true"}
<div id="someId" class="mboxDefault"></div>
<script>
 mboxDefine('someId','mboxName','param1=value1','param2=value2');
 mboxUpdate('mboxName','param3=value3','param4=value4');
</script>
```

**at.js 2.*x*等效项**：

`mboxDefine()` 和 `mboxUpdate` 的替代项是 `getOffer()` 和 `applyOffer()`，`applyOffer()` 中会使用选择器选项。 此方法允许您使用任何 CSS 选择器将产品建议映射到元素，而不仅仅映射到具有 ID 的元素。

**示例**：

```html {line-numbers="true"}
<div id="someId" class="mboxDefault"> 
  default content to replace by offer 
</div> 
<script> 
  adobe.target.getOffer({
    mbox: "mboxName",
    params: {
      param1: "value1",
      param2: "value2",
      param3: "value3",
      param4: "value4" 
    },
    success: function(offer) {
      adobe.target.applyOffer({
        mbox: "mboxName",
        selector: "#someId",
        offer: offer
      });
    },
    error: function(error) {
      console.error(error);
      var el = document.getElementById("someId");
      el.style.visibility = "visible";
    }
  });
</script>
```

### adobe.target.registerExtension()

**描述**：

可提供用于注册特定扩展的标准方法。

此函数不再受支持，不应使用。

## 2.*x*&#x200B;中已弃用、新增和受支持的at.js函数的摘要

| 方法 | 受支持? | 新的? | 已弃用?<P>（将显示默认内容） |
| --- | --- | --- | --- |
| `getOffer()` | 是 |  |  |
| `getOffers()` |  | 是 |  |
| `applyOffer()` | 是 |  |  |
| `applyOffers()` |  | 是 |  |
| `triggerView()` |  | 是 |  |
| `trackEvent()` | 是 |  |  |
| `mboxCreate()` |  |  | 是 |
| `mboxDefine()`<P>`mboxUpdate()` |  |  | 是 |
| `targetGlobalSettings()` | 是 |  |  |
| `Data Providers` | 是 |  |  |
| `targetPageParams()` | 是 |  |  |
| `targetPageParamsAll()` | 是 |  |  |
| `registerExtension()` |  |  | 是 |
| `At.js Custom Events` | 是 |  |  |

## 限制和标注

请注意以下限制和标注：

### 转化跟踪

使用 `mboxCreate()` 进行转化跟踪的客户必须使用 `trackEvent()` 或 `getOffer()`。

### 产品建议交付

未使用 `getOffer()` 或 `applyOffer()` 替换 `mboxCreate()` 的客户可能无法交付产品建议。

### 是否可以在某些页面上使用at.js 2.*x*，而在其他页面上使用at.js 1.*x*？

可以，系统会使用不同版本和库保留各个页面中的访客轮廓。 Cookie 格式是相同的。

### at.js 2.*x*&#x200B;中使用的新API

at.js 2.*x*&#x200B;使用新的API，我们称之为“交付API”。 为了调试at.js是否正确调用[!DNL Target]边缘服务器，您可以将浏览器开发人员工具的“网络”选项卡过滤到“交付”、“`tt.omtrdc.net`”或您的客户端代码。 您还会注意到 [!DNL Target] 发送的是 JSON 有效负载而不是键值对。

### 不再使用[!DNL Target]全局Mbox

在at.js 2.*x*&#x200B;中，您不会再在网络调用中看到“`target-global-mbox`”。 我们已在发送到[!DNL Target]服务器的JSON有效负载中将&quot;`target-global-mbox`&quot;语法替换为&quot;`execute > pageLoad`&quot;，如下所示：

```json {line-numbers="true"}
{
  "id": {
    // ...
  },
  "context": {
    "channel": "web",
    // ...
  },
  "execute": {
    "pageLoad": {}
  }
}
```

本质上讲，我们引入全局 mbox 概念是为了告知 [!DNL Target] 在页面加载时是否要检索产品建议和内容。 因此，我们在最新版本中更加明确了此概念。

### at.js 中的全局 mbox 名称是否无关紧要？

客户可以通过&#x200B;**[!UICONTROL Target]** > **[!UICONTROL 管理]** > **[!UICONTROL 实施]** > **[!UICONTROL 编辑at.js设置]**&#x200B;来指定全局mbox名称。 [!DNL Target] 边缘服务器使用此设置来将 execute > pageLoad 转换为 [!DNL Target] UI 中显示的全局 mbox 名称。 这允许客户继续使用服务器端 API、基于表单的编辑器、轮廓脚本，并使用全局 mbox 名称创建受众。 我们强烈建议您还确保在&#x200B;**[!UICONTROL 管理]** > **[!UICONTROL 可视化体验编辑器]**&#x200B;页面上配置相同的全局mbox名称，以防仍有使用at.js 1.*x*&#x200B;的页面，如下图所示。

![修改 at.js 对话框](../assets/modify-atjs.png)

和

![自定义全局 mbox](../assets/custom-global-mbox.png)

### 是否需要为at.js 2.*x*&#x200B;打开自动创建全局mbox设置？

在大多数情况下需要。 此设置会告知at.js 2.*x*&#x200B;在页面加载时向[!DNL Target]边缘服务器触发请求。 由于全局 mbox 被转换为 execute > pageLoad，因此如果要在页面加载时触发请求，则应该启用此设置。

### 即使未从at.js 2.*x*&#x200B;中指定Target全局mbox名称，现有的VEC活动是否仍会继续工作？

会，因为系统会在如 `target-global-mbox` 的 [!DNL Target] 后端处理 execute > pageLoad。

### 如果将我的基于表单的活动定位到 `target-global-mbox`，那么这些活动是否会继续工作？

会，因为和 `target-global-mbox` 一样，系统会在 [!DNL Target] 边缘服务器上处理 execute > pageLoad。

### 受支持和不受支持的at.js 2.*x*&#x200B;设置

| 设置 | 受支持? |
| --- | --- |
| X-Domain | 否 |
| 自动创建全局 Mbox | 是 |
| 全局 Mbox 名称 | 是 |

### at.js 2.x中的跨域跟踪支持

跨域跟踪可拼合跨不同域的访客。 因为必须为每个域创建新 Cookie，所以当访客在不同域之间导航时很难进行跟踪。 要实现跨域跟踪，[!DNL Target] 会使用第三方 Cookie 来跟踪跨域访客。 这允许您创建跨越`siteA.com`和`siteB.com`的[!DNL Target]活动，并且访客在独特域之间导航时保持相同的体验。 此功能与[!DNL Target]的第三方和第一方Cookie行为相关联。

>[!NOTE]
>
>自at.js 2.10起，支持跨域跟踪，但在2.10之前的at.js 2.*x*&#x200B;中不支持开箱即用跟踪。 at.js 2.*x*&#x200B;中通过Experience Cloud ID (ECID)库v4.3.0+支持跨域跟踪。

在[!DNL Target]中，第三方Cookie存储在`<CLIENTCODE>.tt.omtrdc.net`中。 第一方 Cookie 存储在 `clientdomain.com` 中。 第一个请求会返回尝试设置名为 `mboxSession` 和 `mboxPC` 的第三方 Cookie 的 HTTP 响应标头，而会使用额外的参数 (`mboxXDomainCheck=true`) 发送回重定向请求。 如果浏览器接受第三方 Cookie，则该重定向请求将包含这些 Cookie，并且会返回体验。 这个工作流程是可行的，因为我们使用的是 HTTP GET 方法。

但是，在at.js 2.*x*&#x200B;中，未使用HTTP GET。 而是通过at.js 2.*x*&#x200B;使用HTTP POST将JSON有效负载发送到[!DNL Target]个Edge服务器。 使用HTTP POST意味着用于检查浏览器是否支持第三方Cookie的重定向请求将中断。 这是因为 HTTP GET 请求是幂等事务，而 HTTP POST 是非幂等事务，不能任意重复。 因此，at.js 2.*x*（2.10之前的版本）中的跨域跟踪不受开箱即用支持。 只有at.js 1.*x*&#x200B;才对跨域跟踪提供开箱即用支持。

要对at.js v2.10或更高版本使用跨域跟踪，您可以执行以下任一操作：

1. 安装[ECID库v4.3.0+](https://experienceleague.adobe.com/docs/id-service/using/release-notes/release-notes.html?lang=zh-Hans)和at.js 2.*x*。 ECID 库可以管理用于跨域识别访客的永久 ID。 安装ECID库v4.3.0+和at.js 2.*x*&#x200B;后，您将能够创建跨独特域的活动并跟踪用户。 需要注意的是，此功能仅在会话过期后才能正常工作。

1. 如果您有at.js v2.10或更高版本，则不必安装ECID库，而是可以在&#x200B;**[!UICONTROL 管理]** > **[!UICONTROL 实施]**&#x200B;的[!DNL Target] UI中启用跨域设置。 （或者，您可以在at.js代码中将&#x200B;_crossDomain_&#x200B;选项设置为&#x200B;_enabled_。）

要对2.10之前的at.js v2.*x*&#x200B;版本使用跨域跟踪，您可以实施上面的选项#1（安装ECID库）。

### 支持自动创建全局 Mbox

此设置会告知at.js 2.*x*&#x200B;在页面加载时向[!DNL Target]边缘服务器触发请求。 由于全局 mbox 已转换为 execute > pageLoad，并且这由 [!DNL Target] 边缘服务器来解释，所以如果客户想要在页面加载时触发请求，则应该打开此设置。

### 支持全局 Mbox 名称

客户可以通过&#x200B;**[!UICONTROL Target]** > **[!UICONTROL 管理]** > **[!UICONTROL 实施]** > **[!UICONTROL 编辑]**&#x200B;来指定全局mbox名称。 [!DNL Target] 边缘服务器使用此设置来将 execute > pageLoad 转换为输入的全局 mbox 名称。 这允许客户继续使用服务器端 API、基于表单的编辑器、轮廓脚本，并创建针对全局 mbox 的受众。

### 以下 at.js 自定义事件是否适用于 `triggerView()`，还是仅适用于 `applyOffer()` 或 `applyOffers()`？

* `adobe.target.event.CONTENT_RENDERING_FAILED`
* `adobe.target.event.CONTENT_RENDERING_SUCCEEDED`
* `adobe.target.event.CONTENT_RENDERING_NO_OFFERS`
* `adobe.target.event.CONTENT_RENDERING_REDIRECT`

是，at.js 自定义事件也适用于 `triggerView()`。

### 它说当我使用&amp;lbrace；`"page" : "true"`&amp;rbrace；调用`triggerView()`时，它将向[!DNL Target]后端发送通知并增加展示次数。 它是否还会导致系统执行轮廓脚本？

当对 [!DNL Target] 后端进行预取调用时，将会执行轮廓脚本。 此后，受影响的轮廓数据将被加密并传递回客户端。 在调用使用 `{"page": "true"}` 的 `triggerView()` 后，将会发送通知以及加密的轮廓数据。 之后，[!DNL Target] 后端将解密轮廓数据并将其存储到数据库中。

### 我们是否需要在调用 `triggerView()` 之前添加预隐藏代码以避免闪烁？

不需要，在调用 `triggerView()` 之前，您不需要添加预隐藏代码。 at.js 2.*x*&#x200B;会在显示和应用视图之前管理预隐藏和闪烁逻辑。

### at.js 2.*x*&#x200B;不支持哪些用于创建受众的at.js 1.*x*&#x200B;参数？

使用at.js 2.*x*&#x200B;时，以下at.js 1.x参数当前不支持创建受众&#x200B;*NOT*：

* browserHeight
* browserWidth
* browserTimeOffset
* screenHeight
* screenWidth
* screenOrientation
* colorDepth
* devicePixelRatio
* vst.*参数（见下文）

### at.js 2.*x*&#x200B;不支持使用vst.*参数创建受众

at.js 1.*x*&#x200B;上的客户可以使用vst.* mbox参数创建受众。 这是at.js 1.*x*&#x200B;如何将mbox参数发送到[!DNL Target]后端的一个意外副作用。 迁移到at.js 2.*x*&#x200B;后，您将无法再使用这些参数创建受众，因为at.js 2.*x*&#x200B;发送mbox参数的方式有所不同。

## at.js 兼容性

以下表格介绍了 at.js. 2.*x*&#x200B;与不同活动类型、集成、功能和at.js函数的兼容性。

### 活动类型

| 类型 | 受支持? |
| --- | --- |
| [!UICONTROL A/B 测试] | 是 |
| [!UICONTROL 自动分配] | 是 |
| [!UICONTROL Auto-Target（自动定位）] | 是 |
| [!UICONTROL 体验定位] | 是 |
| [!UICONTROL 多变量测试] | 是 |
| [!UICONTROL 自动个性化] | 是 |
| [!DNL Recommendations] | 是 |

>[!NOTE]
>
>当所有修改都应用于`Page Load Event`时，将通过at.js 2.*x*&#x200B;和VEC支持[!UICONTROL 自动定位]活动。 将修改添加到特定视图时，仅支持[!UICONTROL A/B测试]、[!UICONTROL 自动分配]和[!UICONTROL 体验定位] (XT)活动。

### 集成

| 类型 | 受支持? |
| --- | --- |
| [!UICONTROL Analytics for Target] (A4T) | 是 |
| 受众 | 是 |
| 客户属性 | 是 |
| AEM 体验片段 | 是 |
| [Adobe Experience Platform扩展](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) | 是 |
| 调试程序 | 是 |
| 审核 | at.js 2.*x*&#x200B;尚未更新规则 |
| 对[GDPR](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md)的选择加入支持 | [at.js版本2.1.0](/help/dev/implement/client-side/atjs/target-atjs-versions.md#atjs-version-210-june-3-2019)或更高版本支持此功能。 |
| 由[!DNL Adobe Target]提供支持的AEM增强Personalization | 否 |

### 功能

| 功能 | 受支持? |
| --- | --- |
| X-Domain | 否 |
| 属性/工作区 | 是 |
| QA 链接 | 是 |
| 基于表单的体验编辑器 | 是 |
| 可视化体验编辑器 (VEC) | 是 |
| 自定义代码 | 是 |
| [响应令牌](#response-tokens) | 是 |
| 点击跟踪 | 是 |
| 多活动交付 | 是 |
| targetGlobalSettings | 是（但不支持 x 域） |
| at.js 方法 | 除以下各项外，其他所有方法均受支持<P>`mboxCreate()`<P>`mboxUpdate()`<P>`mboxDefine()`<P>将显示默认内容。 |

### 查询字符串参数

| 参数 | 受支持? |
| --- | --- |
| `?mboxDisable` | 是 |
| `?mboxDisable` | 是 |
| `?mboxTrace` | 是 |
| `?mboxSession` | 否 |
| `?mboxOverride.browserIp` | 是 |

## 响应令牌

at.js 2.*x*&#x200B;与at.js 1.*x*&#x200B;一样，使用自定义事件`at-request-succeeded`来显示响应令牌。 有关使用 `at-request-succeeded` 自定义事件的代码示例，请参阅[响应令牌](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html)。

## at.js 1.*x*&#x200B;参数到at.js 2.*x*&#x200B;有效负载的映射

本节概述了at.js 1.*x*&#x200B;和at.js 2.*x*&#x200B;之间的映射。

在深入研究参数映射之前，这些库版本当前使用的端点已发生更改：

* at.js 1.*x* - `http://<client code>.tt.omtrdc.net/m2/<client code>/mbox/json`
* at.js 2.*x* - `http://<client code>.tt.omtrdc.net/rest/v1/delivery`

另一个重要区别是：

* at.js 1.*x* — 客户端代码是路径的一部分
* at.js 2.*x* — 客户端代码将作为查询字符串参数发送，例如：
  `http://<client code>.tt.omtrdc.net/rest/v1/delivery?client=democlient`

以下部分列出了每个at.js 1.*x*&#x200B;参数、其描述以及相应的2.*x* JSON有效负载（如果适用）：

### at_property

（at.js 1.*x*&#x200B;参数）

用于[企业用户权限](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=zh-Hans)。

```json {line-numbers="true"}
{
  ....
  "property": {
    "token": "1213213123122313121"
  }
  ....
}
```

### mboxHost

（at.js 1.*x*&#x200B;参数）

运行[!DNL Target]库的页面的域。

at.js 2.*x* JSON有效负载：

```json {line-numbers="true"}
{
  "context": {
    "browser": {
       "host": "test.com"
    }
  }
}
```

### webGLRenderer

（at.js 1.*x*&#x200B;参数）

浏览器的 WEB GL 渲染器功能。 我们的设备检测机制使用此参数来确定访客的设备是桌面设备、iPhone、Android 设备，还是其他设备。

at.js 2.*x* JSON有效负载：

```json {line-numbers="true"}
{
  "context": {
    "browser": {
       "webGLRenderer": "AMD Radeon Pro 560X OpenGL Engine"
    }
  }
}
```

### mboxURL

（at.js 1.*x*&#x200B;参数）

页面 URL。

at.js 2.*x* JSON有效负载：

```json {line-numbers="true"}
{
  "context": {
    "address": {
       "url": "http://test.com"
    }
  }
}
```

### mboxReferrer

（at.js 1.*x*&#x200B;参数）

页面反向链接。

at.js 2.*x* JSON有效负载：

```json {line-numbers="true"}
{
  "context": {
    "address": {
       "referringUrl": "http://google.com"
    }
  }
}
```

### mbox（名称）等于全局 mbox

（at.js 1.*x*&#x200B;参数）

交付 API 不再具有全局 mbox 概念。 在 JSON 有效负载中，您必须使用 `execute > pageLoad`。

at.js 2.*x* JSON有效负载：

```json {line-numbers="true"}
{
  "execute": {
    "pageLoad": {
       "parameters": ....
       "profileParameters": ...
       .....
    }
  }
}
```

### mbox（名称）*不*&#x200B;等于全局 mbox

（at.js 1.*x*&#x200B;参数）

要使用 mbox 名称，请将其传递到 `execute > mboxes`。 mbox 需要索引和名称。

at.js 2.*x* JSON有效负载：

```json {line-numbers="true"}
{
  "execute": {
    "mboxes": [{
       "index": 0,
       "name": "some-mbox",
       "parameters": ....
       "profileParameters": ...
       .....
    }]
  }
}
```

### mboxId

（at.js 1.*x*&#x200B;参数）

已不再使用。

### mboxCount

（at.js 1.*x*&#x200B;参数）

已不再使用。

### mboxRid

（at.js 1.*x*&#x200B;参数）

下游系统用来帮助进行调试的请求 ID。

at.js 2.*x* JSON有效负载：

```json {line-numbers="true"}
{
  "requestId": "2412234442342"
  ....
}
```

### mboxTime

（at.js 1.*x*&#x200B;参数）

已不再使用。

### mboxSession

（at.js 1.*x*&#x200B;参数）

会话 ID 作为查询字符串参数 (`sessionId`) 发送到交付 API 端点。

### mboxPC

（at.js 1.*x*&#x200B;参数）

TNT ID 被传递到 `id > tntId`。

at.js 2.*x* JSON有效负载：

```json {line-numbers="true"}
{
  "id": {
    "tntId": "ca5ddd7e33504c58b70d45d0368bcc70.21_3"
  }
  ....
}
```

### mboxMCGVID

（at.js 1.*x*&#x200B;参数）

Marketing Cloud 访客 ID 被传递到 `id > marketingCloudVisitorId`。

at.js 2.*x* JSON有效负载：

```json {line-numbers="true"}
{
  "id": {
    "marketingCloudVisitorId": "797110122341429343505"
  }
  ....
}
```

### `vst.aaaa.id` 和 `vst.aaaa.authState`

（at.js 1.*x*&#x200B;参数）

客户 ID 应被传递到 `id > customerIds`。

at.js 2.*x* JSON有效负载：

```json {line-numbers="true"}
{
  "id": {
    "customerIds": [{
       "id": "1232131",
       "integrationCode": "aaaa",
       "authenticatedState": "....."
     }]
  }
  ....
}
```

### mbox3rdPartyId

（at.js 1.*x*&#x200B;参数）

用于链接不同[!DNL Target] ID的客户第三方ID。

at.js 2.*x* JSON有效负载：

```json {line-numbers="true"}
{
  "id": {
    "thirdPartyId": "1232312323123"
  }
  ....
}
```

### mboxMCSDID

（at.js 1.*x*&#x200B;参数）

SDID，也称为补充数据 ID。 应被传递到 `experienceCloud > analytics > supplementalDataId`。

at.js 2.*x* JSON有效负载：

```json {line-numbers="true"}
{
  "experienceCloud": {
    "analytics": {
      "supplementalDataId": "1212321132123131"
    }
  }
  ....
}
```

### vst.trk

（at.js 1.*x*&#x200B;参数）

[!UICONTROL Analytics]跟踪服务器。 应被传递到 `experienceCloud > analytics > trackingServer`。

at.js 2.*x* JSON有效负载：

```json {line-numbers="true"}
{
  "experienceCloud": {
    "analytics": {
      "trackingServer": "analytics.test.com"
    }
  }
  ....
}
```

### vst.trks

（at.js 1.*x*&#x200B;参数）

Analytics 跟踪服务器的安全性。 应被传递到 `experienceCloud > analytics > trackingServerSecure`。

at.js 2.*x* JSON有效负载：

```json {line-numbers="true"}
{
  "experienceCloud": {
    "analytics": {
      "trackingServerSecure": "secure-analytics.test.com"
    }
  }
  ....
}
```

### mboxMCGLH

（at.js 1.*x*&#x200B;参数）

Audience Manager 位置提示。 应被传递到 `experienceCloud > audienceManager > locationHint`。

at.js 2.*x* JSON有效负载：

```json {line-numbers="true"}
{
  "experienceCloud": {
    "audienceManager": {
      "locationHint": 9
    }
  }
  ....
}
```

### mboxAAMB

（at.js 1.*x*&#x200B;参数）

Audience Manager Blob。 应被传递到 `experienceCloud > audienceManager > blob`。

at.js 2.*x* JSON有效负载：

```json {line-numbers="true"}
{
  "experienceCloud": {
    "audienceManager": {
      "blob": "2142342343242342"
    }
  }
  ....
}
```

### mboxVersion

（at.js 1.*x*&#x200B;参数）

版本将通过 version 参数作为查询字符串参数发送。

## 培训视频： at.js 2.*x*&#x200B;架构图![概述徽章](../../assets/overview.png)

at.js 2.*x*&#x200B;增强了Adobe [!DNL Target]对SPA的支持，并与其他Experience Cloud解决方案集成。 该视频介绍了如何将所有内容结合到一起。

>[!VIDEO](https://video.tv.adobe.com/v/26250/?quality=12)

有关详细信息，请参阅[了解at.js 2.*x*&#x200B;的工作方式](https://experienceleague.adobe.com/docs/target-learn/tutorials/implementation/understanding-how-atjs-20-works.html)。
