---
keywords: at.js FAQ, at.js 常见问题解答, 常见问题解答, 闪烁, 加载器, 页面加载器, 跨域, 文件大小, x-domain, at.js 和 mbox.js, 仅限 x, Safari, 单页应用程序, 缺少选择器, 选择器, tt.omtrdc.net, spa, Adobe Experience Manager, AEM, IP 地址, httponly, HttpOnly, 安全, IP, Cookie 域
description: 阅读关于 [!DNL Adobe Target] at.js JavaScript库。
title: 有关at.js的常见问题和解答有哪些？
feature: at.js
exl-id: 362ccc5b-8731-46c0-bc52-3e55c273e216
source-git-commit: 448c43c0c10e22ad054f4ee98bfc282f8c96cdcb
workflow-type: tm+mt
source-wordcount: '2938'
ht-degree: 39%

---

# at.js 常见问题解答

关于的常见问题解答 [!DNL Adobe Target] at.js JavaScript库。

## 与mbox.js相比，使用at.js具有哪些优势？

at.js库将取代mbox.js。 不再支持mbox.js库。 但是，对于大多数人来说，at.js将能够比mbox.js提供更大的优势。

使用at.js具有许多好处，包括缩短Web实施的页面加载时间，增强安全性，以及为单页应用程序提供更好的实施选项，等等。

下图说明了使用 mbox.js 与使用 at.js 时的页面加载性能。

（单击图像可展开至全宽。）

![比较mbox.js与at.js的页面性能图](/help/dev/implement/client-side/atjs/assets/atjs_versus_mboxjs.png "比较mbox.js与at.js的页面性能图"){zoomable=&quot;yes&quot;}

如上图所示，使用mbox.js时，页面内容直到 [!DNL Target] 呼叫完成。 使用 at.js 时，在 [!DNL Target] 调用启动后即会开始加载页面内容，而不会等到调用完成才开始加载。

## at.js和mbox.js对页面加载时间有何影响？

许多客户和顾问都想了解at.js和mbox.js对页面加载时间的影响，尤其是对于新用户与旧用户的情况。 遗憾的是，由于每位客户的实施不尽相同，因此很难评测at.js或mbox.js对页面加载时间的影响并给出具体的数字。

但是，如果页面上存在访客API， [!DNL Target] 可以更好地了解at.js和mbox.js对页面加载时间有何影响。

>[!NOTE]
>
>仅当您使用全局mbox时，访客API以及at.js或mbox.js才会对页面加载时间造成影响（由于采用了主体隐藏技术）。 区域 mbox 不受访客 API 集成的影响。

下表介绍了为新访客和旧访客执行的一系列操作：

### 新访客

1. 加载、解析并执行访客 API。
1. 加载、解析并执行 at.js/mbox.js。
1. 如果启用了全局mbox自动创建，则 [!DNL Target] JavaScript库：

   * 对访客对象实例化。
   * 此 [!DNL Target] 库尝试检索Experience Cloud访客ID数据。
   * 由于此访客是新访客，因此访客API会触发对demdex.net的跨域请求。
   * 在检索Experience Cloud访客ID数据后，请求执行以下操作 [!DNL Target] 被炒了。

### 旧访客

1. 加载、解析并执行访客 API。
1. 加载、解析并执行 at.js/mbox.js。
1. 如果启用了全局mbox自动创建，则 [!DNL Target] JavaScript库：

   * 对访客对象实例化。
   * 此 [!DNL Target] 库尝试检索Experience Cloud访客ID数据。
   * 访客 API 从 Cookie 中检索数据。
   * 在检索Experience Cloud访客ID数据后，请求执行以下操作 [!DNL Target] 被炒了。

>[!NOTE]
>
>对于新访客，当存在访客API时， [!DNL Target] 得反复检查电线才能确定 [!DNL Target] 请求包含Experience Cloud的访客ID数据。 对于旧访客， [!DNL Target] 越过电线只能 [!DNL Target] 以检索个性化内容。

## 为何从以前版本的 at.js 升级到版本 1.0.0 后，响应时间似乎变长了？

at.js版本1.0.0及更高版本可并行触发所有请求。 以前的版本会按顺序执行请求，这意味着请求会被放入队列中，并且 [!DNL Target] 会等待第一个请求完成，然后再转到下一个请求。

早期版本的at.js执行请求的方式容易受到“队头阻塞”的影响。 在at.js 1.0.0及更高版本中， [!DNL Target] 切换到并行请求执行。

例如，如果您检查at.js 0.9.1的“网络”选项卡瀑布图，则下一步将看到该瀑布图 [!DNL Target] 在前一个请求完成之前，不会启动请求。 at.js 1.0.0及更高版本的情况并非如此，所有请求基本上可以同时启动。

从响应时间的角度，从数学上讲，这一顺序可以这样概括

<ul class="simplelist"> 
 <li> at.js 0.9.1：全部的响应时间 [!DNL Target] 请求=请求响应时间总和 </li> 
 <li> at.js 1.0.0及更高版本：全部的响应时间 [!DNL Target] 请求=最大请求响应时间 </li> 
</ul>

at.js库版本1.0.0可以更快地完成请求。 此外，at.js请求是异步执行的，因此 [!DNL Target] 不会阻止页面渲染。 即使请求需要几秒钟才能完成，您仍可以看到渲染的页面，在之前，只有页面的某些部分显示为空白 [!DNL Target] 从获取响应 [!DNL Target] 边缘。

## 我能否加载 [!DNL Target] 是否异步库？

at.js 1.0.0版本使您可以加载 [!DNL Target] 库异步运行。

要异步加载 at.js，请执行以下操作：

* 推荐的方法是通过Adobe Experience Platform中的标记进行实施。
* 您还可以通过向加载 at.js 的脚本标记中添加 async 属性来异步加载 at.js。使用如下代码：

  ```
  <script src="<URL to at.js>" async></script>
  ```

* 您还可以使用以下代码异步加载 at.js：

  ```
  var script = document.createElement('script'); 
  script.async = true; 
  script.src = "<URL to at.js>"; 
  document.head.appendChild(script);
  ```

异步加载 at.js 有利于避免阻止浏览器渲染；但是，此技术可能会导致网页闪烁。

您可以避免闪烁，方法是使用预先隐藏的代码片段先隐藏页面（或指定部分），然后在加载at.js和全局请求后显示该页面。 在加载 at.js 之前，必须先添加该代码片段。

如果您通过异步部署at.js [!UICONTROL Adobe Experience Platform] 实施，请确保在实施之前直接在您的页面上包含预隐藏代码片段 [!DNL Target] 使用 [!UICONTROL Adobe Experience Platform] 嵌入代码。

如果要通过同步 DTM 实施部署 at.js，则可通过页面顶部触发的“页面加载”规则添加预先隐藏的代码片段。

有关更多信息，请参阅 [at.js 如何管理闪烁](/help/dev/implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md)。

## at.js是否与 [!DNL Adobe Experience Manager] 集成(Experience Manager)？

[!DNL Adobe Experience Manager] 现在，带有FP-11577的6.2（或更高版本）支持通过其 [!UICONTROL Adobe TargetCloud Service] 集成。

## 使用at.js时，我如何才能阻止页面加载闪烁？

[!DNL Target] 提供了几种防止页面加载闪烁的方法。 有关更多信息，请参阅 [使用at.js阻止闪烁](/help/dev/implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md).

## at.js的文件大小是多少？

at.js 文件在下载后大约为 109 KB。但是，由于大多数服务器会自动压缩文件以缩小文件大小，因此在服务器上压缩（使用 GZIP 或其他方法）后，at.js 的大小约为 34 KB，并且该文件会在用户访问您的网站时加载。安装 at.js 的服务器上的压缩设置决定了其实际压缩大小。

## at.js为何比mbox.js大？

at.js实施使用单个库( at.js)，而mbox.js实施则实际使用两个库（ mbox.js和target.js）。 因此，更公平的比较方式是将 at.js 与 mbox.js *和* `target.js` 进行比较。若比较两个版本的 gzip 压缩文件大小，at.js 版本 1.2 的大小为 34 KB，而 mbox.js 版本 63 的大小则为 26.2 KB。

at.js 更大，因为与 mbox.js 相比，它执行更多的 DOM 解析。该解析是必需的，因为 at.js 会在 JSON 响应中获取“原始”数据，并且必须了解这些数据的含义。使用的mbox.js `document.write()` 所有的解析都是由浏览器完成的。

尽管文件较大，但我们的测试表明，与使用 mbox.js 相比，使用 at.js 可加快页面加载速度。此外，at.js的安全性也更高，因为它不会动态加载其他文件或使用 `document.write`.

## at.js 中是否有 jQuery？如果我的网站上已有jQuery，我是否可以删除at.js中的这一部分？

at.js当前使用部分jQuery，因此您会在at.js顶部看到MIT许可证通知。 jQuery 不会显示，且不会影响您的页面上已有的 jQuery 库，页面上已有的 jQuery 版本可能不同。不支持删除 at.js 内的 jQuery 代码。

## at.js是否支持Safari和将跨域设置为“仅限x”？

不需要，如果跨域设置为x-only且Safari禁用了第三方Cookie，则mbox.js和at.js会设置一个禁用的Cookie，并且不会为该特定客户端的域执行任何mbox请求。

为了支持Safari访客，更好的X-Domain应该是“禁用”（仅设置第一方Cookie）或“启用”（仅在Safari上设置第一方Cookie，在其他浏览器上设置第一方和第三方Cookie）。

## 我能否使用Target [!UICONTROL 可视化体验编辑器] (VEC)？

能，如果您使用at.js 2.x，则可以将VEC用于SPA。有关更多信息，请参阅 [单页(SPA)可视化体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/spa-visual-experience-composer.html).

## 我能否将 Adobe Experience Cloud 调试器与 at.js 实施结合使用？

是. 您也可以使用 mboxTrace 来进行调试或使用浏览器的开发人员工具来检查网络请求，并按“mbox”进行筛选以隔离出 mbox 调用。

## 我能否在使用 at.js 的 mbox 名称中使用特殊字符？

能，与使用 mbox.js 的 mbox 名称一样。

## 为何 mbox 没有在我的网页上触发？

[!DNL Target] 客户有时会将基于云的实例与结合使用 [!DNL Target] 用于测试或简单的概念验证。 这些域以及其他许多域均是[公共后缀列表](https://publicsuffix.org/list/public_suffix_list.dat)的一部分。

如果您使用这些域，则新型浏览器不会保存Cookie，除非您自定义 `cookieDomain` 使用targetGlobalSettings()设置。 有关更多信息，请参阅 [结合使用基于云的实例 [!DNL Target]](/help/dev/implement/client-side/target-debugging-atjs/targeting-using-cloud-based-instances.md).

## 使用 at.js 时，IP 地址能否用作 Cookie 域？

能，只要您使用的是 [at.js 版本 1.2 或更高版本](/help/dev/implement/client-side/atjs/target-atjs-versions.md)。但是，Adobe强烈建议您保持当前版本为最新版本。

>[!NOTE]
>
>如果您使用的是 at.js 版本 1.2 或更高版本，则无需查看以下示例。

根据您使用 [targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md) 的方式，您可能需要在下载 at.js 后对代码进行额外的修改。例如，如果您需要对不同网站上的 [!DNL Target] 实施进行稍微不同的设置，而又无法使用自定义 JavaScript 动态定义这些设置，则需在下载该文件之后以及将该文件上传到相应网站之前手动自定义这些设置。

以下示例允许您使用 `targetGlobalSettings()` at.js 函数插入一个代码片段来支持 IP 地址：

此示例适用于单个 IP 地址：

```
if (window.location.hostname === '123.456.78.9') { 
    window.targetGlobalSettings = window.targetGlobalSettings || {}; 
    window.targetGlobalSettings.cookieDomain = window.location.hostname; 
}
```

此示例适用于 IP 地址范围：

```
if (/^123\.456\.78\..*/g.test(window.location.hostname)) { 
    window.targetGlobalSettings = window.targetGlobalSettings || {}; 
    window.targetGlobalSettings.cookieDomain = window.location.hostname; 
}
```

## 为何我会看到诸如“操作缺少选择器”之类的警告消息？

这些消息与at.js功能无关。 at.js库会尝试报告无法在DOM中找到的任何内容。

如果看到此类警告消息，则根本原因可能如下所示：

* 页面正在动态生成，且at.js无法找到该元素。
* 页面构建缓慢（由于网络速度慢），并且at.js无法在DOM中找到选择器。
* 正在运行活动的页面结构发生更改。如果您在可视化体验编辑器 (VEC) 中重新打开活动，则应会收到警告消息。更新活动，以便能够找到所有必需的元素。
* 基础页面是单页应用程序(SPA)的一部分，或者该页面包含显示在页面更靠底部的元素，并且at.js“选择器轮询机制”无法找到这些元素。 增加 `selectorsPollingTimeout` 可能会有所帮助。有关更多信息，请参阅 [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md)。
* 任何点击跟踪量度都会尝试将其自身添加到每个页面，而不考虑已设置量度的 URL。这种情况虽然无害，但使许多此类消息得以显示。

  为了获得最佳结果，请下载并使用 [最新版本的at.js](/help/dev/implement/client-side/atjs/target-atjs-versions.md). 有关如何下载at.js的更多信息，请参阅 [使用下载at.js [!DNL Target] 界面](how-to-deployatjs/implement-target-without-a-tag-manager.md#download-atjs-using-the-target-interface) 中的部分 [*如何部署at.js* > *实施 [!DNL Target] 没有标签管理器*](how-to-deployatjs/implement-target-without-a-tag-manager.md) 文章。

## 什么是tt.omtrdc.net域， [!DNL Target] 服务器调用转至？

tt.omtrdc.net是AdobeEDGE网络的域名，用于接收所有服务器调用 [!DNL Target].

## 为什么at.js不始终使用HttpOnly和Secure Cookie标记？

HttpOnly 只能通过服务器端代码进行设置。[!DNL Target] Cookie（例如mbox）是通过JavaScript代码创建和保存的，因此 [!DNL Target] 无法使用HttpOnly Cookie标记。 [!DNL Target] 启用跨域后，不为从服务器端设置的第三方Cookie使用set HttpOnly。

只有在通过 HTTPS 加载页面时，才能通过 JavaScript 设置 Secure 标记。如果页面最初通过 HTTP 加载，则 JavaScript 无法设置此标记。此外，如果使用Secure标记，则Cookie仅在HTTPS页面上可用。 对于通过HTTPS加载的页面， [!DNL Target] 设置Secure和SameSite=None属性。

为确保 [!DNL Target] 能够正确跟踪用户，并且由于Cookie是在客户端生成的， [!DNL Target] 除了上述情况外，不使用这些标记中的任何一个。

## at.js如何处理XSS和MITM攻击等安全问题？

与at.js启用的Adobe Edge网络的通信仅通过HTTPS进行，只要 `secureOnly` 选项在targetGlobalSettings()函数([targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md))，否则，将允许at.js根据页面协议在HTTP和HTTPS之间切换。

默认情况下，强制使用以下标头：
* HTTP严格传输安全(HSTS)
* X-XSS保护
* X内容类型选项
* 反向链接策略

可以强制实施已在客户端页面中使用的所有标头。 一种常用的方法是通过“HTTP请求标头授权”。 Adobe客户关怀团队可以就最佳方法和实践提供进一步的建议。

此外，对Adobe Edge网络的请求是公开的（因为它们设计为从访客的浏览器中发出），并且不包含可见的访客详细信息（它们仅包含访客ID）。 这些请求为访客提供体验，并包含有关访客应在页面上看到的内容的详细信息。

请注意，对于在这些请求中传输的响应令牌和会话ID：

* 他们跟踪通信会话
* 它们由随机字符组成
* 会话ID的有效期为30分钟
* 可以禁用响应令牌([响应令牌](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html))
* 它们仅在Adobe解决方案的环境中有用。

预计将会看到 `Access-Control-Allow-Origin` at.js请求中具有值“*”的标头，由于它们是公共的，因此无需身份验证，并且需要通过JavaScript调用从任何域访问Adobe Edge网络。

但是，需要在页面上实施内容安全策略(CSP)。 有关at.js的CSP要求的更多信息，请参阅 [内容安全策略](/help/dev/before-implement/privacy/content-security-policy.md) 和 [targetGlobalSettings](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md).

## at.js 多久触发一次网络请求？

[!DNL Target] 在服务器端执行其所有决策。 这意味着每次重新加载页面或调用 at.js 公共 API 时，at.js 都会触发网络请求。

## 在最佳情况下，当执行隐藏、替换和显示内容这类页面加载操作时，用户是否不会受到明显影响？

at.js会试图避免长时间预先隐藏HTMLBODY或其他DOM元素，但这具体取决于网络条件和活动设置。 at.js 会提供[设置](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md)，您可以使用这些设置来自定义主体隐藏 CSS 样式，这样您可以预先隐藏页面的某些部分，而不清空整个 HTML 主体。预期的情况是这些部分包含必须进行“个性化”的 DOM 元素。

## 在用户符合活动条件的一般场景中，事件的序列是怎样的？

由于 at.js 请求是异步 `XMLHttpRequest`，因此我们会执行以下步骤：

1. 页面加载。
1. at.js 预先隐藏 HTML 主体。有一个设置可用来预先隐藏特定容器而不是 HTML 主体。
1. at.js 请求触发。
1. 在 [!DNL Target] 已收到响应， [!DNL Target] 提取CSS选择器。
1. 使用CSS选择器， [!DNL Target] 创建STYLE标记以预先隐藏将自定义的DOM元素。
1. 删除 HTML 主体预先隐藏 STYLE。
1. [!DNL Target] 开始轮询DOM元素。
1. 如果找到DOM元素， [!DNL Target] 应用DOM更改并删除元素预隐藏样式。
1. 如果未找到DOM元素，则全局超时将取消隐藏这些元素，以避免页面损坏。

## 当at.js最终取消隐藏活动正在更改的元素时，系统将以何种频率充分加载和显示页面内容？

考虑到上述情况，当at.js最终取消隐藏活动正在更改的元素时，系统将以何种频率充分加载和显示页面内容？ 换言之，除了活动内容之外，页面会完全可见，而活动内容会在其他内容稍后显示。

at.js 不会阻止页面呈现。用户可能会注意到页面上的一些空白区域，这些区域表示由自定义的元素 [!DNL Target]. 如果要应用的内容未包含大量远程资产（例如 SCRIPT 或 IMG），则所有内容都应会快速呈现。

## 已完全缓存的页面对上述情景有何影响？活动内容是否很可能会在页面的其他内容加载相当一段时间后才会显示？

如果页面缓存在靠近用户位置但不靠近用户位置的CDN上 [!DNL Target] edge，该用户可能会看到一些延迟。 [!DNL Target] 边缘分布在全球各地，因此大多数情况下这并不是问题。

## 是否可以先显示主页图像，然后在短暂延迟后将其换掉？

请考虑以下情况：

此 [!DNL Target] 超时为5秒。 用户加载的页面具有自定义主页图像的活动。at.js 发送请求以确定是否有可应用的活动，但没有收到初始响应。由于未收到来自的响应，因此假设用户看到了主页图像的常规内容 [!DNL Target] 关于是否存在关联的活动。 四秒后， [!DNL Target] 会返回包含活动内容的响应。

此时，是否可以显示替代版本？那么四秒后，是否可以换掉主页图像？同时，用户是否可以查看此图像切换过程？

最初，主页图像 DOM 元素处于隐藏状态。在收到来自的响应后 [!DNL Target] 接收后，at.js会应用DOM更改，例如替换IMG并显示自定义的主页图像。

## at.js 需要何种 HTML doctype？

at.js 需要 HTML 5 doctype。

此语法为：

`<!DOCTYPE html>`

HTML 5 doctype 可确保页面以标准模式加载。在 Quirks 模式下加载时，at.js 所依赖的一些 JS API 将被禁用。[!DNL Target] 在Quirks模式下禁用at.js。

## at.js是否可以在Ionic应用程序环境中工作。

此实施从未进行过测试，因为at.js并不打算在非Web环境中工作。 [!DNL Adobe] 建议其 [适用于移动实施的SDK](/help/dev/implement/mobile/overview.md).
