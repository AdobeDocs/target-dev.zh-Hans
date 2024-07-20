---
keywords: 全局mbox参数， targetPageParams，查询字符串，数组， json， dtm
description: 了解如何使用[!UICONTROL targetPageParams]函数将其他定位或上下文信息传递到 [!DNL Adobe Target] 全局mbox。
title: 如何将参数传递到全局mbox？
feature: at.js
exl-id: 2a6be3e4-a618-4812-9e87-b01789705c40
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 61%

---

# 将参数传递到全局 mbox

JavaScript `targetPageParams`函数用于将参数传递到[!DNL Adobe Target]中的全局mbox。 任何要将其他定位/上下文信息传递到[!DNL Target]的方案都需要此项。

例如，在“推荐”活动中，使用相应参数来表示当前正在查看的产品或类别。

无论全局mbox是作为at.js的一部分触发，还是手动包含在页面代码中，调用JavaScript函数的代码都必须位于页面上的全局mbox之前。

>[!NOTE]
>
>如果要将参数添加到页面上的所有mbox，而不只是添加到全局mbox，请使用[targetPageParamsAll()](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparamsall.md)函数。

您可以按照以下任一方式使用 `targetPageParams()` 函数将参数传递到 `target-global-mbox`：

* 数组
* JSON 对象
* 以与号 (&amp;) 分隔的列表

使用这三种方法可验证参数是否正确传递。您还可以使用 [Adobe Experience Cloud 调试器](https://experienceleague.adobe.com/docs/debugger/using/experience-cloud-debugger.html)来验证参数的传递。

您必须先定义 JavaScript 函数，然后再向页面中添加全局 mbox。函数名称必须为 `targetPageParams`。

## 查询字符串

```
p1=v1&p2=v2&p3=hello%20world
```

* 名称: `targetPageParams`
* 返回值：以“&amp;”分隔的参数，这些参数包含 URL 编码参数值。

  示例：

  在此示例中，p3 的值为 `hello world`，该值已进行 URL 编码。

请考虑以下示例页面代码：

```html {line-numbers="true"}
<html> 
  <head> 
    <title>Title here..</title> 
    <script type="text/javascript"> 
        function targetPageParams() { 
          return "p1=v1&p2=v2&p3=hello%20world";
        } 
    </script> 
    <script src="mbox.js" type="text/javascript"></script> 
  </head> 
  <body>Body here... 
  </body> 
</html>
```

此示例将以下数据发送到 mbox 边缘：

* p1=v1
* p2=v2
* p3=hello world

## 数组

```javascript {line-numbers="true"}
<!--window.-->targetPageParams = function() { 
  return ["a=1", "b=2", "c=hello world"]; 
}; 
```

不需要对值进行 URL 编码。例如，如果某个值中包含空格，则无需对空格进行编码。

此示例将以下数据发送到 mbox 边缘：

* a=1
* b=2
* c=hello world

## JSON

JSON 是传递参数的有效方式。[!DNL Target]使用JSON对象键将复杂结构扁平化为简单参数。

```json {line-numbers="true"}
<!--window.-->targetPageParams = function() { 
  return { 
    "a": 1, 
    "b": 2, 
    "profile": { 
                  "memberStatus": Gold, 
                  "country": { 
                                "city": "San Francisco" 
                            } 
              } 
  }; 
}; 
```

不需要对值进行 URL 编码。例如，“San Francisco”不需要对空格进行编码。只需使用空格即可。

此示例将以下数据发送到 mbox 边缘：

* a=1
* b=2
* `profile.memberStatus`=金级
* `profile.country.city`=San Francisco
