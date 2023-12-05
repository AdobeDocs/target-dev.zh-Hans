---
title: 获取配置文件
description: 了解如何使用Adobe Target配置文件API来获取访客数据，以用于 [!DNL Target].
contributors: https://github.com/icaraps
feature: APIs/SDKs
source-git-commit: e5a1c38d448cb7446b7b26cd0dc882976ba94dd3
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---

# 更新用户档案

A [!DNL Target] 可通过两种方式获取配置文件：使用 `tntid` 或 `thirdPartyId`.

## 使用tntid

[!DNL Target] 自动分配 `tntid` 每个请求都可以。

以下示例显示了使用获取配置文件的请求格式 `tntid`：

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/your-tnt-id?client=<your-client-code>
```

替换 `<your-client-code>` 和 `your-tnt-id` 并触发GET请求。 以下是使用的配置文件提取调用示例 `tntid`；

```
http://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/111492025094307-353046?client=<your-client-code>
```

## 使用thirdPartyId

[!DNL Adobe Target] 可使用您自己的标识符来扩充用户档案(例如：CRM id， `uuid`、会员资格号等)。

请参阅 [更新用户档案](/help/dev/administer/profile-api/profile-api-overview.md) 以了解如何附加 `thirdPartyId` 到您的个人资料中。

以下示例显示了使用获取配置文件的请求格式 `thirdPartyId`：

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/thirdPartyId/your-thirdpartyid?client=<your-client-code>
```

替换 `<your-client-code>` 和 `your-thirdpartyid` 并触发GET请求。 以下是使用的配置文件提取调用示例 [!UICONTROL thirdpartyid]：

```
https://<your-client-code>.tt.omtrdc.net/rest/v1/profiles/thirdPartyId/a1-mbox3rdPartyId?client=<your-client-code>
```

当进行此调用时， [!DNL Target] 会尝试首先在边缘请求中所述的集群中找到用户档案，或找到用户档案并返回内容。 配置文件内容以JSON格式返回。

## 身份验证

此 [!DNL Target Profile API] 可以通过以下方式打开身份验证 [!DNL Target] UI，如此处所述。 身份验证打开后，所有配置文件API请求必须在请求标头中设置配置文件身份验证令牌。 可以使用生成令牌本身 [!DNL Target] UI或使用中所述步骤 [配置文件身份验证令牌](https://developers.adobetarget.com/api/#authentication-tokens){target=_blank} 部分。

## 测光

这些调用不计入您的mbox调用。

## 错误处理

在调用时 `/thirdPartyId` 具有无效或过期的 `thirdPartyId` 指定：

```
{"status" : 404, "message" : "No profile found for client <client_code> with third party id=<third_party_id>"}
```

如果找不到配置文件或配置文件已过期：

```
{"status" : 404, "message" : "No profile found for client <client_code> with mboxPC=<mbox_pc>"}
```
