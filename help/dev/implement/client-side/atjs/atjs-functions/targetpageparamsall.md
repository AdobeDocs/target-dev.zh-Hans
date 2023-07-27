---
keywords: targetPageParamsAll， targetpageparamsall， PageParamsAll， pageparamsall，页面参数，页面参数， at.js，函数，函数， targetPageParamsAll0
description: 使用 [!UICONTROL targetPageParamsAll()] 函数 [!DNL Adobe Target] at.js JavaScript库将参数从请求代码外部附加到所有mbox。
title: 如何使用 [!UICONTROL targetPageParamsAll()] 功能？
feature: at.js
exl-id: 32045e60-6904-42a1-bf71-fd7e167a829f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 55%

---

# [!UICONTROL targetPageParamsAll()]

此方法允许您从请求代码外部将参数附加到所有 mbox。

在多个 mbox 调用中包含相同的一组参数时，这非常有用。该函数需由客户定义。它应返回一个参数数组，这些参数将传递给页面上的所有 mbox 请求。此函数可在加载at.js之前或在以下位置定义： **[!UICONTROL 管理]** > **[!UICONTROL 实现]** > **[!UICONTROL 编辑]** > **[!UICONTROL 代码设置]** > **[!UICONTROL 库标题]**.

您可以使用以下代码将参数传递到target-global-mbox [!UICONTROL targetPageParamsAll()] 函数：

* 以与号 (&amp;) 分隔的列表
* 数组
* JSON 对象

## 示例

以 &amp; 符号分隔的列表（值必须进行 URL 编码）：

```javascript {line-numbers="true"}
function targetPageParamsAll() { 
    return "param1=value1&param2=value2&p3=hello%20world"; 
}
```

数组（值不需要进行 URL 编码）：

```javascript {line-numbers="true"}
targetPageParamsAll = function() { 
     return ["a=1", "b=2", "c=hello world"]; 
};
```

JSON（值不需要进行 URL 编码）：

```javascript {line-numbers="true"}
targetPageParamsAll = function() { 
  return { 
    "a": 1, 
    "b": 2, 
    "profile": { 
        "age": 26, 
        "country": { 
          "city": "San Francisco" 
        } 
      } 
  }; 
};
```
