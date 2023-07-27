---
keywords: 实施、at.js非javascript、adbox、重定向器、mbox
description: 了解如何实施 [!DNL Adobe Target] 在非JavaScript场景中，例如使用AdBox或重定向器。
title: 如何实施 [!DNL Target] 用于电子邮件？
feature: Implement Email
exl-id: dda00b75-5d58-4405-ae58-75e7883a30ed
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 64%

---

# 电子邮件：实施 [!DNL Target]

关于实施的信息 [!DNL Target] 在非JavaScript场景中，例如使用AdBox或重定向器。

您可以跟踪对广告和其他站外内容的访问次数。您还能识别您站内和站外的同一用户，并根据其全部的网络活动情况展示符合其特点的体验。AdBox通过使用单个URL来进行测试，而无需使用JavaScript或at.js。

AdBox对于没有at.js的网站（例如联属网站）非常有用。 如果您的活动需要动态创意（例如，您需要在广告中显示已从购物车中放弃的产品），那么您将不能使用 AdBox。

AdBox 广告和重定向器可用于任何类型的活动。下表比较了 Adbox 和重定向器，同时还介绍了二者分别在何时使用：

| | 用途 | 何时使用 | URL 结构 | 选件类型 | 选件内容 |
|--- |--- |--- |--- |--- |--- |
| AdBox | 向广告返回不同的图像 | 改变广告的内容 | `clientcode&#x200B;.tt.&#x200B;omtrdc&#x200B;.net/&#x200B;m2&#x200B;/&#x200B;clientcode/ubox/&#x200B;image?` | 重定向选件 | 图像 URL |
| 重定向器 | 将访客重新导向另一个网页 | 改变广告的登陆页 | `clientcode&#x200B;.tt.omtrdc.net/&#x200B;m2/clientcode&#x200B;/ubox/page?` | 重定向选件 | 页面 URL |

## 安全最佳实践

请注意，使用重定向器，您可能会面临开放重定向漏洞的风险。 为避免第三方未经授权即使用重定向程序链接，我们建议您使用“授权的主机”来允许列表默认的重定向URL域。 [!DNL Target] 使用主机将您要允许重定向到的域列入允许列表。有关更多信息，请参阅 [创建指定有权将mbox调用发送到的主机的允许列表 [!DNL Target]](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html#allowlist) 在 *主机*.

## 限制

* 标准 mbox 不存在客户端超时。如果 [!DNL Target] 完全关闭，广告访客将不会看到内容，甚至不会看到默认内容。
* 使用第三方 Cookie 来跟踪访问次数。如果 PCID 不相同，则默认情况下会将访客的第三方配置文件与任何现有的第一方配置文件合并到一起。
* 要在 AdBox 自身中使用第一方 Cookie，您需要在 URL 中传递 mBox 会话。请咨询您的客服专员以实现此操作。
* 要使用第一方 Cookie 来跟踪广告点击次数，需在 URL 中传递 mbox 会话。请咨询您的客服专员以实现此操作。
* 您必须在 URL 中传递 Mbox 会话才能在同一页面上使用多个 AdBox。请咨询您的客服专员以实现此操作。同一个页面上可能会具有一个 AdBox 和一个重定向器链接（因为重定向器实际上位于另一个页面上）。
