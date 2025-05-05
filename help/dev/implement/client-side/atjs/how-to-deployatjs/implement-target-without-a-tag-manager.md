---
keywords: 实施target，实施，实施at.js，标签管理器，设备上决策，设备决策
description: 了解如何指定设置（帐户详细信息、实施方法等） 在不使用标签管理器的情况下实施 [!DNL Adobe Target] at.js库。
title: 我可以在没有标签管理器的情况下实施 [!DNL Target] 吗？
feature: Implement Server-side
exl-id: f675ae21-105d-4aa3-9926-59291f1136b5
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1693'
ht-degree: 35%

---

# 不通过标签管理器实施[!DNL Target]

有关在不使用[!DNL Adobe Experience Platform]中的标记管理器或标记的情况下实现[!DNL Adobe Target]的信息。

>[!NOTE]
>
>[Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md)中的标记是实现[!DNL Target]和at.js库的首选方法。 使用[!DNL Adobe Experience Platform]中的标记实施[!DNL Target]时，以下信息不适用。

要访问“实现”页面，请单击&#x200B;**[!UICONTROL Administration]** > **[!UICONTROL Implementation]**。

您可以在此页上指定以下设置：

* 帐户详细信息
* 实施方法
* 配置文件API
* 调试器工具
* 隐私

>[!NOTE]
>
>您可以覆盖at.js库中的设置，而不是在[!DNL Target] Standard/Premium UI中或通过使用REST API来配置它们。 有关更多信息，请参阅 [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md)。

## 帐户详细信息

您可以查看以下帐户详细信息。 无法更改这些设置。

| 设置 | 描述 |
| --- | --- |
| [!UICONTROL Client Code] | 客户端代码是特定于客户端的字符序列，使用[!DNL Target] API时通常需要使用此序列。 |
| [!UICONTROL IMS Organization ID] | 此ID可将您的实施绑定到您的Adobe Experience Cloud帐户。 |
| [!UICONTROL On-Device Decisioning] | 要启用设备上决策，请将切换开关滑动到“开”位置。<p>通过设备上决策，可在服务器上缓存A/B和体验定位(XT)营销活动，并以近乎零延迟的速度执行内存中决策。 有关详细信息，请参阅[设备上决策简介](../../../server-side/sdk-guides/on-device-decisioning/overview.md)。 |
| [!UICONTROL Include all existing on-device decisioning qualified activities in the artifact] | （视情况而定）如果您启用设备上决策，则会显示此选项。<p>如果您希望所有符合设备上决策条件的实时[!DNL Target]活动自动包含在项目中，请将切换开关滑动到“开”位置。<p>将此开关保留为关闭状态表示您必须重新创建和激活任何设备上决策活动，才能将其包含在生成的规则工件中。 |

## 实施方法

可以在“实施方法”面板中配置以下设置：

### 全局设置

>[!NOTE]
>
>这些设置应用于所有[!DNL Target] .js库。 在“实施方法”部分中进行更改后，必须下载库并在实施中对其进行更新。

| 设置 | 描述 |
| --- | --- |
| [!UICONTROL Page load enabled (Auto-create global mbox)] | 选择是否要将全局 mbox 调用嵌入到 at.js 文件中，以使其在每次加载页面时自动触发。 |
| [!UICONTROL Global mbox] | 为全局 mbox 选择一个名称。默认情况下，此名称为 target-global-mbox。<p>对于at.js，mbox名称中可以使用特殊字符，包括与号(&amp;)。 |
| [!UICONTROL Timeout (seconds)] | 如果 [!DNL Target] 未在定义的时间段内做出响应并显示相应内容，则服务器调用会超时，此时会显示默认内容。在访客会话期间会继续尝试发起其他调用。默认时间为 5 秒。<p>at.js库使用`XMLHttpRequest`中的超时设置。 超时从请求被触发时开始，并在[!DNL Target]从服务器获得响应时停止。 有关详细信息，请参阅Mozilla开发人员网络上的[XMLHttpRequest.timeout](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/timeout)。<p>如果在指定的超时内未收到响应，则会显示默认内容，且访客可能会被计为活动的参与者，因为所有数据收集都发生在[!DNL Target]边缘。 如果请求到达[!DNL Target]边缘，则访客被计为参加者。<p>配置超时设置时，请考虑以下事项：<ul><li>如果超时值过低，则用户大部分时间可能都会看到默认内容，即使访客可被计为活动参加者也是如此。</li><li>如果超时值过高，则在延长的时间段内，访客可能会在您的网页上看到空白区域，如果您使用了主体隐藏技术，则可能还会看到空白页面。</li></ul>要更好地了解 mbox 响应时间，请查看浏览器“开发人员工具”中的“网络”选项卡。您还可以使用第三方 Web 性能监测工具，例如 Catchpoint。<p>**注意**： [visitorApiTimeout](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#visitorapitimeout)设置可确保[!DNL Target]等待访客API响应的时间不会太长。 此设置和此处介绍的 at.js 中的“超时”设置不会相互影响。 |
| [!UICONTROL Profile Lifetime] | 此设置可决定访客配置文件的存储时长。默认情况下，配置文件会存储两周时间。此设置最多可增加90天。<p>要更改配置文件生命周期设置，请联系[客户关怀团队](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html?lang=zh-Hans#reference_ACA3391A00EF467B87930A450050077C)。 |

### 主要实现方法

>[!NOTE]
>
>[!DNL Adobe Target]同时支持at.js 1。*x* 和 at.js 2 中的“隐藏主体”和“显示主体”调用。*x* 使用跨域跟踪功能时。升级到at.js任一主要版本的最新更新，以确保您运行的是受支持的版本。

要下载所需的at.js版本，请单击相应的&#x200B;**下载**&#x200B;按钮。

要编辑at.js设置，请单击所需的at.js版本旁边的&#x200B;**[!UICONTROL Edit]**。

>[!WARNING]
>
>在更改这些默认设置之前，请咨询[客户关怀团队](https://experienceleague.adobe.com/docs/target/using/cmp-resources-and-contact-information.html?lang=zh-Hans#reference_ACA3391A00EF467B87930A450050077C)，以免影响当前的实施。

除了上述设置之外，还提供以下特定的at.js设置：

| 设置 | 描述 |
|--- |--- |
| 跨域 | 对于at.js v1.*x*，通过选择`enabled`（浏览器同时设置第一方Cookie和第三方Cookie），指定跨域功能是`disabled` (浏览器仅在您的域中设置Cookie（第一方Cookie）)、`x only` （浏览器仅在Target的域中设置Cookie）还是同时设置这两者。 对于at.js v2.10及更高版本，请指定跨域功能是`enabled` （浏览器同时设置第一方Cookie和第三方Cookie）还是`disabled` （浏览器不设置第三方Cookie）。 |
| 自定义库标头 | 将任何自定义 JavaScript 添加到库顶部。 |
| 自定义库页脚 | 将任何自定义 JavaScript 添加到库底部。 |

### 配置文件API

可为通过 API 进行的批量更新启用或禁用身份验证，并生成配置文件身份验证令牌。

有关详细信息，请参阅[配置文件API设置](/help/dev/before-implement/methods-to-get-data-into-target/profile-api-settings.md)。

### 调试器工具

生成授权令牌以使用高级[!DNL Target]调试工具。 单击 **[!UICONTROL Generate New Authentication Token]**。

![生成新的身份验证令牌](../../../../before-implement/methods-to-get-data-into-target/assets/debugger-auth-token.png)

### 隐私

这些设置允许您按照适用的数据隐私法使用[!DNL Target]。

从模糊化访客IP地址下拉列表中选择所需的设置：

* 最后一个八位字节模糊处理
* 整个IP模糊处理
* 无

有关更多信息，请参阅[隐私](/help/dev/before-implement/privacy/privacy.md)。

>[!NOTE]
>
>at.js版本0.9.3及更低版本中提供了“旧版浏览器支持”选项。 at.js 版本 0.9.4 中已删除此选项。要获取 at.js 支持的浏览器列表，请参阅[受支持的浏览器](/help/dev/before-implement/supported-browsers.md)。<p>旧版浏览器是指早期推出的不完全支持 CORS（跨域资源共享）的浏览器。这些浏览器包括：Internet Explorer 版本 11 之前的浏览器，以及 Safari 版本 6 及更低版本。如果禁用了旧版浏览器支持，则[!DNL Target]不会在这些浏览器的报表中提供内容或计算访客数。 如果已启用此选项，则建议在旧版浏览器中执行质量保证操作，以确保获得良好的客户体验。

## 下载 at.js

有关使用[!DNL Target]界面或下载API下载库的说明。

>[!NOTE]
>
>[Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md)是实现[!DNL Target]和at.js库的首选方法。 使用[!DNL Adobe Experience Platform]中的标记实施[!DNL Target]时，以下信息不适用。
>
>[!DNL Adobe Target]同时支持at.js 1。*x* 和 at.js 2 中的“隐藏主体”和“显示主体”调用。*x* 使用跨域跟踪功能时。请升级到任一主要版本的at.js的最新更新，以确保您运行的是受支持的版本。 有关每个版本中功能的更多信息，请参阅 [at.js 版本详细信息](/help/dev/implement/client-side/atjs/target-atjs-versions.md)。

### 使用[!DNL Target]界面下载at.js

要从[!DNL Target]界面下载at.js，请执行以下操作：

1. 单击&#x200B;**[!UICONTROL Administration]** > **[!UICONTROL Implementation]**。
1. 在“实施方法”部分中，单击所需的at.js版本旁边的&#x200B;**[!UICONTROL Download]**&#x200B;按钮。

### 使用[!DNL Target]下载API下载at.js

要使用API下载at.js，请执行以下操作：

1. 获取您的客户端代码。

   您的客户端代码位于[!DNL Target]界面的&#x200B;**[!UICONTROL Administration]** > **[!UICONTROL Implementation]**&#x200B;页面顶部。

1. 获取您的管理员编号。

   加载以下 URL：

   ```
   https://admin.testandtarget.omniture.com/rest/v1/endpoint/<varname>client code</varname>
   ```

   将`client code`替换为步骤1中的客户端代码。

   加载此 URL 后，应该会出现类似于以下示例的结果：

   ```
   { 
     "api": "https://admin6.testandtarget.omniture.com/admin/rest/v1" 
   }
   ```

   在此示例中，“6”表示管理员编号。

1. 下载at.js。

   加载具有以下结构的URL。 加载此URL后，便会开始下载自定义的at.js文件。

   ```
   https://admin<varname>admin number</varname>.testandtarget.omniture.com/admin/rest/v1/libraries/atjs/download?client=<varname>client code</varname>&version=<version number>
   ```

   * 将`admin number`替换为您的管理员编号。
   * 将`client code`替换为步骤1中的客户端代码。
   * 将`version number`替换为所需的at.js版本号（例如，2.2）。

>[!WARNING]
>
>[!DNL Target]团队仅维护两个版本的at.js：当前版本和当前版本的上一个版本。 请根据需要升级at.js，以确保您运行的是受支持的版本。 有关每个版本中功能的更多信息，请参阅 [at.js 版本详细信息](/help/dev/implement/client-side/atjs/target-atjs-versions.md)。

## at.js 实施

at.js 应该在您网站每个页面的 `<head>` 元素中实施。

[!DNL Target]的典型实现不使用标签管理器，例如[Adobe Experience Platform](/help/dev/implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md)中的标签，如下所示：

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

* 应使用HTML5 Doctype（例如，`<!doctype html>`）。 不支持或更早的doctypes可能会导致[!DNL Target]无法发出请求。
* “预连接”和“预提取”选项可帮助提升网页加载速度。如果您使用这些配置，请确保将`<client code>`替换为您自己的客户端代码，此代码可从&#x200B;**[!UICONTROL Administration]** > **[!UICONTROL Implementation]**&#x200B;页面中获取。
* 如果您拥有数据层，那么在 at.js 加载之前，最好在页面的 `<head>` 中定义尽可能多的数据层。此位置提供了在[!DNL Target]中使用此信息进行个性化的最大能力。
* 特殊[!DNL Target]函数（如`targetPageParams()`、`targetPageParamsAll()`、数据提供程序和`targetGlobalSettings()`）应在数据层加载之后和at.js加载之前定义。 或者，这些函数也可以保存在“编辑at.js设置”页面的“库标题”部分中，并保存为at.js库本身的一部分。 有关这些函数的更多信息，请参阅[at.js函数](/help/dev/implement/client-side/atjs/atjs-functions/atjs-functions.md)。
* 如果您使用JavaScript帮助程序库（如jQuery），请在[!DNL Target]之前包含它们，以便在构建[!DNL Target]体验时可以使用它们的语法和方法。
* 将 at.js 包含在您页面的 `<head>` 中。

## 跟踪转化

订单确认 mbox 将记录您网站上订单的详细信息，并能够基于收入和订单生成报表。订单确认 mbox 还可驱动推荐算法，例如“购买了产品 x，也购买了产品 y 的人”。

>[!NOTE]
>
>如果用户在您的网站上进行购买，Adobe建议实施订单确认mbox，即使您使用Analytics for [!DNL Target] (A4T)进行报表也是如此。

1. 在订单详细信息页面，按照以下模式插入 mbox 脚本。
1. 使用您目录中的动态或静态值替换大写的文字。

   >[!TIP]
   >
   >您也可以在任意mbox中传递订单信息（名称不必是`orderConfirmPage`）。 还可以在同一营销活动之内的多个 mbox 中传递订单信息。

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
| orderId | 针对转化计数标识订单的唯一值。<p>`orderId` 必须是唯一的。报表中会忽略重复订单。 |
| orderTotal | 所购产品的币值。<p>请勿传递货币符号。使用小数点（而非逗号）表示小数值。 |
| productPurchasedId（可选） | 订单中所购产品的产品 ID（逗号分隔）列表。<p>这些产品 ID 显示在审计报告中以支持其他报告分析。 |
