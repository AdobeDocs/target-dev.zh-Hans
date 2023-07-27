---
title: Adobe Target投放API注意事项和已知限制
description: 使用时，应考虑哪些注意事项和已知限制 [!UICONTROL Adobe Target交付API]？
keywords: 投放api
exl-id: 49fe13b0-efcb-4b1c-a4cb-03b64fbd9214
feature: APIs/SDKs
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 7%

---

# 注意事项和已知限制

* 没有针对以下项的身份验证 [!DNL Target] 投放API。
* 此 API 不处理 Cookie 或重定向调用。
* 支持 [!UICONTROL Automated Personalization] (AP)和 [!UICONTROL Recommendations] 活动：此API具有两种获取内容的模式：执行和预取模式。 预取模式只能用于 [!UICONTROL AB测试] 和 [!UICONTROL 体验定位] (XT)活动。 请勿对使用预取模式 [!UICONTROL Automated Personalization] （美联社）， [!UICONTROL 自动分配]， [!UICONTROL 自动定位]，或 [!UICONTROL Recommendations] 活动类型。
* HTTP/1.1和HTTP/2标头名称不区分大小写；但是，HTTP/2强制使用小写标头名称。 欲了解更多信息，请参见 [超文本传输协议版本2 (HTTP/2)文档](https://www.rfc-editor.org/rfc/rfc7540#section-8.1.2){target=_blank}.

  如果您使用通过我们的新负载平衡器基础架构路由访客的端点，则其连接会自动升级到HTTP/2。 此升级过程会将请求标头转换为小写标头，以便它们不会被视为格式不正确。

  如果客户的库设置为查找区分大小写（尤其是小写）的请求/响应标头，则此问题可能会为客户带来问题。
