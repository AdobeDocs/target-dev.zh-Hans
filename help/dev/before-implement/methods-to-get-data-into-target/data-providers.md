---
keywords: 实施，实施，设置，设置，数据提供程序
description: 将数据导入 [!DNL Target] 使用数据提供程序。
title: 如何将数据导入 [!DNL Target] 使用数据提供程序？
feature: Implementation
exl-id: 9971bd96-f736-4965-afe2-b4901c12d006
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 53%

---

# 数据提供程序

数据提供程序是一项功能，允许您轻松地将数据从第三方传递到 [!DNL Adobe Target].

>[!NOTE]
>
>数据提供程序需要使用at.js 1.3或更高版本。

## 格式

`window.targetGlobalSettings.dataProviders` 设置是一个数据提供程序数组。

有关每个数据提供程序的结构的更多信息，请参阅[数据提供程序](../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers)。

## 示例用例

从第三方收集数据，例如气象服务、DMP，甚至您自己的 Web 服务。然后，您可以使用这些数据来构建受众、定位内容并丰富访客配置文件。

## 方法的优势

通过此设置，客户可以从第三方数据提供商（如Demandbase、BlueKai和自定义服务）收集数据，并将这些数据传递到 [!DNL Target] 作为mbox参数。

支持通过异步和同步请求从多个提供程序收集数据。

使用这种方法可以轻松管理默认页面内容的闪烁，同时包含每个提供程序的独立超时时间以限制对页面性能的影响

## 注意事项

如果数据提供程序添加到 `window.targetGlobalSettings.dataProviders` 是异步的，它们将并行执行。 访客API请求与添加到中的函数并行执行 `window.targetGlobalSettings.dataProviders` 允许最小等待时间。

at.js不尝试缓存数据。 如果数据提供程序仅提取一次数据，则应确保数据已缓存，并且在调用提供程序函数时为第二次调用提供缓存的数据。

## 代码示例

在[数据提供程序](../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers)中可以找到几个示例。

## 相关信息的链接

文档：[数据提供程序](../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers)

## 培训视频：

* [在 Adobe Target 中使用数据提供程序](https://experienceleague.adobe.com/docs/target-learn/tutorials/integrations/use-data-providers-to-integrate-third-party-data.html)
* [在 Adobe Target 中实施数据提供程序](https://experienceleague.adobe.com/docs/target-learn/tutorials/integrations/implement-data-providers-to-integrate-third-party-data.html)
