---
title: 如何在中使用异步请求 [!DNL Adobe Target] Python SDK
description: 了解如何 [!DNL Target] Python SDK支持异步请求，这可以将有效目标时间减少为零。
feature: APIs/SDKs
exl-id: fafb9e28-5ac5-41c1-8e7f-f40550b6749f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 14%

---

# 获取属性(Python)

## 描述

`get_attributes()` 用于从获取试验性和个性化体验 [!DNL Target] 和提取属性值。


## 方法

### getAttributes

```python {line-numbers="true"}
target_client_instance.get_attributes(mbox_names, options)
```

## 参数

| 名称 | 类型 | 必需 | 默认 | 描述 |
| --- | --- | --- | --- | --- |
| mbox名称(_N) | 列表[str] | 是 | 无 | mbox名称列表 |
| options | dict | 否 | 无 | 与使用的选项相同 [获取优惠](get-offers.md) |

## 属性提供程序

此 `AttributesProvider` 返回者 `target_client.get_attributes()` 具有以下方法：

| 方法 | 返回类型 | 描述 |
| --- | --- | --- |
| get_value(mbox_name， key) | any | 返回指定mbox名称和属性键的值 |
| as_object(mbox_name) | dict | 返回具有键值对的简单json对象 |
| get_response() | [TargetDeliveryResponse](https://github.com/adobe/target-python-sdk/blob/main/target_python_sdk/types/target_delivery_response.py) | 返回通常由返回的响应对象 `get_offers` |

## 示例

### Python

```python {line-numbers="true"}
def client_ready_callback():
    context = Context(channel=ChannelType.WEB)
    mboxes = [MboxRequest(name="a1-serverside-ab", index=1)]
    execute = ExecuteRequest(mboxes=mboxes)
    delivery_request = DeliveryRequest(context=context, execute=execute)

    get_attributes_options = {
      "request": delivery_request
    }

    attributes_provider = target_client.get_attributes(["demo-engineering-flags"], get_attributes_options)
    # returns just the value of searchProviderId from the demo-engineering-flags mbox offer
    search_provider_id = attributes_provider.get_value("demo-engineering-flags", "searchProviderId")

    # returns a simple dict object representing the demo-engineering-flags mbox offer
    engineering_flags = attributes_provider.as_object("demo-engineering-flags")
    """  the value of engineeringFlags looks like this
        {
            "cdnHostname": "cdn.cloud.corp.net",
            "searchProviderId": 143,
            "hasLegacyAccess": false
        }
    """

    asset_url = "http://{}/path/to/asset".format(engineering_flags.get("cdnHostname"))


client_options = {
    "client": "acmeclient",
    "organization_id": "1234567890@AdobeOrg",
    "events": {
        "client_ready": client_ready_callback
    }
}
target_client = TargetClient.create(client_options)
```
