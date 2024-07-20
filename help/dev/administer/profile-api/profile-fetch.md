---
title: 获取配置文件
description: 了解如何使用Adobe Target配置文件API来获取访客数据，以便在 [!DNL Target]中使用。
contributors: https://github.com/icaraps
feature: APIs/SDKs
exl-id: b422ae68-49b3-4d60-9ea4-0fa67b6934b0
source-git-commit: b8ccfdcaff6aa17a325727df0a9ffd716e44519b
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---

# 获取配置文件

可以通过三种方式获取[!DNL Target]配置文件：使用`[!DNL Experience Cloud Visitor ID]` (`ECID`)、`tntid`或`thirdPartyId`。

## 使用[!DNL Experience Cloud Visitor ID] (ECID)

您可以根据`ECID`获取配置文件。 HTTP方法必须GET。

该URL类似于以下示例：

```
https://<clientCode>.tt.omtrdc.net/rest/v1/profiles/marketingCloudVisitorId/<ECID>?client=<clientCode>
```

将`<clientCode>`替换为您的[!DNL Target] [!UICONTROL Client Code]，将`<ECID>`替换为您的[!DNL Experience Cloud Visitor ID] ([!DNL Marketing Cloud Visitor ID])。

## 使用tntid

[!DNL Target]为每个请求自动分配`tntid`。

以下示例显示使用`tntid`获取配置文件的请求格式：

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/your-tnt-id?client=<your-client-code>
```

替换`<your-client-code>`和`your-tnt-id`并触发GET请求。 以下是使用`tntid`的配置文件提取调用示例：

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/111492025094307-353046?client=<your-client-code>
```

## 使用thirdPartyId

[!DNL Adobe Target]配置文件可以使用您自己的标识符进行扩充（例如：CRM ID、`uuid`、成员资格号等）。

请参阅[更新配置文件](/help/dev/administer/profile-api/profile-api-overview.md)，了解如何将`thirdPartyId`附加到配置文件。

以下示例显示使用`thirdPartyId`获取配置文件的请求格式：

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/thirdPartyId/your-thirdpartyid?client=<your-client-code>
```

替换`<your-client-code>`和`your-thirdpartyid`并触发GET请求。 以下是使用[!UICONTROL thirdpartyid]的配置文件提取调用示例：

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/thirdPartyId/a1-mbox3rdPartyId?client=<your-client-code>
```

进行此调用时，[!DNL Target]会尝试首先在边缘请求中记录的集群中或配置文件所在的任何位置找到配置文件并返回内容。 配置文件内容以JSON格式返回。

## 身份验证

通过从[!DNL Target] UI中打开身份验证，可以保护[!DNL Target Profile API]，如下所述。 身份验证打开后，所有配置文件API请求必须在请求标头中设置配置文件身份验证令牌。 令牌本身可以使用[!DNL Target] UI生成，也可以使用上文[配置文件身份验证令牌](https://developers.adobetarget.com/api/#authentication-tokens){target=_blank}部分中描述的步骤生成。

## 测光

这些调用不计入您的mbox调用。

## 错误处理

如果调用的`/thirdPartyId`指定了无效或过期的`thirdPartyId`：

```
{"status" : 404, "message" : "No profile found for client <client_code> with third party id=<third_party_id>"}
```

如果找不到配置文件或配置文件已过期：

```
{"status" : 404, "message" : "No profile found for client <client_code> with mboxPC=<mbox_pc>"}
```
