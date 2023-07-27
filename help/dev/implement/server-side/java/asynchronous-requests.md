---
title: 如何在中使用异步请求 [!DNL Adobe Target] Java SDK
description: 了解如何 [!DNL Target] Java SDK支持异步请求，这可以将有效目标时间减少为零。
feature: APIs/SDKs
exl-id: e11f8d16-76f6-4d39-822a-34a1cf7f623f
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 3%

---

# 异步请求(Java)

## 描述

服务器端集成的一个好处是，通过使用并行机制，您可以利用服务器端提供的巨大带宽和计算资源。 [!DNL Target] Java SDK支持异步请求，这可以将有效目标时间减少为零。

## 支持的方法

### 方法

```javascript {line-numbers="true"}
CompletableFuture<TargetDeliveryResponse> getOffersAsync(TargetDeliveryRequest request);
CompletableFuture<ResponseStatus> sendNotificationsAsync(TargetDeliveryRequest request);
CompletableFuture<Attributes> getAttributesAsync(TargetDeliveryRequest targetRequest, String ...mboxes);
```

## 示例

示例 `Spring` application Controller可能如下所示：

### 示例控制器

```javascript {line-numbers="true"}
@RestController
public class TargetRestController {

    @Autowired
    private TargetClient targetJavaClient;

    @GetMapping("/mboxTargetOnlyAsync")
        public TargetDeliveryResponse mboxTargetOnlyAsync(
                @RequestParam(name = "mbox", defaultValue = "server-side-mbox") String mbox,
                HttpServletRequest request, HttpServletResponse response) {
            ExecuteRequest executeRequest = new ExecuteRequest()
                    .mboxes(getMboxRequests(mbox));

            TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
                    .context(getContext(request))
                    .execute(executeRequest)
                    .cookies(getTargetCookies(request.getCookies()))
                    .build();
            CompletableFuture<TargetDeliveryResponse> targetResponseAsync =
                    targetJavaClient.getOffersAsync(targetDeliveryRequest);
            targetResponseAsync.thenAccept(tr -> setCookies(tr.getCookies(), response));
            simulateIO();
            TargetDeliveryResponse targetResponse = targetResponseAsync.join();
            return targetResponse;
        }

    /**
     * Function for simulating network calls like other microservices and database calls
     */
    private void simulateIO() {
        try {
            Thread.sleep(200L);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

}
```

此示例假设您拥有 [已初始化SDK](initialize-sdk.md) 就象个春豆，你有 [实用工具方法](utility-methods.md) 可用。

此 [!DNL Target] 请求触发于 `simulateIO` 到执行时，目标结果也应准备就绪。 即使不是这样，在大多数情况下您仍可节省大量成本。
