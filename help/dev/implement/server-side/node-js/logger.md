---
title: 初始化 [!DNL Adobe Target] 用于记录请求的Node.js SDK
description: 了解如何在中记录请求 [!DNL Adobe Target] Node.js SDK.
feature: APIs/SDKs
exl-id: 5db3e301-47b3-4330-b185-c0c03f72e790
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 2%

---

# 记录器(Node.js)

## 描述

时间 [初始化SDK](initialize-sdk.md)， `options.logger` 对象是可选对象。 但是，为了在发生问题时有效调试， `logger` 初始化SDK时应提供对象。

此 `logger` 对象应具有 `debug()` 和 `error()` 方法。 在提供合适的记录器时，例如 `console`， [!DNL Target] 将记录请求和响应。

## 示例

### Node.js

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg",
  logger: console
};

const targetClient = TargetClient.create(CONFIG);

const request = {
    execute: {
        mboxes: [{
            name: "a1-serverside-ab",
            index: 1
        }]
    }
};

const response = await targetClient.getOffers({ request, targetCookie });
```

您应该会看到控制台中正在打印的请求和响应。
