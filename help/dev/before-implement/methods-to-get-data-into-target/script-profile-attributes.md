---
keywords: 实施、实施、设置、设置、脚本配置文件属性
description: 使用脚本配置文件属性将数据导入 [!DNL Target] 。
title: 如何使用脚本配置文件属性将数据导入 [!DNL Target] ？
feature: Implementation
exl-id: ba11f1de-e68b-4505-8e3e-cd4d46ef59a2
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 74%

---

# 脚本配置文件属性

脚本配置文件属性是在[!DNL Adobe Target]解决方案中定义的名称/值对。 该值是在每个服务器调用时，通过在 Target 服务器上执行一段 JavaScript 代码来确定。

为访客评估受众和活动用户编写一小段代码，该代码片段会在每次 mbox 调用时、且在评估访客的受众群体和活动成员资格之前执行。

## 格式

脚本配置文件属性在 Target 的“受众”区域中创建。任何属性名称都有效，该值是[!DNL Target]用户编写的JavaScript函数的结果。 该属性名称自动在 Target 中添加“user. [!DNL Target]中的&quot;，以将其与页面内配置文件属性区分开。

代码片段以 Rhino JS 语言编写，可引用令牌和其他值。

## 使用示例

* **购物车放弃**：当访客到达购物车时，将配置文件脚本设为 1。当访客转化后，将其重置为 0。如果值 = 1，则访客在购物车中有一个商品。
* **访问计数**：每新增一次访问，计数将增加 1，以跟踪访客返回网站的频率。

## 方法的优势

不需要更新页面代码。

在受众和活动成员资格决策之前执行，这样这些配置文件脚本属性会影响单个服务器调用的成员资格。

此方法操作容量非常大。每个脚本可以执行多达 2,000 条指令。

## 注意事项

需要 JavaScript 知识。

无法保证配置文件脚本的执行顺序，因此它们不能相互依赖。

可能很难调试。

## 代码示例

配置文件脚本非常灵活：

```
user.purchase_recency: var dayInMillis = 3600 * 24 * 1000; if (mbox.name == 'orderThankyouPage') {  user.setLocal('lastPurchaseTime', new Date().getTime()); } var lastPurchaseTime = user.getLocal('lastPurchaseTime'); if (lastPurchaseTime) {  return ((new Date()).getTime()-lastPurchaseTime)/dayInMillis; }
```

### 相关信息的链接

[配置文件脚本属性](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/profile-parameters.html?lang=zh-Hans#concept_8C07AEAB0A144FECA8B4FEB091AED4D2)
