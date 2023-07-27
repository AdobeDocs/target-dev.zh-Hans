---
keywords: Cookie， Cookie，删除Cookie，删除 [!DNL Target] cookie， google chrome， chrome， mozilla firefox， firefox， microsoft edge， safari， cookie1
description: 了解如何删除您的 [!DNL Target] 浏览器Cookie，以便您验证自己的体验。
title: 如何删除 [!DNL Target] Cookie？
feature: Privacy & Security
exl-id: c975c47f-8d81-4abe-aa89-f65275a73002
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 4%

---

# 删除 [!DNL Target] Cookie

您可以删除 [!DNL Adobe Target] 浏览器Cookie (mbox)，以便您在测试期间验证所有体验。

如果没有 [!DNL Target] cookie (mbox)时，您会被视为新访客并显示新体验。 有多种方法可在不删除所有 的情况下删除您的 mbox Cookie。

>[!NOTE]
>
>以下说明适用于列出的浏览器和版本。 在Internet上搜索有关特定浏览器或版本的说明。

## 删除 [!DNL Target] Google Chrome中的Cookie

版本 84.0.4147.105

1. 单击 **[!UICONTROL 铬黄]** 菜单> **[!UICONTROL 偏好设置]**.
1. 单击 **[!UICONTROL 隐私和安全性]** 选项卡。
1. 单击 **[!UICONTROL Cookie和其他站点数据]**.
1. 单击 **[!UICONTROL 查看所有Cookie和网站数据]**.
1. 展开 `adobe.com` 部分，选择 **mbox** cookie，然后单击删除图标(X)。

## 删除 [!DNL Target] 来自Mozilla Firefox的Cookie

版本 79.0

### 删除与关联的所有Cookie `adobe.com`

1. 单击 **[!UICONTROL Firefox]** 菜单> **[!UICONTROL 偏好设置]**.
1. 单击 **[!UICONTROL 隐私和安全性]** 选项卡。
1. 在**Cookie和网站数据*，单击 **[!UICONTROL 管理数据]**.
1. 选择 `adobe.com` 站点，然后单击 **[!UICONTROL 删除选定项]**.

>[!WARNING]
>
>这将删除与关联的所有Cookie `adobe.com` 站点。 如果要删除网站的单个Cookie，请按照以下说明操作。

### 删除单个Cookie (mbox)

1. 在Firefo中，单击 **[!UICONTROL 工具]** > **[!UICONTROL Web开发人员]** > **[!UICONTROL 存储检查器]**.
1. 单击 **[!UICONTROL 高级]** 选项卡。
1. 导航到包含要删除的Cookie的网页。
1. 展开 **[!UICONTROL Cookies]** 部分，然后单击 `https://experience.adobe.com`.
1. 右键单击 **[!UICONTROL mbox]** cookie，然后单击 **[!UICONTROL 删除]**.

## 删除 [!DNL Target] Microsoft Edge中的Cookie

版本 84.0.522.52

1. 单击 **[!UICONTROL Microsoft Edge]** 菜单> **[!UICONTROL 偏好设置]**.
1. 单击 **[!UICONTROL 网站权限]** 选项卡。
1. 单击 **[!UICONTROL Cookie和网站数据]**.
1. 单击 **[!UICONTROL 查看所有Cookie和网站数据]**.
1. 展开 `adobe.com` 部分，选择 **mbox** cookie，然后单击删除图标(X)。

## 删除 [!DNL Target] 来自Apple Safari的Cookie

版本 13.1.2

### 删除与关联的所有Cookie `adobe.com`

1. 单击 **[!UICONTROL Safari]** 菜单> **[!UICONTROL 偏好设置]**.
1. 单击 **[!UICONTROL 隐私]** 选项卡。
1. 单击 **[!UICONTROL 管理网站数据]**.
1. 为要删除的Cookie选择站点，然后单击 **[!UICONTROL 移除]**.

>[!WARNING]
>
>这将删除与关联的所有Cookie `adobe.com` 站点。 如果要删除网站的单个Cookie，请按照以下说明操作。

### 删除单个Cookie (mbox)

1. 单击 **[!UICONTROL Safari]** 菜单> **[!UICONTROL 偏好设置]**.
1. 单击 **[!UICONTROL 高级]** 选项卡。
1. 选择 **[!UICONTROL 在菜单栏中显示开发菜单]** 选项。
1. 导航到包含要删除的Cookie的网页。
1. 单击 **[!UICONTROL 开发]** 菜单> **[!UICONTROL 显示Web检查器]**.
1. 单击 **[!UICONTROL 存储]** 选项卡。
1. 展开 **[!UICONTROL Cookies]** 部分，然后单击 `www.adobe.com`.
1. 右键单击 **mbox** cookie，然后单击 **[!UICONTROL 删除]**.
