---
title: Adobe Target单个配置文件更新API
description: 了解如何使用 [!DNL Adobe Target] [!UICONTROL Single Profile Update API]将单个访客的配置文件数据发送到 [!DNL Target]。
feature: APIs/SDKs
contributors: https://github.com/icaraps
exl-id: 4e022db3-215f-461b-9222-38ce2f2dbc28
source-git-commit: e2462d12cf58ab5a588c13a96df5e6abafb9d675
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 3%

---

# [!DNL Adobe Target Single Profile Update API]

[!DNL Adobe Target] [!UICONTROL Single Profile Update API]允许您为单个用户发送配置文件更新。 [!UICONTROL Single Profile Update API]几乎与[!UICONTROL Bulk Profile Update API]相同，但一次更新一个访客资料，与API调用内联，而不是.cvs文件。

[!UICONTROL Single Profile Update API]和通常用于必须发生与未实现[!DNL Target]的渠道中发生的事务相关的更新时。 例如，要更新执行某些离线操作的单个访客的配置文件。 操作包括联系呼叫中心、资助贷款、在商店中使用会员卡、访问自助服务亭等。

[!UICONTROL Single Profile Update API]的优点包括：

* 配置文件属性的数量没有限制。
* 通过网站发送的用户档案属性可以通过API更新，反之亦然。

## 注意事项

* [!UICONTROL Single Profile Update API]被限制为在任何滚动的24小时内执行100万次更新。
* 更新通常在一小时内发生，但可能需要24小时才能反映出来。

  如果必须发送更多更新，或需要在较短的时间范围内处理更新，请考虑通过客户端更新（首选）或通过[!DNL Adobe Target]服务器端[投放API](/help/dev/implement/delivery-api/overview.md)发送事务性用户档案更新。

* [!UICONTROL Single Profile Update API]是服务器到服务器API，设计为在网页中工作。 若要从您的网页中更新访客资料，您可以使用[trackEvent()](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)函数或[交付API](/help/dev/implement/delivery-api/overview.md)。

## 格式

以`profile.paramName=value`格式指定配置文件参数。

要更新`pcId`的配置文件，请使用：

``````
https://<your-client-code>.tt.omtrdc.net/m2/client/profile/update?mboxPC=1368007744041-575948.01_00&profile.attr=0&profile.attr2=1...
``````

要更新`mbox3rdPartyId`的配置文件，请使用：

``````
shell http://<your-client-code>.tt.omtrdc.net/m2/client/profile/update?mbox3rdPartyId=123456&profile.attr=0&profile.attr2=1...
``````

[!UICONTROL Single Profile Update API]仅供更新。 如果未找到任何内容，则不会创建配置文件。

## 注释

* 参数和值必须使用UTF-8进行URL编码。
* 参数格式为`profile.paramName`。
* 并非所有pcIds和mbox3rdPartyIds都必须存在所有参数值。
* 参数和值区分大小写。
* 同时支持GET和POST。
* 当前的大小限制为：GET为8 KB，POST为60 KB。

## 响应

上述请求的示例响应如下所示：

`trueRequest successfully submitted`

此响应表示响应已提交，将很快处理。
