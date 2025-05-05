---
keywords: 内容安全策略， csp， at.js，白名单， 允许列表，闪烁，预隐藏，预隐藏，内容安全策略， iFrame， iframe
description: 了解在使用 [!DNL Adobe Target]时应该添加的内容安全策略(CSP)指令。
title: ' [!DNL Target] 如何处理内容安全策略 (CSP)？'
feature: Privacy & Security
exl-id: ec6942e5-36d8-4f88-b3d6-47f9eaca03a8
source-git-commit: c43c79b29768694eac534e22047b5ee6a3d0ccd5
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 28%

---

# 内容安全策略 (CSP) 指令

如果您在为[!DNL Adobe Target]实施使用[内容安全策略](https://zh.wikipedia.org/wiki/Content_Security_Policy) (CSP)，则在使用[at.js 2.1或更高版本](../../implement/client-side/atjs/target-atjs-versions.md)时应该添加以下CSP指令：

* `connect-src` 与 `*.tt.omtrdc.net` 已列入允许列表。要允许将网络请求发送到 [!DNL Target] 边缘时是必需的。
* `style-src unsafe-inline`。对于预隐藏和闪烁控制是必需的。
* `script-src unsafe-inline`。需要此项以允许可能作为 HTML 选件一部分的 JavaScript 执行。

## 常见问题解答 (FAQs)

有关安全策略，请参阅以下常见问题解答：

### 跨源资源共享 (CORS) 和 Flash 跨域策略是否存在安全问题？

实施 CORS 策略的推荐方法是，只允许通过受信任域的允许列表访问需要它的受信任来源。Flash 跨域策略亦是如此。 有些[!DNL Target]客户担心在Target中的域使用通配符。 问题在于，如果用户登录到应用程序，并访问策略允许的域，则该域上运行的任何恶意内容都可能从应用程序中检索敏感内容，并在登录用户的安全上下文中执行操作。 这种情况通常称为跨站点请求伪造(CSRF)。

但是，在[!DNL Target]实施中，这些策略不应代表安全问题。

&quot;adobe.tt.omtrdc.net&quot; 是 Adobe 拥有的域。 [!DNL Adobe Target] 是一种测试和个性化工具，预计 [!DNL Target] 可以接收和处理来自任何地方的请求，而无需任何身份验证。 这些请求包含用于 A/B 测试、建议或内容个性化的键/值对。

Adobe未在“adobe.tt.omtrdc.net”指向的[!DNL Adobe Target]边缘服务器上存储个人身份信息(PII)或其他敏感信息。

可以通过 JavaScript 调用从任何域访问 [!DNL Target]。 允许此访问的唯一方法是应用带有通配符的“Access-Control-Allow-Origin”。

### 如何允许或阻止我的站点被嵌入为外部域下的iFrame？

要允许[可视化体验编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/vec/visual-experience-composer.html?lang=zh-Hans){target=_blank} (VEC)将您的网站嵌入到iFrame中，必须在您的Web服务器设置上更改CSP（如果已设置）。 必须将[!DNL Adobe]个域列入白名单并进行配置。

出于安全原因，您可能希望阻止将站点作为iFrame嵌入到外部域下。

以下部分将说明如何允许或阻止VEC将您的网站嵌入到iFrame中。

#### 允许VEC将您的网站嵌入到iFrame中

启用VEC将您的网站嵌入到iFrame的最简单解决方案是允许使用最广泛的通配符`*.adobe.com`。

例如：

`Content-Security-Policy: frame-ancestors 'self' *.adobe.com`

如下图所示（单击放大）：


带有最广泛通配符的![CSP](/help/dev/before-implement/privacy/assets/csp-adobe.png){width="600" zoomable="yes"}

您可能希望仅允许实际的[!DNL Adobe]服务。 可使用`*.experiencecloud.adobe.com + https://experiencecloud.adobe.com`实现此方案。

例如：

`Content-Security-Policy: frame-ancestors 'self' https://*.experiencecloud.adobe.com https://experiencecloud.adobe.com https://experience.adobe.com`

如下图所示（单击放大）：

ExperienceCloud作用域为![CSP](/help/dev/before-implement/privacy/assets/csp-experiencecloud.png){width="600" zoomable="yes"}

使用`https://<Client Code>.experiencecloud.adobe.com https://experience.adobe.com`对公司帐户的访问限制最严格，其中`<Client Code>`代表您的特定客户端代码。

例如：

`Content-Security-Policy: frame-ancestors 'self'  https://ags118.experiencecloud.adobe.com https://experience.adobe.com`

如下图所示（单击放大）：

![CSP的clientcode作用域为](/help/dev/before-implement/privacy/assets/csp-clientcode.png){width="600" zoomable="yes"}

>[!NOTE]
>
>如果您实施了[Launch/标记](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md)，则还必须将其解锁。
>
>例如：
>
> `Content-Security-Policy: frame-ancestors 'self' *.adobe.com *.assets.adobedtm.com;`

#### 阻止VEC将您的网站嵌入到iFrame中

要阻止VEC将您的网站嵌入到iFrame中，您可以仅将其限制为“自身”。

例如：

`Content-Security-Policy: frame-ancestors 'self'`

如下图所示（单击以放大）：

![CSP错误](/help/dev/before-implement/privacy/assets/csp-error.png){width="600" zoomable="yes"}

将显示以下错误消息：

`Refused to frame 'https://kuehl.local/' because an ancestor violates the following Content Security Policy directive: "frame-ancestors 'self'".`

