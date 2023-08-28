---
keywords: 移动应用程序，aep sdk，本机应用程序，Web视图，本机；swift，adobe experience platform移动sdk，移动sdk，本机代码
description: 了解如何实施 [!DNL Adobe Target] 使用 [!DNL AEP Mobile SDK] 在本机应用程序中使用Web视图。
title: 实施 [!DNL Adobe Target] 在通过Web视图使用本机代码的移动设备应用程序中
feature: Implement Mobile
role: Developer
source-git-commit: c0fda36cb5472d71438c47b8b484716003da4214
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 0%

---


# 实施 [!DNL Target] 使用 [!DNL AEP Mobile SDK] 在本机应用程序中使用Web视图

本文分享了实施的最佳实践 [!DNL Adobe Target] 在将本机代码与Web视图结合使用的移动应用程序中，使用 [!DNL Adobe Experience Platform Mobile SDK].

本文使用示例iOS应用程序，其中 [[!DNL Adobe Experience Platform Mobile SDK]](https://developer.adobe.com/client-sdks/documentation/getting-started/){target=_blank} and a [!DNL Target] integration written in [Swift from the GitHub repository](https://github.com/adobe/aep-sdk-app/){target=_blank}.

在现实中，您的企业应用程序可能会使用移动应用程序中的Web视图。 Web视图是一个使用URL加载网页的容器。 该容器类似于没有控件的浏览器窗口。 在iOS中，处理网页时，Web视图容器可充当Safari浏览器。

## 先决条件

要开始使用 [!DNL Adobe Experience Platform Mobile SDK]中，您必须执行一些先决任务。

有关更多信息，请参阅 [Adobe Target](https://developer.adobe.com/client-sdks/documentation/adobe-target/){target=_blank} in the [[!DNL Adobe Experience Platform Mobile SDK]](https://developer.adobe.com/client-sdks/documentation/){target=_blank} 文档。

## 将本机代码与Web视图同步

实施方面的挑战 [!DNL Target] 在具有Web视图的本机应用程序中， [!DNL Adobe Experience Platform Mobile SDK] 已生成以下项所需的所有必需标识符： [!DNL Adobe] 解决方案无缝工作。 但是，这些标识符对Web视图尚不可见，因为这些标识符在本机Platform环境中不存在。 因此，您必须创建一个桥接器以将某些SDK标识符传递到Web视图，以便访客身份保留在Web环境中。 如果不正确执行此操作，则会导致重复访问，从而影响您的报表。

幸运的是， [!DNL Adobe Experience Platform Mobile SDK] 提供了一种简便的生成方法 [!DNL Adobe] Web视图需要参数来使用和保留同一访客，如以下示例代码中所示：

```swift
Identity.appendTo(url: URL(string: url), completion: {appendedURL, error in
  print("appendedURL \(String(describing: appendedURL))")
  // load the url with ECID on the main thread
  DispatchQueue.main.async {
    let request = NSMutableURLRequest(url: appendedURL!)
    self.webView.load(request as URLRequest)
  }
});
```

欲知关于 `Identity.appendTo` 方法，要了解如何使用该方法的示例，请参阅 [Swift >示例](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/tabs/api-reference/){target=_blank} 在 *移动SDK文档*.

使用 `Identity.appendTo`，此URL：

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2
```

转换为：

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2&adobe_mc=TS%3D1660667205%7CMCMID%3D69624092487065093697422606480535692677%7CMCORGID%3DEB9CAE8B56E003697F000101%40AdobeOrg
```

如您所见，有 `adobe_mc` 附加到URL的参数。 此参数包含下列内容的编码值：

* TS=1660667205：当前时间戳。 此时间戳可确保Web视图不会接收过期的值。
* MCMID=69624092487065093697422606480535692677： [!UICONTROL EXPERIENCE CLOUDID] (ECID)。 也称为MID或 [!UICONTROL MARKETING CLOUDID] 需要 [!DNL Adobe] 跨解决方案访客识别。
* MCORGID=EB9CAE8B56E003697F000101@AdobeOrg： [!UICONTROL Adobe组织ID].

此 `Identity.getUrlVariables` 是替代项 [!DNL Adobe Experience Platform Mobile SDK] 方法，返回一个格式正确的字符串，该字符串包含 [!DNL Experience Cloud Identity Service] URL变量。 有关更多信息，请参阅 [getUrlVariables](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/api-reference/#geturlvariables){target=_blank} 在 *身份API引用*.

## 传递 [!DNL Target] 相同会话体验的会话ID

还需要执行一个额外的步骤，以使 [!DNL Target] 用户历程可在本机视图和Web视图之间无缝工作。 此步骤包括提取和传递 [!DNL Target] 来自的会话ID [!DNL Adobe Experience Platform Mobile SDK] 移动应用程序的Web视图。

此 `Target.getSessionId` 提取可以作为Web视图URL传递的会话ID `mboxSession` 参数：

```swift
Target.getSessionId { (id, err) in
    // read Target sessionId
}
```

## 在Web视图中测试

Web预览链接生成于 [!UICONTROL 活动详细信息] 页面，方法是单击 [[!UICONTROL ADOBEQA] 链接](/help/dev/implement/mobile/target-mobile-preview.md) 要显示用于复制每个体验预览链接的弹出窗口，请执行以下操作：

```
?at_preview_token=mhFIzJSF7JWb-RsnakpBqi_s83Sl64hZp928VWpkwvI&at_preview_index=1_1&at_preview_listed_activities_only=true
```

Web预览链接包含其他 `at_preview_index` 和 `at_preview_listed_activities_only` 参数。 复制这些参数以使用Web链接参数构建移动友好的预览链接。

例如：

```
com.adobe.targetmobile://?at_preview_token=mhFIzJSF7JWb-RsnakpBqhBwj-TiIlZsRTx_1QQuiXLIJFdpSLeEZwKGPUyy57O_&at_preview_index=1_1&at_preview_listed_activities_only=true
```

在iOS Safari浏览器中打开该链接后，您的应用程序会捕获 `AppDelegate` 类类似于以下示例：

```swift
func application(_ app: UIApplication, open url: URL, options: [UIApplicationOpenURLOptionsKey : Any] = [:]) -> Bool {
  print("url= \(String(describing: url.absoluteString))")
  //...
```

现在，您已捕获应用程序中的所有必要参数，可以在必要时将这些参数传递到Web：

```swift
Identity.appendTo(url: URL(string: url), completion: {appendedURL, error in
  let urlWithWebPreviewLink = appendedURL + "&" + myPreviewLinkFromAppDelegate
```

Web视图链接的最终输出可能如下所示：

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2&adobe_mc=TS%3D1660667205%7CMCMID%3D69624092487065093697422606480535692677%7CMCORGID%3DEB9CAE8B56E003697F000101%40AdobeOrg&at_preview_token=mhFIzJSF7JWb-RsnakpBqi_s83Sl64hZp928VWpkwvI&at_preview_index=1_1&at_preview_listed_activities_only=true
```
