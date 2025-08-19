---
title: Adobe Target批量配置文件更新API
description: 了解如何使用 [!DNL Adobe Target] [!UICONTROL Bulk Profile Update API]将多个访客的配置文件数据发送到 [!DNL Target] 以用于定位。
feature: APIs/SDKs
contributors: https://github.com/icaraps
exl-id: 0f38d109-5273-4f73-9488-80eca115d44d
source-git-commit: dae198fd8ef3fc8473ad31807c146802339b1832
workflow-type: tm+mt
source-wordcount: '917'
ht-degree: 7%

---

# [!DNL Adobe Target Bulk Profile Update API]

[!DNL Adobe Target] [!UICONTROL Bulk Profile Update API]允许您使用批处理文件批量更新网站多个访客的用户配置文件。

使用[!UICONTROL Bulk Profile Update API]，您可以方便地将许多用户的详细访客配置文件数据以配置文件参数的形式从任何外部源发送到[!DNL Target]。 外部来源可能包括客户关系管理(CRM)或销售点(POS)系统，这些系统通常无法在网页上使用。

| 版本 | URL示例 | 功能 |
| --- | --- | --- |
| v1 | `http://CLIENTCODE.tt.omtrdc.net/m2/CLIENTCODE/profile/batchUpdate` | 仅支持批量配置文件更新。 |
| v2 | `http://CLIENTCODE.tt.omtrdc.net/m2/CLIENTCODE/v2/profile/batchUpdate` | <ul><li>如果未找到，则创建配置文件。</li><li>每行状态更新。</li></ul> |

>[!NOTE]
>
>[!DNL Bulk Profile Update API]的版本2 (v2)是当前版本。 但是，[!DNL Target]仍支持版本1 (v1)。
>
>* 如果您的[!DNL Target]实现使用[!DNL Experience Cloud ID] (ECID)作为匿名访客的配置文件标识符之一，请不要在版本2 (v2)批处理文件中使用`pcId`作为密钥。 将`pcId`与[!DNL Bulk Profile Update API]的v2结合使用仅适用于不依赖于ECID的独立[!DNL Target]实施。
>
>* 如果您的实施使用ECID进行配置文件标识，并且您想使用`pcId`作为批处理文件中的密钥，请使用API版本1 (v1)。
>
>* 如果您的实施使用`thirdPartyId`进行配置文件识别，请使用版本2 (v2)的API并将`thirdPartyId`用作密钥。

## [!UICONTROL Bulk Profile Update API]的优势

* 配置文件属性的数量没有限制。
* 通过网站发送的用户档案属性可以通过API更新，反之亦然。

## 注意事项

* 批处理文件必须小于 50 MB。另外，每次上传的总行数不应超过 500,000 行。
* 更新通常在一小时内发生，但可能需要24小时才能反映出来。
* 对于在后续批次中可以在24小时内上传的一个或多个行数没有限制。 但是，为了确保其他进程能够高效运行，这些数据的吸收过程在工作时间可能会受到节流限制。
* 对于相同thirdPartyId，如果连续的v2批量更新调用之间没有mbox调用，则会覆盖在第一次批量更新调用中更新的属性。
* [!DNL Adobe]不保证100%的批次配置文件数据将被载入并保留在Target中，因此可用于定位。 在当前设计中，有可能不会载入或保留一小部分数据（最多占大批量生产的0.1%）。

## 批处理文件

要批量更新用户档案数据，请创建批处理文件。 批处理文件是一个文本文件，其值由逗号分隔，类似于以下示例文件。

``````
batch=pcId,param1,param2,param3,param4
123,value1
124,value1,,,value4
125,,value2
126,value1,value2,value3,value4
``````

>[!NOTE]
>
>`batch=`参数是必需的，必须在文件开头指定。

您在[!DNL Target]服务器的POST调用中引用此文件以处理该文件。 创建批处理文件时，请考虑以下事项：

* 文件的第一行必须指定列标题。
* 第一个标头应为`pcId`或`thirdPartyId`。 不支持[!UICONTROL Marketing Cloud visitor ID]。 [!UICONTROL pcId]是[!DNL Target]生成的访客ID。 `thirdPartyId`是由客户端应用程序指定的ID，它通过mbox调用作为[!DNL Target]传递给`mbox3rdPartyId`。 它必须在此作为`thirdPartyId`引用。
* 出于安全原因，您在批处理文件中指定的参数和值必须使用UTF-8进行URL编码。 参数和值可以转发到其他边缘节点以供通过HTTP请求进行处理。
* 参数必须仅采用`paramName`格式。 参数在[!DNL Target]中显示为`profile.paramName`。
* 如果您使用[!UICONTROL Bulk Profile Update API] v2，则不需要为每个`pcId`指定所有参数值。 已为`pcId`中未找到的任何`mbox3rdPartyId`或[!DNL Target]创建配置文件。 如果您使用的是v1，则不会为缺少的pcIds或mbox3rdPartyIds创建配置文件。
* 批处理文件必须小于 50 MB。此外，总行数不应超过500,000。 此限制可确保服务器不会因请求过多而泛滥。
* 您可以发送多个文件。 但是，您一天内发送的所有文件的行总数不应超过每个客户端的100万。
* 您可以上传的属性数量没有限制。 但是，外部配置文件数据（包括客户属性、配置文件API、Mbox内配置文件参数和配置文件脚本输出）的总大小不得超过64 KB。
* 参数和值区分大小写。

## HTTP POST请求

向[!DNL Target]边缘服务器发出HTTP POST请求以处理该文件。 以下是使用curl命令对文件batch.txt发出的HTTP POST请求示例：

``````
curl -X POST --data-binary @BATCH.TXT http://CLIENTCODE.tt.omtrdc.net/m2/CLIENTCODE/v2/profile/batchUpdate
``````

其中：

BATCH.TXT是文件名。 CLIENTCODE是[!DNL Target]客户端代码。

如果您不知道客户端代码，请在[!DNL Target]用户界面中单击&#x200B;**[!UICONTROL Administration]** > **[!UICONTROL Implementation]**。 客户端代码显示在[!UICONTROL Account Details]部分中。

### 检查响应

配置文件API可返回批处理的提交状态，以及“batchStatus”下的链接以指向显示特定批处理作业整体状态的其他URL。

### 示例API响应

以下代码片段是Profiles API响应的示例：

```
<response>
    <success>true</success>
    <batchStatus>http://mboxedge45.tt.omtrdc.net/m2/demo/profile/batchStatus?batchId=demo-1701473848678-13029383</batchStatus>
    <message>Batch submitted for processing</message>
</response>
```

如果出现错误，则响应包含`success=false`和详细的错误消息。

### 默认批次状态响应

单击上述`batchStatus` URL链接时成功的默认响应如下所示：

```
<response><batchId>demo4-1701473848678-13029383</batchId><status>complete</status><batchSize>1</batchSize></response>
```

状态字段的预期值包括：

| 状态 | 详细信息 |
| --- | --- |
| [!UICONTROL complete] | 配置文件批量更新请求已成功完成。 |
| [!UICONTROL incomplete] | 用户档案批量更新请求仍在处理中，尚未完成。 |
| [!UICONTROL stuck] | 配置文件批次更新请求卡住，无法完成。 |

### 详细的批次状态URL响应

通过将参数`showDetails=true`传递到上面的`batchStatus` URL，可以获取更详细的响应。

例如：

```
http://mboxedge45.tt.omtrdc.net/m2/demo/profile/batchStatus?batchId=demo-1701473848678-13029383&showDetails=true
```

#### 详细响应

```
<response>
    <batchId>demo4-1701473848678-13029383</batchId>
    <status>complete</status>
    <batchSize>1</batchSize>
    <consumedCount>1</consumedCount>
    <successfulUpdates>1</successfulUpdates>
    <profilesNotFound>0</profilesNotFound>
    <failedUpdates>0</failedUpdates>
</response>
```
