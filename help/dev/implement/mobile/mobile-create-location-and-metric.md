---
keywords: 移动设备应用程序, 移动设备应用程序位置, 定位移动设备应用程序, 移动设备 Target 位置, 移动设备应用程序成功量度
description: 查看示例代码，以帮助您了解如何在iOS应用程序中创建位置和成功量度以便使用 [!DNL Adobe Target] 以个性化和优化您的应用程序。
title: 如何创建 [!DNL Target] iOS应用程序中的位置和成功量度？
feature: Implement Mobile
exl-id: 755c8b26-5c60-48fc-9e7e-5e97a25edb78
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 67%

---

# iOS — 创建 [!DNL Target] 位置和成功量度

使用 [!DNL Target] 在您的移动设备应用程序中，创建位置和成功量度。

>[!IMPORTANT]
>
>支持 [!DNL Adobe Mobile] 版本4。*x* SDK已于2021年8月31日结束，不再建议用于 [!DNL Adobe Target] 移动用户。
>
>此 [适用于移动应用程序的Adobe Experience Platform SDK](https://developer.adobe.com/client-sdks/documentation/){target=_blank} 是推荐的电源解决方案 [!DNL Adobe Experience Cloud] 解决方案和服务。

本节包含的示例代码可用作应用程序的模板。本节中的示例包含适用于 iOS 的代码。相同的模式也适用于 Android。在[](https://experienceleague.adobe.com/docs/mobile-services/android/target-android/target-main.html)《适用于 Experience Cloud 解决方案的 Android SDK 4.x》指南中可以找到特定于 Android 的语法。

>[!NOTE]
>
>请参阅 [移动设备文档](https://experienceleague.adobe.com/docs/mobile-services/ios/target-ios/c-target-methods.html) 以获取所有可用的 [!DNL Target] 方法。

创建 [!DNL Target] 在您的应用程序中放置位置并进行请求，主要可以使用以下两种方法：

* `targetCreateRequestWithName`
* `targetLoadRequest`

1. 创建 [!DNL Target] 位置。

   下面是用于创建请求的示例调用：

   ```
   // make your request 
   ADBTargetLocationRequest *myRequest = [ADBMobile targetCreateRequestWithName:@"heroBanner" 
                                                    defaultContent:@"default.png" 
                                                    parameters:nil];
   ```

   | 参数 | 描述 |
   |---|---|
   | `ADBTargetLocationRequest *myRequest` | 将 `myRequest` 替换为应用程序中您的 `targetLocation` 的名称。 |
   | `targetCreateRequestWithName:@"heroBanner"` | 将 `heroBanner` 替换为 Target 中您的 `targetLocation` 的名称。此名称与 mbox 名称相同。此主页横幅显示在 Target 界面中。 |
   | `defaultContent:@"default.png"` | 将 `default.png` 替换为 Target 未做出响应时应用程序所使用的值。 |
   | `parameters:nil` | 指定配置文件或 mbox 参数。有关更多信息，请参阅“传递自定义数据”部分。 |

   下面是用于加载请求的示例调用：

   ```
   // load your request 
   [ADBMobile targetLoadRequest:myRequest callback:^(NSString *content) { 
                                        // do something with content 
                                        heroImage.image = [UIImage imageNamed:content]; 
   }];
   ```

   | 参数 | 描述 |
   |---|---|
   | `targetLoadRequest:myRequest` | 将 `myRequest` 替换为应用程序中您的 `targetLocation` 的名称。 |
   | `NSString *content` | 将 content 替换为从 Adobe 返回的实际内容。该字符串可以是 XML、JSON 或纯字符串。使用此部分代码，可定义变量、设置图像路径、查看控制器流和交易点，或执行任何其他所需操作。Target 会以完全相同的格式在 UI 中返回输入的内容。 |
   | `heroImage.image = [UIImage imageNamed:content];` | 例如：获取内容并设置主页图像的路径。 |

1. 创建成功量度。

   方法 `targetCreateOrderConfirmRequestWithName` 可用于跟踪您应用程序中的转化/成功量度。

   ```
   ADBTargetLocationRequest *req = [ADBMobile targetCreateOrderConfirmRequestWithName: "orderConfirm" 
                                              orderId: orderId 
                                              orderTotal: @"39.95" 
                                              productPurchasedId: _galleryItem.title 
                                              parameters: nil]; 
   [ADBMobile targetLoadRequest: req callback: nil];
   ```

   | 参数 | 描述 |
   |---|---|
   | `orderId` | 替换为表示唯一订单 ID 的动态变量。 |
   | `@"39.95"` | 替换为表示唯一订单总量的动态变量。 |
   | `_galleryItem.title` | 替换为表示已购产品的逗号分隔列表的动态变量。 |
   | `parameters: nil` | 其他参数的可选字典。 |

1. 构建应用程序。

   步骤结果：在成功创建 Target 位置并标记成功量度后，请创建 A/B 测试。可使用基于表单的体验编辑器来创建该活动。
