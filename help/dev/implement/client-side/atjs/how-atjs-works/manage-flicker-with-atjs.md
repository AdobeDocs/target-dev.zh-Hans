---
keywords: 闪烁， at.js，实施，异步，异步，同步，同步， $8
description: 了解at.js和 [!DNL Target] 如何在页面或应用程序加载期间阻止闪烁（默认内容在被活动内容替换之前暂时显示）。
title: at.js如何管理闪烁？
feature: at.js
exl-id: 8aacf254-ec3d-4831-89bb-db7f163b3869
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 57%

---

# at.js 如何管理闪烁

有关[!DNL Adobe Target] at.js JavaScript库如何在页面或应用程序加载期间阻止闪烁的信息。

在默认内容被替换为活动内容之前，系统会暂时向访客显示默认内容，在此期间会发生闪烁。闪烁可能会使访客感到困惑，因此是一种不良体验。

## 使用自动创建的全局mbox

如果启用[自动创建全局 Mbox](/help/dev/implement/client-side/atjs/global-mbox/customize-global-mbox.md) 设置，at.js 会在页面加载时通过更改不透明度设置来管理闪烁。加载at.js时，它会将`<body>`元素的不透明度设置更改为“0”，从而使访客在最初时看不到该页面。 收到来自[!DNL Target]的响应后，或者如果检测到[!DNL Target]请求出错，at.js会将不透明度重置为“1”。 这可确保访客只有在应用您的活动内容后才会看到该页面。

在配置 at.js 时，如果您启用该设置，at.js 会将 HTML 主体样式的不透明度设置为 0。收到来自[!DNL Target]的响应后，at.js会将HTML正文不透明度重置为1。

通过将不透明度设置为 0，可保持页面内容处于隐藏状态以防止闪烁，但浏览器仍会渲染页面并加载所有必需的资产，如 CSS、图像等。

如果`opacity: 0`在您的实施中不起作用，您还可以通过自定义`bodyHiddenStyle`并将其设置为`body {visibility:hidden !important}`来管理闪烁。 您可以使用`body {opacity:0 !important}`或`body {visibility:hidden !important}`，在这两者中，选择最适合您的特定环境的那个选项。

下图显示了 at.js 1.*x* 和 at.js 2.x 中的“隐藏主体”和“显示主体”调用。

**at.js 2.x**

（单击图像可展开至全宽。）

![Target流程： at.js页面加载请求](/help/dev/implement/client-side/assets/atjs-20-flow-page-load-request.png "Target流程： at.js页面加载请求"){zoomable="yes"}

**at.js 1.*x***

（单击图像可展开至全宽。）

![Target流程：自动创建的全局mbox](/help/dev/implement/client-side/atjs/how-atjs-works/assets/target-flow2.png "Target流程：自动创建的全局mbox"){zoomable="yes"}

有关 `bodyHiddenStyle` 覆盖的更多信息，请参阅 [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md)。

## 异步加载 at.js 时管理闪烁

异步加载 at.js 有利于避免阻止浏览器渲染；但是，此技术可能会导致网页闪烁。

您可以通过使用预先隐藏的代码片段来避免闪烁，在Target对相关HTML元素进行个性化后，系统会显示这些代码片段。

at.js可以进行异步加载，可以直接嵌入到页面上，也可以通过标签管理器(例如Adobe Experience Platform Launch)进行加载。

如果页面上嵌入了at.js，则在加载at.js之前必须添加代码片段。 如果通过标签管理器（也异步加载）加载at.js，则必须在加载标签管理器之前添加代码片段。 如果同步加载标记管理器，则脚本可能包含在位于at.js之前的标记管理器中。

预先隐藏的代码片段如下所示：

```
;(function(win, doc, style, timeout) {
  var STYLE_ID = 'at-body-style';

  function getParent() {
    return doc.getElementsByTagName('head')[0];
  }

  function addStyle(parent, id, def) {
    if (!parent) {
      return;
    }

    var style = doc.createElement('style');
    style.id = id;
    style.innerHTML = def;
    parent.appendChild(style);
  }

  function removeStyle(parent, id) {
    if (!parent) {
      return;
    }

    var style = doc.getElementById(id);

    if (!style) {
      return;
    }

    parent.removeChild(style);
  }

  addStyle(getParent(), STYLE_ID, style);
  setTimeout(function() {
    removeStyle(getParent(), STYLE_ID);
  }, timeout);
}(window, document, "body {opacity: 0 !important}", 3000));
```

默认情况下，该代码片段会预先隐藏整个 HTML 主体。在某些情况下，您可能只想预先隐藏某些 HTML 元素，而不是整个页面。您可以通过自定义样式参数来实现这一点。可以将该参数替换为仅预先隐藏页面特定区域的内容。

例如，您有两个分别采用 ID container-1 和 container-2 进行标识的区域，则可以将样式替换为以下内容：

```
#container-1, #container-2 {opacity: 0 !important}
```

而不是默认内容：

```
body {opacity: 0 !important}
```

## 在at.js 2.x的triggerView()中管理闪烁

当使用 `triggerView()` 在 SPA 中显示目标内容时，开箱即用地提供闪烁管理。这意味着无需手动添加预先隐藏逻辑。相反，at.js 2.x 会在应用目标内容之前预先隐藏需要显示视图的位置。

## 使用getOffer()和applyOffer()管理闪烁

因为 `getOffer()` 和 `applyOffer()` 都是较低级别的 API，因此没有内置的闪烁控制。您可以将某个选择器或 HTML 元素作为一个选项传递到 `applyOffer()`，在此示例中，`applyOffer()` 会将活动内容添加到此特定元素；但是在调用 `getOffer()` 和 `applyOffer()` 之前，您必须确保已相应地预先隐藏该元素。

```
document.documentElement.style.opacity = "0";
 
adobe.target.getOffer({
    mbox: 'target-global-mbox',
    success: function(offer) {
        adobe.target.applyOffer({
            mbox: 'target-global-mbox',
            offer: offer
        });
 
        document.documentElement.style.opacity = "1";
    },
    error: function() {
        document.documentElement.style.opacity = "1";        
    }
});
```

## 在at.js 1.x的mboxCreate()中使用区域mbox（在at.js 2.x中不受支持）

如果您使用区域 mbox 实施，则可以在配置以下类似示例代码的页面中使用 `mboxCreate()`：

```
<div class="mboxDefault">
Some default content
</div>
<script>
mboxCreate('some-mbox');
</script>
```

如果您的页面进行了正确配置，at.js 将会使用 mboxDefault 类相应转换元素的 CSS“可见性”属性，从而管理闪烁。
