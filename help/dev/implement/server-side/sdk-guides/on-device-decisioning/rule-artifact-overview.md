---
title: 了解设备上决策规则构件
description: 了解如何使用规则构件，它是 [!DNL Adobe Target] [!UICONTROL on-device decisioning]活动的JSON表示形式。
feature: APIs/SDKs
exl-id: 3dfb08df-eaa9-43d4-b009-e5f64c3a96d7
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# 规则工件概述

规则工件是[!DNL Adobe Target] [!UICONTROL on-device decisioning]活动的JSON表示形式。 它由[!DNL Adobe Target]生成并传播到Akamai CDN，以确保有一个尽可能接近最终用户的规则工件。 它包含元数据，可确保准确执行和交付活动，同时允许通过事件跟踪进行实时分析。 [!DNL Adobe Target] SDK的配置方式可允许自动管理规则构件，根据用户指定的时间间隔可下载或更新该构件。 此外，您还可以使用分布式内存缓存系统（如[Memcached](https://memcached.org/)）维护自己的规则工件的本地副本，以初始化[!DNL Adobe Target] SDK，以便无状态服务器可以立即处理请求。 要了解有关这些选项的更多信息，请参阅以下指南：

* [通过 [!DNL Adobe Target] SDK自动下载、存储和更新规则构件](rule-artifact-sdk.md)
* [通过JSON有效负载下载、存储和更新规则构件](rule-artifact-json.md)

## 示例规则构件

单击此处查看[规则构件](rule-artifact-example.md)的示例。

## 如何查看客户端的规则构件

启用跟踪将输出[!DNL Adobe Target]中有关规则工件的其他信息，特别是URL。

1. 导航到Target UI。

   &lt;！ — 插入image-target-ui-1.png —>
   ![替代图像](assets/asset-rule-artifact-1.png)

1. 导航到&#x200B;**[!UICONTROL Administration]** > **[!UICONTROL Implementation]**&#x200B;并单击&#x200B;**[!UICONTROL Generate New Authorization Token]**。

   &lt;！ — 插入image-target-ui-2.png —>
   ![替代图像](assets/asset-rule-artifact-2.png)

1. 将新生成的授权令牌复制到剪贴板并将其添加到您的Target请求。

   ```javascript {line-numbers="true"}
   const request = {
     trace: {
       authorizationToken: '88f1a924-6bc5-4836-8560-2f9c86aeb36b'
     },
     execute: {
       mboxes: [{
         address: getAddress(req),
         name: "node-sdk-mbox"
       }]
   }};
   ```

1. 通过终端输出Target跟踪以查看有关工件的详细信息。 该URL可通过`artifactLocation`变量访问。

   ```
   "trace": {
     "clientCode": "your-client-code",
     "artifact": {
       "artifactLocation": "https://assets.adobetarget.com/your-client-code/production/v1/rules.bin",
       "pollingInterval": 300000,
       "pollingHalted": false,
       "artifactVersion": "1.0.0",
       "artifactRetrievalCount": 10,
       "artifactLastRetrieved": "2020-09-20T00:09:42.707Z",
        "clientCode": "your-client-code",
      "environment": "production",
       "generatedAt": "2020-09-22T17:17:59.783Z"
     },
   ```
