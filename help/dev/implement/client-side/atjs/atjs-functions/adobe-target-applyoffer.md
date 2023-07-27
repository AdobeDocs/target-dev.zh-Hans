---
keywords: adobe.target.applyOffer， applyOffer， applyoffer，申请选件， at.js，函数，函数， $8
description: 使用 [!UICONTROL adobe.target.applyOffer()] 函数 [!DNL Adobe Target] at.js JavaScript库来应用响应内容。
title: 如何使用 [!UICONTROL adobe.target.applyOffer()] 功能？
feature: at.js
exl-id: 957bbe92-8012-4bd5-95d6-1ae38b72bb16
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 69%

---

# [!UICONTROL adobe.target.applyOffer(options)]

此函数用于应用响应内容，其中 [!DNL Adobe Target].

>[!NOTE]
>
>`applyOffer` 需要使用 `mbox` 参数。如果未指定 mbox 名称，则会发生错误。

options 参数是强制性的，具有以下结构：

| 键值 | 类型 | 必需 | 描述 |
|--- |--- |--- |--- |
| mbox | 字符串 | 是 | Mbox 名称<br />使用 at.js 1.3.0（及更高版本）的 Target 强制使用 mbox 键值。以往，这些键值是要求使用的，但现在，Target 强制使用该键值以确保 Target 正确验证并且客户正确地使用该函数。 |
| selector | 字符串或 DOM 元素 | 否 | HTML 元素或 CSS 选择器，用于标识 Target 应将选件内容放置在其中的 HTML 元素。如果未提供选择器，则Target会假定HTML元素应使用HTMLHEAD。 |
| 优惠 | 数组 | 是 | 应用于元素的数组操作。 |

## 示例

以下示例显示如何将 `[!UICONTROL getOffer]` 和 `[!UICONTROL applyOffer]` 一起使用：

```javascript {line-numbers="true"}
adobe.target.getOffer({   
  "mbox": "mbox",   
  "success": function(offers) {           
        adobe.target.applyOffer( {  
           "mbox": "mbox", 
           "offer": offers  
        } ); 
  },   
  "error": function(status, error) {           
      if (console && console.log) { 
        console.log(status); 
        console.log(error); 
      } 
  }, 
 "timeout": 5000 
}); 
```
