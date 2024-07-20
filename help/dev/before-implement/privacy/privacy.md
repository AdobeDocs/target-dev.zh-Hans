---
keywords: 隐私， ip地址，地域划分，选择退出，选择退出，数据隐私，政府法规，法规， gdpr， ccpa，隐私，个人身份信息， PII
description: 了解 [!DNL Adobe Target] 如何遵守适用的数据隐私法，包括IP地址、PII和选择退出指令的收集和处理。
title: Target如何处理隐私问题（包括PII）？
feature: Privacy & Security
exl-id: 4330e034-2483-4a25-9c87-48dbef6fc9de
source-git-commit: 88bde40aa6dfb96e1d53e4db6ba5547d38dbbb99
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 43%

---

# 隐私

[!DNL Adobe Target] 启用了一些流程和设置，使您能够在遵守适用数据隐私法律的情况下使用 [!DNL Target]

## IP地址和个人身份信息(PII)的收集

网站访客的 IP 地址会传输到 Adobe 数据处理中心 (DPC)。根据访客的网络配置，IP地址不一定代表访客计算机的IP地址。 例如，IP 地址可能为网络地址转换 (NAT) 防火墙、HTTP 代理或互联网网关的外部 IP 地址。

>[!IMPORTANT]
>
>[!DNL Target]不存储用户的任何IP地址或任何个人身份信息(PII)。 IP地址仅由[!DNL Target]在会话（内存中，从不保留）期间使用。

## 替换 IP 地址的最后一个八位字节

Adobe开发了“通过设计保护隐私”设置，用户可以为Adobe[!DNL Target]启用该设置。 启用后，Adobe[!DNL Target]会在收集IP地址时立即模糊处理IP地址的最后八位字节（最后一部分）。 此匿名化在 IP 地址的任意处理之前执行，包括在可选的 IP 地址地理位置查找之前。

当启用此功能时，会对 IP 地址进行充分地匿名化处理，以便它不能再被识别为个人信息。因此，在不允许收集个人信息的国家/地区，[!DNL Target]可用于遵守数据隐私法。 获取城市级别信息很有可能会受到 IP 地址模糊处理的影响。获得地区和国家级别信息应该只会受到轻微影响。

通过导航到&#x200B;**[!UICONTROL Administration]** > **[!UICONTROL Implementation]**，可在[!DNL Target] UI中使用以下设置：

* [!UICONTROL Last octet obfuscation]： [!DNL Target]隐藏IP地址的最后一个八位字节。
* [!UICONTROL Entire IP obfuscation]： [!DNL Target]隐藏整个IP地址。
* [!UICONTROL None]： [!DNL Target]不隐藏IP地址的任何部分。

  ![obfuscate-ip-options](assets/obfuscate-ip.png)

[!DNL Target]接收完整IP地址并根据指定对其进行模糊处理（如果设置为“最后八位字节”或“整个IP”）。 然后，[!DNL Target]仅在当前会话期间将模糊处理的IP地址保存在内存中。

### 使用[!DNL Adobe Experience Platform Web SDK]时的数据流级别IP模糊处理 {#aep}

使用[!DNL Platform Web SDK]（版本23.4或更高版本）时，数据流级别的IP模糊处理设置优先于[!DNL Target]中设置的任何IP模糊处理选项。 例如，如果数据流级别的IP模糊处理选项设置为[!UICONTROL Full]，而[!DNL Target] IP模糊处理选项设置为[!UICONTROL Last octet obfuscation]，则[!DNL Target]接收完全模糊处理的IP。

有关详细信息，请参阅&#x200B;*[!DNL Adobe Experience Platfrom]数据流指南*&#x200B;中的[配置数据流](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=zh-Hans){target=_blank}中的[!UICONTROL IP Obfuscation]。

## 地域划分

如果启用替换IP地址的最后八位字节，则可以使用[!DNL Target]中的报告分析IP地址的剩余值。 如果未对IP地址的最后一个八位字节进行模糊处理，则可在[!DNL Target]中分析完整的IP地址。 您可以使用地域划分功能来按地理区域在地图上标出访客位置。地域划分数据只精确到城市级别或邮政编码级别，而不能精确到个人级别。

如果对 IP 地址进行了完全模糊处理，则无法使用地域划分和地域定位。

## 选择退出链接

您可以向网站添加选择退订链接，使访客可以选择退订所有计数和内容发送服务。

1. 请为您的网站添加以下链接：

   `<a href="https://clientcode.tt.omtrdc.net/optout"> Your Opt Out Language Here</a>`

1. （视情况而定）如果您在使用CNAME，则链接应包含“client=`clientcode`参数，例如：
   `https://my.cname.domain/optout?client=clientcode`。

1. 使用您的客户端代码替换 `clientcode`，然后添加要链接到选择退出 URL 的文本或图像。

点击该链接的任何访客都不会包含在通过浏览会话调用的任何 mbox 请求中，直到他们删除 Cookie 或两年后（以时间在先者为准）为止。这通过在 `disableClient` 域中为访客设置称为 `clientcode.tt.omtrdc.net` 的 Cookie 实现。

即使您使用第一方 Cookie 实施，提供的选择退订也将通过第三方 Cookie 进行设置。如果客户端仅使用第一方Cookie，[!DNL Target]会检查是否设置了选择退出Cookie。

## 隐私和数据保护法规

有关欧盟的通用数据保护条例(GDPR)、加州消费者隐私法案(CCPA)和其他国际隐私要求的信息，以及这些法规对您的组织和[!DNL Target]的影响，请参阅[隐私和数据保护法规](/help/dev/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.md)。

## 功能使用数据集合

单独的功能使用情况数据会被收集用于内部Adobe，以确定[!DNL Target]功能是否按意图执行或者确定利用率不足的功能。 各个延迟测量值会被收集用于帮助解决性能问题。不收集个人数据。

您可在客户端初始化选项中，通过将 `telemetryEnabled` 设置为 false 来选择在 SDK 中禁用报表使用情况数据。有关更多信息，请参阅 [targetGlobalSettings 中的 telemetryEnabled](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md#telemetryenabled)。
