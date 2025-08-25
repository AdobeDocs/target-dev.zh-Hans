---
title: Adobe Target投放API注意事项和已知限制
description: 使用[!UICONTROL Adobe Target Delivery API]时应该考虑哪些注意事项和已知限制？
keywords: 投放api
exl-id: 49fe13b0-efcb-4b1c-a4cb-03b64fbd9214
feature: APIs/SDKs
source-git-commit: 94a4122244065384f487ca9a29dfa1b414168cb8
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 6%

---

# 注意事项和已知限制

以下信息列出了使用[!DNL Adobe Target] [!DNL Delivery API]的注意事项和已知限制。

* [!DNL Target]投放API没有身份验证。
* 此 API 不处理 Cookie 或重定向调用。
* HTTP/1.1和HTTP/2标头名称不区分大小写；但是，HTTP/2强制使用小写标头名称。 有关详细信息，请参阅[超文本传输协议版本2 (HTTP/2)文档](https://www.rfc-editor.org/rfc/rfc7540#section-8.1.2){target=_blank}。

  如果您使用通过我们的新负载平衡器基础架构路由访客的端点，则其连接会自动升级到HTTP/2。 此升级过程会将请求标头转换为小写标头，以便它们不会被视为格式不正确。

  如果客户的库设置为查找区分大小写（尤其是小写）的请求/响应标头，则此问题可能会为客户带来问题。
