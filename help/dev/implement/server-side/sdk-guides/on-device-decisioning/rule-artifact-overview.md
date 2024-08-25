---
title: 了解设备上的决策规则伪像
description: 了解如何使用规则工件，它是您的 [!DNL Adobe Target] [!UICONTROL on-device decisioning]活动的JSON表示形式。
feature: APIs/SDKs
exl-id: 3dfb08df-eaa9-43d4-b009-e5f64c3a96d7
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# 规则对象概述

规则项目是您的[!DNL Adobe Target] [!UICONTROL on-device decisioning]活动的JSON表示形式。 它是由[!DNL Adobe Target]生成并传播到Akamai CDN，以确保您的最终用户尽可能使用规则工件。 它包含可确保准确执行和交付活动的元数据，同时允许通过事件跟踪进行实时分析。 [!DNL Adobe Target] SDK的配置方式允许自动管理规则对象，可根据用户指定的时间间隔下载或更新规则对象。 此外，您还可以使用分布式内存缓存系统（如[Memcached](https://memcached.org/)）来初始化[!DNL Adobe Target] SDK，以维护规则对象的本地副本，以便无状态服务器可以立即处理请求。 要了解有关这些选项的更多信息，请参阅以下指南：

* [通过 [!DNL Adobe Target] SDK自动下载、存储和更新规则对象](rule-artifact-sdk.md)
* [通过JSON负载下载、存储和更新规则对象](rule-artifact-json.md)

## 规则伪像示例

单击此处显示[规则对象](rule-artifact-example.md)的示例。

## 如何查看客户的规则对象

启用跟踪将从[!DNL Adobe Target]输出有关规则对象（特别是URL）的其他信息。

1. 导航至目标UI。

   &lt;！— Insert image-target-ui-1.png —>
   ![替代图像](assets/asset-rule-artifact-1.png)

1. 导航到&#x200B;**[!UICONTROL Administration]** > **[!UICONTROL Implementation]**，然后单击&#x200B;**[!UICONTROL Generate New Authorization Token]**。

   &lt;！— Insert image-target-ui-2.png —>
   ![替代图像](assets/asset-rule-artifact-2.png)

1. 将新生成的授权令牌复制到剪贴板，并将其添加到您的Target请求。

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

1. 通过终端输出目标跟踪以查看有关对象的详细信息。 可通过`artifactLocation`变量访问URL。

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
