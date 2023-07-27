---
keywords: 浏览器，先决条件，要求， internet explorer， chrome， firefox， safari， android， surface，浏览器0
description: 了解哪些互联网浏览器 [!DNL Adobe Target] 支持其界面和内容交付。
title: 浏览器的功能 [!DNL Target] 支持？
feature: Implementation
exl-id: 1d778e14-26b0-477b-ac28-d304db70a133
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 43%

---

# 支持的浏览器

已在各种浏览器和设备上对 [!DNL Adobe Target] 应用程序和内容交付进行了测试。

有关TLS的更多信息，请参阅 [TLS（传输层安全性）加密更改](tls-transport-layer-security-encryption.md).

## [!DNL Target] Standard/Premium 界面

此 [!DNL Target] 界面支持以下浏览器和设备：

| 设备类型 | 浏览器版本 |
|--- |--- |
| Windows | <ul><li>Microsoft Edge</li><li>Google Chrome（最新版本，最新版本减去1）</li><li>Mozilla Firefox（最新版本，最新版本减去1）</li></ul> |
| Mac | <ul><li>Firefox （最新版本，最新版本减去1）</li><li>Chrome（最新版本，最新版本减去1）</li></ul> |

## 内容投放

已在以下浏览器和设备上对内容交付进行了测试：

| 设备类型 | 浏览器版本 |
|--- |--- |
| Windows | <ul><li>Microsoft Internet Explorer 9 和 10. 测试是在模拟模式下进行的。**注意**：at.js 1.3.0（及更高版本）不再支持IE 9上的内容交付。 at.js 2.5.0（及更高版本）不再支持IE 10、11和所有旧版本上的内容交付。</li><li>Internet Explorer 11. **注意**：at.js 2.5.0（及更高版本）不再支持IE 10、11和所有旧版本上的内容交付。</li><li>Microsoft Edge</li><li>Chrome（最新版本，最新版本减去1）</li><li>Firefox （最新版本，最新版本减去1）</li></ul> |
| Mac | <ul><li>Apple Safari（最新版本）。**注意**：有关 Safari 如何处理第一方 Cookie 和第三方 Cookie 的更多信息，请参阅 [Target Cookie](../implement/client-side/atjs/atjs-cookies.md)。</li><li>Firefox （最新版本，最新版本减去1）</li><li>Chrome（最新版本，最新版本减去1）</li></ul> |
| 移动设备/平板电脑 | <ul><li>Apple iOS（最新）</li><li>Android 设备和平板电脑（Android 4 及更高版本）</li><li>Microsoft Surface (Windows 8.1)</li></ul> |

请注意以下事项：

* 对于at.js实施， [!DNL Target] 在早期版本的Internet Explorer中以及上述浏览器的早期版本中可能显示默认内容。
* Internet Explorer将所有未知元素（如自定义元素）视为相同的元素类型。 因此，投放不适用于自定义元素。
* [!DNL Target]在上面未列出的浏览器以及使用[怪异模式](https://en.wikipedia.org/wiki/Quirks_mode)的浏览器中， 会显示默认内容。at.js 要求使用可在标准模式下渲染的文档类型，例如：`<!DOCTYPE html>`。
* [!DNL Adobe] 交付基础架构已确定在 2018 年 9 月 12 日之后“不”支持 TLS 1.0 设备和浏览器。请参阅 [TLS（传输层安全性）加密更改](../before-implement/tls-transport-layer-security-encryption.md)以了解此更改带来的总体影响。
