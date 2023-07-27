---
keywords: 实施，实施，设置，设置，页面参数
description: 将数据导入 [!DNL Target] 使用页面内配置文件属性。
title: 如何将数据导入 [!DNL Target] 是否使用页面内配置文件属性？
feature: Implementation
exl-id: c19fd746-21a2-4eb5-8c2a-c24806e09324
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 45%

---

# 页面内个人资料属性

中的页面内配置文件属性 [!DNL Adobe Target] （也称为“in-mbox profile attributes”）是直接通过页面代码传递的名称/值对，这些名称/值对存储在访客的配置文件中以供将来使用。

页面内配置文件属性允许将特定于用户的数据存储在 Target 的配置文件中，供以后进行定位和分段。

## 格式

页面内配置文件属性被传递到 [!DNL Target] 通过作为前缀为“profile”的字符串名称/值对的服务器调用。 带有前缀“profile.”。

属性名称和值是可自定义的（但存在一些用于特定用途的“保留名称”）。

以下是有关页面内配置文件属性的一些示例：

* `profile.membershipLevel=silver`
* `profile.visitCount=3`

## 示例用例

* **登录信息**[!DNL Target]：根据用户的登录信息，将非 PII（个人身份信息）数据共享到 此数据可以是成员资格状态、订单历史记录等。
* **存储信息**：跟踪哪个商店是该用户最喜欢的位置。
* **以前的互动**：跟踪用户以前在该网站上的操作，以便为其将来的个性化提供参考依据。

## 方法的优势

数据被发送到 [!DNL Target] 实时，并可用于数据传入的同一服务器调用。

## 注意事项

需要更新页面代码（直接或通过标记管理系统）。

属性和值在服务器调用中可见，因此访客可以查看这些值。如果共享信息（如信用范围或其他潜在的私人信息），此方法可能不是最佳方法。

## 代码示例

targetPageParamsAll（将属性附加到页面上的所有 mbox 调用）：

`function targetPageParamsAll() { return "profile.param1=value1&profile.param2=value2&profile.p3=hello%20world"; }`

targetPageParams（将属性附加到页面上的全局 mbox）：

`function targetPageParams() { return profile.param1=value1&profile.param2=value2&profile.p3=hello%20world"; }`

mboxCreate 代码中的属性：

`<div class="mboxDefault"> default content to replace by offer </div> <script> mboxCreate('mboxName','profile.param1=value1','profile.param2=value2'); </script>`

## 相关信息的链接

[配置文件属性](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html)

[访客资料](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/categories-audiences/visitor-profile.html)
