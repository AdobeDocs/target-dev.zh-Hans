---
keywords: 移动应用程序，aep sdk，本机应用程序，Web视图，本机；swift，adobe experience platform移动sdk，移动sdk，本机代码
description: 了解如何在具有Web视图的本机应用程序中使用 [!DNL AEP Mobile SDK] 实施 [!DNL Adobe Target] 。
title: 在使用带有Web视图的本机代码的移动应用程序中实施 [!DNL Adobe Target]
feature: Implement Mobile
role: Developer
exl-id: 3dd2e1d7-c744-4ba8-aaa4-6c2fe64d01fa
source-git-commit: 50ee7e66e30c0f8367763a63b6fde5977d30cfe7
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# 在具有Web视图的本机应用程序中通过[!DNL AEP Mobile SDK]实施[!DNL Target]

本文分享在移动应用程序中实施[!DNL Adobe Target]的最佳实践，该应用程序使用[!DNL Adobe Experience Platform Mobile SDK]在Web视图中使用本机代码。

本文使用来自GitHub存储库[&#128279;](https://github.com/adobe/aep-sdk-app/){target=_blank}的[[!DNL Adobe Experience Platform Mobile SDK]](https://developer.adobe.com/client-sdks/documentation/getting-started/){target=_blank}和在Swift中编写的[!DNL Target]集成作为示例iOS应用程序。

在现实中，您的企业应用程序可能会使用移动应用程序中的Web视图。 Web视图是一个使用URL加载网页的容器。 该容器类似于没有控件的浏览器窗口。 在iOS中，处理网页时，Web视图容器可充当Safari浏览器。

## 先决条件

要开始使用[!DNL Adobe Experience Platform Mobile SDK]，您必须执行一些先决任务。

有关详细信息，请参阅[[!DNL Adobe Experience Platform Mobile SDK]](https://developer.adobe.com/client-sdks/documentation/){target=_blank}文档中的[Adobe Target](https://developer.adobe.com/client-sdks/documentation/adobe-target/){target=_blank}。

## 将本机代码与Web视图同步

在使用Web视图的本机应用程序中实施[!DNL Target]时，面临的挑战是[!DNL Adobe Experience Platform Mobile SDK]已生成了[!DNL Adobe]解决方案无缝工作所需的所有必要标识符。 但是，这些标识符对Web视图尚不可见，因为这些标识符在本机Platform环境中不存在。 因此，您必须创建一个桥接器以将某些SDK标识符传递到Web视图，以便访客身份保留在Web环境中。 如果不正确执行此操作，则会导致重复访问，从而影响您的报表。

幸运的是，[!DNL Adobe Experience Platform Mobile SDK]提供了一种方便的方法来生成Web视图使用并保留同一访客所需的[!DNL Adobe]参数，如以下示例代码中所示：

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

有关`Identity.appendTo`方法的详细信息，并查看如何使用该方法的示例，请参阅&#x200B;*Mobile SDK文档*&#x200B;中的[Swift >示例](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/tabs/api-reference/){target=_blank}。

使用`Identity.appendTo`，此URL：

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2
```

转换为：

```
https://vadymus.github.io/ateng/at-order-confirmation/index.html?a=1&b=2&adobe_mc=TS%3D1660667205%7CMCMID%3D69624092487065093697422606480535692677%7CMCORGID%3DEB9CAE8B56E003697F000101%40AdobeOrg
```

如您所见，URL附加了`adobe_mc`参数。 此参数包含下列内容的编码值：

* TS=1660667205：当前时间戳。 此时间戳可确保Web视图不会接收过期的值。
* MCMID=69624092487065093697422606480535692677： [!UICONTROL Experience Cloud ID] (ECID)。 也称为[!DNL Adobe]跨解决方案访客识别所需的MID或[!UICONTROL Marketing Cloud ID]。
* MCORGID=EB9CAE8B56E003697F000101@AdobeOrg： [!UICONTROL Adobe Organization ID]。

`Identity.getUrlVariables`是一种替代[!DNL Adobe Experience Platform Mobile SDK]方法，它返回包含[!DNL Experience Cloud Identity Service] URL变量的格式正确的字符串。 有关详细信息，请参阅&#x200B;*标识API引用*&#x200B;中的[getUrlVariables](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/api-reference/#geturlvariables){target=_blank}。

## 传递用于相同会话体验的[!DNL Target]会话ID

还需要执行一个额外的步骤，以使[!DNL Target]用户历程在本机视图和Web视图之间无缝工作。 此步骤包括从[!DNL Adobe Experience Platform Mobile SDK]提取[!DNL Target]会话ID并将其传递给移动设备应用程序的Web视图。

`Target.getSessionId`提取可以作为`mboxSession`参数传递到Web视图URL的会话ID：

```swift
Target.getSessionId { (id, err) in
    // read Target sessionId
}
```

## 在Web视图中测试

通过单击[[!UICONTROL Adobe QA]链接](/help/dev/implement/mobile/target-mobile-preview.md)在[!UICONTROL Activity detail]页面上生成Web预览链接，以显示弹出窗口来复制每个体验预览链接，如下所示：

```
?at_preview_token=mhFIzJSF7JWb-RsnakpBqi_s83Sl64hZp928VWpkwvI&at_preview_index=1_1&at_preview_listed_activities_only=true
```

Web预览链接包含其他`at_preview_index`和`at_preview_listed_activities_only`参数。 复制这些参数以使用Web链接参数构建移动友好的预览链接。

例如：

```
com.adobe.targetmobile://?at_preview_token=mhFIzJSF7JWb-RsnakpBqhBwj-TiIlZsRTx_1QQuiXLIJFdpSLeEZwKGPUyy57O_&at_preview_index=1_1&at_preview_listed_activities_only=true
```

在iOS Safari浏览器中打开该链接后，您的应用程序会捕获`AppDelegate`类中的URL，类似于以下示例：

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
