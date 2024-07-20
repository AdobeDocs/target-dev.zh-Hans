---
keywords: adobe.target.getOffer， getOffer， getoffer， get offer， at.js，函数，函数， $8
description: 对 [!DNL Adobe Target] at.js库使用[!UICONTROL adobe.target.getOffer()]函数及其选项以触发获取 [!DNL Target] 选件的请求。
title: 如何使用[!UICONTROL adobe.target.getOffer()]函数？
feature: at.js
exl-id: 7b917d42-06e8-4838-a09d-0c4872c9beaa
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '460'
ht-degree: 79%

---

# [!DNL adobe.target.getOffer(options)]

此函数会触发用于获取[!DNL Target]选件的请求。

使用 `[!UICONTROL adobe.target.applyOffer()]` 来处理响应或使用您自己的成功处理。options 参数是强制性的，具有以下结构：

| 键 | 类型 | 必需 | 描述 |
|--- |--- |--- |--- |
| mbox | 字符串 | 是 | Mbox 名称 |
| 参数 | 对象 | 否 | Mbox 参数。键值对这一对象具有以下结构：<P>`{ "param1": "value1", "param2": "value2"}` |
| success | 函数 | 是 | 当我们从服务器获得响应时执行的回调函数。success 回调函数将接收一个参数，该参数表示一组选件对象。以下是一个success回调示例：<P>`function handleSuccess(response){......}`<P>有关详细信息，请参阅下文的“响应”。 |
| error | 函数 | 是 | 我们遇到错误时执行的回调函数。以下是几个出现错误的案例：<ul><li>HTTP 状态码不是 200 OK</li><li>响应无法解析。例如，我们不当地构造了 JSON，或者构造了 HTML 而不是 JSON。</li><li>响应包含“error”键值。例如，在边缘服务器上引发异常，无法正确处理请求。我们可能会在 mbox 被阻止并且无法为其检索任何内容等情况发生时收到错误。error 回调函数将接收两个参数：status 和 error。以下是一个错误回调示例： `function handleError(status, error){......}`</li></ul>有关详细信息，请参阅下文的“错误响应”。 |
| timeout | 数值 | 否 | 以毫秒为单位的超时时间。如果未指定，将使用 at.js 中的默认超时设置。<P>可以在[!UICONTROL Administration] > [!UICONTROL Implementation]下的[!DNL Target] UI中设置默认超时。 |

## 示例

正在添加带[!UICONTROL getOffer()]的参数并使用[!UICONTROL applyOffer()]进行成功处理：

```javascript {line-numbers="true"}
adobe.target.getOffer({   
  "mbox": "target-global-mbox", 
  "params": { 
     "a": 1, 
     "b": 2 
  }, 
  "success": function(offer) {           
        adobe.target.applyOffer( {  
           "mbox": "target-global-mbox", 
           "offer": offer  
        } ); 
  },   
  "error": function(status, error) {           
      console.log('Error', status, error); 
  } 
});
```

正在添加参数和[!UICONTROL getOffer()]的配置文件参数，并使用[!UICONTROL applyOffer()]进行成功处理：

```javascript {line-numbers="true"}
adobe.target.getOffer({   
  "mbox": "target-global-mbox", 
  "params": { 
     "a": 1, 
     "b": 2, 
     "profile.age": 27, 
     "profile.gender": "male" 
  }, 
  "success": function(offer) {           
        adobe.target.applyOffer( {  
           "mbox": "target-global-mbox", 
           "offer": offer  
        } ); 
  },   
  "error": function(status, error) {           
      console.log('Error', status, error); 
  } 
});
```

对[!UICONTROL getOffer()]使用自定义超时和自定义成功处理：

“YOUR_OWN_CUSTOM_HANDLING_FUNCTION”是客户要定义的函数的占位符。

```javascript {line-numbers="true"}
adobe.target.getOffer({     
  "mbox": "target-global-mbox",   
  "success": function(offer) { 
    YOUR_OWN_CUSTOM_HANDLING_FUNCTION(offer);   
  }, 
  "error": function(status, error) {                 
    console.log('Error', status, error);   
  },   
  "timeout": 2000 
});
```

## 响应

传递给 success 回调函数的响应参数将是一组操作。操作是一个通常具有以下格式的对象：

| 名称 | 类型 | 描述 |
|--- |--- |--- |
| action | 字符串 | 要应用于所标识元素的操作类型。 |
| selector | 字串符 | 表示一个 Sizzle 选择器。 |
| cssSelector | 字符串 | DOM 原生选择器，用于预隐藏元素。 |
| content | 字符串 | 要应用于所标识元素的内容。 |

## 示例

```javascript {line-numbers="true"}
{ 
    "sessionId": "1444512212156-384616", 
    "tntId": "1444512212156-384616.17_35", 
    "offers": [{ 
        "plugins": ["<script type=\"text/javascript\">\r\n/*mboxHighlight+ (1of2) v1 ==> Response Plugin*/\r\nwindow.ttMETA=(typeof(window.ttMETA)!='undefined')?window.ttMETA:[];window.ttMETA.push({'mbox':'target-global-mbox','campaign':'at: redirect ootb','experience':'Experience B','offer':'/at_redirect_ootb/experiences/1/pages/0/1442082890250'});window.ttMBX=function(x){var mbxList=[];for(i=0;i<ttMETA.length;i++){if(ttMETA[i].mbox==x.getName()){mbxList.push(ttMETA[i])}}return mbxList[x.getId()]}\r\n</script>"], 
        "actions": { 
            "content": [{ 
                "passMboxSession": false, 
                "selector": "body", 
                "action": "redirect", 
                "url": "https://example.com/04.html", 
                "includeAllUrlParameters": true 
            }] 
        } 
    }] 
}
```

## 错误响应

传递给 error 回调函数的“status”和“error”参数将具有以下格式：

| 名称 | 类型 | 描述 |
|--- |--- |--- |
| status | 字符串 | 表示错误状态。该参数可以具有以下值：<ul><li>timeout：表示请求超时。</li><li>parseerror：表示无法解析响应，例如，如果我们收到 HTML 或纯文本而不是 JSON。</li><li>error：表示常规错误，例如我们收到的 HTTP 状态不是 200 OK</li></ul> |
| error | 字符串 | 包含其他数据，例如异常消息或其他任何可能对故障诊断有用的信息。 |
