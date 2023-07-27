---
title: 在中使用getOffers() [!DNL Adobe Target] 使用Python SDK时
description: 了解如何使用getOffers()执行决策并从中检索体验 [!DNL Adobe Target].
feature: APIs/SDKs
exl-id: 9539b806-e070-430e-80cf-cf632ce3f207
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '379'
ht-degree: 13%

---

# 获取选件(Python)

## 描述

`get_offers()` 用于执行决策并从以下位置检索体验 [!DNL Adobe Target].


## 方法

### getOffers

```python {line-numbers="true"}
target_client_instance.get_offers(options)
```

## 参数

此 `options` dict具有以下结构：

| 名称 | 类型 | 必需 | 默认 | 描述 |
| --- | --- | --- | --- | --- |
| request | DeliveryRequest | 是 | 无 | 符合 [[!DNL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) 请求 |
| target_cookie | str | 否 | 无 | [!DNL Target] Cookie |
| target_location_hint | str | 否 | 无 | [!DNL Target] 位置提示 |
| consumer_id | str | 否 | 无 | 在拼接多个调用时，应提供不同的消费者ID |
| customer_ids | 列表[CustomerId] | 否 | 无 | 与VisitorId兼容的格式的客户ID列表 |
| session_id | str | 否 | 无 | 用于链接多个请求 |
| callback | 可调用 | 否 | 无 | 如果异步处理请求，则会在响应就绪时调用回调 |
| err_callback | 可调用 | 否 | 无 | 如果异步处理请求，则在引发异常时会调用错误回调 |

## 返回结果

返回 `TargetDeliveryResponse` 如果同步调用（默认），或者 `AsyncResult` 如果通过回调调用，则为。 `TargetDeliveryResponse` 具有以下结构：

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| 响应 | DeliveryResponse | 符合 [[!UICONTROL Target投放API]](/help/dev/implement/delivery-api/overview.md) 响应 |
| target_cookie | dict | [!DNL Target] Cookie |
| target_location_hint_cookie | dict | [!DNL Target] 位置提示Cookie |
| analytics_details | 列表[Analytics响应] | 在使用客户端Analytics的情况下，使用Analytics有效负载 |
| trace | 列表[dict] | 所有请求mbox/视图的汇总跟踪数据 |
| response_tokens | 列表[dict] | 列&#x200B;表[响应令牌](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html) |
| meta | dict | 用于设备上决策的其他决策元数据 |

`target_cookie` 和 `target_location_hint_cookie` 用于将数据传递回浏览器的对象具有以下结构：

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| name | str | Cookie 名称 |
| value | any | Cookie值，该值将转换为字符串 |
| max_age | int | 此 `max_age option` 方便设置相对于当前时间（以秒为单位）的过期时间 |

此 `meta` 用于指示目标响应状态的对象具有以下结构：

| 名称 | 类型 | 描述 |
| --- | --- | --- |
| decisioning_method | str | 使用的决策方法：设备上或服务器端 |
| remote_mboxes | list`[str]` | 当决策方法为 `on-device`，则给出了设备上无法完全决定的mbox名称数组。 换句话说， [[!UICONTROL Target投放API]](/help/dev/implement/delivery-api/overview.md) 需要请求。 |
| remote_view | list`[str]` | 当决策方法为设备上时，给出了无法完全决策为设备上视图名称的数组。 换句话说， [[!UICONTROL Target投放API]](/help/dev/implement/delivery-api/overview.md) 需要请求。 |

## 示例

### Python

```python {line-numbers="true"}
def client_ready_callback():
    context = Context(channel=ChannelType.WEB)
    mboxes = [MboxRequest(name="a1-serverside-ab", index=1)]
    execute = ExecuteRequest(mboxes=mboxes)
    delivery_request = DeliveryRequest(context=context, execute=execute)

    get_offers_options = {
      "request": delivery_request
    }

    target_delivery_response = target_client.get_offers(get_offers_options)


client_options = {
    "client": "acmeclient",
    "organization_id": "1234567890@AdobeOrg",
    "events": {
        "client_ready": client_ready_callback
    }
}
target_client = TargetClient.create(client_options)
```
