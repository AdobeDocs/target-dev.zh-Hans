---
keywords: mboxDefine， mboxdefine， mbox define， mboxUpdate， mboxupdate， mbox更新， at.js，函数，函数， mboxDefine0
description: 对 [!DNL Adobe Target] at.js JavaScript库使用[!UICONTROL mboxDefine()]和[!UICONTROL mboxUpdate()]函数来定义或更新mbox。 (at.js 1.x)
title: 如何使用[!UICONTROL mboxDefine()]和[!UICONTROL mboxUpdate()]函数？
feature: at.js
exl-id: 0a7dbea2-1cbd-4a5b-ba68-4c76a88d65c4
TQID: https://experienceleague.adobe.com/Fn-Ej8jk2AMEn79tOtRoP9GQc36Ugy6FtXyn6x7jkmA
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 208
ht-degree: 46%

---

# [!UICONTROL mboxDefine()]和[!UICONTROL mboxUpdate()] - at.js 1.x

在[!DNL Adobe Target]中定义和更新mbox。

>[!NOTE]
>
>这些函数仅适用于at.js版本1.*x*。 这些函数已在at.js 2.*x*&#x200B;版本中弃用。 如果与at.js 2.*x*&#x200B;一起使用，这些函数将返回默认内容。

`[!UICONTROL mboxDefine()]` 和 `[!UICONTROL mboxCreate()]` 绑定到应显示产品建议的 HTML DIV 元素。 这些 HTML DIV 元素应具有 `mboxDefault` 类。 如果 HTML 元素不会附加此类，则您可能会看到一些明显的闪烁。

## mboxDefine

创建 nodeId 和 mbox 名称之间的内部映射，但不执行请求。 与 `[!UICONTROL mboxUpdate()]` 一起使用。 内置于at.js，主要用于简化从mbox.js（现已弃用）到at.js的转换。

## mboxUpdate

执行请求并将产品建议应用到由 `nodeId` () 中的 `mboxDefine()` 标识的元素。 也可以用来更新由 `[!UICONTROL mboxCreate]` 发起的 mbox。 内置于at.js，主要用于简化从mbox.js（现已弃用）到at.js的转换。 `mboxDefine()`/`mboxUpdate()` 可以使用选项器替换为 [adobe.target.getOffer()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffer.md) 和 [adobe.target.applyOffer()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffer.md)。

## 示例

```javascript {line-numbers="true"}
<div id="someId" class="mboxDefault"></div> 
<script> 
 mboxDefine('someId','mboxName','param1=value1','param2=value2'); 
 mboxUpdate('mboxName','param3=value3','param4=value4'); 
</script>
```
