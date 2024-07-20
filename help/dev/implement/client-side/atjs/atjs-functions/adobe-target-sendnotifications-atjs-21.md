---
keywords: adobe.target.sendNotifications， sendNotifications， sendnotifications，发送通知，通知， at.js，函数，函数， $9
description: 呈现体验时，使用at.js的[!UICONTROL adobe.target.sendNotifications()]向 [!DNL Target] 边缘发送通知，而不使用[!UICONTROL applyOffer]。 (at.js.2.1 +)
title: 如何使用adobe.target.sendNotifications()函数？
feature: at.js
exl-id: 1a08da10-31a0-4b0b-af7d-91ed7d32c308
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 83%

---

# [!UICONTROL adobe.target.sendNotifications(options)]

在不使用`[!UICONTROL adobe.target.applyOffer()]`或`[!UICONTROL adobe.target.applyOffers()]`呈现体验时，此函数会向[!DNL Target]边缘发送通知。

>[!NOTE]
>
>此函数已在 at.js 2.1.0 中引入，可用于 2.1.0 以上的任何版本。

| 键 | 类型 | 必需？ | 描述 |
| --- | --- | --- | --- |
| consumerId | 字符串 | 否 | 如果未提供，则默认值为客户端的全局 mbox。可使用此键值生成用于 A4T 集成的补充数据 ID。 |
| 请求 | 对象 | 是 | 请参阅下文的“请求”表。 |
| timeout | 数值 | 否 | 请求超时. 如果未指定，将使用默认的 at.js 超时值。 |

## 请求

| 字段名称 | 类型 | 必需？ | 限制 | 描述 |
| --- | --- | --- | --- | --- |
| Request > notifications | 对象数组 | 是 |  | 有关显示的内容、点击的选择器和/或访问的视图或 mbox 的通知。 |
| Request > notifications > address | 对象 | 否 |  |  |
| Request > notifications > address > url | 字符串 | 否 |  | 从中触发通知的 URL。 |
| Request > notifications > address > referringUrl | 字符串 | 否 |  | 从中触发通知的引荐 URL。 |
| Request > notifications > parameters | 字符串 | 否 | 参数不允许使用以下名称：<ul><li>orderId</li><li>orderTotal</li><li>productPurchasedIds</li></ul>请考虑以下事项：<ul><li>参数上限为 50 个。</li><li>参数名称不应为空。</li><li>参数名称的最大长度为 128。</li><li>参数名称不应以“profile”开头。</li><li>参数值的最大长度为 5000。</li></ul> |  |
| Request > notifications > profileParameters | 字符串 | 否 | 参数不允许使用以下名称：<ul><li>orderId</li><li>orderTotal</li><li>productPurchasedIds</li></ul>请考虑以下事项：<ul><li>参数上限为 50 个。</li><li>参数名称不应为空。</li><li>参数名称的最大长度为 128。</li><li>参数名称不应以“profile”开头。</li><li>参数值的最大长度为 5000。</li></ul> |  |
| Request > notifications > order | 对象 | 否 |  | 描述订单详细信息的对象。 |
| Request > notifications > order > id | 字符串 | 否 | `<=` 250 个字符。 | 订单 ID。 |
| Request > notifications > order > total | 字符串 | 否 | `>=` 0 | 订单总计。 |
| Request > notifications > order > purchasedProductIds | 字符串数组 | 否 | <ul><li>不允许使用空值。</li><li>每个产品 ID 的最大长度为 50。</li><li>产品 ID 用逗号分隔和连接，总长度不应超过 250。</li></ul> | 订单产品 ID。 |
| Request > notifications > product | 对象 | 否 |  |  |
| Request > notifications > product > id | 字符串 | 否 | `<=` 128 个字符；不能为空。 | 产品 ID。 |
| Request > notifications > product > categoryId | 字符串 | 否 | `<=` 128 个字符；不能为空。 | 类别 ID。 |
| Request > notifications > id | 字符串 | 是 | `<=` 200 个字符。 | 通知 ID 将在响应中返回，并指示通知已成功处理。 |
| Request > notifications > impressionId | 字符串 | 否 | `<= 128` 个字符。 | 展示 ID 用于将当前通知与先前的通知或执行请求拼合（链接）到一起。如果两者匹配，则第二个和其他后续请求不会生成活动或体验的新展示。 |
| Request > notifications > type | 字符串 | 是 | 支持“click”或“display”。 | 通知类型。 |
| Request > notifications > timestamp | 数值`<int64>` | 是 |  | 通知的时间戳（以自 UNIX 纪元以来所经过的毫秒数为单位）。 |
| Request > notifications > tokens | 字符串数组 | 是 |  | 基于通知类型的已显示内容或已点击选择器的令牌列表。 |
| Request > notifications > mbox | 对象 | 否 |  | 有关 mbox 的通知。 |
| Request > notifications > mbox > name | 字符串 | 否 | 不允许使用空值。<p>允许的字符：请参阅此表后面的注释。 | mbox 名称。 |
| Request > notifications > mbox > state | 字符串 | 否 |  | mbox 状态令牌。 |
| Request > notifications > view | 对象 | 否 |  |  |
| Request > notifications > view > id | 整数 `<int64>` | 否 |  | 视图 ID。通过视图 API 创建视图时分配给视图的 ID。 |
| Request > notifications > view > name | 字符串 | 否 | `<= 128` 个字符。 | 视图的名称。 |
| Request > notifications > view > key | 字符串 | 否 | `<=` 512 个字符。 | 视图键。通过 API 在视图中设置的键。 |
| Request > notifications > view > state | 字符串 | 否 |  | 视图状态令牌。 |

**注意**： `Request > notifications > mbox > name`不允许使用以下字符&#x200B;**：

```
- '-, ./=`:;&!@#$%^&*()+|?~[]{}'
```

## 呈现预取的 mbox 后调用 sendNotifications()

```javascript {line-numbers="true"}
function createTokens(options) {
  return options.map(e => e.eventToken);
}

function createNotification(mbox, type, tokens) {
  const id = 11111; // here we should use a random ID like UUID
  const timestamp = Date.now();
  const { name, state, parameters, profileParameters, order, product } = mbox;
  const result = {
    id,
    type,
    timestamp,
    parameters,
    profileParameters,
    order,
    product
  };

  result.mbox = { name, state };
  result.tokens = tokens;

  return result;
}

adobe.target.getOffers({
  request: {
    prefetch: {
      mboxes: [
        {
          index: 0,
          name: "a1-serverside-ab"
        }
      ]
    }
  }
})
.then(response => {
  const mboxes = response.prefetch.mboxes;
  const notifications = mboxes.map(mbox => {
    const type = "display";
    const tokens = createTokens(mbox.options);

    return createNotification(mbox, type, tokens);
  });
  
  adobe.target.sendNotifications({
    request: { notifications }
  });
})
```

>[!NOTE]
>
>如果您正在使用[!DNL Adobe Analytics]、`[!UICONTROL getOffers()]`和`[!UICONTROL sendNotifications()]`，则在执行`[!UICONTROL sendNotifications()]`后必须触发[!DNL Analytics]请求。 其目的在于确保`[!UICONTROL sendNotifications()]`生成的SDID与发送到[!DNL Analytics]和[!DNL Target]的SDID匹配。
