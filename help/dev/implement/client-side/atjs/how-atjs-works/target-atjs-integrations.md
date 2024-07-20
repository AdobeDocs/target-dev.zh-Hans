---
keywords: at.js 集成, 受支持的集成, 不受支持的集成, 第三方集成
description: 查看 [!DNL Adobe Target] at.js支持（和不支持）的集成，包括[!UICONTROL Analytics for Target] (A4T)、[!UICONTROL Experience Cloud ID Service]等。
title: at.js支持哪些集成？
feature: at.js
exl-id: d2c61e77-5fc7-4c35-905b-76b8c4f9df4b
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 57%

---

# at.js 集成

有关与 [!DNL Adobe Target] 的常见集成及其对 at.js 的支持状态的信息。

如果您迫切需要不受支持或此处未提及的集成，请联系您的客户代表或顾问。

## 受支持的集成

| 集成 | 详细信息 |
|--- |--- |
| [!UICONTROL Analytics for Target] (A4T) | 请参阅[将 Adobe Analytics 作为 Adobe Target 报表源 (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html)。 |
| [!UICONTROL Profiles & Audiences] (P&amp;A) | 请参阅&#x200B;*核心服务用户指南*&#x200B;中的[受众](https://experienceleague.adobe.com/docs/core-services/interface/audiences/audience-library.html??lang=zh-Hans)。 |
| [!UICONTROL Experience Cloud ID Service] | 请参阅 [Adobe Experience Cloud ID 服务文档](https://experienceleague.adobe.com/docs/id-service/using/home.html)。 |
| [!UICONTROL Tags in Adobe Experience Platform] | [!UICONTROL Tags in Adobe Experience Platform]是新一代[!DNL Adobe]的标签管理功能。 [!UICONTROL Tags]为客户提供了一种简单的方式来部署和管理用来加强相关客户体验的分析、营销和广告标记。 请参阅[使用Adobe Experience Platform](../how-to-deployatjs/implement-target-using-adobe-launch.md)实施 [!DNL Target] 。 |
| [!UICONTROL Adobe Experience Manager] (AEM)Cloud Service | [!UICONTROL AEM Cloud Service]允许在AEM工作流中创建[!UICONTROL A/B Test]和[!UICONTROL Experience Targeting]活动。 支持带有[!UICONTROL Adobe Experience Manager]的at.js带有FP-11577的6.2（或更高版本）。 有关详细信息，请参阅[与 [!DNL Adobe Target]集成](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html)并选择您的AEM版本。 |
| [!UICONTROL AEM Experience Fragments] | 通过在[!DNL Target]活动的AEM中创建的体验片段，您可以将AEM的易用性和强大功能与[!DNL Target]中强大的自动智能(AI)和机器学习(ML)功能相结合，以测试和大规模个性化体验。  AEM 可将您的所有内容和资产汇集到一个中心位置，以帮助实施您的个性化策略。通过 AEM，您能够在一个位置轻松创建适用于桌面、平板电脑和移动设备的内容，而无需编写代码。无需为每个设备创建页面，AEM会自动使用您的内容来调整每个体验。  请参阅[AEM 体验片段](https://experienceleague.adobe.com/docs/target/using/experiences/offers/aem-experience-fragments.html)。 |

## 不受支持的集成

| 集成 | 详细信息 |
|--- |--- |
| 旧版[!DNL Target]与[!DNL SiteCatalyst]的集成 | 该集成通过页面调用将营销活动ID和方法ID发送到[!DNL SiteCatalyst]，以便您可以在[!DNL SiteCatalyst] UI中生成报表。 此功能已被 A4T 所替代。 |
| 旧版[!DNL Target]与[!DNL SiteCatalyst]的集成 | 该集成可发起名为 `"SiteCatalyst: Event"` 和 `"SiteCatalyst: Purchase"` 的 mbox 调用，从而根据 evar 和 prop 构建成功量度和用户配置文件。此功能已被 A4T 和 P&amp;A 所替代。 |
| 旧版[!DNL Audience Manager] (AAM)与[!DNL Target]的集成 | 该集成可发起前端 API 调用以检索 AAM 区段，然后将检索到的区段作为页面上各个 mbox 调用中的 mbox 参数进行发送。 |

## 第三方集成

| 集成 | 详细信息 |
|--- |--- |
| 其他标签管理器 | at.js 应该可以在非 Adobe 标签管理平台中使用，但是使用由其他供应商开发的自定义集成功能时要小心谨慎。其他供应商提供的集成可能会依赖一些内部 mbox.js 函数，而 at.js 中已不再存在这些函数。 |
| 第三方数据提供程序（例如 Demandbase、Bluekai、天气 API） | 使用 at.js [数据提供程序](../atjs-functions/targetglobalsettings.md#data-providers)功能，可以集成许多用于补充 Target 用户分析的第三方数据提供程序. |
