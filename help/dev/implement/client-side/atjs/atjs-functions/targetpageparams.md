---
keywords: targetPageParams， targetpageparams， pageParams， pageparams，页面参数，页面参数， at.js，函数，函数， targetPageParams0
description: 对 [!DNL Adobe Target] at.js JavaScript库使用[!UICONTROL targetPageParams()]函数可将参数从请求代码外部附加到全局mbox。
title: 如何使用[!UICONTROL targetPageParams()]函数？
feature: at.js
exl-id: 274e4d1f-843a-443b-ad98-7139dc4a13f8
TQID: https://experienceleague.adobe.com/xaSxd1biZ8G-LmgYN4YW9BZ2lDyjZyPHOOlfnbXC2jU
product_v2: id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2: id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2: id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 170
ht-degree: 66%

---

# [!UICONTROL targetPageParams()]

此方法允许您从请求代码外部将参数附加到全局 mbox。

在多个 mbox 调用中包含相同的一组参数时，此函数非常有用。 该函数需由客户定义。 它应返回一个只传递给全局 mbox 请求的参数数组。 此函数可在at.js加载之前或在&#x200B;**[!UICONTROL 管理]** > **[!UICONTROL 实现]** > **[!UICONTROL 编辑]** > **[!UICONTROL 库标头]**&#x200B;中定义。

您可以按照以下任一方式使用 `[!UICONTROL targetPageParams()]` 函数将参数传递到 target-global-mbox：

* 以与号 (&amp;) 分隔的列表
* 数组
* JSON 对象

## 示例

以 &amp; 符号分隔的列表（值必须进行 URL 编码）：

```javascript {line-numbers="true"}
function targetPageParams() { 
    return "param1=value1&param2=value2&p3=hello%20world"; 
}
```

数组（值不需要进行 URL 编码）：

```javascript {line-numbers="true"}
targetPageParams = function() { 
     return ["a=1", "b=2", "c=hello world"]; 
};
```

JSON（值不需要进行 URL 编码）：

```javascript {line-numbers="true"}
targetPageParams = function() { 
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
