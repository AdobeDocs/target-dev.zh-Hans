---
keywords: 移动设备应用程序, 移动设备应用程序发送数据, 定位移动设备应用程序, 移动设备自定义用户数据, 移动设备应用程序自定义数据
description: 了解如何以名称 — 值对的形式向 [!DNL Adobe Target] 发送有关位置或用户的其他信息，以帮助您构建自定义受众。
title: 如何在iOS应用程序中发送自定义用户数据？
feature: Implement Mobile
exl-id: 9cf8e8fd-1898-43b1-b339-d7a21cb35d57
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 55%

---

# iOS - 发送自定义用户数据

您可以将有关位置或用户的其他信息以名称 — 值对的形式发送到[!DNL Target]。

>[!IMPORTANT]
>
>支持[!DNL Adobe Mobile]版本4。*x* SDK已于2021年8月31日结束，不再推荐用于[!DNL Adobe Target]移动用户。
>
>适用于移动设备应用程序的[Adobe Experience Platform SDK](https://developer.adobe.com/client-sdks/documentation/){target=_blank}是推荐的解决方案，旨在为您的移动设备应用程序中的[!DNL Adobe Experience Cloud]解决方案和服务提供支持。

此信息可用于在报表中构建自定义受众（例如，距离超过 25000 英里的用户）。

有两种类型的参数可以通过[!DNL Target]调用发送：

* **mbox参数**： mbox参数不是跨会话持久性的。
* **配置文件参数**：配置文件参数存储在访客配置文件存储中，并且跨会话持续存在。 mbox参数不持久。 虽然保留了一些键，但是配置文件参数和 mbox 参数都可以是自定义键值对。

虽然存在一些保留键，但是配置文件参数和 mbox 参数都可以包含自定义键值对。

1. 创建字典。

   首先，使用您发送的要传递到[!DNL Target]的值创建一个字典。 为方便起见，请将此字典添加到 `welcomeMessageCampaign` 方法中，这样便无需担心范围问题。

   以下是一个示例字典。您可以将此字典复制并粘贴到 `(void)welcomeMessageCampaign` 中。在此示例中，对 `userLevel` 和 `userMiles` 等键的值进行了硬编码。一般情况下，您需要传入对应的变量。

   ```
   NSDictionary *targetParams = [[NSDictionary alloc] initWithObjectsAndKeys: 
                                 @"platinum",@"userLevel", 
                                 @26500,@"userMiles", 
                                 @"1067007",@"entity.id", 
                                 @"dealsapp.qa", @"host", 
                                 @"fashion",@"entity.categoryId", 
                                 @"millenial", @"profile.persona", 
                                 @"cohort_5", @"profile.cohort", 
                                 nil];
   ```

   * 前缀为“profile”的键（例如 `profile.persona`）存储在用户的配置文件中。

     这些配置文件属性可以在不同的活动和渠道中使用。

   * 没有任何前缀的键（例如 `userMiles`）为 mbox 参数。

     这些参数只能在会话期间使用。

   * 前缀为“entity”的键（例如 `entity.category.id`）用于产品推荐。

1. 验证数据。
   1. 在应用程序 `didFinishLaunchingWithOptions` 中，取消注释或添加 `[ADBMobile setDebugLogging:YES];`。

      这会打印详细的调试日志。
   1. 构建应用程序。
   1. 确认已将参数传入 Target 调用。

      在调试控制台中搜索您的 Target 位置名称。您将会看到对 `YOUR-CLIENT-CODE.tt.omtrdc.net` 的调用，其中包含您刚刚传递的所有参数。

      （单击图像可展开至全宽。）

      ![调试控制台中的Target位置](/help/dev/implement/mobile/assets/mobile-debug.png "调试控制台中的Target位置"){zoomable="yes"}

   您可以在[!DNL Target]中使用这些参数构建受众，并限制或定位内容显示。
