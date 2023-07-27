---
keywords: 云实例、公共后缀列表、公共后缀、Cookie、第一方Cookie、azurewebsites.net、cloudapp.net、amazonaws.com、cloudfront.net、herokuapp.com、firebaseapp.com、targetGlobalSettings、cookieDomain、云实例5、云实例6、云实例7、云实例8、云实例9、公共后缀列表0、公共后缀列表1、公共后缀列表2、公共后缀列表3、公共后缀列表4、公共后缀列表5
description: 探索客户（使用解决方案）在使用基于云的实例进行测试时遇到的问题 [!DNL Adobe Target] 或用于概念验证目的。
title: 我可以使用 [!DNL Target] 使用基于云的实例？
feature: at.js
exl-id: 4b24fdc0-6c74-4b29-bbf9-7a761d4564a2
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 46%

---

# 结合使用基于云的实例和 [!DNL Target]

此信息介绍了客户在使用基于云的实例来测试 [!DNL Adobe Target] 时遇到的一些问题。

[!DNL Target] 客户有时会将基于云的实例与 [!DNL Target] 结合使用来进行测试或简单的概念验证。这些实例可能包含以下域：

`azurewebsites.net`、`cloudapp.net`、`amazonaws.com`、`cloudfront.net`、`herokuapp.com` 或 `firebaseapp.com`

这些域以及其他许多域均是[公共后缀列表](https://publicsuffix.org/list/public_suffix_list.dat)的一部分。

**问题：**&#x200B;如果您使用这些域，新式浏览器不会保存 Cookie。

at.js JavaScript库使用Cookie来跟踪用户，以确保[！DNL [!DNL Target]]始终提供一致的体验。 如果 [!DNL Target] JavaScript库无法保存Cookie，Target请求已禁用。

**解决方案：**&#x200B;最佳做法是，如果您打算将基于云的实例与公共后缀列表中包含的域结合使用，请务必自定义 `cookieDomain` 设置。有关更多信息，请参阅 [targetGlobalSettings()](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md)。
