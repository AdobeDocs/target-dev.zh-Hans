---
user-guide-title: Adobe Target开发人员指南
breadcrumb-title: Target开发人员指南
user-guide-description: 了解如何定制和个性化客户体验，从而最大限度地提升网站和移动网站、应用程序、社交媒体和其他数字渠道的收入。
source-git-commit: 524eb6aea6141d69eb7f30795d6b16a3f07cccd9
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 44%

---


# Adobe Target开发人员指南 {#developer}

+ [Adobe Target开发人员指南](overview.md)
+ 入门指南 {#implementation}
   + 实施之前 {#before-implement}
      + [实施之前](before-implement/considerations-before-you-implement-target.md)
      + [准备实施 Target](before-implement/prepare-to-implement-target.md)
   + 隐私和安全性 {#privacy}
      + [隐私概述](before-implement/privacy/privacy.md)
      + [隐私和数据保护法规](before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md)
      + [Target Cookie](before-implement/privacy/cookie-behavior.md)
      + [删除 Target Cookie](before-implement/privacy/cookie-deleting.md)
      + [第三方Cookie弃用对Target (at.js)的影响](/help/dev/before-implement/privacy/third-party-cookie-deprecation.md)
      + [Google Chrome SameSite Cookie 策略](before-implement/privacy/google-chrome-samesite-cookie-policies.md)
      + [Apple 智能防跟踪 (ITP) 2.x](before-implement/privacy/apple-itp-2x.md)
      + [内容安全策略 (CSP) 指令](before-implement/privacy/content-security-policy.md)
      + [将 Target 边缘节点列入允许列表](before-implement/privacy/allowlist-edges.md)
   + 将数据导入 Target 的方法 {#methods}
      + [方法概述](before-implement/methods-to-get-data-into-target/methods-to-get-data-into-target.md)
      + [页面参数](before-implement/methods-to-get-data-into-target/page-parameters.md)
      + [页面内轮廓属性](before-implement/methods-to-get-data-into-target/in-page-profile-attributes.md)
      + [脚本轮廓属性](before-implement/methods-to-get-data-into-target/script-profile-attributes.md)
      + [数据提供程序](before-implement/methods-to-get-data-into-target/data-providers.md)
      + [批量配置文件更新API](before-implement/methods-to-get-data-into-target/bulk-profile-update-api.md)
      + [单个配置文件更新API](before-implement/methods-to-get-data-into-target/single-profile-update-api.md)
      + [客户属性](before-implement/methods-to-get-data-into-target/customer-attributes.md)
      + [轮廓 API 设置](before-implement/methods-to-get-data-into-target/profile-api-settings.md)
   + [Target 安全概述](before-implement/target-security-overview.md)
   + [支持的浏览器](before-implement/supported-browsers.md)
   + [TLS（传输层安全性）加密更改](before-implement/tls-transport-layer-security-encryption.md)
   + [CNAME 和 Adobe Target](before-implement/implement-cname-support-in-target.md)
+ 客户端实施 {#client-side}
   + [概述：为客户端 Web 实施 Target](implement/client-side/overview.md)
   + Adobe Experience Platform Web SDK实施 {#aep}
      + [Adobe Experience Platform Web SDK实施概述](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md)
      + [单页应用程序实施](/help/dev/implement/client-side/aep-web-sdk/spa-implementation.md)
      + [访问响应令牌](/help/dev/implement/client-side/aep-web-sdk/accessing-response-tokens.md)
      + [将at.js库与Platform Web SDK进行比较](/help/dev/implement/client-side/aep-web-sdk/web-sdk-atjs-comparison.md)
   + at.js 实施 {#at-js-implementation}
      + [at.js概述](implement/client-side/atjs/how-atjs-works/overview.md)
      + at.js 的工作原理 {#at-js}
         + [at.js 的工作原理概述](implement/client-side/atjs/how-atjs-works/how-atjs-works.md)
         + [at.js 如何管理闪烁](implement/client-side/atjs/how-atjs-works/manage-flicker-with-atjs.md)
         + [at.js 集成](implement/client-side/atjs/how-atjs-works/target-atjs-integrations.md)
      + 如何部署 at.js {#deploy-at-js}
         + [如何部署 at.js](implement/client-side/atjs/how-to-deployatjs/how-to-deployatjs.md)
         + [使用 Adobe Experience Platform 实施 Target](implement/client-side/atjs/how-to-deployatjs/implement-target-using-adobe-launch.md)
         + [不通过标记管理器实施 Target](implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md)
         + [使用动态标记管理器 (DTM) 实施 Target](implement/client-side/atjs/how-to-deployatjs/implement-target-using-dtm.md)
         + [为单页面应用程序 (SPA) 实施 Target](implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md)
      + 设备上决策 {#on-device-decisioning}
         + [设备上决策概述](implement/client-side/atjs/on-device-decisioning/on-device-decisioning.md)
         + [受支持的功能](implement/client-side/atjs/on-device-decisioning/supported-features.md)
         + [规则构件](implement/client-side/atjs/on-device-decisioning/rule-artifact.md)
         + [故障排除](implement/client-side/atjs/on-device-decisioning/troubleshooting-on-device-decisioning.md)
      + at.js 函数 {#functions-overview}
         + [at.js 函数概述](implement/client-side/atjs/atjs-functions/atjs-functions.md)
         + [adobe.target.getOffer()](implement/client-side/atjs/atjs-functions/adobe-target-getoffer.md)
         + [adobe.target.getOffers() - at.js 2.x](implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)
         + [adobe.target.applyOffer()](implement/client-side/atjs/atjs-functions/adobe-target-applyoffer.md)
         + [adobe.target.applyOffers() - at.js 2.x](implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)
         + [adobe.target.triggerView() - at.js 2.x](implement/client-side/atjs/atjs-functions/adobe-target-triggerview-atjs-2.md)
         + [adobe.target.trackEvent()](implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)
         + [mboxCreate() - at.js 1.x](implement/client-side/atjs/atjs-functions/mboxcreate-atjs.md)
         + [targetGlobalSettings()](implement/client-side/atjs/atjs-functions/targetglobalsettings.md)
         + [mboxDefine() 和 mboxUpdate() - at.js 1.x](implement/client-side/atjs/atjs-functions/mboxdefine-mboxupdate-atjs-1x.md)
         + [targetPageParams()](implement/client-side/atjs/atjs-functions/targetpageparams.md)
         + [targetPageParamsAll()](implement/client-side/atjs/atjs-functions/targetpageparamsall.md)
         + [registerExtension() - at.js 1.x](implement/client-side/atjs/atjs-functions/registerextension-atjs-1x.md)
         + [sendNotifications() - at.js 2.1](implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21.md)
         + [at.js 自定义事件](implement/client-side/atjs/atjs-functions/atjs-custom-events.md)
         + [使用 Adobe Experience Cloud Debugger 调试 at.js](implement/client-side/target-debugging-atjs/target-debugging-atjs.md)
         + [结合使用基于云的实例和 Target](implement/client-side/target-debugging-atjs/targeting-using-cloud-based-instances.md)
      + [at.js 常见问题解答](implement/client-side/atjs/target-atjs-faq.md)
      + [at.js 版本详细信息](implement/client-side/atjs/target-atjs-versions.md)
      + [从 at.js 1.x 升级到 at.js 2.x](implement/client-side/atjs/upgrading-from-atjs-1x-to-atjs-20.md)
      + [at.js Cookie](implement/client-side/atjs/atjs-cookies.md)
   + [用户代理和客户端提示](implement/client-side/atjs/user-agent-and-client-hints.md)
   + 了解全局 mbox {#global-mbox}
      + [了解全局 mbox 概述](implement/client-side/atjs/global-mbox/global-mbox-overview.md)
      + [自定义全局 mbox](implement/client-side/atjs/global-mbox/customize-global-mbox.md)
      + [使用旧版实施中的全局 mbox](implement/client-side/atjs/global-mbox/mbox-global-target-standard.md)
      + [将参数传递到全局 mbox](implement/client-side/atjs/global-mbox/pass-parameters-to-global-mbox.md)
      + [全局 mbox 常见问题解答](implement/client-side/atjs/global-mbox/global-mbox-faq.md)
+ 服务器端实施 {#server-side}
   + [服务器端：实施 Target 概述](implement/server-side/server-side-overview.md)
   + [Target SDK快速入门](implement/server-side/sdk-guides/getting-started/getting-started.md)
   + [示例应用程序](implement/server-side/sdk-guides/sample-apps/sample-apps.md)
   + [从 Target 旧版 API 迁移到 Adobe I/O](implement/server-side/transition-from-target-classic-apis.md)
   + 核心原则 {#core-principles}
      + [核心原则概述](implement/server-side/sdk-guides/core-principles/overview.md)
      + [用户ID和分段](implement/server-side/sdk-guides/core-principles/user-identification-and-bucketing.md)
      + [受众定位](implement/server-side/sdk-guides/core-principles/audience-targeting.md)
      + [事件跟踪](implement/server-side/sdk-guides/core-principles/event-tracking.md)
      + [用户权限和属性](implement/server-side/sdk-guides/core-principles/user-permissions-and-properties.md)
   + 集成 {#integration}
      + [集成概述](implement/server-side/sdk-guides/integration-with-experience-cloud/overview.md)
      + [Experience Cloud ID服务(ECID)](implement/server-side/sdk-guides/integration-with-experience-cloud/ecid.md)
      + [Analytics for Target (A4T) 报表](implement/server-side/sdk-guides/integration-with-experience-cloud/a4t-reporting.md)
      + [AAM 区段](implement/server-side/sdk-guides/integration-with-experience-cloud/aam-segments.md)
   + 设备上决策 {#on-device-decisioning}
      + [设备上决策概述](implement/server-side/sdk-guides/on-device-decisioning/overview.md)
      + 规则构件 {#rule-artifact}
         + [规则工件概述](implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md)
         + [通过Adobe Target SDK下载](implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-sdk.md)
         + [通过JSON有效负载下载](implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-json.md)
         + [示例规则构件](implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-example.md)
      + [使用功能标志执行A/B测试](implement/server-side/sdk-guides/on-device-decisioning/execute-ab-tests-with-feature-flags.md)
      + [使用属性执行功能测试](implement/server-side/sdk-guides/on-device-decisioning/execute-feature-tests-with-attributes.md)
      + [管理功能测试的转出](implement/server-side/sdk-guides/on-device-decisioning/manage-rollouts-for-feature-tests.md)
      + [提供个性化](implement/server-side/sdk-guides/on-device-decisioning/deliver-personalization.md)
      + [支持的功能概述](implement/server-side/sdk-guides/on-device-decisioning/supported-features.md)
      + [设备上决策疑难解答](implement/server-side/sdk-guides/on-device-decisioning/troubleshooting.md)
      + [最佳实践](implement/server-side/sdk-guides/best-practices/best-practices.md)
   + Node.js SDK参考 {#node-js}
      + [Node.js SDK概述](implement/server-side/node-js/overview.md)
      + [安装Node.js SDK](implement/server-side/node-js/install-sdk.md)
      + [初始化Node.js SDK](implement/server-side/node-js/initialize-sdk.md)
      + [获取选件(Node.js)](implement/server-side/node-js/get-offers.md)
      + [获取属性(Node.js)](implement/server-side/node-js/get-attributes.md)
      + [发送通知(Node.js)](implement/server-side/node-js/send-notifications.md)
      + [SDK事件(Node.js)](implement/server-side/node-js/sdk-events.md)
      + [记录器(Node.js)](implement/server-side/node-js/logger.md)
      + [代理配置(Node.js)](implement/server-side/node-js/proxy-configuration.md)
   + Java SDK参考 {#java}
      + [Java SDK概述](implement/server-side/java/overview.md)
      + [安装Java SDK](implement/server-side/java/install-sdk.md)
      + [初始化Java SDK](implement/server-side/java/initialize-sdk.md)
      + [获取选件(Java)](implement/server-side/java/get-offers.md)
      + [获取属性(Java)](implement/server-side/java/get-attributes.md)
      + [发送通知(Java)](implement/server-side/java/send-notifications.md)
      + [SDK Events (Java)](implement/server-side/java/sdk-events.md)
      + [Logger (Java)](implement/server-side/java/logger.md)
      + [异步请求(Java)](implement/server-side/java/asynchronous-requests.md)
      + [代理配置(Java)](implement/server-side/java/proxy-configuration.md)
      + [自定义HTTP客户端配置(Java)](implement/server-side/java/custom-http-client.md)
      + [实用程序方法(Java)](implement/server-side/java/utility-methods.md)
   + .NET SDK参考 {#net}
      + [.NET SDK概述](implement/server-side/net/overview.md)
      + [安装.Net SDK](implement/server-side/net/install-sdk.md)
      + [初始化.NET SDK](implement/server-side/net/initialize-sdk.md)
      + [获取选件(.NET)](implement/server-side/net/get-offers.md)
      + [获取属性(.NET)](implement/server-side/net/get-attributes.md)
      + [发送通知(.NET)](implement/server-side/net/send-notifications.md)
      + [SDK事件(.NET)](implement/server-side/net/sdk-events.md)
      + [异步请求(.NET)](implement/server-side/net/asynchronous-requests.md)
   + Python SDK参考 {#python}
      + [Python SDK概述](implement/server-side/python/overview.md)
      + [安装Python SDK](implement/server-side/python/install-sdk.md)
      + [初始化Python SDK](implement/server-side/python/initialize-sdk.md)
      + [获取选件(Python)](implement/server-side/python/get-offers.md)
      + [获取属性(Python)](implement/server-side/python/get-attributes.md)
      + [发送通知(Python)](implement/server-side/python/send-notifications.md)
      + [SDK Events (Python)](implement/server-side/python/sdk-events.md)
      + [异步请求(Python)](implement/server-side/python/asynchronous-requests.md)
      + [Logger (Python)](implement/server-side/python/logger.md)
+ [混合实施](implement/hybrid/hybrid-overview.md)
+ [Recommendations实施](implement/recommendations/recommendations.md)
+ [Recommendations实施测试版](/help/dev/implement/recommendations/recommendations-beta.md)
+ 移动应用程序实施 {#mobile-apps}
   + [适用于移动应用程序的 Target 概述](implement/mobile/overview.md)
   + [Target 移动设备预览](implement/mobile/target-mobile-preview.md)
   + [使用位置服务](implement/mobile/use-location-service.md)
   + [Target 移动应用程序版常见问题解答](implement/mobile/mobile-faq.md)
   + [在具有Web视图的本机应用程序中使用AEP Mobile SDK实施Target](/help/dev/implement/mobile/native-app.md)
+ 电子邮件实施 {#implement-email}
   + [电子邮件：实施 Target 概述](implement/email/overview.md)
   + [为图像创建 Adbox](implement/email/testing-content-with-the-adbox.md)
   + [测试电子邮件图像 Adbox](implement/email/testing-email-image-adbox.md)
   + [使用重定向程序](implement/email/working-with-redirectors.md)
+ API指南 {#api}
   + [Target API概述](/help/dev/before-administer/target-api-overview.md)
   + [为Target API配置身份验证](/help/dev/before-administer/configure-authentication.md)
   + 投放API指南 {#delivery-api}
      + [投放API概述](/help/dev/implement/delivery-api/overview.md)
      + [用于与投放API交互的SDK](/help/dev/before-implement/delivery-api-overview/sdks.md)
      + [入门指南](/help/dev/before-implement/delivery-api-overview/getting-started.md)
      + [用户权限(Premium)](/help/dev/before-implement/delivery-api-overview/user-permissions.md)
      + [识别访客](/help/dev/before-implement/delivery-api-overview/identifying-visitors.md)
      + [单次或批量交付](/help/dev/before-implement/delivery-api-overview/single-or-batch.md)
      + [预取](/help/dev/before-implement/delivery-api-overview/prefetch.md)
      + [通知](/help/dev/before-implement/delivery-api-overview/notifications.md)
      + [与Experience Cloud集成](before-implement/delivery-api-overview/integration.md)
      + [注意事项和已知限制](/help/dev/before-implement/delivery-api-overview/known-limitations.md)
      + [客户端提示](/help/dev/before-implement/delivery-api-overview/client-hints.md)
      + [投放 API](/help/dev/implement/delivery-api/delivery-api.md)
   + 管理员API {#admin-api}
      + [管理员API概述](before-administer/admin-api-overview/admin-api-overview.md)
      + [Adobe Target管理API](/help/dev/administer/admin-api/admin-api-overview-new.md)
   + 配置文件API {#profile-apis}
      + [配置文件API概述](/help/dev/administer/profile-api/profiles-api.md)
      + [获取配置文件](/help/dev/administer/profile-api/profile-fetch.md)
      + [更新用户档案](/help/dev/administer/profile-api/profile-api-overview.md)
      + [单个配置文件更新API](/help/dev/administer/profile-api/profile-single-api.md)
      + [批量配置文件更新API](/help/dev/administer/profile-api/profile-bulk-api.md)
   + [报表 API](/help/dev/administer/reporting-api/reporting-api.md)
   + 推荐API {#recommendations-api}
      + [推荐API概述](before-administer/recs-api/overview.md)
      + [使用API管理您的目录](before-administer/recs-api/manage-catalog.md)
      + [管理自定义标准](before-administer/recs-api/manage-custom-criteria.md)
      + [将投放API与推荐配合使用](before-administer/recs-api/fetch-recs-server-side-delivery-api.md)
      + [推荐API](/help/dev/administer/recommendations-api/recommendations-api.md)
   + 模型API {#models-api}
      + [模型API(列入阻止列表)概述](before-administer/models-api.md)
      + [模型API](/help/dev/administer/models-api/models-api-overview.md)
   + [ADOBE ADMIN CONSOLE API](/help/dev/before-implement/delivery-api-overview/adobe-console-api.md)
   + [Adobe Experience Platform Edge Network服务器API](/help/dev/before-implement/delivery-api-overview/aep-edge-network-server-api.md)
+ 实施模式 {#implementation-patterns}
   + [实施模式概述](/help/dev/patterns/pattern-overview.md)
   + 使用at.js的“推荐”实施模式 {#atjs}
      + [使用at.js的“推荐”实施模式概述](/help/dev/patterns/recs-atjs/recs-implementation-pattern-atjs.md)
      + [初始化SDK](/help/dev/patterns/recs-atjs/initialize-sdk.md)
      + [配置数据收集](/help/dev/patterns/recs-atjs/data-collection.md)
      + [渲染体验](/help/dev/patterns/recs-atjs/render-experiences.md)
      + [通知Target](/help/dev/patterns/recs-atjs/notify-target.md)


