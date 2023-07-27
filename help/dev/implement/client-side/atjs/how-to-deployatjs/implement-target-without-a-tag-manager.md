---
keywords: 实施target，实施，实施at.js，标签管理器，设备上决策，设备决策
description: 了解如何指定设置（帐户详细信息、实施方法等） 实施 [!DNL Adobe Target] at.js库，而不使用标签管理器。
title: 我是否可以实施 [!DNL Target] 没有Tag Manager？
feature: Implement Server-side
exl-id: f675ae21-105d-4aa3-9926-59291f1136b5
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1752'
ht-degree: 44%

---

# 实施 [!DNL Target] 没有标签管理器

关于实施的信息 [!DNL Adobe Target] 无需使用标签管理器或中的标签 [!DNL Adobe Experience Platform].

>[!NOTE]
>
>中的标记 [Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) 是实现的首选方法 [!DNL Target] 和at.js库。 以下信息不适用于在中使用标记 [!DNL Adobe Experience Platform] 实施 [!DNL Target].

要访问“实施”页面，请单击 **[!UICONTROL 管理]** > **[!UICONTROL 实现]**.

您可以在此页上指定以下设置：

* 帐户详细信息
* 实施方法
* 配置文件API
* 调试器工具
* 隐私

>[!NOTE]
>
>您可以覆盖at.js库中的设置，而不是在中配置它们 [!DNL Target] Standard/Premium UI或使用REST API进行配置。 有关更多信息，请参阅 [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md)。

## 帐户详细信息

您可以查看以下帐户详细信息。 无法更改这些设置。

| 设置 | 描述 |
| --- | --- |
| [!UICONTROL 客户代码] | 客户端代码是指特定于客户端的字符序列，使用 [!DNL Target] API 时通常需要使用此设置。 |
| [!UICONTROL IMS 组织 ID] | 此 ID 可将您的实施绑定到您的 Adobe Experience Cloud 帐户。 |
| [!UICONTROL 设备上决策] | 要启用设备上决策，请将切换开关滑动到“开”位置。<p>通过设备上决策，可在服务器上缓存A/B和体验定位(XT)营销活动，并以近乎零延迟的速度执行内存中决策。 有关更多信息，请参阅 [设备上决策简介](../../../server-side/sdk-guides/on-device-decisioning/overview.md). |
| [!UICONTROL 将所有符合设备端决策条件的活动都包含在项目中] | （视情况而定）如果您启用设备上决策，则会显示此选项。<p>如果要让所有活动内容都处于实时状态，请将切换开关滑动到“开”位置 [!DNL Target] 符合设备上决策资格的活动将自动包含在项目中。<p>将此开关保留为关闭状态表示您必须重新创建和激活任何设备上决策活动，才能将其包含在生成的规则工件中。 |

## 实施方法

可以在“实施方法”面板中配置以下设置：

### 全局设置

>[!NOTE]
>
>这些设置将应用于所有 [!DNL Target] .js库。 在“实施方法”部分中进行更改后，必须下载库并在实施中对其进行更新。

| 设置 | 描述 |
| --- | --- |
| [!UICONTROL 已启用页面加载（自动创建全局mbox）] | 选择是否要将全局 mbox 调用嵌入到 at.js 文件中，以使其在每次加载页面时自动触发。 |
| [!UICONTROL 全局 mbox] | 为全局 mbox 选择一个名称。默认情况下，此名称为 target-global-mbox。<p>使用 at.js 的 mbox 名称中可以使用特殊字符，包括与号 (&amp;)。 |
| [!UICONTROL 超时（秒）] | 如果 [!DNL Target] 未在定义的时间段内做出响应并显示相应内容，则服务器调用会超时，此时会显示默认内容。在访客会话期间会继续尝试发起其他调用。默认时间为 5 秒。<p>at.js 库使用的是 `XMLHttpRequest` 中的超时设置。超时从请求被触发时开始，直到 [!DNL Target] 收到来自服务器的响应时结束。有关更多信息，请参阅 Mozilla 开发人员网络上的 [XMLHttpRequest.timeout](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/timeout)。<p>如果在指定的超时内未收到响应，则会显示默认内容，且访客可能会被计为活动的参加者，因为所有数据收集都是在 [!DNL Target] 边缘网络中进行的。如果 [!DNL Target] 边缘网络收到了请求，则访客会被计为参加者。<p>配置超时设置时，请考虑以下事项：<ul><li>如果超时值过低，则用户大部分时间可能都会看到默认内容，即使访客可被计为活动参加者也是如此。</li><li>如果超时值过高，则在延长的时间段内，访客可能会在您的网页上看到空白区域，如果您使用了主体隐藏技术，则可能还会看到空白页面。</li></ul>要更好地了解 mbox 响应时间，请查看浏览器“开发人员工具”中的“网络”选项卡。您还可以使用第三方 Web 性能监测工具，例如 Catchpoint。<p>**注意**：[visitorApiTimeout](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#visitorapitimeout) 设置可确保 [!DNL Target] 等待访客 API 响应的时间不会太长。此设置和此处介绍的 at.js 中的“超时”设置不会相互影响。 |
| [!UICONTROL 配置文件生命周期] | 此设置可决定访客配置文件的存储时长。默认情况下，配置文件会存储两周时间。此设置最多可增加90天。<p>要更改“配置文件生命周期”设置，请联系[客户关怀团队](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html#reference_ACA3391A00EF467B87930A450050077C)。 |

### 主要实现方法

>[!NOTE]
>
>[!DNL Adobe Target]  同时支持at.js 1.*x* 与 at.js 2.*x* 之间的映射。升级到at.js任一主要版本的最新更新，以确保您运行的是受支持的版本。

要下载所需的at.js版本，请单击相应的 **下载** 按钮。

要编辑at.js设置，请单击 **[!UICONTROL 编辑]** ，位于所需的at.js版本旁边。

>[!WARNING]
>
>在更改这些默认设置之前，请咨询 [客户关怀](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html#reference_ACA3391A00EF467B87930A450050077C) 这样您就不会影响当前的实施。

除了上述设置之外，还提供以下特定的at.js设置：

| 设置 | 描述 |
|--- |--- |
| 跨域 | 对于at.js v1.*x*，指定跨域功能是否 `disabled` (浏览器在您的域中设置Cookie（仅限第一方Cookie）)， `x only` （浏览器仅在Target域中设置Cookie），或同时选择两者 `enabled` （浏览器同时设置第一方和第三方Cookie）。 对于at.js v2.10及更高版本，指定跨域功能是否 `enabled` （浏览器同时设置第一方和第三方Cookie）或 `disabled` （浏览器不设置第三方Cookie）。 |
| 自定义库标头 | 将任何自定义 JavaScript 添加到库顶部。 |
| 自定义库页脚 | 将任何自定义 JavaScript 添加到库底部。 |

### 配置文件API

可为通过 API 进行的批量更新启用或禁用身份验证，并生成配置文件身份验证令牌。

有关更多信息，请参阅 [配置文件API设置](/help/dev/before-implement/methods-to-get-data-into-target/profile-api-settings.md).

### 调试器工具

生成授权令牌以使用高级 [!DNL Target] 调试工具。 单击 **[!UICONTROL 生成新的身份验证令牌]**.

![生成新的身份验证令牌](../../../../before-implement/methods-to-get-data-into-target/assets/debugger-auth-token.png)

### 隐私

这些设置允许您使用 [!DNL Target] 符合适用的数据隐私法。

从模糊化访客IP地址下拉列表中选择所需的设置：

* 最后一个八位字节模糊处理
* 整个IP模糊处理
* 无

有关更多信息，请参阅[隐私](/help/dev/before-implement/privacy/privacy.md)。

>[!NOTE]
>
>at.js版本0.9.3及更低版本中提供了“旧版浏览器支持”选项。 at.js 版本 0.9.4 中已删除此选项。要获取 at.js 支持的浏览器列表，请参阅[受支持的浏览器](/help/dev/before-implement/supported-browsers.md)。<p>旧版浏览器是指早期推出的不完全支持 CORS（跨域资源共享）的浏览器。这些浏览器包括：Internet Explorer 版本 11 之前的浏览器，以及 Safari 版本 6 及更低版本。如果禁用了旧版浏览器支持， [!DNL Target] 在这些浏览器的报表中，不提供内容或对访客计数。 如果已启用此选项，则建议在旧版浏览器中执行质量保证操作，以确保获得良好的客户体验。

## 下载 at.js

使用下载库的说明 [!DNL Target] 界面或下载API。

>[!NOTE]
>
>[Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) 是实现的首选方法 [!DNL Target] 和at.js库。 以下信息不适用于在中使用标记 [!DNL Adobe Experience Platform] 实施 [!DNL Target].
>
>[!DNL Adobe Target] 同时支持at.js 1.*x* 与 at.js 2.*x* 之间的映射。请升级到任一主要版本的at.js的最新更新，以确保您运行的是受支持的版本。 有关每个版本中功能的更多信息，请参阅 [at.js 版本详细信息](/help/dev/implement/client-side/atjs/target-atjs-versions.md)。

### 使用下载at.js [!DNL Target] 界面

要从以下位置下载at.js： [!DNL Target] 界面：

1. 单击&#x200B;**[!UICONTROL “管理”]**>**[!UICONTROL “实现”]**。
1. 在“实施方法”部分，单击 **[!UICONTROL 下载]** 按钮中指定目标页面的at.js版本。

### 使用下载at.js [!DNL Target] 下载API

要使用 API 下载 at.js，请执行以下操作：

1. 获取您的客户端代码。

   您的客户端代码位于 **[!UICONTROL 管理]** > **[!UICONTROL 实现]** 第页，共 [!DNL Target] 界面。

1. 获取您的管理员编号。

   加载以下 URL：

   ```
   https://admin.testandtarget.omniture.com/rest/v1/endpoint/<varname>client code</varname>
   ```

   替换 `client code` 使用步骤1中的客户端代码。

   加载此 URL 后，应该会出现类似于以下示例的结果：

   ```
   { 
     "api": "https://admin6.testandtarget.omniture.com/admin/rest/v1" 
   }
   ```

   在此示例中，“6”表示管理员编号。

1. 下载 at.js.

   加载具有以下结构的URL。 加载此 URL 后，便会开始下载您的自定义 at.js 文件。

   ```
   https://admin<varname>admin number</varname>.testandtarget.omniture.com/admin/rest/v1/libraries/atjs/download?client=<varname>client code</varname>&version=<version number>
   ```

   * 替换 `admin number` 使用您的管理员编号。
   * 替换 `client code` 使用步骤1中的客户端代码。
   * 替换 `version number` 替换为所需的at.js版本号（例如，2.2）。

>[!WARNING]
>
>此 [!DNL Target] 团队仅维护两个版本的at.js：当前版本和当前版本的上一个版本。 请根据需要升级 at.js，以确保您运行的是受支持的版本。有关每个版本中功能的更多信息，请参阅 [at.js 版本详细信息](/help/dev/implement/client-side/atjs/target-atjs-versions.md)。

## at.js 实施

at.js 应该在您网站每个页面的 `<head>` 元素中实施。

的典型实施 [!DNL Target] 不使用标签管理器，例如中的标签 [Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md) 如下所示：

```
<!doctype html> 
<html> 
<head> 
    <meta charset="utf-8"> 
    <title>Title of the Page</title> 
    <!--Preconnect and DNS-Prefetch to improve page load time--> 
    <link rel="preconnect" href="//<client code>.tt.omtrdc.net"> 
    <link rel="dns-prefetch" href="//<client code>.tt.omtrdc.net"> 
    <!--/Preconnect and DNS-Prefetch--> 
    <!--Data Layer to enable rich data collection and targeting--> 
    <script> 
        var digitalData = { 
            "page": { 
                "pageInfo": { 
                    "pageName": "Home" 
                } 
            } 
        }; 
    </script> 
    <!--/Data Layer--> 
    <!-- targetPageParams(), targetPageParamsAll(), Data Providers or targetGlobalSettings() functions to enrich the visitor profile or modify the library settings--> 
    <script> 
        targetPageParams = function() { 
            return { 
                "a": 1, 
                "b": 2, 
                "pageName": digitalData.page.pageInfo.pageName, 
                "profile": { 
                    "age": 26, 
                    "country": { 
                        "city": "San Francisco" 
                    } 
                } 
            }; 
        }; 
    </script> 
    <!--/targetPageParams()--> 
 
    <!--jQuery or other helper libraries should be implemented before at.js if you would like to use their methods in Target--> 
    <script src="jquery-3.3.1.min.js"></script> 
    <!--/jQuery--> 
    <!--Target's JavaScript SDK, at.js--> 
    <script src="at.js"></script> 
    <!--/at.js--> 
</head>
<body> 
    The default content of the page 
</body> 
</html>
```

请注意以下重要说明：

* HTML5 Doctype(例如， `<!doctype html>`)。 不支持或较旧的doctypes可能会导致 [!DNL Target] 无法发出请求。
* “预连接”和“预提取”选项可帮助提升网页加载速度。如果您使用这些配置，请确保将 `<client code>` ，可从获取 **[!UICONTROL 管理]** > **[!UICONTROL 实现]** 页面。
* 如果您拥有数据层，那么在 at.js 加载之前，最好在页面的 `<head>` 中定义尽可能多的数据层。此位置提供了在中使用此信息的最大能力 [!DNL Target] 进行个性化。
* 特殊 [!DNL Target] 函数，如 `targetPageParams()`， `targetPageParamsAll()`、数据提供程序和 `targetGlobalSettings()` 应在数据层加载之后和at.js加载之前定义。 或者，这些函数也可以保存在“编辑at.js设置”页面的“库标题”部分中，并保存为at.js库本身的一部分。 有关这些函数的更多信息，请参见 [at.js函数](/help/dev/implement/client-side/atjs/atjs-functions/atjs-functions.md).
* 如果您使用JavaScript帮助程序库（例如jQuery），请在之前包含它们 [!DNL Target] 因此您可以在构建时使用它们的语法和方法 [!DNL Target] 体验。
* 将 at.js 包含在您页面的 `<head>` 中。

## 跟踪转化

订单确认 mbox 将记录您网站上订单的详细信息，并能够基于收入和订单生成报表。订单确认 mbox 还可驱动推荐算法，例如“购买了产品 x，也购买了产品 y 的人”。

>[!NOTE]
>
>如果用户在您的网站上进行购买，则Adobe建议实施订单确认mbox，即使您将Analytics用于 [!DNL Target] (A4T)作为您的报表。

1. 在订单详细信息页面，按照以下模式插入 mbox 脚本。
1. 使用您目录中的动态或静态值替换大写的文字。

   >[!TIP]
   >
   >您也可以在任意mbox（必须命名为）中传递订单信息 `orderConfirmPage`)。 还可以在同一营销活动之内的多个 mbox 中传递订单信息。

   ```
   <script type="text/javascript"> 
   adobe.target.trackEvent({ 
       "mbox": "orderConfirmPage", 
       "params":{  
           "orderId": "ORDER ID FROM YOUR ORDER PAGE",  
           "orderTotal": "ORDER TOTAL FROM YOUR ORDER PAGE",  
           "productPurchasedId": "PRODUCT ID FROM YOUR ORDER PAGE, PRODUCT ID2, PRODUCT ID3"  
       } 
   }); 
   </script> 
   ```

>[!NOTE]
>
>在订单确认mbox中，使用逗号分隔多个产品ID。

订单确认 mbox 使用以下参数：

| 参数 | 描述 |
|--- |--- |
| orderId | 针对转化计数标识订单的唯一值。<p>`orderId` 必须唯一。报表中会忽略重复订单。 |
| orderTotal | 所购产品的币值。<p>不要传递货币符号。使用小数点（而非逗号）表示小数值。 |
| productPurchasedId（可选） | 订单中所购产品的产品 ID（逗号分隔）列表。<p>这些产品 ID 显示在审计报表中，以支持其他报表分析。 |
