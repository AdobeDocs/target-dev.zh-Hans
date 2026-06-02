---
keywords: 预隐藏SDK，闪烁，防闪烁，预隐藏，预隐藏， alloy， at.js，实现，同意， CMP，脚本放置，内联，外部， SDK选择
description: 了解如何集成 [!DNL Adobe Target] 预隐藏SDK以消除页面加载期间非个性化内容的闪烁（闪烁）。 SDK可与Adobe Alloy (Web SDK)和at.js配合使用。
title: 预隐藏SDK集成指南
feature: Implementation
hide: true
source-git-commit: 2f7a53b667990474dfab7ca66a8ea93d2e946548
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---


# 预隐藏SDK集成指南

一个小型的同步JavaScript库，可防止因[!DNL Adobe Target]个性化在渲染期间重写页面而导致的视觉闪烁。 在`<head>`的顶部添加一个内联`<script>`标记，只有在个性化内容准备就绪或安全计时器触发后，才会显示页面。

## 集成步骤 {#integration-steps}

1. 下载包。

   使用Flicker Manager UI下载`prehide.min.js`。 该文件已预先配置了您的客户端代码和保护超时，因此不需要`PrehideConfig`块。

1. 在`<head>`的最顶部内联嵌入它。

   将`prehide.min.js`的内容直接粘贴到内联`<script>`标记中，作为`<head>`的第一个子级。 请参阅[内联与外部](#inline-vs-external)以了解为什么首选内联。

   ```html
   <!-- 1. Prehide SDK: must be FIRST in <head> and BEFORE any Adobe SDK -->
   <script>
     // paste the contents of prehide.min.js here
   </script>
   
   <!-- 2. Then load Alloy.js OR at.js -->
   <script src="https://your-cdn/alloy.min.js"></script>
   ```

1. （可选）添加运行时配置块。

   仅在无需通过UI下载即可自行托管捆绑包时才需要，或者需要覆盖SDK选择时才需要。 将配置块放在预隐藏脚本之前：

   ```html
   <script>
     window.PrehideConfig = {
       sdk: "alloy"            // or "atjs" (defaults to "alloy")
     };
   </script>
   <script> /* prehide.min.js inline contents */ </script>
   <script src="https://your-cdn/alloy.min.js"></script>
   ```

1. （可选）获取同意电邮。

   如果您的实施使用同意管理平台(CMP)，则一旦知道同意状态，立即调用`window.Prehide.setConsent(...)`。 请参阅[同意管理](#consent-management)。

1. 验证。

   打开DevTools并确认在首次绘制时`<head>`中出现`<style id="alloy-prehiding">`（或at.js的`at-body-style`），并在SDK完成后将其删除。 在控制台中运行`window.Prehide.getState()`以检查运行时状态。

## 脚本的放置位置 {#script-placement}

>[!IMPORTANT]
>
>预隐藏SDK必须在Alloy/at.js之前运行。如果Alloy先加载，则页面会呈现非个性化内容，然后重新呈现。这正是此SDK旨在防止的闪烁。
></br>>不要将`async`或`defer`添加到“预隐藏SDK”脚本标记中。需要同步执行，以便在浏览器开始布局页面之前注入隐藏规则。

预隐藏SDK在文档中的显示时间必须比在其之后清理的[!DNL Adobe Target]SDK更早。 装货单不可协商：

```html
<!doctype html>
<html>
<head>
  <!-- ① Prehide SDK FIRST. Inline. Synchronous. No async/defer. -->
  <script> /* prehide.min.js inline contents */ </script>

  <!-- ② Alloy or at.js loads next -->
  <script src="https://cdn.alloy.adobe.com/alloy.min.js"></script>

  <!-- ③ Then everything else: meta, css, third-party tags, ... -->
  <link rel="stylesheet" href="main.css">
</head>
<body> ... your page ... </body>
</html>
```

## 内联与外部 {#inline-vs-external}

有两种方法可以包含`prehide.min.js`：

| 方法 | 示例 | 注释 |
| --- | --- | --- |
| 内联（首选） | `<script>/* full contents of prehide.min.js pasted directly into the page */</script>` | 零网络来回。 SDK会在呈现任何其他内容之前执行。 |
| 外部（仅当无法内联时） | `<script src="/static/prehide.min.js"></script>` | 在首次渲染之前引入阻止网络请求。 即使使用HTTP/2和边缘缓存，这通常也需要30-80毫秒。 |

### 为什么首选内联

>[!TIP]
>
>直接在HTML模板的`<script>...</script>`内联捆绑包。 将其视为关键CSS块：小、内联，并始终位于最顶部。

* 无渲染阻止获取。 预隐藏SDK的目的是在&#x200B;*首次渲染之前*&#x200B;插入隐藏规则。 外部`<script src>`在该关键窗口中添加网络往返次数。
* 没有新的故障模式。 外部文件可能出现404错误、超时或被广告拦截器阻止。 不能使用内联副本。
* 包很小(~6 KB)。 内联成本低于典型的收藏集，并且没有任何缓存优势足以超过首次渲染时的额外往返次数。
* 缓存友好。 在HTML响应中内联时，现有缓存层（CDN或浏览器HTTP缓存）会将SDK与文档的其余部分一起缓存。
* 特定于客户的捆绑包。 下载的文件在下载时已将您的客户端代码存入。 内联确保每位访客无需其他请求即可收到正确的自定义捆绑包。

## 配置 {#configuration}

SDK按优先级接受来自两个源的配置。 它会读取最先提供的任何内容。

### 运行时`window.PrehideConfig` （手动集成）

对于自托管或未修改的包，请在运行预隐藏脚本之前声明配置对象：

```html
<script>
  window.PrehideConfig = {
    sdk: "alloy"             // optional: "alloy" (default) or "atjs"
  };
</script>
```

| 字段 | 类型 | 必需 | 描述 |
| --- | --- | --- | --- |
| `sdk` | `"alloy"` \| `"atjs"` | 否 | 页面上加载了Adobe SDK。 请参阅[SDK选择](#sdk-selection)。 |

## SDK选择 {#sdk-selection}

[!DNL Adobe Target]提供两个交付SDK：Alloy（新版Web SDK）和at.js（经典库）。 个性化完成后，每个页面都将查找&#x200B;*不同的* `<style>`元素`id`，并将其删除以显示页面。 预隐藏SDK必须注入匹配的`id`；否则，在安全计时器触发之前，页面将保持隐藏状态。

| `sdk`值 | 样式标记ID已插入 | 删除者 | 使用时间 |
| --- | --- | --- | --- |
| `"alloy"` *（默认）* | `<style id="alloy-prehiding">` | Alloy SDK on personalization-complete | 您正在此页面上加载Alloy/Adobe Web SDK。 |
| `"atjs"` | `<style id="at-body-style">` | 个性化完成后的at.js | 您正在加载此页面上的经典at.js库。 |

>[!NOTE]
>
>对于at.js SDK，仅支持版本2.x及更高版本。

### 如何设置

```html
<!-- For at.js -->
<script>
  window.PrehideConfig = { sdk: "atjs" };
</script>
<script> /* prehide.min.js inline */ </script>
<script src="https://cdn.adobe.com/.../at.js"></script>
```

>[!WARNING]
>
>不匹配。 在加载at.js时设置`sdk: "alloy"`（反之亦然）意味着SDK将找不到要删除的预隐藏元素。 保护计时器最终将显示页面，但访客将体验到较长的隐藏窗口。 始终设置`sdk`以匹配正在加载的库。

未知或缺少的值回退到`"alloy"`，因此现有Alloy集成将继续工作而不进行任何配置更改。

## 同意管理 {#consent-management}

>[!NOTE]
>
>* 同意值从未存储在`window`上。 仅公开函数；内部状态对SDK保持私有状态。
>* 从`"out"`过渡到`"in"`不会重新隐藏页面，因为重新隐藏完全渲染的内容在视觉上可能会造成干扰。
>* 可以在单个页面查看中多次调用`setConsent`。 每次调用都会替换以前的状态。

预隐藏SDK包括用于与CMP进行协调的同意感知API。 使用它是可选的。 如果从未调用`setConsent`，则SDK的行为类似于标准的未经同意集成。

### API表面

```js
// Single function call. Pass a status string.
window.Prehide.setConsent("pending");  // banner shown, awaiting decision
window.Prehide.setConsent("in");       // user accepted personalization
window.Prehide.setConsent("out");      // user declined personalization

// Read-only debug snapshot.
window.Prehide.getState();
// → { sdk, version, consentStatus, consentApiUsed,
//      rulesResolved, hasSelectorsToGuard, guardTimeout }
```

### 每种状态的用途

| 调用 | 对保护计时器的影响 | 对隐藏内容的影响 |
| --- | --- | --- |
| `setConsent("pending")` | 已清除活动计时器。 在解决同意问题之前，没有任何安全可取消隐藏火灾。 | 选择器会无限期地保持隐藏。 |
| `setConsent("in")` | 已清除，然后在配置的超时下重新启动。 如果规则尚未解决，请等待规则解决。 | 在SDK个性化或触发保护计时器之前，内容将保持隐藏状态。 |
| `setConsent("out")` | 已清除。 此时将立即取消隐藏页面。 | 页面随即显示。 稍后解析的规则不会&#x200B;*会*&#x200B;重新隐藏内容。 |
| *（从未调用）* | 默认计时器从`init()`开始运行所配置的持续时间。 | 在SDK个性化或触发保护计时器之前，内容将保持隐藏状态。 （向后兼容的旧模式。） |

### 建议的模式：显式挂起阶段

1. 一旦您的CMP显示同意UI，请调用`setConsent("pending")`。 这会清除安全计时器，以便访客在决策时页面保持隐藏状态，从而防止在横幅后面闪烁非个性化内容。

   ```js
   window.Prehide.setConsent("pending");
   ```

1. 当访客接受个性化设置时，调用`setConsent("in")`。 Guard计时器将重新启动，并且Alloy/at.js将接管系统，在应用个性化后显示页面。

   ```js
   window.Prehide.setConsent("in");
   ```

1. 当访客拒绝个性化设置时，调用`setConsent("out")`。 该页面会立即显示并保持可见。 稍后解析的CDN规则将不会重新隐藏它。

   ```js
   window.Prehide.setConsent("out");
   ```

### 示例：OneTrust样式集成

```js
// Called once OneTrust has rendered its banner.
function onOneTrustReady() {
  // Pause the guard timer while the banner is visible.
  window.Prehide.setConsent("pending");

  OneTrust.OnConsentChanged(function (event) {
    if (event.consentedToTargeting) {
      window.Prehide.setConsent("in");
    } else {
      window.Prehide.setConsent("out");
    }
  });
}
```

### 示例：TCF/IAB样式

```js
// Optional: pause the guard while UI is up.
window.Prehide.setConsent("pending");

// Your CMP eventually emits the final TC string.
function onTcData(tcData) {
  const hasTargetConsent = /* derive from tcData */;
  window.Prehide.setConsent(hasTargetConsent ? "in" : "out");
}
```

