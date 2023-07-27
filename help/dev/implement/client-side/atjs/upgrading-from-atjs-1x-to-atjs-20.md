---
keywords: at.js发行版、at.js版本、单页应用程序、spa、跨域、跨域
description: 了解如何从升级 [!DNL Adobe Target] at.js 1.x到at.js 2.x。检查系统流程图，了解新函数和已弃用的函数等。
title: 如何从at.js版本1.x升级到版本2.x？
feature: at.js
exl-id: fbfa5743-0fa5-44c6-89b3-fdee9b50e126
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '2925'
ht-degree: 73%

---

# 从 at.js 1.*x* 升级到 at.js 2.*x*

[!DNL Adobe Target] 中最新版本的 at.js 提供了丰富的功能集，使您的企业能够在下一代客户端技术上实现个性化。这个新版本着重升级了 at.js 以与单页应用程序 (SPA) 进行良性的交互。

以下是使用 at.js 2.*x* 的一些好处，这些好处在以前的版本中未提供：

* 能够在页面加载时缓存所有选件，将多次服务器调用减少至一次服务器调用。
* 由于选件是通过缓存立即显示的，不存在传统服务器调用引入的任何时间延迟，因此极大地提升了最终用户在您网站上的体验。
* 通过简单的单行代码和一次性开发人员设置，您的营销人员可以创建和运行 [!UICONTROL A/B测试] 和 [!UICONTROL 体验定位] (XT)通过SPA上的VEC进行的活动。

## at.js 2.*x* 系统图

下图可帮助您了解含有视图的 at.js 2.*x* 工作流程以及其如何增强 SPA 集成。要更好地了解 at.js 2.*x* 中使用的概念，请参阅[单页应用程序实施](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md)。

（单击图像可展开至全宽。）

![使用at.js 2.x的Target流程](/help/dev/implement/client-side/assets/system-diagram-atjs-20.png "使用at.js 2.x的Target流程"){zoomable=&quot;yes&quot;}

| 调用 | 详细信息 |
| --- | --- |
| 1 | 调用返回 [!UICONTROL EXPERIENCE CLOUDID] 如果用户通过了身份验证；另一调用会同步客户ID。 |
| 2 | at.js 库会同步加载，并隐藏文档正文。<P>也可以选择预先隐藏页面上实施的代码段，以异步方式加载 at.js。 |
| 3 | 将会发出页面加载请求，其中包括已配置的所有参数（例如，MCID、SDID 和客户 ID）。 |
| 4 | 配置文件脚本在执行后进入配置文件存储区。存储区向受众库请求符合条件的受众（例如从 [!DNL Adobe Analytics]、[!DNL Audience Manager] 等共享的受众）。<P>客户属性会以批量过程发送到配置文件存储区。 |
| 5 | 根据 URL 请求参数和配置文件数据，[!DNL Target] 可决定将哪些活动和体验返回给查看当前页面和未来视图的访客。 |
| 6 | 目标内容会发送回页面，其中可能包含其他个性化的配置文件值。<P>当前页面上的目标内容会在默认内容不发生闪烁的情况下尽快显示。<P>视图中作为 SPA 用户操作结果显示的目标内容会缓存在浏览器中，因此当通过 `triggerView()` 触发视图时，可以立即应用它而无需额外的服务器调用。 |
| 7 | [!UICONTROL Analytics 数据会发送到数据收集服务器。] |
| 8 | 目标数据与 [!UICONTROL 分析] 数据通过SDID并处理到 [!UICONTROL 分析] 报告存储。<P>之后，便可以在 [!UICONTROL Analytics] 和 [!UICONTROL  中通过 ]Analytics for Target[!DNL Target] (A4T) 报表查看 [!UICONTROL Analytics] 数据。 |

现在，无论在 SPA 上的什么位置实施 `triggerView()`，都会从缓存中检索查看次数和操作，并在没有服务器调用的情况下显示给用户。`triggerView()` 还会向 [!DNL Target] 后端发出通知请求，以增加和记录展示次数计数。

（单击图像可展开至全宽。）

![Target流程at.js 2.*x* triggerView](/help/dev/implement/client-side/assets/atjs-20-triggerview.png "Target流程at.js 2.*x* triggerView"){zoomable=&quot;yes&quot;}

| 调用 | 详细信息 |
| --- | --- |
| 1 | 在 SPA 中调用 `triggerView()` 以渲染视图并应用操作来修改可视化元素。 |
| 2 | 从缓存中读取视图的目标内容。 |
| 3 | 目标内容会在默认内容不发生闪烁的情况下尽快显示。 |
| 4 | 通知请求将发送到 [!DNL Target] 配置文件存储区，以计算活动中的访客和递增量度。 |
| 5 | [!UICONTROL Analytics 数据会发送到数据收集服务器。] |
| 6 | [!DNL Target] 数据会通过 SDID 匹配到 Analytics 数据，并且会进行相应处理以保存到 Analytics 报表存储中。[!UICONTROL 之后，便可以在 Analytics 和 中通过 A4T 报表查看 Analytics 数据。][!DNL Target] |

## 部署 at.js 2.*x*

部署 at.js 2.*x* 通过中的标记 [Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) 扩展。

>[!NOTE]
>
>使用中的标记部署at.js [!DNL Adobe Experience Platform] 是首选方法。
>
>或
>
>手动下载at.js 2.*x* 使用 [!DNL Target] UI并使用 [您选择的方法](/help/dev/implement/client-side/atjs/how-to-deployatjs/how-to-deployatjs.md).

## 已弃用的 at.js 函数

at.js 2.*x* 中有几个函数已被弃用。

>[!WARNING]
>
>在部署 at.js 2.*x* 时，如果在您的网站上仍使用这些已弃用的函数，则将会看到控制台警告。升级时，建议在测试环境中测试 at.js 2.*x* 的部署，并确保查看控制台中已记录的每个警告，然后将已弃用的函数转换为 at.js 2.*x* 中引入的新函数。

您可以在下面找到已弃用的函数及其对应的等效函数。有关函数的完整列表，请参阅 [at.js 函数](/help/dev/implement/client-side/atjs/atjs-functions/atjs-functions.md)。

>[!NOTE]
>
>at.js 2.*x* 不再自动预隐藏 `mboxDefault` 标记的元素。因此，客户必须在网站上手动或通过标签管理器容纳预隐藏逻辑。

### mboxCreate(mbox,params)

**描述**：

可使用 `mboxDefault` 类名称执行请求并将选件应用到最近的 DIV。

**示例**：

```html {line-numbers="true"}
<div class="mboxDefault">
  default content to replace by offer
</div>
<script>
  mboxCreate('mboxName','param1=value1','param2=value2');
</script>
```

**at.js 2.*x* 等效项**

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

创建元素和 mbox 名称之间的内部映射，但不执行请求。与 `mboxUpdate()` 结合使用，后者执行请求并将选件应用于 `mboxDefine()` 中 nodeId 标识的元素。也可以用来更新由 `mboxCreate` 发起的 mbox。

**示例**：

```html {line-numbers="true"}
<div id="someId" class="mboxDefault"></div>
<script>
 mboxDefine('someId','mboxName','param1=value1','param2=value2');
 mboxUpdate('mboxName','param3=value3','param4=value4');
</script>
```

**at.js 2.*x* 等效项**：

`mboxDefine()` 和 `mboxUpdate` 的替代项是 `getOffer()` 和 `applyOffer()`，`applyOffer()` 中会使用选择器选项。此方法允许您使用任何 CSS 选择器将选件映射到元素，而不仅仅映射到具有 ID 的元素。

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

## at.js 2 中已弃用、新增和受支持的函数的摘要.*x*

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

### 选件交付

未使用 `getOffer()` 或 `applyOffer()` 替换 `mboxCreate()` 的客户可能无法交付选件。

### 是否可以在某些页面上使用 at.js 2.*x*，而在其他页面上使用 at.js 1.*x* 是否在其他页面上？

可以，系统会使用不同版本和库保留各个页面中的访客配置文件。Cookie 格式是相同的。

### at.js 2.*x* 中使用的新 API

at.js 2.*x* 使用一个新的 API，我们称之为“交付 API”。为了调试at.js是否正在调用 [!DNL Target] edge server正确，您可以将浏览器开发人员工具的“网络”选项卡过滤到“交付”， “`tt.omtrdc.net`，”或您的客户端代码。 您还会注意到 [!DNL Target] 发送的是 JSON 有效负载而不是键值对。

### [!DNL Target]不再使用 全局 Mbox

在 at.js 2.*x*，您不会再看到“`target-global-mbox`”在网络调用中可见。 我们已改为使用“`target-global-mbox`“ ”的语法`execute > pageLoad`”在发送到的JSON有效负载中 [!DNL Target] 服务器，如下所示：

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

本质上讲，我们引入全局 mbox 概念是为了告知 [!DNL Target] 在页面加载时是否要检索选件和内容。因此，我们在最新版本中更加明确了此概念。

### at.js 中的全局 mbox 名称是否无关紧要？

客户可以通过以下方式指定全局mbox名称： **[!UICONTROL Target]** > **[!UICONTROL 管理]** > **[!UICONTROL 实现]** > **[!UICONTROL 编辑at.js设置]**. [!DNL Target] 边缘服务器使用此设置来将 execute > pageLoad 转换为 [!DNL Target] UI 中显示的全局 mbox 名称。这允许客户继续使用服务器端 API、基于表单的编辑器、配置文件脚本，并使用全局 mbox 名称创建受众。我们强烈建议您还确保在上配置了相同的全局mbox名称， **[!UICONTROL 管理]** > **[!UICONTROL 可视化体验编辑器]** 页面，以防仍有使用at.js 1.*x*，如下图所示。

![修改 at.js 对话框](../assets/modify-atjs.png)

和

![自定义全局 mbox](../assets/custom-global-mbox.png)

### 是否需要为 at.js 2.*x* 打开自动创建全局 mbox 设置？

在大多数情况下需要。此设置会告知 at.js 2.*x* 在页面加载时向 [!DNL Target] 边缘服务器发出请求。由于全局 mbox 被转换为 execute > pageLoad，因此如果要在页面加载时触发请求，则应该启用此设置。

### 即使未从 at.js 2.*x* 中指定 Target 全局 mbox 名称，现有的 VEC 活动是否仍会继续工作？

会，因为系统会在如 `target-global-mbox` 的 [!DNL Target] 后端处理 execute > pageLoad。

### 如果将我的基于表单的活动定位到 `target-global-mbox`，那么这些活动是否会继续工作？

会，因为和 `target-global-mbox` 一样，系统会在 [!DNL Target] 边缘服务器上处理 execute > pageLoad。

### 受支持和不受支持的 at.js 2.*x* 设置

| 设置 | 受支持? |
| --- | --- |
| X-Domain | 否 |
| 自动创建全局 Mbox | 是 |
| 全局 Mbox 名称 | 是 |

### at.js 2.x 中的跨域跟踪支持

跨域跟踪可拼合跨不同域的访客。因为必须为每个域创建新 Cookie，所以当访客在不同域之间导航时很难进行跟踪。要实现跨域跟踪，[!DNL Target] 会使用第三方 Cookie 来跟踪跨域访客。这允许您创建 [!DNL Target] 跨越的活动 `siteA.com` 和 `siteB.com` 和访客在独特域之间导航时保持相同的体验。 此功能将绑定到 [!DNL Target]的第三方和第一方Cookie行为。

>[!NOTE]
>
>自at.js 2.10起，支持跨域跟踪，但在at.js 2.*x* 2.10之前。at.js 2.*x* 通过 Experience Cloud ID (ECID) 库 v4.3.0+ 支持跨域跟踪。

在 [!DNL Target]，第三方Cookie存储在中 `<CLIENTCODE>.tt.omtrdc.net`.第一方Cookie存储在中 `clientdomain.com`. 第一个请求会返回尝试设置名为 `mboxSession` 和 `mboxPC` 的第三方 Cookie 的 HTTP 响应标头，而会使用额外的参数 (`mboxXDomainCheck=true`) 发送回重定向请求。如果浏览器接受第三方 Cookie，则该重定向请求将包含这些 Cookie，并且会返回体验。这个工作流程是可行的，因为我们使用的是 HTTP GET 方法。

但是，在at.js 2.*x*，未使用HTTPGET。 POST而是通过at.js 2.*x*[!DNL Target] 来使用 HTTP POST 将 JSON 有效负载发送到 边缘服务器。使用HTTPPOST意味着用于检查浏览器是否支持第三方Cookie的重定向请求将中断。 这是因为 HTTP GET 请求是幂等事务，而 HTTP POST 是非幂等事务，不能任意重复。因此，不再对 at.js 2.*x* （低于2.10）不支持开箱即用。 只有 at.js 1.*x* 对跨域跟踪功能提供开箱即用支持。

要对at.js v2.10或更高版本使用跨域跟踪，您可以执行以下任一操作：

1. 安装 [ECID库v4.3.0+](https://experienceleague.adobe.com/docs/id-service/using/release-notes/release-notes.html?lang=zh-Hans) 与at.js 2.*x*。ECID 库可以管理用于跨域识别访客的永久 ID。安装 ECID 库 v4.3.0+ 和 at.js 2.*x* 之后，您将能够创建跨越独特域的活动并跟踪用户。需要注意的是，此功能仅在会话过期后才能正常工作。

1. 如果您有at.js v2.10或更高版本，则可以在中启用跨域设置，而不是安装ECID库。 [!DNL Target] 中的UI **[!UICONTROL 管理]** > **[!UICONTROL 实现]**. (或者，您可以设置 _crossdomain_ 选项至 _已启用_ （在at.js代码中。）

对at.js v2的版本使用跨域跟踪。*x* 在2.10之前，您可以实施以上选项#1（安装ECID库）。

### 支持自动创建全局 Mbox

此设置会告知 at.js 2.*x* 在页面加载时向 [!DNL Target] 边缘服务器发出请求。由于全局 mbox 已转换为 execute > pageLoad，并且这由 [!DNL Target] 边缘服务器来解释，所以如果客户想要在页面加载时触发请求，则应该打开此设置。

### 支持全局 Mbox 名称

客户可以通过以下方式指定全局mbox名称： **[!UICONTROL Target]** > **[!UICONTROL 管理]** > **[!UICONTROL 实现]** > **[!UICONTROL 编辑]**. [!DNL Target] 边缘服务器使用此设置来将 execute > pageLoad 转换为输入的全局 mbox 名称。这允许客户继续使用服务器端 API、基于表单的编辑器、配置文件脚本，并创建针对全局 mbox 的受众。

### 以下 at.js 自定义事件是否适用于 `triggerView()`，还是仅适用于 `applyOffer()` 或 `applyOffers()`？

* `adobe.target.event.CONTENT_RENDERING_FAILED`
* `adobe.target.event.CONTENT_RENDERING_SUCCEEDED`
* `adobe.target.event.CONTENT_RENDERING_NO_OFFERS`
* `adobe.target.event.CONTENT_RENDERING_REDIRECT`

是，at.js 自定义事件也适用于 `triggerView()`。

### 上面写着，当我打电话时 `triggerView()` 带大括号(&amp;L)`"page" : "true"`&amp;rbrace；，它将向 [!DNL Target] 后端并增加展示次数。 它是否还会导致系统执行配置文件脚本？

当对 [!DNL Target] 后端进行预取调用时，将会执行配置文件脚本。此后，受影响的配置文件数据将被加密并传递回客户端。在调用使用 `{"page": "true"}` 的 `triggerView()` 后，将会发送通知以及加密的配置文件数据。之后，[!DNL Target] 后端将解密配置文件数据并将其存储到数据库中。

### 我们是否需要在调用 `triggerView()` 之前添加预隐藏代码以避免闪烁？

不需要，在调用 `triggerView()` 之前，您不需要添加预隐藏代码。at.js 2.*x* 会在显示和应用视图之前管理预隐藏和闪烁逻辑。

### 哪个at.js 1.*x* at.js 2.*x* 的 SPA 中），会出现什么情况？

以下at.js 1.x参数为 *NOT* 在使用at.js 2.*x* 中的 Target 流程 - 页面加载请求：

* browserHeight
* browserWidth
* browserTimeOffset
* screenHeight
* screenWidth
* screenOrientation
* colorDepth
* devicePixelRatio
* vst.*参数（见下文）

### at.js 2.*x* 不支持使用 vst.*参数

at.js 1.*x* 能够使用vst。* mbox参数以创建受众。 这是at.js 1.*x* 已将mbox参数发送到 [!DNL Target] 后端。 迁移到at.js 2.*x*&#x200B;中，您无法再使用这些参数创建受众，因为at.js 2.*x* 以不同的方式发送mbox参数。

## at.js 兼容性

以下表格介绍了 at.js. 2.*x* 兼容不同的活动类型、集成、功能和at.js函数。

### 活动类型

| 类型 | 受支持? |
| --- | --- |
| [!UICONTROL A/B 测试] | 是 |
| [!UICONTROL 自动分配] | 是 |
| [!UICONTROL 自动定位] | 是 |
| [!UICONTROL 体验定位] | 是 |
| [!UICONTROL 多变量测试] | 是 |
| [!UICONTROL Automated Personalization] | 是 |
| [!DNL Recommendations] | 是 |

>[!NOTE]
>
>[!UICONTROL 自动定位] 通过at.js 2.*x* 和VEC(当所有修改都应用于 `Page Load Event`. 将修改添加到特定视图时， [!UICONTROL A/B测试]， [!UICONTROL 自动分配]、和 [!UICONTROL 体验定位] 仅支持(XT)活动。

### 集成

| 类型 | 受支持? |
| --- | --- |
| [!UICONTROL Analytics for Target] (A4T) | 是 |
| 受众 | 是 |
| 客户属性 | 是 |
| AEM 体验片段 | 是 |
| [Adobe Experience Platform扩展](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) | 是 |
| 调试程序 | 是 |
| 审核 | at.js 2.*x* 尚未更新规则 |
| 支持以下项的选择加入 [GDPR](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md) | 中支持此功能 [at.js版本2.1.0](/help/dev/implement/client-side/atjs/target-atjs-versions.md#atjs-version-210-june-3-2019) 或更高版本。 |
| 由提供支持的AEM增强型个性化 [!DNL Adobe Target] | 否 |

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

at.js 2.*x*（与 at.js 1.*x* 一样）使用自定义事件 `at-request-succeeded` 来显示响应令牌。有关使用 `at-request-succeeded` 自定义事件的代码示例，请参阅[响应令牌](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html)。

## at.js 1.*x* 参数到 at.js 2.*x* 有效负载的映射

本节概述了 at.js 1.*x* 与 at.js 2.*x* 之间的映射。

在深入研究参数映射之前，这些库版本当前使用的端点已发生更改：

* at.js 1.*x* - `http://<client code>.tt.omtrdc.net/m2/<client code>/mbox/json`
* at.js 2.*x* - `http://<client code>.tt.omtrdc.net/rest/v1/delivery`

另一个重要区别是：

* at.js 1.*x* - 客户端代码是路径的一部分
* at.js 2.*x* - 客户端代码将作为查询字符串参数发送，例如：
  `http://<client code>.tt.omtrdc.net/rest/v1/delivery?client=democlient`

以下部分列出了每个 at.js 1.*x* 参数、其描述以及相应的2.*x* JSON有效负载（如果适用）：

### at_property

（at.js 1.*x* 参数）

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

（at.js 1.*x* 参数）

页面的域，其中 [!DNL Target] 库运行。

at.js 2.*x* JSON 有效负载：

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

（at.js 1.*x* 参数）

浏览器的 WEB GL 渲染器功能。我们的设备检测机制使用此参数来确定访客的设备是桌面设备、iPhone、Android 设备，还是其他设备。

at.js 2.*x* JSON 有效负载：

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

（at.js 1.*x* 参数）

页面 URL。

at.js 2.*x* JSON 有效负载：

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

（at.js 1.*x* 参数）

页面反向链接。

at.js 2.*x* JSON 有效负载：

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

（at.js 1.*x* 参数）

交付 API 不再具有全局 mbox 概念。在 JSON 有效负载中，您必须使用 `execute > pageLoad`。

at.js 2.*x* JSON 有效负载：

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

（at.js 1.*x* 参数）

要使用 mbox 名称，请将其传递到 `execute > mboxes`。mbox 需要索引和名称。

at.js 2.*x* JSON 有效负载：

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

（at.js 1.*x* 参数）

已不再使用。

### mboxCount

（at.js 1.*x* 参数）

已不再使用。

### mboxRid

（at.js 1.*x* 参数）

下游系统用来帮助进行调试的请求 ID。

at.js 2.*x* JSON 有效负载：

```json {line-numbers="true"}
{
  "requestId": "2412234442342"
  ....
}
```

### mboxTime

（at.js 1.*x* 参数）

已不再使用。

### mboxSession

（at.js 1.*x* 参数）

会话 ID 作为查询字符串参数 (`sessionId`) 发送到交付 API 端点。

### mboxPC

（at.js 1.*x* 参数）

TNT ID 被传递到 `id > tntId`。

at.js 2.*x* JSON 有效负载：

```json {line-numbers="true"}
{
  "id": {
    "tntId": "ca5ddd7e33504c58b70d45d0368bcc70.21_3"
  }
  ....
}
```

### mboxMCGVID

（at.js 1.*x* 参数）

Marketing Cloud 访客 ID 被传递到 `id > marketingCloudVisitorId`。

at.js 2.*x* JSON 有效负载：

```json {line-numbers="true"}
{
  "id": {
    "marketingCloudVisitorId": "797110122341429343505"
  }
  ....
}
```

### `vst.aaaa.id` 和 `vst.aaaa.authState`

（at.js 1.*x* 参数）

客户 ID 应被传递到 `id > customerIds`。

at.js 2.*x* JSON 有效负载：

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

（at.js 1.*x* 参数）

用于链接其他内容的客户第三方ID [!DNL Target] ID。

at.js 2.*x* JSON 有效负载：

```json {line-numbers="true"}
{
  "id": {
    "thirdPartyId": "1232312323123"
  }
  ....
}
```

### mboxMCSDID

（at.js 1.*x* 参数）

SDID，也称为补充数据 ID。应被传递到 `experienceCloud > analytics > supplementalDataId`。

at.js 2.*x* JSON 有效负载：

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

（at.js 1.*x* 参数）

[!UICONTROL Analytics 跟踪服务器。]应被传递到 `experienceCloud > analytics > trackingServer`。

at.js 2.*x* JSON 有效负载：

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

（at.js 1.*x* 参数）

Analytics 跟踪服务器的安全性。应被传递到 `experienceCloud > analytics > trackingServerSecure`。

at.js 2.*x* JSON 有效负载：

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

（at.js 1.*x* 参数）

Audience Manager 位置提示。应被传递到 `experienceCloud > audienceManager > locationHint`。

at.js 2.*x* JSON 有效负载：

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

（at.js 1.*x* 参数）

Audience Manager Blob。应被传递到 `experienceCloud > audienceManager > blob`。

at.js 2.*x* JSON 有效负载：

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

（at.js 1.*x* 参数）

版本将通过 version 参数作为查询字符串参数发送。

## 培训视频：at.js 2.*x* 架构图 ![“概述”标记](../../assets/overview.png)

at.js 2.*x* 增强了Adobe [!DNL Target]支持SPA，并与其他Experience Cloud解决方案集成。 该视频介绍了如何将所有内容结合到一起。

>[!VIDEO](https://video.tv.adobe.com/v/26250/?quality=12)

请参阅 [了解at.js 2.*x* 工作](https://experienceleague.adobe.com/docs/target-learn/tutorials/implementation/understanding-how-atjs-20-works.html) 以了解更多信息。
