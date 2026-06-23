---
keywords: registerExtension， registerextension，注册扩展， at.js，函数，函数， clientCode， serverDomain， globalMboxName， globalMboxAutoCreate， timeout， registerExtension2
description: 对 [!DNL Adobe Target] at.js JavaScript库使用[!UICONTROL registerExtension()]函数注册特定扩展。 (at.js 1.x)
title: 如何使用[!UICONTROL registerExtension()]函数？
feature: at.js
exl-id: 71decf00-84c5-4914-b0cd-bb061fa6265f
TQID: https://experienceleague.adobe.com/qTWubp0dNesN-8vsooz8pdbjfSw1W1ktm-0bG6YRzJw
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 4d0e7f9f2887db71229061fa64b2633a84c6d054
workflow-type: tm+mt
source-wordcount: 277
ht-degree: 62%

---

# [!UICONTROL registerExtension()] - at.js 1.x

可提供用于注册特定扩展的标准方法。

>[!NOTE]
>
>此函数仅适用于at.js 1.*x*&#x200B;版。 at.js 2.*x*&#x200B;版本已弃用此函数。 如果与at.js 2.x一起使用，此函数将返回默认内容。

options 参数是强制性的，具有以下结构：

| 键 | 类型 | 必需 | 描述 |
|--- |--- |--- |--- |
| name | 字符串 | 是 | 扩展名。 |
| modules | Array[String] | 是 | 一个字符串数组，表示请求的模块名称。 |
| register | 函数 | 是 | 用于初始化和构建扩展的函数。 该函数接收基于模块数组的参数。 |

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
| log | 函数 | 将参数变量列表记录到浏览器控制台（如果存在）。 只有当 `mboxDebug=true` 传递到 URL 时才会激活它。 |
| error | 函数 | 将参数变量列表记录到浏览器控制台。 只有在出现严重错误（如网络超时、未找到 HTML 节点等）时才会激活它。 |

