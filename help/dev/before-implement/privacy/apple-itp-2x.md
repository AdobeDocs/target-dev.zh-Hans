---
keywords: apple， ITP，智能防跟踪， experience cloud id， ecid， itp
description: 了解 [!DNL Adobe Target] 以及旨在保护Safari用户隐私的Apple智能防跟踪(ITP)计划的影响。
title: ' [!DNL Target] 如何处理Apple ITP支持？'
feature: Privacy & Security
exl-id: 6deee03b-df86-4d0d-999c-b11855ddfda5
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 30%

---

# Apple 智能防跟踪 (ITP) 2.x

智能防跟踪(ITP)是Apple的一项旨在保护Safari用户隐私的举措。 第一版 ITP 于 2017 年发布，主要针对使用第三方 Cookie 的情况。事实上，Apple 完全阻止了第三方 Cookie，这反而给广告技术公司和营销技术公司造成严重的困扰，因为这些公司通常使用第三方 Cookie 来跟踪访客并收集访客数据。现在，Apple 正在对如何在 Safari 中使用第一方 Cookie 进行限制和约束。

这些版本的 ITP 包含以下限制：

| 版本 | 详细信息 |
| --- | --- |
| [ITP 2.1](https://webkit.org/blog/8613/intelligent-tracking-prevention-2-1/) | 对使用 `document.cookie` API 放到浏览器中的客户端 Cookie 设置上限，七天到期。<br />发布于 2019 年 2 月 21 日。 |
| [ITP 2.2](https://webkit.org/blog/8828/intelligent-tracking-prevention-2-2/) | 七天到期的上限大幅缩短为一天。<br />发布于 2019 年 4 月 24 日。 |
| [ITP 2.3](https://webkit.org/blog/9521/intelligent-tracking-prevention-2-3/) | 消除了多种解决方法，例如使用localStorage或使用JavaScript `Document.referrer property`。<br />发布于2019年9月23日。<br />在Safari 14、macOS Big Sur、Catalina、Mojave、iOS 14和iPadOS 14中发布的ITP的CNAME遮蔽防御功能。 由第三方CNAME遮蔽的HTTP响应创建的所有Cookie将设置为在7天后过期。<br />于2020年11月12日宣布。 |

## 这对作为[!DNL Target]客户的我有何影响？

Target提供了JavaScript库可供您在页面上部署，以便[!DNL Target]可以为访客提供实时个性化。 有三个[!DNL Target]JavaScript库at.js 1.*x*，at.js 2.*x*，通过[!DNL Adobe Experience Cloud Web SDK] API将客户端[!DNL Target] Cookie放置到访客浏览器上的`document.cookie`。 因此，[!DNL Target] Cookie将会受到Apple ITP 2.1、2.2和2.3的影响，并且会在七天（使用ITP 2.1）和一天（使用ITP 2.2和ITP 2.3）后过期。

Apple ITP 2.x在以下方面影响[!DNL Target]：

| 影响 | 详细信息 |
| --- | --- |
| 潜在增加独特访客计数 | 由于过期时间窗口分别设置为七天（使用ITP 2.1）和一天（使用ITP 2.2和ITP 2.3），您可能会看到来自Safari浏览器的独特访客数量增加。 如果您的访客在七天后(ITP 2.1)或一天后（ITP 2.2和ITP 2.3）重新访问域，[!DNL Target]将强制在您的域上放置新的[!DNL Target] Cookie来替换过期的Cookie。 即便是同一用户，新 [!DNL Target] Cookie 仍会转换为新的独特访客。 |
| 缩短了 [!DNL Target] 活动的回溯期限 | [!DNL Target] 活动的访客轮廓可能会缩短决策的回溯期限。利用 [!DNL Target] Cookie 可识别访客和存储用于个性化的用户轮廓属性。鉴于[!DNL Target] Cookie可以在7天(ITP 2.1)或一天（ITP 2.2和2.3）后Safari过期，与已清除的[!DNL Target] Cookie绑定的用户配置文件数据无法用于决策。 |
| 基于 3rdPartyID 的轮廓脚本 | 由于过期时间窗口分别设置为七天（使用ITP 2.1）和一天（使用ITP 2.2和ITP 2.3），基于3rdPartyID Cookie的[配置文件脚本](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html)将在过期后停止运行。 |
| iOS 设备中的 QA/预览 URL | 由于过期时间窗口分别设置为七天（使用ITP 2.1）和一天（使用ITP 2.2和ITP 2.3），[QA/预览URL](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html)将在过期时停止运行，因为这些URL基于3rdPartyID Cookie。 |

## 我当前已实施的 [!DNL Target] 是否会受到影响？

如果除了[!DNL Target] JavaScript库之外，您还在使用Experience Cloud ID (ECID)库，则您的实施会受到下文所述的影响：[Safari ITP 2.1对Adobe Experience Cloud和Experience Platform客户的影响](https://medium.com/adobetech/safari-itp-2-1-impact-on-adobe-experience-cloud-customers-9439cecb55ac)。
