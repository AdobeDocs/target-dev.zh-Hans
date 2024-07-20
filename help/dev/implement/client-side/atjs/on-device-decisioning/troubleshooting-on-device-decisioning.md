---
keywords: 实施， javascript库， js， atjs，设备上决策，设备上决策， at.js，设备上，设备上，故障排除，故障排除，实施2
description: 了解如何使用at.js库对[!UICONTROL on-device decisioning]进行故障排除。
title: 如何使用at.js JavaScript库为设备上决策排除故障？
feature: at.js
exl-id: b9530cc7-5e83-4fdf-bde9-b2492e0861ff
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# 针对at.js的[!UICONTROL on-device decisioning]进行故障排除

完成以下步骤以使用at.js JavaScript库对[!UICONTROL Adobe Target]中的[!UICONTROL on-device decisioning]进行故障排除：

## 步骤1：为at.js启用控制台日志

附加URL参数`mboxDebug=1`可让at.js在浏览器的控制台中打印消息。

所有消息都包含前缀“AT：”，以便于概述。 要确保成功加载项目，控制台日志应包含类似于以下内容的消息：

```
AT: LD.ArtifactProvider fetching artifact - https://assets.adobetarget.com/your-client-cide/production/v1/rules.json
AT: LD.ArtifactProvider artifact received - status=200
```

下图显示了控制台日志中的这些消息：

（单击图像可展开至全宽。）

![包含项目消息的控制台日志](/help/dev/implement/client-side/atjs/on-device-decisioning/assets/browser-console.png "包含项目消息的控制台日志"){zoomable="yes"}

## 步骤2：验证浏览器的“网络”选项卡中的规则工件下载

打开浏览器的“网络”选项卡。

例如，要在Google Chrome中打开DevTools，请执行以下操作：

1. 按Ctrl+Shift+J (Windows)或Command+Option+J (Mac)。
1. 导航到“网络”选项卡。
1. 按关键词“rules.json”筛选调用，以确保仅显示工件规则文件。

   此外，您可以按“/delivery|rules.json/”进行筛选，以显示所有Target调用和构件rules.json。

   Google Chrome中的![网络选项卡](assets/rule-json.png)

## 步骤3：使用at.js自定义事件验证规则工件下载

at.js库调度两个新的自定义事件以支持[!UICONTROL on-device decisioning]。

* `adobe.target.event.ARTIFACT_DOWNLOAD_SUCCEEDED`
* `adobe.target.event.ARTIFACT_DOWNLOAD_FAILED`

您可以订阅在应用程序中侦听这些自定义事件，以便在下载工件规则文件成功或失败时执行操作。

以下示例显示了一个代码示例，该代码用于侦听工件下载成功和失败事件：

```javascript {line-numbers="true"}
document.addEventListener(adobe.target.event.ARTIFACT_DOWNLOAD_SUCCEEDED, function(e) { 
  console.log("Artifact successfully downloaded", e.detail);
}, false);

document.addEventListener(adobe.target.event.ARTIFACT_DOWNLOAD_FAILED, function(e) { 
  console.log("Artifact failed to download", e.detail);
}, false);
```
