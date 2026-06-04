---
keywords: cookie， cookie，删除cookie，删除 [!DNL Target] cookie， google chrome， chrome， mozilla firefox， firefox， microsoft edge， safari， cookie1
description: 了解如何删除 [!DNL Target] 浏览器Cookie，以便验证您的体验。
title: 如何删除 [!DNL Target] Cookie？
feature: Privacy & Security
exl-id: c975c47f-8d81-4abe-aa89-f65275a73002
TQID: https://experienceleague.adobe.com/t4ieDzmphu8NHTM9eGnaZMoeXk-Y1G05E4K6spdSs6Y
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 07d73101a14b986fa9b016350c1ddeac0df4fdc2
workflow-type: tm+mt
source-wordcount: 424
ht-degree: 1%

---

# 删除[!DNL Target] Cookie

您可以删除[!DNL Adobe Target]浏览器Cookie (mbox)，以便在测试期间验证您的所有体验。

如果没有[!DNL Target] Cookie (mbox)，则您会被视为新访客并向您显示新体验。 有多种方法可以在不删除所有浏览器Cookie的情况下删除您的mbox。

>[!NOTE]
>
>以下说明适用于列出的浏览器和版本。 在Internet上搜索有关特定浏览器或版本的说明。

## 从Google Chrome中删除[!DNL Target] Cookie

版本 84.0.4147.105

1. 单击&#x200B;**[!UICONTROL Chrome]**&#x200B;菜单> **[!UICONTROL 首选项]**。
1. 单击&#x200B;**[!UICONTROL 隐私和安全]**&#x200B;选项卡。
1. 单击&#x200B;**[!UICONTROL Cookie和其他站点数据]**。
1. 单击&#x200B;**[!UICONTROL 查看所有Cookie和网站数据]**。
1. 展开`adobe.com`部分，选择&#x200B;**mbox** Cookie，然后单击删除图标(X)。

## 从Mozilla Firefox中删除[!DNL Target] Cookie

版本 79.0

### 删除与`adobe.com`关联的所有Cookie

1. 单击&#x200B;**[!UICONTROL Firefox]**&#x200B;菜单> **[!UICONTROL 首选项]**。
1. 单击&#x200B;**[!UICONTROL 隐私和安全]**&#x200B;选项卡。
1. 在&#x200B;**&#x200B; Cookie和站点数据*下，单击&#x200B;**&#x200B;[!UICONTROL 管理数据]**。
1. 选择`adobe.com`站点，然后单击&#x200B;**[!UICONTROL 删除选定项]**。

>[!WARNING]
>
>这将删除与`adobe.com`站点关联的所有Cookie。 如果要删除网站的单个Cookie，请按照以下说明操作。

### 删除单个Cookie (mbox)

1. 在Firefo中，单击&#x200B;**[!UICONTROL 工具]** > **[!UICONTROL Web Developer]** > **[!UICONTROL 存储检查器]**。
1. 单击&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡。
1. 导航到包含要删除的Cookie的网页。
1. 展开&#x200B;**[!UICONTROL Cookie]**&#x200B;部分，然后单击`https://experience.adobe.com`。
1. 右键单击&#x200B;**[!UICONTROL mbox]** Cookie，然后单击&#x200B;**[!UICONTROL 删除]**。

## 从Microsoft Edge中删除[!DNL Target] Cookie

版本84.0.522.52

1. 单击&#x200B;**[!UICONTROL Microsoft Edge]**&#x200B;菜单> **[!UICONTROL 首选项]**。
1. 单击&#x200B;**[!UICONTROL 网站权限]**&#x200B;选项卡。
1. 单击&#x200B;**[!UICONTROL Cookie和网站数据]**。
1. 单击&#x200B;**[!UICONTROL 查看所有Cookie和网站数据]**。
1. 展开`adobe.com`部分，选择&#x200B;**mbox** Cookie，然后单击删除图标(X)。

## 从Apple Safari中删除[!DNL Target] Cookie

版本 13.1.2

### 删除与`adobe.com`关联的所有Cookie

1. 单击&#x200B;**[!UICONTROL Safari]**&#x200B;菜单> **[!UICONTROL 首选项]**。
1. 单击&#x200B;**[!UICONTROL 隐私]**&#x200B;选项卡。
1. 单击&#x200B;**[!UICONTROL 管理网站数据]**。
1. 为要删除的Cookie选择站点，然后单击&#x200B;**[!UICONTROL 删除]**。

>[!WARNING]
>
>这将删除与`adobe.com`站点关联的所有Cookie。 如果要删除网站的单个Cookie，请按照以下说明操作。

### 删除单个Cookie (mbox)

1. 单击&#x200B;**[!UICONTROL Safari]**&#x200B;菜单> **[!UICONTROL 首选项]**。
1. 单击&#x200B;**[!UICONTROL 高级]**&#x200B;选项卡。
1. 选择&#x200B;**[!UICONTROL 在菜单栏]**&#x200B;中显示开发菜单选项。
1. 导航到包含要删除的Cookie的网页。
1. 单击&#x200B;**[!UICONTROL 开发]**&#x200B;菜单> **[!UICONTROL 显示Web检查器]**。
1. 单击&#x200B;**[!UICONTROL 存储]**&#x200B;选项卡。
1. 展开&#x200B;**[!UICONTROL Cookie]**&#x200B;部分，然后单击`www.adobe.com`。
1. 右键单击&#x200B;**mbox** Cookie，然后单击&#x200B;**[!UICONTROL 删除]**。
