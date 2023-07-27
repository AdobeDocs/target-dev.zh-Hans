---
title: 如何使用投放API获取Recommendations
description: 本文会指导开发人员完成使用Adobe Target交付API获取推荐内容所需的步骤。
feature: APIs/SDKs, Recommendations, Administration & Configuration
kt: 3815
thumbnail: null
author: Judy Kim
exl-id: 9b391f42-2922-48e0-ad7e-10edd6125be6
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '1521'
ht-degree: 1%

---

# 使用投放API获取Recommendations

Adobe Target和Adobe Target Recommendations API可用于提供对网页的响应，也可用于不基于HTML的体验，包括应用程序、屏幕、控制台、电子邮件、网亭和其他显示设备。 换句话说，当无法使用Target库和JavaScript时， [Target投放API](/help/dev/implement/delivery-api/overview.md) 仍然允许访问所有的Target功能，以便提供个性化的体验。

>[!NOTE]
>
>在请求包含实际推荐（推荐产品或项目）的内容时，请使用Target交付API。

要检索推荐，请发送包含相应上下文信息的Adobe Target交付APIPOST调用，其中可能包括用户ID（用于用户最近查看过的项目等特定于配置文件的推荐）、相关mbox名称、mbox参数、配置文件参数或其他属性。 响应将包含JSON或HTML格式的推荐entity.ids（并可能包含其他实体数据），这些数据随后可以显示在设备中。

此 [投放API](/help/dev/implement/delivery-api/overview.md) for Adobe Target会公开标准Target请求提供的所有现有功能。

投放API：

* 使您能够以RESTful方式检索位置和受众的体验或选件。
* 无需身份验证。
* 仅限帖子。
* 不处理Cookie或重定向调用。
* 不需要或识别“用户角色”。 它只是获取内容或向Target边缘服务器报告事件。

要使用交付API来交付Target体验（包括推荐），请执行以下步骤：

1. 使用基于表单的编辑器（而非可视化体验编辑器）创建Target活动(A/B、XT、AP或Recommendations)。
1. 使用交付API获取对刚刚创建的Target活动生成的请求的响应。

&lt;! — 问：为何需要同时采取这两个步骤？ 如果您为mbox定义了基于表单的推荐，那么也通过投放API步骤来检索结果有什么好处？ 为什么不能让基于表单的Rec将结果传送到目标设备……?? 答：请参阅下面的用例……这是您希望“拦截”待处理结果，以便在显示结果之前执行更多操作的情况。 与库存水平进行实时比较等。 --->

## 使用基于表单的体验编辑器创建推荐

要创建可与Delivery API一起使用的推荐，请使用 [基于表单的编辑器](https://experienceleague.adobe.com/docs/target/using/experiences/form-experience-composer.html).

1. 首先，创建并保存要在推荐中使用的基于JSON的设计。 有关示例JSON以及有关在配置基于表单的活动时如何返回JSON响应的背景信息，请参阅相关的文档 [创建推荐设计](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-design/create-design.html). 在此示例中，设计名为 *简单JSON。*
   ![server-side-create-recs-json-design.png](assets/server-side-create-recs-json-design.png)

1. 在Target中，导航到 **[!UICONTROL 活动]** > **[!UICONTROL 创建活动]** > **[!UICONTROL Recommendations]**，然后选择 **[!UICONTROL 表单]**.

   ![server-side-create-recs.png](assets/server-side-create-recs.png)

1. 选择一个资产，然后单击 **[!UICONTROL 下一个]**.
1. 定义您希望用户收到推荐响应的位置。 以下示例使用名为的位置 *api_charter*. 选择您之前创建的基于JSON的名为的设计 *简单JSON。*
   ![server-side-create-recs-form.png](assets/server-side-create-recs-form1.png)
1. 保存并激活推荐。 那个产生结果。 [一旦结果准备好](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-activity/previewing-and-launching-your-recommendations-activity.html)，您可以使用交付API检索它们。

## 使用投放API

的语法 [投放API](/help/dev/implement/delivery-api/overview.md) 为：

`POST https://{{CLIENT_CODE}}.tt.omtrdc.net/rest/v1/delivery`

1. 请注意，客户端代码为必填项。 提醒一下，您可以通过导航到，在Adobe Target中找到您的客户端代码 **[!UICONTROL Recommendations]** > **[!UICONTROL 设置]**. 请注意 **客户代码** 中的值 **推荐API令牌** 部分。
   ![client-code.png](assets/client-code.png)
1. 获得客户端代码后，即可构建投放API调用。 下面的示例以 **[!UICONTROL Web批处理Mbox投放API调用]** 中提供 [投放API Postman收藏集](../../implement/delivery-api/overview.md/#section/Getting-Started/Postman-Collection)，进行相关修改。 例如：
   * 该 **浏览器** 和 **地址** 对象已从 **正文**，因为非HTML用例不需要这些参数
   * *api_charter* 在此示例中列为位置名称
   * 指定了entity.id，因为此推荐基于内容相似度，它要求将当前项目键传递到Target。
     ![server-side-Delivery-API-call.png](assets/server-side-delivery-api-call2.png)
请记住正确配置查询参数。 例如，确保指定 `{{CLIENT_CODE}}` 视需要而定。 &lt;!— Q：在更新的调用语法中，entity.id作为profileParameter列出，而不作为mboxParameter在旧版本中列出。 ---> &lt;! — 问：旧图像 ![server-side-create-recs-post.png](assets/server-side-create-recs-post.png) 旧的随附文本：“请注意，此推荐基于基于mboxParameters发送的entity.id的‘内容类似’产品。” — >
     ![client-code3](assets/client-code3.png)
1. 发送请求。 此项针对执行 *api_charter* 位置上运行有活动推荐，该位置使用JSON设计定义，将输出推荐实体列表。
1. 接收基于JSON设计的响应。
   ![server-side-create-recs-json-response2.png](assets/server-side-create-recs-json-response2.png)
响应包括键ID以及推荐实体的实体ID。

通过这种方式将投放API与Recommendations结合使用，您可以在向非HTML设备上的访客显示推荐之前，执行其他步骤。 例如，您可以在显示最终结果之前，从投放API获得响应，以从另一个系统（例如CMS、PIM或电子商务平台）执行额外的实体属性详细信息（库存、价格、评级等）实时查找。

使用本指南中概述的方法，您可以获得任何应用程序来利用Target的响应提供个性化推荐！

## 实施示例

以下资源提供了各种以非HTML为重点的实施示例。 请记住，由于涉及的系统和设备，每个实施都是唯一的。

| 资源 | 详细信息 |
| --- | --- |
| [Adobe Target Everywhere — 在服务器端或物联网中实施](https://expleague.azureedge.net/labs/L733/index.html) | Adobe Summit2019实验室，为利用Adobe Target服务器端API的React应用程序提供实践体验。 |
| [移动设备应用程序中的Adobe Target(不带AdobeSDK)](https://community.tealiumiq.com/t5/Universal-Data-Hub/Adobe-Target-in-a-Mobile-App-Without-the-Adobe-SDK/ta-p/26753) | 本指南向您展示如何在不安装Adobe Target SDK的情况下在移动应用程序中设置Adobe。 此解决方案使用Tealium SDK Webview和远程命令模块向Adobe访客API(Experience Cloud)和Adobe Target API发送请求并进行接收。 |
| [Adobe Target在移动设备应用程序中的工作原理](../../implement/mobile/how-target-works-mobile-apps.md) | Target如何与Mobile SDK配合使用 |
| [在Experience Platform Launch和实施Target API中配置Target扩展](https://developer.adobe.com/client-sdks/documentation/adobe-target/) | 在Experience Platform Launch中配置Target扩展、将Target扩展添加到您的应用程序以及实施Target API以请求活动、预取选件和进入可视化预览模式的步骤。 |
| [Adobe Target节点客户端](https://www.npmjs.com/package/@adobe/target-nodejs-sdk) | 开源Target Node.js SDK v1.0 |
| [服务器端概述](../../implement/server-side/server-side-overview.md) | 有关Adobe Target服务器端交付API、服务器端批量交付API、Node.js SDK和Adobe Target Recommendations API的信息。 |
| [电子邮件中的Adobe Campaign Content Recommendations](https://medium.com/adobetech/adobe-campaign-content-recommendations-in-email-b51ced771d7f) | 介绍如何在Adobe Campaign中通过Adobe Target和Adobe I/O Runtime利用电子邮件中的内容推荐的博客。 |

## 使用API管理Recommendations设置

大多数情况下，出于以上部分所述的原因，推荐是在Adobe Target UI中配置，然后通过Target API使用或访问。 这种UI-API协调是常见的。 但是，有时，用户可能希望通过API执行所有操作 — 包括设置和结果使用。 尽管不太常见，但用户可以完全配置、执行 *和* 完全使用API来利用推荐的结果。

我们在 [上一节](manage-catalog.md) 如何管理Adobe Target Recommendations实体并在服务器端交付它们。 同样地， [Adobe Developer控制台](https://developer.adobe.com/console/home) 让您无需登录Adobe Target即可管理标准、促销活动、收藏集和设计模板。 可以找到所有Recommendations API的完整列表 [此处](http://developers.adobetarget.com/api/recommendations/)，但此处提供了一份摘要以供参考。

| 资源 | 详细信息 |
| --- | --- |
| [收藏集](http://developers.adobetarget.com/api/recommendations/#tag/Collections) | 列出、创建、获取、编辑和删除收藏集。 |
| [标准](http://developers.adobetarget.com/api/recommendations/#tag/Criteria) | 列出并获取条件。 |
| [设计](http://developers.adobetarget.com/api/recommendations/#tag/Designs) | 列出、创建、获取、编辑、删除和验证设计。 |
| [实体](http://developers.adobetarget.com/api/recommendations/#tag/Entities) | 保存、删除和获取实体。 |
| [促销活动](http://developers.adobetarget.com/api/recommendations/#tag/Promotions) | 列出、创建、获取、编辑和删除促销活动。 |
| [类别标准](http://developers.adobetarget.com/api/recommendations/#tag/Category-Criteria) | 列出、创建、获取、编辑和删除类别标准。 |
| [自定义标准](http://developers.adobetarget.com/api/recommendations/#tag/Custom-Criteria) | 列出、创建、获取、编辑和删除自定义标准。 |
| [项目条件](http://developers.adobetarget.com/api/recommendations/#tag/Item-Criteria) | 列出、创建、获取、编辑和删除项目标准。 |
| [热门程度标准](http://developers.adobetarget.com/api/recommendations/#tag/Popularity-Criteria) | 列出、创建、获取、编辑和删除热门程度标准。 |
| [配置文件属性标准](http://developers.adobetarget.com/api/recommendations/#tag/Profile-Attribute-Criteria) | 列出、创建、获取、编辑和删除配置文件属性标准。 |
| [最新标准](http://developers.adobetarget.com/api/recommendations/#tag/Recent-Criteria) | 列出、创建、获取、编辑和删除最近使用的标准。 |
| [序列标准](http://developers.adobetarget.com/api/recommendations/#tag/Sequence-Criteria) | 列出、创建、获取、编辑和删除序列标准。 |

## 参考文档

* [Adobe Target交付API文档](/help/dev/implement/delivery-api/overview.md)
* [将“推荐”与电子邮件集成](https://experienceleague.adobe.com/docs/target/using/recommendations/recommendations-faq/integrating-recs-email.html)

## 摘要和审查

恭喜！通过完成本指南，您已了解如何：
* [使用Recommendations API管理您的目录](manage-catalog.md)
* [使用Recommendations API管理自定义标准](manage-custom-criteria.md)
* [在Recommendations中使用交付API](fetch-recs-server-side-delivery-api.md)
