---
title: 在 [!DNL Adobe Target] Node.js SDK中实施代理配置
description: 了解如何在 [!DNL Adobe Target] Node.js SDK中配置[!UICONTROL TargetClient]代理配置。
feature: APIs/SDKs
exl-id: c9f04e81-3fa3-4e64-a974-379420b0518a
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---

# 代理配置(Node.js)

要为节点SDK的HTTP请求配置代理，请覆盖SDK在初始化期间使用的获取API。

以下是一个基本示例，说明如何在`TargetClient`初始化期间覆盖`fetchApi`以添加代理：

```javascript {line-numbers="true"}
const { ProxyAgent } = require("undici");

const proxyAgent = new ProxyAgent("your proxy address here");

const fetchImpl = (url, options) => {
  const fetchOptions = options;
  fetchOptions.dispatcher = proxyAgent;
  return fetch(url, fetchOptions);
};

client = TargetClient.create({
    ...,
    fetchApi: fetchImpl
});
```

请注意，这仅适用于节点版本18.2+，其中`undici.fetch`是节点的默认`fetch`。
请访问[Node SDK示例存储库](https://github.com/adobe/target-nodejs-sdk-samples/tree/master/proxy-configuration)
有关旧版节点的代理配置示例及更多信息。
