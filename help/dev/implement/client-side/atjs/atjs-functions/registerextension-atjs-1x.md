---
keywords: registerExtension， registerextension，注册扩展， at.js，函数，函数， clientCode， serverDomain， globalMboxName， globalMboxAutoCreate， timeout， registerExtension2
description: 对 [!DNL Adobe Target] at.js JavaScript库使用[!UICONTROL registerExtension()]函数来注册特定扩展。 (at.js 1.x)
title: 如何使用[!UICONTROL registerExtension()]函数？
feature: at.js
exl-id: 71decf00-84c5-4914-b0cd-bb061fa6265f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 69%

---

# [!UICONTROL registerExtension()] - at.js 1.x

可提供用于注册特定扩展的标准方法。

>[!NOTE]
>
>此函数仅可用于 at.js 版本 1.*x*。此函数已在at.js 2版本中弃用。*x* 使用跨域跟踪功能时。如果与at.js 2.x一起使用，此函数将返回默认内容。

options 参数是强制性的，具有以下结构：

| 键 | 类型 | 必需 | 描述 |
|--- |--- |--- |--- |
| name | 字符串 | 是 | 扩展名。 |
| modules | Array[String] | 是 | 一个字符串数组，表示请求的模块名称。 |
| register | 函数 | 是 | 用于初始化和构建扩展的函数。该函数接收基于模块数组的参数。 |

注释:

* 如果未提供其中任何一个参数，都会引发异常。
* 如果模块数组为空，则会引发异常。

有关如何使用`[!UICONTROL registerExtension]`的更多信息和示例，请参阅GitHub上的[Adobe Experience Cloud Target atjs扩展](https://github.com/Adobe-Marketing-Cloud/target-atjs-extensions)页面。

## 设置模块方法

| 键 | 类型 | 描述 |
|--- |--- |--- |
| clientCode | 字符串 | 客户端代码 |
| serverDomain | 字符串 | 边缘服务器域 |
| globalMboxName | 字符串 | [!DNL Target]全局mbox名称 |
| globalMboxAutoCreate | 布尔值 | 指示是否已启用自动创建 |
| timeout | 数值 | 请求超时 |

## 记录器模块方法

| 键 | 类型 | 描述 |
|--- |--- |--- |
| log | 函数 | 将参数变量列表记录到浏览器控制台（如果存在）。只有当 `mboxDebug=true` 传递到 URL 时才会激活它。 |
| error | 函数 | 将参数变量列表记录到浏览器控制台。只有在出现严重错误（如网络超时、未找到 HTML 节点等）时才会激活它。 |
