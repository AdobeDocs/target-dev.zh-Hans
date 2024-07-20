---
title: 如何在 [!DNL Adobe Target] Python SDK中使用异步请求
description: 了解 [!DNL Target] Python SDK如何支持异步请求，这可以将有效目标时间减少为零。
feature: APIs/SDKs
exl-id: 44ab74e5-3c1a-49cf-9fff-fe523b0c2592
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 4%

---

# 异步请求(Python)

## 描述

服务器端集成的一个好处是，通过使用并行机制，您可以利用服务器端提供的巨大带宽和计算资源。 [!DNL Target] Python SDK支持异步请求，这可以将有效目标时间减少为零。

## 支持的方法

### Python

```python {line-numbers="true"}
get_offers(options)
send_notifications(options)
get_attributes(mbox_names, options)
```

## 示例

在Python 3.9及更高版本中使用`asyncio`模块的非同步/等待的示例应用程序可能如下所示：

### Python

```python {line-numbers="true"}
async def execute_mboxes(self, mboxes):
    context = Context(channel=ChannelType.WEB)
    execute = ExecuteRequest(mboxes=mboxes)
    delivery_request = DeliveryRequest(context=context, execute=execute)

    get_offers_options = {
      "request": delivery_request
    }
    return await asyncio.to_thread(target_client.get_offers, get_offers_options)

async def get_target_delivery_response(mboxes):
    target_delivery_response = await execute_mboxes(mboxes)
    response = Response(target_delivery_response.get("response").to_str(), status=200, mimetype='application/json')
    return response

mboxes = [MboxRequest(name="a1-serverside-ab", index=1)]
return asyncio.run(get_target_delivery_response(mboxes)
```

此示例假设您使用的是Python 3.9及以上版本。 如果使用旧版本的Python，您仍然可以通过将`options.callback`传递到`get_offers`来发送异步请求。 查看示例Flask应用程序，了解有关使用回调或异步/等待异步执行的更多详细信息，请单击[此处](https://github.com/adobe/target-python-sdk/blob/main/samples/app.py)。
