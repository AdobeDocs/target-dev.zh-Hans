---
keywords: 实施, mbox.js 非 javascript, 重定向器, 每次点击成本, 每次点击收入
description: 了解如何在电子邮件实施中使用重定向器，就像在 [!DNL Adobe Target] 活动中使用mbox一样。
title: 如何使用重定向器？
feature: Implement Email
exl-id: 072368ff-9f17-4709-ac2d-c9e1f0d888bb
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '668'
ht-degree: 64%

---

# 使用重定向程序

使用重定向器的方法和您在测试中使用 mbox 的方法类似。

重定向器是使用一种特定的重定向器 URL 创建的，该重定向器 URL 将重定向器 mbox（重定向器）加载到您的帐户中。使用此重定向器的方法和您在测试中使用 mbox 的方法类似。将重定向器 URL 以广告目标链接的形式提交到您的广告网络。

使用重定向器执行以下操作：

* 跟踪从您的展示广告链接到您网站的点击量
* 创建单个集中化报表，跟踪多广告网络中对展示广告的点击量
* 多样化展示广告目标。

  例如，在您的主页、类别页面和产品页面上放置相同的横幅。

* 找出哪个登陆页能引起更多的转化

有关确定正确设置的帮助，请参阅[不基于JavaScript的实施](/help/dev/implement/email/overview.md)。

## 创建重定向器

必须先创建重定向器才能使用重定向功能。

1. 决定广告的目标变量，包括默认的目标。
1. 创建重定向器 URL。

   ```
   https://<your_testandtarget_clientcode>.tt.omtrdc.net/​m2/yourclientcode/ubox
   /​page?mbox=redirectorlink_456
   &mboxDefault=http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2Fusualdestination%2Ehtm
   ```

   * 其中，`yourclientcode` 是您公司的客户端代码。您公司的客户端代码全部为小写字母，且不含任何特殊字符。

     您的客户端代码位于[!DNL Target]界面的&#x200B;**[!UICONTROL Administration]** > **[!UICONTROL Implementation]**&#x200B;页面顶部。

   * `redirectorlink_456` 是出现在您帐户中并在营销活动和测试中使用的重定向器 mbox 的名称。

     重定向器与其他 mbox 的运行方式不同，但是与其他任何 mbox 一样，都会显示在您的帐户中。为重定向器命名，以便能够轻松地将它与您帐户中其他标准类型的 mbox 区分开来。作为最佳实践，重定向器 mbox 的名称应该以“redirectorlink”开头。

   * 其中，`http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2Fusualdestination%2Ehtm` 是默认目标。

     这必须是进行了编码的 URL，且必须是绝对引用。您可以使用[HTMLURL编码引用](https://www.w3schools.com/tags/ref_urlencode.asp)来快速对您的URL进行编码。

   >[!WARNING]
   >
   >请注意，使用重定向器，您可能会面临开放重定向漏洞的风险。 为避免第三方未经授权即使用重定向程序链接，Adobe建议您使用“授权的主机”来允许列表默认的重定向URL域。 [!DNL Target]使用主机允许列表您要允许重定向的域。 有关详细信息，请参阅[创建允许列表，指定有权将mbox调用发送到&#x200B;*主机*&#x200B;中的 [!DNL Target]](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html#allowlist)的主机。

1. 验证重定向器。
   1. 列入允许列表 *安全最佳实践*：确保重定向器中使用的域已，如上所述。 如果您使用未列入允许列表的域，则Adobe将阻止对该域的任何调用，以防止恶意行为者使用重定向器重定向到潜在的恶意域。
   2. 将重定向器 URL 插入到浏览器中并刷新。
   3. 登录到您的帐户，刷新 mbox 列表，然后验证以 mbox 形式列出的新的重定向器。
1. 如果您要为一个广告测试不同目标，则请为每个版本创建[重定向选件](https://experienceleague.adobe.com/docs/target/using/experiences/vec/redirect-offer.html)。
1. 创建营销活动。

   请参阅[不基于 JavaScript 的实施](/help/dev/implement/email/overview.md)，以了解如何正确设置来实现您的目标。
1. 完成营销活动质量保证工作。

   使用包含重定向器 URL 的 `<a href>` 创建一个虚拟页面。示例：

   ```
   <a href=https://<your_clientcode>.tt.omtrdc.net/​m2/yourclientcode/ubox/​page?mbox=
   
   redirectorlink_456&mboxDefault=http%3A%2F%2Fwww%2Eyourcompany%2Ecom%2F​usualdestination%2Ehtm>
   ```

1. 验证所有体验、默认内容和报表，确保它们在所有环境下能通过所有类型的浏览器按照预期工作。

   >[!NOTE]
   >
   >“选件预览”或“浏览 mbox”功能不支持重定向器。直接在浏览器中预览体验。 此外，`mboxDebug`不适用于重定向器。

1. 将整个重定向 URL 作为广告的目标链接提交给您的展示广告网络。

## 使用重定向器传递“每次点击成本”和“每次点击收入”

有关使用重定向器传递每次点击成本和每次点击收入的信息。

### 传递每次点击成本

使用重定向器传递每次点击成本。

>[!NOTE]
>
>最佳实践是使用&#x200B;**[!UICONTROL Score per visit]**&#x200B;参与度量度确定成本值。

将 `&mboxPageValue=-value` 添加到 URL。请注意负值。

例如，每次点击成本为 .10 美分时，如下所示：

```
https://<your_clientcode>.tt.omtrdc.net/​m2/yourclientcode/ubox/​page?mbox=redirectorlink_456
&mboxPageValue=-0.1&mboxDefault=​https://www.yourcompany.com/usualdestination.htm
```

### 传递每次点击收入

使用重定向器传递每次点击收入。

>[!NOTE]
>
>最佳实践是使用&#x200B;**[!UICONTROL Score per visit]**&#x200B;参与度量度确定收入值。

将 `&mboxPageValue=value` 添加到 URL。

例如，每次点击收入为 .10 美分时，如下所示：

```
https://<​your_clientcode>​​​​.tt​​.omtrdc​.net/​​m2/​yourclientcode/​ubox/​​​page?mbox=redirectorlink_456
&mboxPageValue=0.1​&mbox​Default=​​http%3A%2F%2Fwww%2E​yourcompany%2Ecom​%2Fusualdestination%2Ehtm
```
