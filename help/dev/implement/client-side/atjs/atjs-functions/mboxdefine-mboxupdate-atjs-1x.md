---
keywords: mboxDefine， mboxdefine， mbox define， mboxUpdate， mboxupdate， mbox更新， at.js，函数，函数， mboxDefine0
description: 使用 [!UICONTROL mboxDefine()] 和 [!UICONTROL mboxUpdate()] 函数 [!DNL Adobe Target] at.js JavaScript库来定义或更新mbox。 (at.js 1.x)
title: 如何使用 [!UICONTROL mboxDefine()] 和 [!UICONTROL mboxUpdate()] 功能？
feature: at.js
exl-id: 0a7dbea2-1cbd-4a5b-ba68-4c76a88d65c4
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 52%

---

# [!UICONTROL mboxDefine()] 和 [!UICONTROL mboxUpdate()] - at.js 1.x

在中定义和更新mbox [!DNL Adobe Target].

>[!NOTE]
>
>这些函数仅可用于 at.js 版本 1.*x*。这些函数已在at.js 2版本中弃用。*x*.如果与at.js 2.*x*.

`[!UICONTROL mboxDefine()]` 和 `[!UICONTROL mboxCreate()]` 绑定到应显示选件的 HTML DIV 元素。这些 HTML DIV 元素应具有 `mboxDefault` 类。如果 HTML 元素不会附加此类，则您可能会看到一些明显的闪烁。

## mboxDefine

创建 nodeId 和 mbox 名称之间的内部映射，但不执行请求。与 `[!UICONTROL mboxUpdate()]` 一起使用。内置于at.js，主要用于简化从mbox.js（现已弃用）到at.js的转换。

## mboxUpdate

执行请求并将选件应用到由 `nodeId` () 中的 `mboxDefine()` 标识的元素。也可以用来更新由 `[!UICONTROL mboxCreate]` 发起的 mbox。内置于at.js，主要用于简化从mbox.js（现已弃用）到at.js的转换。 `mboxDefine()`/`mboxUpdate()` 可以使用选项器替换为 [adobe.target.getOffer()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffer.md) 和 [adobe.target.applyOffer()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffer.md)。

## 示例

```javascript {line-numbers="true"}
<div id="someId" class="mboxDefault"></div> 
<script> 
 mboxDefine('someId','mboxName','param1=value1','param2=value2'); 
 mboxUpdate('mboxName','param3=value3','param4=value4'); 
</script>
```
