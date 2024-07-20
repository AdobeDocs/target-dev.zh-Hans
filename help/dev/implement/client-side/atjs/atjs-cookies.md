---
keywords: at.js、2.0、1.x、Cookie
description: 有关 [!DNL Adobe Target] at.js 2.x和at.js 1.x如何处理Cookie的详细信息
title: at.js Cookies
feature: at.js
exl-id: 154a844a-6855-4af7-8aed-0719b4c389f5
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1716'
ht-degree: 72%

---

# at.js Cookie

有关 at.js 2.x 和 at.js 1.*x* Cookie 行为的信息。

## at.js 2.x Cookie 行为

对于at.js版本2.x（最高版本2.10.0，但不包括版本2.10.0），*仅支持第一方Cookie*。 如同在 at.js 1.*x*，第一方Cookie“mbox”存储在`clientdomain.com`中，其中`clientdomain`是您的域。

at.js 会生成一个会话 ID 并将其存储在 Cookie 中。第一个响应包含任何活动信息，以及 [!DNL Target] 服务器生成的 `TNT` 或 `PC ID`。然后，at.js 将 `TNT/PC ID` 写入 Cookie。

`AMCV_###@AdobeOrg`第一方Cookie始终由Experience CloudID服务设置，尽管在[!DNL Target]请求中传递了`ECID`。

>[!NOTE]
>
>对于at.js版本2.10.0及更高版本，支持第一方和跨域Cookie。

### 支持第三方Cookie和跨域跟踪

通过跨域跟踪，可以将在不同域中两个相关的站点上的会话作为单个会话查看。您可以创建一个跨越 `siteA.com` 和 `siteB.com` 的 [!DNL Target] 活动，这样访客在跨域访问时将会保持相同的体验。此功能将与 at.js 1.*x* 第三方和第一方 Cookie 行为联系在一起。

>[!NOTE]
>
>对于at.js版本2.10.0及更高版本，支持第三方Cookie和跨域跟踪。


## at.js 1.*x* Cookie行为

对于 at.js 版本 1.*x*，Cookie 行为取决于它是第一方 Cookie、第三方和第一方 Cookie，还是仅仅为第三方 Cookie。

### 何时使用第一方或第三方 Cookie

您的网站设置决定了您要使用的 Cookie。在尝试了解第一方和第三方Cookie时，了解[!DNL Target]的工作方式会很有帮助。 有关详细信息，请参阅[工作方式 [!DNL Adobe Target] ](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html)。

下面提供了 Cookie 的三个主要用例：

1. 一个域。

   所有测试都将在一个顶级域（`www.domain.com`、`store.domain.com`、`anysub.domain.com` 等）中进行。

   仅使用第一方 Cookie。这是默认方法。

1. 用户跨域，而您想要跟踪和测试用户在这些域里的行为。

   示例：一个用户来到您的网站上购物，但通过 Yahoo 商店结账。此时有三种方法（请与您的客服专员合作以确定最佳方法）：

   * 启用第一方和第三方 Cookie。
   * 仅启用第三方 Cookie（非常少见，但有利于在您的域以外保留 at.js Cookie）。
   * 跨域时只启用第一方 Cookie 并传递 `mboxSession` 参数。

     必须将 `mboxSession` 参数传递到引用 at.js 的登陆页。不能是中间重定向页面。

1. 您在第三方网站上只使用 adbox 或 Flashbox。

   此时有两种方法（请与您的客户服务经理合作以确定最佳方法）：

   * 启用第一方和第三方 Cookie。

     Flashbox 和动态创意需要使用第一方和第三方 Cookie。

   * 仅启用第三方 Cookie。

     这种方法只适用于极少数情况，即使用 AdBox 实施但不进行现场定位的情况。

### 第一方 Cookie 行为

第一方 Cookie 存储在 `clientdomain.com` 中，其中 `clientdomain` 是您的域。

at.js 会生成一个 `mboxSession ID` 并将其存储在 Cookie 中。第一个 响应包含选件和 JavaScript，后者将应用程序生成的 `mboxPC ID` 存储在 Cookie 中。

>[!NOTE]
>
>`AMCV_###@AdobeOrg`第一方Cookie始终使用Experience Cloud访客ID进行设置。

### 第三方 Cookie 行为

第三方 Cookie 存储在 `clientcode.tt.omtrdc.net` 中，第一方 Cookie 存储在 `clientdomain.com` 中，其中 `clientdomain` 是您的域。

at.js 生成一个 `mboxSession ID`。第一个位置请求会返回尝试设置名为 `mboxSession` 和 `mboxPC` 的第三方 Cookie 的 HTTP 响应标头，并且会使用额外的参数 (`mboxXDomainCheck=true`) 发送回重定向请求。

如果浏览器接受第三方 Cookie，则该重定向请求将包含这些 Cookie，同时会返回选件。

如果浏览器拒绝第三方 Cookie，则该重定向请求将不包含这些 Cookie，并且会在页面上的所有位置显示默认内容。由于没有设置 Cookie，因此每次请求访问页面时都会再次发生上述相同的过程。

### 第三方和第一方 Cookie 行为

第三方 Cookie 存储在 `clientcode.tt.omtrdc.net` 中，第一方 Cookie 存储在 `clientdomain.com` 中，其中 `clientdomain` 是您的域。

at.js 生成一个 `mboxSession ID`。第一个位置请求会返回尝试设置名为 `mboxSession` 和 `mboxPC` 的第三方 Cookie 的 HTTP 响应标头，并且会使用额外的参数 (`mboxXDomainCheck=true`) 发送回重定向请求。

如果浏览器接受第三方 Cookie，则该重定向请求将包含这些 Cookie，同时会返回选件。

某些浏览器会拒绝第三方 Cookie。如果第三方 Cookie 被阻止，则第一方 Cookie 仍将可用。[!DNL Target] 会尝试设置第三方 Cookie，如果失败，则 [!DNL Target] 只能跟踪客户端的特定域。如果第三方 Cookie 被阻止，则无法执行跨域跟踪，除非将 `mboxSession` 附加到跨域的链接中。在这种情况下，系统会设置另一个第一方 Cookie，并将其与先前域的第一方 Cookie 进行同步。

## Cookie 设置

Cookie 有多个默认设置。您可以根据需要更改这些设置，但 Cookie 持续时间除外。更改 Cookie 设置时可咨询您的客服专员。

| 设置 | 信息 |
|--- |--- |
| Cookie 名称 | mbox。 |
| Cookie 域 | 您从中提供内容的的第二级域和顶级域。由于这是来自您的公司域，所以此 Cookie 是第一方 Cookie。示例: `mycompany.com`。 |
| 服务器域 | `clientcode.tt.omtrdc.net`，使用您帐户的客户代码。 |
| Cookie 持续时间 | 自访客上次登录起，Cookie在访客的浏览器中保留两年。<P>`deviceIdLifetime`设置可在[at.js版本2.3.1或更高版本](../atjs/target-atjs-versions.md)中覆盖。 有关更多信息，请参阅 [targetGlobalSettings()](../../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md)。 |
| P3P 政策 | 根据大多数浏览器默认设置的要求，使用 P3P 政策发布 Cookie。P3P 政策指示提供 Cookie 的浏览器以及使用该信息的方式。 |

此 Cookie 保存一系列值，以控制您的访客体验营销活动的方式：

| 值 | 定义 |
|--- |--- |
| session ID | 用户会话的唯一 ID。默认情况下，该 ID 持续 30 分钟。 |
| pc ID | 访客浏览器的半永久性 ID。持续 14 天。 |
| check | 用来确定访客是否支持 Cookie 的简单测试值。每次用户请求页面时设置。 |
| disable | 如果访客的加载时间超过了Adobe Experience Platform Web SDK或at.js文件中配置的超时值，则进行设置。 默认情况下，该设置持续 1 小时。 |

## 由于Apple WebKit跟踪更改而对Safari访客的[!DNL Target]产生的影响

请牢记以下内容：

### [!DNL Adobe Target]跟踪如何工作？

| Cookie | 详细信息 |
|--- |--- |
| 第一方域 | 这是[!DNL Target]客户的标准实施。  “mbox”Cookie 在客户的域中进行设置。 |
| 第三方跟踪 | 第三方跟踪对于[!DNL Target]和[!DNL Adobe Audience Manager] (AAM)中的广告和定位用例非常重要。  第三方跟踪需要跨站点脚本技术。[!DNL Target]使用在`clientcode.tt.omtrd.net`域中设置的两个Cookie：“mboxSession”和“mboxPC”。 |

### Apple 的方法是什么？

来自 Apple：

“智能防跟踪是一项新的 WebKit 功能，用于通过进一步限制 Cookie 和其他网站数据来减少跨站点跟踪。”

“这就是所谓的跨站点跟踪，`example-tracker.com` 使用的 Cookie 称为第三方 Cookie。在我们的测试中，我们发现一些热门网站具有超过 70 个此类跟踪器，它们都在默默地收集用户相关数据。”

| 方法 | 详细信息 |
|--- |--- |
| 智能防跟踪 | 有关更多信息，请参阅 WebKit 开源 Web 浏览器引擎网站上的[智能防跟踪](https://webkit.org/blog/7675/intelligent-tracking-prevention/)。 |
| Cookie | Safari 如何处理 Cookie：<ul><li>用户直接访问的域中未包含的第三方 Cookie 从不会进行保存。这不是一种新的行为。Safari 中还不支持第三方 Cookie。</li><li>24 小时后会清除在用户直接访问的域中设置的第三方 Cookie。</li><li>如果第一方域被分类为跨站点跟踪用户，则第一方 Cookie 会在 30 天后清除。此问题可能适用于将用户在线发送到不同域的大型公司。Apple 并未明确说明将如何对这些域进行正确分类，或者如何确定域是否已被分类为跨站点跟踪用户。</li></ul> |
| 机器学习以识别跨站点的域 | 来自 Apple：<P>机器学习分类器：机器学习模型用于根据收集的统计数据，对能够跨站点跟踪用户的顶级私人控制域进行分类。在收集的各种统计数据中，根据当前的跟踪实践，以下三个矢量证明具有强烈的分类信号：唯一域数量下的子资源、唯一域数量下的子框架以及重定向到的唯一域数量。所有数据收集和分类均在设备上进行。<P>但是，如果用户与作为顶级域的（通常称为第一方域）example.com进行交互，则智能防跟踪会将此视为用户对该网站感兴趣的信号，并且会暂时调整其行为，如此时间轴所示：<P>如果用户在过去24小时内与example.com进行了交互，则当`example.com`是第三方时，其Cookie将可用。 这允许“使用我的 X 帐户登录到 Y”登录方案。<ul><li>作为顶级域访问的域不会受到影响。例如，OKTA 等网站</li><li>标识跨多个唯一域作为当前页面的子域或子帧的域。</li></ul> |

### Adobe 将受到何种影响？

| 受影响的功能 | 详细信息 |
|--- |--- |
| 选择退出支持 | Apple 的 WebKit 跟踪更改会中断选择退出支持。<P>[!DNL Target]选择退出使用`clientcode.tt.omtrdc.net`域中的Cookie。 有关更多详细信息，请参阅[隐私](/help/dev/before-implement/privacy/privacy.md)。<P>[!DNL Target]支持两种选择退出：<ul><li>一种是按客户端退出（客户端管理选择退出链接）。</li><li>一个通过Adobe，用于选择用户退出所有客户的所有[!DNL Target]功能。</li></ul>这两种方法都使用第三方 Cookie。 |
| [!DNL Target]活动 | 客户可以为其[!DNL Target]帐户选择其[配置文件生命周期长度](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/visitor-profile-lifetime.html) — 最长90天。 问题在于如果帐户的配置文件生命周期超过30天，并且由于客户的域已被标记为跨站点跟踪用户而清除了第一方Cookie，则Safari访客的行为将在[!DNL Target]的以下区域中受到影响：<P>**[!DNL Target]报告**：如果Safari用户进入活动，30天后返回转化，则该用户将计为两个访客和一次转化。<P>对于使用[!DNL Analytics]作为报表源(A4T)的活动，此行为是相同的。<P>**配置文件和活动成员资格**：<ul><li>第一方 Cookie 过期后会擦除配置文件数据。</li><li>第一方 Cookie 过期后会擦除活动成员资格。</li><li> 对于使用第三方Cookie实施或第一方和第三方Cookie实施的帐户，[!DNL Target]在Safari中不起作用。 请注意，这不是一种新的行为。Safari 暂时还不允许使用第三方 Cookie。</li></ul><P>**建议**：如果担心客户域可能会被标记为跨会话跟踪访客，则最安全的做法是将[!DNL Target]中的配置文件生命周期设置为等于或少于30天。 这可确保在 Safari 和所有其他浏览器中以类似的方式对用户进行跟踪。 |
