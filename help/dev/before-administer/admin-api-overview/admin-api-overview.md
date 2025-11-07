---
title: Adobe Target管理API概述
description: ' [!DNL Adobe Target Admin API]概述'
exl-id: 1168d376-c95b-4c5a-b7a2-c7815799a787
feature: APIs/SDKs
source-git-commit: 67cc93cf697f8d5bca6fedb3ae974e4012347a0b
workflow-type: tm+mt
source-wordcount: '1305'
ht-degree: 2%

---

# Target管理员API概述

本文概述成功理解和使用[!DNL Adobe Target Admin API]所需的背景信息。 以下内容假设您了解如何[为](../configure-authentication.md)配置身份验证[!DNL Adobe Target Admin API]。

>[!NOTE]
>
>如果您希望通过UI管理[!DNL Target]，请参阅[Adobe Target商业从业者指南&#x200B;**&#x200B;的](https://experienceleague.adobe.com/docs/target/using/administer/administrating-target.html?lang=en)管理部分。
>
>管理员API和配置文件API通常统称为“管理员API和配置文件API”)，但也可以单独称为（“管理员API”和“配置文件API”）。 推荐API是[!DNL Target]管理员API的特定实施。

## 开始之前

在为[管理员API](../../administer/admin-api/admin-api-overview-new.md)提供的所有代码示例中，将{tenant}替换为您的租户值，`your-bearer-token`替换为您使用JWT生成的访问令牌，将`your-api-key`替换为您从[Adobe Developer Console](https://developer.adobe.com/console/home)生成的API密钥。 有关租户和JWT的详细信息，请参阅关于如何[为Adobe &#x200B;](../configure-authentication.md)管理员API配置身份验证[!DNL Target]的文章。

## 版本控制

所有API都有一个关联的版本。 提供您要使用的API的正确版本很重要。

如果请求包含有效负载(POST或PUT)，则使用请求的`Content-Type`标头指定版本。

如果请求不包含有效负载(GET、DELETE或OPTIONS)，则使用`Accept`标头指定版本。

如果未提供版本，则调用将默认使用V1 (application/vnd.adobe.target.v1+json)。

>[!NOTE]
>
>如果未指定正确的版本（例如，如果您使用V2有效负载但未能指定Content-Type标头），则当API不向后兼容时，该API将做出响应并显示不支持的错误。

不支持的功能的错误消息

```
{
    "httpStatus": 406,
    "requestId": "8752b736-cf71-4d81-86c3-94be2b5ae648",
    "requestTime": "2018-02-02T21:39:06.405Z",
    "errors": [
        {
            "errorCode": "Unsupported.Feature",
            "message": "Unsupported features detected"
        }
    ]
}
```

管理员Postman收藏集

Postman是一款能够轻松触发API调用的应用程序。 此[Target管理员API Postman集合](https://developers.adobetarget.com/api/#admin-postman-collection)包含所有需要使用活动、受众、选件、报表、Mbox和环境进行身份验证的Target管理员API调用

## 响应代码

以下是Target管理员API的常见响应代码。

| 状态 | 含义 | 描述 |
| --- | --- | --- |
| 200 | [确定](https://www.rfc-editor.org/rfc/rfc7231#section-6.3.1) | 确定 |
| 400 | [错误请求](https://www.rfc-editor.org/rfc/rfc7231#section-6.5.1) | 错误请求。 请求中提供的数据很可能无效。 |
| 401 | [未授权](https://www.rfc-editor.org/rfc/rfc7235#section-3.1) | 不允许用户执行此操作。 |
| 403 | [禁止访问](https://www.rfc-editor.org/rfc/rfc7231#section-6.5.3) | 禁止访问此资源。 |
| 404 | [未找到](https://www.rfc-editor.org/rfc/rfc7231#section-6.5.4) | 未找到引用的资源。 |

## 活动

利用活动，可测试或个性化用户的内容。 活动可以是以下类型之一：

* [A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html)
* [体验定位 (XT)](https://experienceleague.adobe.com/docs/target/using/activities/experience-targeting/experience-target.html)
* [推荐](https://experienceleague.adobe.com/docs/target/using/activities/recommendations-activity.html)
* [Automated Personalization](https://experienceleague.adobe.com/docs/target/using/activities/automated-personalization/automated-personalization.html)
* [多变量测试(MVT)](https://experienceleague.adobe.com/docs/target/using/activities/multivariate-test/multivariate-testing.html)

## 批量更新

多个管理员API可以作为单个批处理请求执行。

### 批量执行调用

`POST /{tenant}/target/batch`

将多个API调用栈叠在一起，并在单个批次中执行。

批量处理允许您在一个HTTP请求中传递多个操作的说明。 还可以指定相关操作之间的从属关系（如下节所述）。 TNT将处理每个独立的操作（可能并行），并将按顺序处理从属操作。 完成所有操作后，将传递回整合的响应，并关闭HTTP连接。

批处理API采用以JSON数组表示的逻辑HTTP请求数组 — 每个请求都有一个方法(对应于HTTP方法GET/PUT/POST/DELETE等)、相对URL（admin/rest/之后URL的部分）、可选标头数组（对应于HTTP标头）和一个可选正文(适用于POST和PUT请求)。 批处理API返回一个以JSON数组表示的逻辑HTTP响应数组 — 每个响应都有一个状态代码、一个可选标头数组和一个可选正文（是一个JSON编码字符串）。 要使请求进行批处理，请构建一个JSON对象，该对象描述要执行的各个操作。 允许的最大操作数为256（从0到255）。

指定请求中操作之间的依赖关系默认情况下，批处理API请求中指定的操作是独立的 — 它们可以在服务器上以任意顺序执行，并且一个操作中的错误不会影响其他操作的执行。

通常，请求中的操作是相互依赖的 — 例如，一个操作的输出可用于下一个操作的输入。 例如，在operationId=0中创建的选件需要在campaign创建operationId=1中使用。

要将两个批处理操作链接在一起，请在依赖操作中指定所需操作的ID，例如：“dependsOnOperationId” ：5。 此外，通过批处理操作的POST请求创建的资源的ID可用于“relativeUrl”和“body”中的依赖操作。

#### 权限和限制

为了执行批处理API操作，基础用户必须至少具有“编辑者”权限（对于每个操作，如果比用户需要更多权限，则单个操作将失败）。 通常对批处理API操作应用节流策略，就像每个操作都已单独执行一样。

批处理完成时，所有操作都已完成，操作可能成功(2xx statusCode)、失败(4xx， 5xx status code)或因依赖项操作失败或已被跳过而跳过。

#### 请求对象参数

| 属性 | 描述 | 限制 | 默认 |
| --- | --- | --- | --- |
| 正文 | HTTP批处理操作的主体。 将忽略除POST和PUT之外的所有操作。 可以引用来自以前的批处理操作的ID，例如：“offerId”：“{operationIdResponse:0}”，“segmentId”：“{operationIdResponse:1}” | 应为有效的JSON；在引用operationIdResponse时，引用的operationId响应应为有效的ID，并且该操作的方法应为POST | 空对象{} |
| dependsOnOperationIds | 约束ID的列表，将确保仅在指定的操作成功完成时才执行当前操作。 可用于实现连锁操作。 | 最多允许255个操作；仅允许唯一值；应指向数组中的有效operationId；不允许循环依赖关系 |  |
| 标头 | 要通过特定操作发送的键值标头数组。 如果已通过授权标头执行批处理API的身份验证，则还会为各个操作复制该标头。 | 数组中允许的最大标头数为50 | Content-Type： application/json |
| 标头 — >名称 | 标头名称 | 应在其他标头名称中唯一。 rfc的标头不区分大小写，否则值将相互覆盖。 |  |
| 标头 — >值 | 标头值 | 不适用 | 空字符串 |
| 方法 | 要使用的HTTP方法。 可用选项：GET、POST、PUT、PATCH、DELETE | 仅允许GET、POST、PUT、PATCH、DELETE方法 |  |
| operationId | 操作ID，用于在用于响应和引用结果的其他操作中标识某个操作。 | 在其他操作中唯一；值介于0至255之间 |  |
| 操作 | 要在批次中执行的操作列表。 顺序不相关。 | 最多允许256个操作 |  |
| relativeUrl | 管理员rest API的相对URL，位于“/admin/rest/”之后。 可以包含查询字符串参数，如：&quot;/v2/campaigns？limit=10&amp;offset=10&quot;。 可以引用具有来自先前批次操作的包含ID的URL，例如：“/v1/offers/{operationIdResponse:0}”。 如果发送查询参数，则这些参数必须进行URL编码。 | 应当以/（相对）开头；仅支持新的有效JSON API；如果relativeURL无效，则将返回特定操作的404响应；如果引用operationIdResponse，则引用的operationId响应应当为有效ID，并且该操作的方法应当为POST |  |

#### 示例请求对象

```
{
  "operations": [
    {
      "operationId": 1,
      "dependsOnOperationIds~": [0],
      "method": "POST",
      "relativeUrl": "/v1/offers",
      "headers~": [
        {
          "name": "Content-Type",
          "value": "application/json"
        }
      ],
      "body~": {
        "key": "value"
      }
    }
  ]
}
```

#### 响应对象参数

| 参数 | 描述 |
| --- | --- |
| operationId | 用于标识其他操作中的操作的操作ID，该ID与在POST请求中发送的操作相同。 |
| 已跳过 | 布尔标记，用于标记操作是否已执行或跳过。 如果当前操作依赖于已失败的操作（返回了与2xx不同的statusCode值），则为true。 |
| 状态代码 | 返回，则将跳过（不执行）所有依赖的操作。 |
| 标头 | 键值标头数组，将作为特定操作的响应发送。 |
| 标头 — >名称 | 标头名称 |
| 标头 — >值 | 标头值 |
| 正文 | HTTP批处理响应操作的主体 |

#### 示例响应对象

```
{
  "results": [
    {
      "operationId": 1,
      "skipped~": false,
      "statusCode~": 200,
      "headers~": [
        {
          "name": "Content-Type",
          "value": "application/json; charset=UTF-8"
        }
      ],
      "body~": {
        "id": 5
      }
    }
  ]
}
```
