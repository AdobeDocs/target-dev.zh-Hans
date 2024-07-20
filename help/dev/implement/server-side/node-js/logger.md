---
title: 初始化 [!DNL Adobe Target] Node.js SDK以记录请求
description: 了解如何在 [!DNL Adobe Target] Node.js SDK中记录请求。
feature: APIs/SDKs
exl-id: 5db3e301-47b3-4330-b185-c0c03f72e790
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 2%

---

# 记录器(Node.js)

## 描述

当[初始化SDK](initialize-sdk.md)时，`options.logger`对象是可选对象。 但是，为了在发生问题时有效调试，应在初始化SDK时提供`logger`对象。

`logger`对象应具有`debug()`和`error()`方法。 在提供了适当的记录器（如`console`、[!DNL Target]请求）后，将记录响应。

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
