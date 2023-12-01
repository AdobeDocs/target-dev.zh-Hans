---
title: Adobe Target单个配置文件更新API
description: 了解如何使用 [!DNL Adobe Target] [!UICONTROL 单个配置文件更新API] 将单个访客的配置文件数据发送到 [!DNL Target].
feature: APIs/SDKs
contributors: https://github.com/icaraps
source-git-commit: dcff5d2eb8740420a9f9cf488474c3bca1628567
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 4%

---

# [!DNL Adobe Target Single Profile Update API]

此 [!DNL Adobe Target] [!UICONTROL 单个配置文件更新API] 允许您为单个用户发送配置文件更新。 此 [!UICONTROL 单个配置文件更新API] 几乎与 [!UICONTROL 批量配置文件更新API]，但一次更新一个访客资料，与API调用而不是.cvs文件内联。

此 [!UICONTROL 单个配置文件更新API] 并且通常用于必须针对在尚未实施的渠道中发生的事务进行更新时 [!DNL Target]. 例如，要更新执行某些离线操作的单个访客的配置文件。 操作包括联系呼叫中心、资助贷款、在商店中使用会员卡、访问自助服务亭等。

的优势 [!UICONTROL 单个配置文件更新API] 包括：

* 配置文件属性的数量没有限制。
* 通过网站发送的用户档案属性可以通过API更新，反之亦然。

## 注意事项

* 此 [!UICONTROL 单个配置文件更新API] 限于在任何滚动的24小时内执行100万次更新。
* 更新通常在一小时内发生，但可能需要24小时才能反映出来。

  如果必须发送更多更新，或需要在较短的时间范围内处理更新，请考虑通过客户端更新（首选）或通过 [!DNL Adobe Target] 服务器端 [投放API](/help/dev/implement/delivery-api/overview.md).

* 此 [!UICONTROL 单个配置文件更新API] 是一个服务器到服务器API，设计初衷不是在网页中工作。 要从您的网页中更新访客资料，您可以使用 [trackEvent()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md) 函数或 [投放API](/help/dev/implement/delivery-api/overview.md).

## 格式

以格式指定配置文件参数 `profile.paramName=value`.

要更新用户档案，请执行以下操作 `pcId`，使用：

``````
https://<your-client-code>.tt.omtrdc.net/m2/client/profile/update?mboxPC=1368007744041-575948.01_00&profile.attr=0&profile.attr2=1...
``````

要更新用户档案的 `mbox3rdPartyId`，使用：

``````
shell http://<your-client-code>.tt.omtrdc.net/m2/client/profile/update?mbox3rdPartyId=123456&profile.attr=0&profile.attr2=1...
``````

此 [!UICONTROL 单个配置文件更新API] 仅用于更新。 如果未找到任何内容，则不会创建配置文件。

## 注释

* 参数和值必须使用UTF-8进行URL编码。
* 参数格式为 `profile.paramName`.
* 并非所有pcIds和mbox3rdPartyIds都必须存在所有参数值。
* 参数和值区分大小写。
* 同时支持GET和POST。
* 当前的大小限制为：GET为8 KB，POST为60 KB。

## 响应

上述请求的示例响应如下所示：

`trueRequest successfully submitted`

此响应表示响应已提交，将很快处理。