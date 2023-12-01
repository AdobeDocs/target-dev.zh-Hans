---
title: Adobe Target批量配置文件更新API
description: 了解如何使用 [!DNL Adobe Target] [!UICONTROL 批量配置文件更新API] 将多个访客的配置文件数据发送到 [!DNL Target].
feature: APIs/SDKs
contributors: https://github.com/icaraps
source-git-commit: 43f4fb8345a77ccb0e112fe196e7e0944cc468c9
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 9%

---

# [!DNL Adobe Target Bulk Profile Update API]

此 [!DNL Adobe Target] [!UICONTROL 批量配置文件更新API] 允许您使用批处理文件批量更新网站多个访客的用户配置文件。

使用 [!UICONTROL 批量配置文件更新API]，您可以方便地以多个用户的配置文件参数的形式将详细的访客配置文件数据发送至 [!DNL Target] 来自任何外部源。 外部来源可能包括客户关系管理(CRM)或销售点(POS)系统，这些系统通常无法在网页上使用。

| 版本 | URL示例 | 功能 |
| --- | --- | --- |
| v1 | `http://CLIENTCODE.tt.omtrdc.net/m2/ CLIENTCODE/profile/batchUpdate` | 仅支持批量配置文件更新。 |
| v2 | `http://CLIENTCODE.tt.omtrdc.net/m2/ CLIENTCODE/v2/profile/batchUpdate` | <ul><li>如果未找到，则创建配置文件。</li><li>每行状态更新。</li></ul> |

>[!NOTE]
>
>的版本2 (v2) [!UICONTROL 批量配置文件更新API] 是当前版本。 但是， [!DNL Target] 仍支持版本1 (v1)。

## 批量配置文件更新API的优势

* 配置文件属性的数量没有限制。
* 通过网站发送的用户档案属性可以通过API更新，反之亦然。

## 注意事项

* 批处理文件必须小于 50 MB。另外，每次上传的总行数不应超过 500,000 行。
* 对于在后续批次中可以在24小时内上传的一个或多个行数没有限制。 但是，为了确保其他进程能够高效运行，这些数据的吸收过程在工作时间可能会受到节流限制。
* 对于相同thirdPartyId，如果连续的v2批量更新调用之间没有mbox调用，则会覆盖在第一次批量更新调用中更新的属性。

## 批处理文件

要批量更新用户档案数据，请创建批处理文件。 批处理文件是一个文本文件，其值由逗号分隔，类似于以下示例文件。

``````
batch=pcId, param1, param2, param3, param4 123, value1 124, value1,,, value4 125,, value2 126, value1, value2, value3, value4
``````

您在POST调用中引用此文件 [!DNL Target] 服务器处理文件。 创建批处理文件时，请考虑以下事项：

* 文件的第一行必须指定列标题。
* 第一个标头应为 `pcId` 或 `thirdPartyId`. 此 [!UICONTROL Marketing Cloud访客ID] 不受支持。 [!UICONTROL pcId] 是 [!DNL Target] — 生成的visitorID。 `thirdPartyId` 是由客户端应用程序指定的ID，传递给 [!DNL Target] 通过mbox调用，作为 `mbox3rdPartyId`. 必须在此将其引用为 `thirdPartyId`.
* 出于安全原因，您在批处理文件中指定的参数和值必须使用UTF-8进行URL编码。 参数和值可以转发到其他边缘节点以供通过HTTP请求进行处理。
* 参数必须采用格式 `paramName` 仅限。 参数显示在中 [!DNL Target] 作为 `profile.paramName`.
* 如果您使用 [!UICONTROL 批量配置文件更新API] v2，您无需为每个参数指定所有参数值 `pcId`. 已为任何对象创建配置文件 `pcId` 或 `mbox3rdPartyId` 在中未找到的 [!DNL Target]. 如果您使用的是v1，则不会为缺少的pcIds或mbox3rdPartyIds创建配置文件。
* 批处理文件必须小于 50 MB。此外，总行数不应超过500,000。 此限制可确保服务器不会因请求过多而泛滥。
* 您可以发送多个文件。 但是，您一天内发送的所有文件的行总数不应超过每个客户端的100万。
* 您上传的属性数量没有限制。 但是，配置文件的整体大小（包括系统数据）不应超过2000 KB。 [!DNL Adobe] 建议为配置文件属性使用的存储空间小于1000 KB。
* 参数和值区分大小写。

## HTTPPOST请求

向发出HTTPPOST请求 [!DNL Target] 用于处理文件的边缘服务器。 以下是使用curl命令获取文件batch.txt的示例HTTPPOST请求：

``````
curl -X POST --data-binary @BATCH.TXT http://CLIENTCODE.tt.omtrdc.net/m2/ CLIENTCODE/v2/profile/batchUpdate
``````

其中：

BATCH.TXT是文件名。 CLIENTCODE [!DNL Target] 客户端代码。

如果您不知道自己的客户端代码，请在 [!DNL Target] 用户界面点击 **[!UICONTROL 管理]** > **[!UICONTROL 实现]**. 客户端代码显示在 [!UICONTROL 帐户详细信息] 部分。

### Inspect响应

v2会返回按配置文件划分的状态，而v1只会返回整体状态。 响应中包含指向其他URL的链接，该URL具有逐个用户档案的成功消息。

### 示例响应

```
true http://mboxedge19.tt.omtrdc.net/m2/demo/v2/profile/batchStatus?batchId=demo-1845664501&m2Node=00 Batch submitted for processing
```

如果出现错误，响应将包含 `success=false` 以及错误的详细消息。

成功的响应如下所示：

``````
demo-1845664501 1436187396849-250353.03_03 success 2403081156529-351655.03_03 success 2403081156529-351656.03_03 success 1436187396849-250351.01_00 success 
``````

状态字段的预期值包括：

**success**：已更新用户档案。 如果未找到配置文件，则使用批次中的值创建一个配置文件。
**错误**：由于失败、异常或消息丢失，未更新或创建用户档案。
**待处理**：尚未更新或创建用户档案。



