---
keywords: 浏览器，先决条件，要求， internet explorer， chrome， firefox， safari， android， surface，浏览器0
description: 了解 [!DNL Adobe Target] 支持哪些互联网浏览器用于其界面和内容交付。
title: ' [!DNL Target] 支持哪些浏览器？'
feature: Implementation
exl-id: 1d778e14-26b0-477b-ac28-d304db70a133
source-git-commit: 1b6dcb24d677b758ed1daf85dc0a7e9e5b42680d
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 20%

---

# 支持的浏览器

已在各种浏览器和设备上对 [!DNL Adobe Target] 应用程序和内容交付进行了测试。

有关TLS的更多重要信息，请参阅[TLS（传输层安全性）加密更改](tls-transport-layer-security-encryption.md)。

## [!DNL Target] Standard/Premium界面

[!DNL Target]接口支持以下浏览器和设备：

>[!NOTE]
>
>Target支持列出的每个浏览器的最新版本，以及最新版本减去1。


| 设备类型 | 浏览器版本 |
|--- |--- |
| [!DNL Windows] | <ul><li>[!DNL Microsoft Edge]</li><li>[!DNL Google Chrome]</li><li>[!DNL Mozilla Firefox]</li></ul> |
| [!DNL Mac] | <ul><li>[!DNL Microsoft Edge]</li><li>[!DNL Google Chrome]</li><li>[!DNL Mozilla Firefox]</li></ul> |

## 可视化编辑要求

若要能够在[!UICONTROL Visual Experience Composer] (VEC)中以可靠的方式打开、创作和预览网页，必须在Web浏览器上安装[Adobe Experience Cloud可视化编辑帮助程序浏览器扩展](https://experienceleague.adobe.com/en/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension){target=_blank}，或者使用[!UICONTROL Enhanced Experience Composer (EEC)]。

>[!NOTE]
>
>[!DNL Google Chrome]和[!DNL Microsoft Edge]目前是唯一支持[!DNL Adobe Target]中网页可视化编辑的浏览器。


## 内容投放

已在以下浏览器和设备上对内容交付进行了测试：

| 设备类型 | 浏览器版本 |
|--- |--- |
| Windows | <ul><li>Microsoft Internet Explorer 9和10。 测试是在模拟模式下进行的。**注意**： at.js 1.3.0（及更高版本）不再支持IE 9上的内容交付。 at.js 2.5.0（及更高版本）不再支持IE 10、11和所有旧版本上的内容交付。</li><li>Internet Explorer 11。 **注意**： at.js 2.5.0（及更高版本）不再支持IE 10、11和所有旧版本上的内容交付。</li><li>Microsoft Edge</li><li>Chrome （最新，最新 — 1）</li><li>Firefox （最新版本，最新版本减去1）</li></ul> |
| Mac | <ul><li>Apple Safari（最新版本）。 **注意**：有关Safari如何处理第一方和第三方Cookie的详细信息，请参阅[Target Cookie](../implement/client-side/atjs/atjs-cookies.md)。</li><li>Firefox （最新版本，最新版本减去1）</li><li>Chrome （最新，最新 — 1）</li></ul> |
| 移动设备/平板电脑 | <ul><li>Apple iOS（最新）</li><li>Android 设备和平板电脑（Android 4 及更高版本）</li><li>Microsoft Surface (Windows 8.1)</li></ul> |

请注意以下事项：

* [!DNL Adobe Experience Platform Web SDK]设计为可在最新版本的[!DNL Google Chrome]、[!DNL Safari]、[!DNL Firefox]和[!DNL Microsoft Edge Chromium]中优化工作。 在这些浏览器的旧版本或已弃用的浏览器（如[!DNL Internet Explorer]）上使用某些功能时可能会遇到问题。
* 对于at.js实施，[!DNL Target]在早期版本的Internet Explorer中以及可能在以上所列浏览器的早期版本中显示默认内容。
* Internet Explorer将所有未知元素（如自定义元素）视为相同的元素类型。 因此，投放不适用于自定义元素。
* [!DNL Target]在上面未列出的浏览器以及使用[怪异模式](https://en.wikipedia.org/wiki/Quirks_mode)的浏览器中显示默认内容。 at.js 要求使用可在标准模式下渲染的文档类型，例如：`<!DOCTYPE html>`。
* [!DNL Adobe]交付基础架构已确定在2018年9月12日之后“不”支持TLS 1.0设备和浏览器。 请参阅 [TLS（传输层安全性）加密更改](../before-implement/tls-transport-layer-security-encryption.md)以了解此更改带来的总体影响。
