---
keywords: 实施、实施、设置、设置、页面参数
description: 将数据导入 [!DNL Target] 使用页面参数。
title: 如何将数据导入 [!DNL Target] 使用页面参数？
feature: Implementation
exl-id: 9bb7157e-a938-4150-8a15-c9bf0a0e2296
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 38%

---

# 页面参数

页面参数（也称为“mbox参数”）是直接通过页面代码传入的名称/值对，这些名称/值对不会存储在访客的配置文件中以供将来使用。

页面参数可用于将页面数据发送到 [!DNL Adobe Target] 这些资源无需与访客的配置文件一起存储以供将来定位使用。 而是用来描述页面或用户在特定页面上执行的操作。

## 格式

页面参数被传递到 [!DNL Target] 通过作为字符串名称/值对的服务器调用。 参数名称和值是可自定义的（但存在一些用于特定用途的“保留名称”）。

以下是页面参数的一些示例

* `page=productPage`

* `categoryId=homeLoans`

## 示例用例

* **产品页面**：发送有关已查看的特定产品的信息(此方法是Recommendations的工作方式)
* **订单详细信息**：发送订单ID、orderTotal等以进行订单收集
* **类别亲和度**[!DNL Target]：将已查看的类别信息发送到 ，以了解用户对特定站点类别的亲和度
* **第三方数据**：发送来自第三方数据源的信息，例如天气定位提供程序、帐户数据（例如 DemandBase）、人口统计数据（例如 Experian）等。

## 方法的优势

数据被发送到 [!DNL Target] 并且可以在同一服务器上实时使用并调用它所传入的数据。

## 注意事项

* 需要更新页面代码（直接或通过标记管理系统）。
* 如果必须在后续页面/服务器调用中使用该数据进行定位，则必须将其转换为配置文件脚本。
* 查询字符串只能包含符合 [Internet 工程任务组 (IETF) 标准](https://www.ietf.org/rfc/rfc3986.txt)的字符。

  除了IETF站点上提到的那些字符之外， [!DNL Target] 允许在查询字符串中使用以下字符：

  ```< > # % " { } | \ ^ [ ] ` ``` {line-numbers=&quot;true&quot;}

  其他所有字符都必须采用 URL 编码。该标准规定了以下格式( [https://www.ietf.org/rfc/rfc1738.txt](https://www.ietf.org/rfc/rfc1738.txt) )，如下所示：

  ![替代图像](assets/ietf1.png)

  或者，简单显示完整列表：

  ![替代图像](assets/ietf2.png)

## 代码示例

targetPageParamsAll（将参数附加到页面上的所有 mbox 调用）：

`function targetPageParamsAll() { return "param1=value1&param2=value2&p3=hello%20world";`

targetPageParams（将参数附加到页面上的全局 mbox）：

`function targetPageParams() { return "param1=value1&param2=value2&p3=hello%20world";`

## 相关信息的链接

推荐：[按照页面类型实施](https://experienceleague.adobe.com/docs/target/using/recommendations/plan-implement.html)

订单确认：[跟踪转化](../../implement/client-side/atjs/how-to-deployatjs/implement-target-without-a-tag-manager.md#track-conversions)

类别亲和度：[类别亲和度](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/category-affinity.html)
