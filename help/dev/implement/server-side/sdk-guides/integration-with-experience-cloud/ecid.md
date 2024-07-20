---
title: Experience CloudID (ECID)服务
description: 虽然使用 [!DNL Target] SDK从 [!DNL Target] 中提取内容可能非常强大，但使用[!UICONTROL Experience Cloud ID] (ECID)进行用户跟踪的附加价值不仅限于Adobe [!DNL Target]. The ECID enables you to leverage [!DNL Adobe Experience Cloud] 产品和功能，如A4T报表和 [!DNL Adobe Audience Manager] (AAM)区段。
exl-id: fd7e5c3e-51c1-4965-ab6a-f50a6b0c910b
feature: Implement Server-side
source-git-commit: 09a50aa67ccd5c687244a85caad24df56c0d78f5
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# [!UICONTROL Experience Cloud ID] (ECID)服务

## [!UICONTROL Experience Cloud ID] (ECID)集成

尽管使用[!DNL Target] SDK从[!DNL Target]中提取内容可能非常强大，但使用[!UICONTROL Experience Cloud ID] (ECID)进行用户跟踪的附加值扩展到了[!DNL Adobe Target]之外。 ECID允许您利用[!DNL Adobe Experience Cloud]产品和功能，例如A4T报表和[!DNL Adobe Audience Manager] (AAM)区段。

ECID由`visitor.js`生成和维护，它保持自己的状态。 `visitor.js`文件将创建一个名为`AMCV_{organizationId}`的Cookie，供[!DNL Target] SDK用于ECID集成。 当返回[!DNL Target]响应时，您需要使用[!DNL Target] SDK返回的`thevisitorState`更新客户端上的访客实例。

```html {line-numbers="true"}
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <title>ECID (Visitor API) Integration Sample</title>
  <script src="VisitorAPI.js"></script>
  <script>
    Visitor.getInstance("${organizationId}", {serverState: ${visitorState}});
  </script>
</head>
<body>
  <pre>Sample content</pre>
</body>
</html>
```

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const express = require("express");
const cookieParser = require("cookie-parser");
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};
const TEMPLATE = `
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <title>ECID (Visitor API) Integration Sample</title>
  <script src="VisitorAPI.js"></script>
  <script>
    Visitor.getInstance("${organizationId}", {serverState: ${visitorState}});
  </script>
</head>
<body>
  <pre>${content}</pre>
</body>
</html>
`;

const app = express();
const targetClient = TargetClient.create(CONFIG);

app.use(cookieParser());
// We assume that VisitorAPI.js is stored in "public" folder
app.use(express.static(__dirname + "/public"));

function saveCookie(res, cookie) {
  if (!cookie) {
    return;
  }

  res.cookie(cookie.name, cookie.value, {maxAge: cookie.maxAge * 1000});
}

const getResponseHeaders = () => ({
  "Content-Type": "text/html",
  "Expires": new Date().toUTCString()
});

function sendSuccessResponse(res, response) {
  res.set(getResponseHeaders());

  const result = TEMPLATE
  .replace("${organizationId}", CONFIG.organizationId)
  .replace("${visitorState}", JSON.stringify(response.visitorState))
  .replace("${content}", response);

  saveCookie(res, response.targetCookie);

  res.status(200).send(result);
}

function sendErrorResponse(res, error) {
  res.set(getResponseHeaders());
  res.status(500).send(error);
}

app.get("/abtest", async (req, res) => {
  const visitorCookie = req.cookies[TargetClient.getVisitorCookieName(CONFIG.organizationId)];
  const targetCookie = req.cookies[TargetClient.TargetCookieName];
  const request = {
      execute: {
        mboxes: [{
          address: { url: req.headers.host + req.originalUrl },
          name: "a1-serverside-ab"
        }]
      }};
```

>[!TAB Java]

```java {line-numbers="true"
  console.log("Request", request);

  try {
      const response = await targetClient.getOffers({ request, visitorCookie, targetCookie });
      sendSuccessResponse(res, response);
    } catch (error) {
      sendErrorResponse(res, error);
    }
});

app.listen(3000, function () {
  console.log("Listening on port 3000 and watching!");
});
@Controller
public class TargetControllerSample {

  @Autowired
  private TargetClient targetClient;

  @GetMapping("/")
  public String targetMcid(Model model, HttpServletRequest request, HttpServletResponse response) {
    Context context = getContext(request);
    TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
        .context(context)
        .prefetch(getPrefetchRequest())
        .cookies(getTargetCookies(request.getCookies()))
        .build();

    TargetDeliveryResponse targetResponse = targetClient.getOffers(targetDeliveryRequest);
    model.addAttribute("visitorState", targetResponse.getVisitorState());
    model.addAttribute("organizationId", "0DD934B85278256B0A490D44@AdobeOrg");
    setCookies(targetResponse.getCookies(), response);
    return "targetMcid";
  }
}
```

>[!ENDTABS]

## ECID与客户ID集成

为了跟踪访客用户帐户和登录状态详细信息，可以通过[!DNL Target] SDK传递`customerIds`。

```html {line-numbers="true"
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <title>ECID (Visitor API) Integration Sample</title>
  <script src="VisitorAPI.js"></script>
  <script>
    Visitor.getInstance("${organizationId}", {serverState: ${visitorState}});
  </script>
</head>
<body>
  <pre>Sample content</pre>
</body>
</html>
```

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const express = require("express");
const cookieParser = require("cookie-parser");
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};
const TEMPLATE = `
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <title>ECID (Visitor API) with Customer IDs Integration Sample</title>
  <script src="VisitorAPI.js"></script>
  <script>
    Visitor.getInstance("${organizationId}", {serverState: ${visitorState}});
  </script>
</head>
<body>
  <pre>${content}</pre>
</body>
</html>
`;

const app = express();
const targetClient = TargetClient.create(CONFIG);

app.use(cookieParser());
// We assume that VisitorAPI.js is stored in "public" folder
app.use(express.static(__dirname + "/public"));

function saveCookie(res, cookie) {
  if (!cookie) {
    return;
  }

  res.cookie(cookie.name, cookie.value, {maxAge: cookie.maxAge * 1000});
}

const getResponseHeaders = () => ({
  "Content-Type": "text/html",
  "Expires": new Date().toUTCString()
});

function sendSuccessResponse(res, response) {
  res.set(getResponseHeaders());

  const result = TEMPLATE
  .replace("${organizationId}", CONFIG.organizationId)
  .replace("${visitorState}", JSON.stringify(response.visitorState))
  .replace("${content}", response);

  saveCookie(res, response.targetCookie);

  res.status(200).send(result);
}

function sendErrorResponse(res, error) {
  res.set(getResponseHeaders());
  res.status(500).send(error);
}

app.get("/abtest", async (req, res) => {
  const visitorCookie = req.cookies[TargetClient.getVisitorCookieName(CONFIG.organizationId)];
  const targetCookie = req.cookies[TargetClient.TargetCookieName];
  const customerIds = {
      "userid": {
        "id": "67312378756723456",
        "authState": TargetClient.AuthState.AUTHENTICATED
      }
    };
  const request = {
    execute: {
      mboxes: [{
        address: { url: req.headers.host + req.originalUrl },
        name: "a1-serverside-ab"
      }]
    }};

  try {
    const response = await targetClient.getOffers({ request, visitorCookie, targetCookie, customerIds });
    sendSuccessResponse(res, response);
  } catch (error) {
    sendErrorResponse(res, error);
  }
});

app.listen(3000, function () {
  console.log("Listening on port 3000 and watching!");
});
```

>[!TAB Java]

```java {line-numbers="true"}
@Controller
public class TargetControllerSample {

  @Autowired
  private TargetClient targetJavaClient;

  @GetMapping("/targetMcid")
  public String targetMcid(Model model, HttpServletRequest request, HttpServletResponse response) {
    Context context = getContext(request);
    Map<String, CustomerState> customerIds = new HashMap<>();
    customerIds.put("userid", CustomerState.authenticated("67312378756723456"));
    customerIds.put("puuid", CustomerState.unknown("550e8400-e29b-41d4-a716-446655440000"));
    TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
       .context(context)
       .prefetch(getPrefetchRequest())
       .cookies(getTargetCookies(request.getCookies()))
       .customerIds(customerIds)
       .build();

    TargetDeliveryResponse targetResponse = targetJavaClient.getOffers(targetDeliveryRequest);
    model.addAttribute("visitorState", targetResponse.getVisitorState());
    model.addAttribute("organizationId", "0DD934B85278256B0A490D44@AdobeOrg");
    setCookies(targetResponse.getCookies(), response);
    return "targetMcid";
  }
}
```

>[!ENDTABS]

## ECID与[!DNL Analytics]集成

要充分利用[!DNL Target] SDK并使用[!DNL Adobe Analytics]提供的强大分析功能，您可以使用跨ECID、[!DNL Analytics]和[!DNL Target]的集成。

通过使用跨ECID、[!DNL Analytics]和[!DNL Target]的集成，您可以：

* 使用来自Adobe Audience Manager (AAM)的区段
* 根据从[!DNL Target]检索到的内容自定义用户体验
* 确保在[!DNL Analytics]中收集所有事件和成功量度
* 使用[!DNL Analytics]的强大查询并受益于其出色的报告可视化图表

ECID、[!DNL Analytics]和[!DNL Target]之间的集成不需要在服务器端对分析进行任何特殊处理。 相反，集成ECID后，请在客户端添加`AppMeasurement.js` （[!DNL Analytics]库）。 [!DNL Analytics]然后使用访客实例与[!DNL Target]同步。

```html {line-numbers="true"}
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <title>ECID and Analytics integration Sample</title>
  <script src="VisitorAPI.js"></script>
  <script>
    Visitor.getInstance("${organizationId}", {serverState: ${visitorState}});
  </script>
</head>
<body>
  <p>Sample content</p>
  <script src="AppMeasurement.js"></script>
  <script>var s_code=s.t();if(s_code)document.write(s_code);</script>
</body>
</html>
```

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const express = require("express");
const cookieParser = require("cookie-parser");
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};
const TEMPLATE = `
<!doctype html>
<html>
<head>
  <meta charset="UTF-8">
  <title>ECID and Analytics integration Sample</title>
  <script src="VisitorAPI.js"></script>
  <script>
    Visitor.getInstance("${organizationId}", {serverState: ${visitorState}});
  </script>
</head>
<body>
  <p>${content}</p>
  <script src="AppMeasurement.js"></script>
  <script>var s_code=s.t();if(s_code)document.write(s_code);</script>
</body>
</html>
`;

const app = express();
const targetClient = TargetClient.create(CONFIG);

app.use(cookieParser());
// We assume that VisitorAPI.js and AppMeasurement.js are stored in "public" directory
app.use(express.static(__dirname + "/public"));

function saveCookie(res, cookie) {
  if (!cookie) {
    return;
  }

  res.cookie(cookie.name, cookie.value, {maxAge: cookie.maxAge * 1000});
}

const getResponseHeaders = () => ({
  "Content-Type": "text/html",
  "Expires": new Date().toUTCString()
});

function sendSuccessResponse(res, response) {
  res.set(getResponseHeaders());

  const result = TEMPLATE
  .replace("${organizationId}", CONFIG.organizationId)
  .replace("${visitorState}", JSON.stringify(response.visitorState))
  .replace("${content}", response);

  saveCookie(res, response.targetCookie);

  res.status(200).send(result);
}

function sendErrorResponse(res, error) {
  res.set(getResponseHeaders());

  res.status(500).send(error);
}

app.get("/abtest", async (req, res) => {
  const visitorCookie = req.cookies[TargetClient.getVisitorCookieName(CONFIG.organizationId)];
  const targetCookie = req.cookies[TargetClient.TargetCookieName];
  const request = {
      execute: {
        mboxes: [{
          address: { url: req.headers.host + req.originalUrl },
          name: "a1-serverside-ab"
        }]
      }};

    try {
      const response = await targetClient.getOffers({ request, visitorCookie, targetCookie });
      sendSuccessResponse(res, response);
    } catch (error) {
      sendErrorResponse(res, error);
    }
});

app.listen(3000, function () {
  console.log("Listening on port 3000 and watching!");
});
```

>[!TAB Java]

```java {line-numbers="true"}
@Controller
public class TargetControllerSample {

    @Autowired
    private TargetClient targetJavaClient;

    @GetMapping("/targetAnalytics")
    public String targetMcid(Model model, HttpServletRequest request, HttpServletResponse response) {
        Context context = getContext(request);
        Map<String, CustomerState> customerIds = new HashMap<>();
        customerIds.put("userid", CustomerState.authenticated("67312378756723456"));
        customerIds.put("puuid", CustomerState.unknown("550e8400-e29b-41d4-a716-446655440000"));
        TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
                .context(context)
                .prefetch(getPrefetchRequest())
                .cookies(getTargetCookies(request.getCookies()))
                .customerIds(customerIds)
                .trackingServer("imsbrims.sc.omtrds.net")
                .build();

        TargetDeliveryResponse targetResponse = targetJavaClient.getOffers(targetDeliveryRequest);
        model.addAttribute("visitorState", targetResponse.getVisitorState());
        model.addAttribute("organizationId", "0DD934B85278256B0A490D44@AdobeOrg");
        setCookies(targetResponse.getCookies(), response);
        return "targetAnalytics";
    }
```

>[!ENDTABS]
