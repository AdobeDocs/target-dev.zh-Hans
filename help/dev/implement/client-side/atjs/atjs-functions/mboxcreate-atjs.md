---
keywords: mboxCreate， mboxcreate， mbox create， at.js，函数，函数
description: 对 [!DNL Adobe Target] at.js JavaScript库使用[!UICONTROL mboxCreate()]函数可将选件应用到具有mboxDefault类名称的最接近DIV。 (at.js 1.x)
title: 如何使用[!UICONTROL mboxCreate()]函数？
feature: at.js
exl-id: 86eba1fc-4e1d-4793-94e7-898bf81f8945
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 56%

---

# [!UICONTROL mboxCreate(mbox,params)] - at.js 1.x

可使用 mboxDefault 类名称执行请求并将选件应用到最近的 DIV。

>[!NOTE]
>
>此函数仅可用于 at.js 版本 1.*x*。此函数已在 at.js 2.x 版本中弃用。如果与 at.js 2.x 一起使用，此函数将返回默认内容。

此函数内置于at.js中，主要用于简化从mbox.js（现已弃用）到at.js的转换。 `[!UICONTROL mboxCreate()]` 的最新替代方案是 `[!UICONTROL adobe.target.getOffer()]`/`[!UICONTROL adobe.target.applyOffer()]` 或 Angular 指令。

## 示例

```javascript {line-numbers="true"}
<div class="mboxDefault"> 
  default content to replace by offer 
</div> 
<script> 
  mboxCreate('mboxName','param1=value1','param2=value2'); 
</script>
```

## 注释

`mboxCreate()` 现在使用“json”端点而不是“standard”端点且会异步触发。因此：

* [调试](/help/dev/implement/client-side/target-debugging-atjs/target-debugging-atjs.md)稍有不同。
* 避免出现需要同步且阻止调用的选件代码。

  例如，设置由站点代码或稍后出现在页面上的其他 mbox 所使用的 JavaScript 变量的选件。

* 调用`[!UICONTROL mboxCreate()]`之前请确保具有`<div class="mboxDefault"></div>`，因为at.js不会为您添加它。

* 不建议将空白页面顶端的 `[!UICONTROL mboxCreate()]` 函数作为全局 mbox。

  at.js中自动创建的全局mbox是一个更好的选项，因为它从`<head>`触发并可以更早返回内容。
