---
keywords: 自定义事件， at.js，请求失败，请求成功，内容渲染失败，内容渲染成功，库已加载，请求开始，内容渲染开始，内容渲染无选件，内容渲染重定向，自定义事件2
description: 使用适用于 [!DNL Adobe Target] at.js JavaScript库的自定义事件，以在mbox请求或选件失败或成功时接收通知。
title: 如何使用at.js自定义事件？
feature: at.js
exl-id: a4baed9a-9eb8-4343-9834-709b03e44ca2
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 71%

---

# at.js 自定义事件

有关 `at.js custom events` 的信息，可让您知道 mbox 请求或产品建议何时失败或成功。

以前，mbox.js（现已弃用）不会让页面上运行的其他JavaScript代码知道后台的情况。 随着 at.js 的进步，我们有一个难得的机会来解决此问题。

根据客户的反映，他们想要在几种情况出现时得到通知，包括：

* 由于超时、状态码错误、JSON 解析错误等原因，mbox 请求失败。
* 某个 mbox 请求成功。
* 由于封装 mbox 元素缺失、无法找到选择器等原因，导致选件渲染失败。
* 选件渲染成功。已应用 DOM 更改。

预定义事件具有一个结构，允许您根据事件类型提取所需的数据。

为了确保可以在不同方案中使用事件，自定义事件具有一个有效负荷对象，该对象被分配给事件对象的详细属性（传递给处理程序）。另外，为了避免将字符串作为事件名称传递，系统会使用 `adobe.target.event` 命名空间将这些事件作为常量显示。

## 结构

| 键 | 类型 | 描述 |
|--- |--- |--- |
| type | 字符串 | 在有些情况下，您希望了解如何跟踪、调试和自定义与 at.js 的交互。<p>下面列出的每个自定义事件都有两种格式：“常量”和“字符串值”。<ul><li>**常量**：前面预置 `adobe.target.event.`，全部大写，并包含下划线字符。要在加载 at.js *之后*、收到 mbox 响应&#x200B;*之前*&#x200B;订阅自定义事件，请使用常量。</li><li>**字符串值**：小写并包含破折号。要在加载 at.js *之前*&#x200B;订阅自定义事件，请使用字符串值。</li></ul>**请求失败**<p>常量： `adobe.target.event.REQUEST_FAILED`<p>字符串值： `at-request-failed`<p>描述：由于超时、状态码错误、JSON 解析错误等原因，mbox 请求失败。<p>**请求成功**<p>常量： `adobe.target.event.REQUEST_SUCCEEDED`<p>字符串值： `at-request-succeeded`<p>描述：mbox 请求成功。<p>**内容渲染失败**<p>常量： `adobe.target.event.CONTENT_RENDERING_FAILED`<p>字符串值： `at-content-rendering-failed`<p>描述：由于封装 mbox 元素缺失、无法找到选择器等原因，选件渲染失败。<p>**内容渲染成功**<p>常量： `adobe.target.event.CONTENT_RENDERING_SUCCEEDED`<p>字符串值： `at-content-rendering-succeeded`<p>描述：选件渲染已成功。已应用 DOM 更改。<p>**已加载库**<p>常量： `adobe.target.event.LIBRARY_LOADED`<p>字符串值： `at-library-loaded`<p>描述：此事件非常适用于跟踪 at.js 何时已完全加载。您可以使用此事件来自定义全局 mbox 执行。您也可以使用此事件来禁用全局 mbox，然后侦听此事件以便稍后再触发全局 mbox。<p>**请求启动**<p>常量： `adobe.target.event.REQUEST_START`<p>字符串值： `at-request-start`<p>描述：此事件在执行 HTTP 请求之前已触发。您可以使用此事件进行使用 Resource Timing API 的性能测量。<p>**内容渲染启动**<p>常量： `adobe.target.event.CONTENT_RENDERING_START`<p>字符串值： `at-content-rendering-start`<p>描述：在启动选择器轮询并将内容渲染到页面之前，已触发此事件。您可以使用此事件来跟踪内容渲染进度。<p>**内容渲染（无选件）**<p>常量： `adobe.target.event.CONTENT_RENDERING_NO_OFFERS`<p>字符串值： `at-content-rendering-no-offers`<p>描述：当未返回选件时，会触发此事件。<p>**内容渲染重定向**<p>常量： `adobe.target.event.CONTENT_RENDERING_REDIRECT`<p>字符串值： `at-content-rendering-redirect`<p>描述：此事件在选件是重定向选件并且[!DNL Target]将重定向到其他URL时触发。 |
| mbox | 字符串 | mbox 名称 |
| message | 字符串 | 包含通俗易懂的描述，例如出现什么错误、错误消息等。 |
| tracking | 对象 | 包含 `sessionId` 和 `deviceId`。在某些情况下，`deviceId` 可能缺失，因为 [!DNL Target] 无法从边缘服务器检索到它。 |
| type | 字符串 | **设备上决策构件已成功**<p>常量：<p>`adobe.target.event.ARTIFACT_DOWNLOAD_SUCCEEDED`<p>字符串值： `artifactDownloadSucceeded`<p>描述：在成功下载设备上决策工件时调用。<p>**设备上决策构件失败**<p>常量： `adobe.target.event.ARTIFACT_DOWNLOAD_FAILED`<p>字符串值： `artifactDownloadFailed`<p>描述：当设备上决策构件下载失败时调用。 |

## 使用情况

```javascript {line-numbers="true"}
document.addEventListener(adobe.target.event.REQUEST_SUCCEEDED, function(event) { 
  console.log('Event', event); 
});
```

## 培训视频：响应令牌和at.js自定义事件![教程徽章](../../../assets/tutorial.png)

观看以下视频，了解如何使用响应令牌和at.js自定义事件将[!DNL Target]中的配置文件信息共享到第三方系统。

>[!VIDEO](https://video.tv.adobe.com/v/33361/?captions=chi_hans&quality=12)
