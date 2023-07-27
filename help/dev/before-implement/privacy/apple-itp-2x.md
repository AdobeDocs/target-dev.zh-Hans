---
keywords: apple， ITP，智能防跟踪， experience cloud id， ecid， itp
description: 了解 [!DNL Adobe Target] 以及旨在保护Safari用户隐私的Apple智能防跟踪(ITP)计划的影响。
title: 如何 [!DNL Target] 处理Apple ITP支持？
feature: Privacy & Security
exl-id: 6deee03b-df86-4d0d-999c-b11855ddfda5
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 32%

---

# Apple 智能防跟踪 (ITP) 2.x

智能防跟踪(ITP)是Apple的一项旨在保护Safari用户隐私的举措。 第一版 ITP 于 2017 年发布，主要针对使用第三方 Cookie 的情况。事实上，Apple 完全阻止了第三方 Cookie，这反而给广告技术公司和营销技术公司造成严重的困扰，因为这些公司通常使用第三方 Cookie 来跟踪访客并收集访客数据。现在，Apple 正在对如何在 Safari 中使用第一方 Cookie 进行限制和约束。

这些版本的 ITP 包含以下限制：

| 版本 | 详细信息 |
| --- | --- |
| [ITP 2.1](https://webkit.org/blog/8613/intelligent-tracking-prevention-2-1/) | 对使用 `document.cookie` API 放到浏览器中的客户端 Cookie 设置上限，七天到期。<br />发布于 2019 年 2 月 21 日。 |
| [ITP 2.2](https://webkit.org/blog/8828/intelligent-tracking-prevention-2-2/) | 七天到期的上限大幅缩短为一天。<br />发布于 2019 年 4 月 24 日。 |
| [ITP 2.3](https://webkit.org/blog/9521/intelligent-tracking-prevention-2-3/) | 消除了多种解决方法，例如使用localStorage或使用JavaScript `Document.referrer property`.<br />发布于2019年9月23日。<br />已在Safari 14、macOS Big Sur、Catalina、Mojave、iOS 14和iPadOS 14中发布的ITP的CNAME遮蔽防御功能。 由第三方CNAME遮蔽的HTTP响应创建的所有Cookie将设置为在7天后过期。<br />2020年11月12日宣布。 |

## 这对我as a [!DNL Target] 客户？

Target提供了JavaScript库供您在页面上部署，以便 [!DNL Target] 可以为访客提供实时个性化。 有三个 [!DNL Target] JavaScript库at.js 1.*x*， at.js 2.*x*， [!DNL Adobe Experience Cloud Web SDK] 放置客户端 [!DNL Target] 通过访问者浏览器上的Cookie `document.cookie` API。 因此， [!DNL Target] Cookie会受Apple ITP 2.1、2.2和2.3的影响，并且会在七天（使用ITP 2.1）和一天（使用ITP 2.2和ITP 2.3）后过期。

Apple ITP 2.x影响 [!DNL Target] 在以下方面：

| 影响 | 详细信息 |
| --- | --- |
| 潜在增加独特访客计数 | 由于过期时间窗口分别设置为七天（使用ITP 2.1）和一天（使用ITP 2.2和ITP 2.3），您可能会看到来自Safari浏览器的独特访客数量增加。 如果访客在七天(ITP 2.1)或一天（ITP 2.2和ITP 2.3）后重新访问域， [!DNL Target] 被迫放置新的 [!DNL Target] 域中的Cookie替换过期的Cookie。 即便是同一用户，新 [!DNL Target] Cookie 仍会转换为新的独特访客。 |
| 缩短了 [!DNL Target] 活动的回溯期限 | [!DNL Target] 活动的访客配置文件可能会缩短决策的回溯期限。利用 [!DNL Target] Cookie 可识别访客和存储用于个性化的用户配置文件属性。有鉴于此 [!DNL Target] Safari中的Cookie可以在七天(ITP 2.1)或一天（ITP 2.2和2.3）后过期，这些是与清除绑定的用户配置文件数据 [!DNL Target] cookie无法用于决策。 |
| 基于 3rdPartyID 的个人资料脚本 | 由于过期时间窗口分别设置为七天（使用ITP 2.1）和一天（使用ITP 2.2和ITP 2.3）， [配置文件脚本](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html) 基于3rdPartyID Cookie将在过期时停止运行。 |
| iOS 设备中的 QA/预览 URL | 由于过期时间窗口分别设置为七天（使用ITP 2.1）和一天（使用ITP 2.2和ITP 2.3）， [QA/预览URL](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html) 过期时将停止运行，因为URL基于3rdPartyID Cookie。 |

## 我当前已实施的 [!DNL Target] 是否会受到影响？

如果您在使用Experience CloudID (ECID)库之外， [!DNL Target] JavaScript库中，您的实施将受到下文所述的影响： [Safari ITP 2.1对Adobe Experience Cloud和Experience Platform客户的影响](https://medium.com/adobetech/safari-itp-2-1-impact-on-adobe-experience-cloud-customers-9439cecb55ac).
