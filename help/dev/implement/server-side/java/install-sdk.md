---
title: 安装Java SDK
description: 了解如何安装 [!DNL Adobe Target] Java SDK。
feature: APIs/SDKs
exl-id: 5828d5b3-c487-49bf-9458-7ef94374e32d
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '46'
ht-degree: 0%

---

# 安装Java SDK

Java SDK由[Maven Central](https://search.maven.org/artifact/com.adobe.target/target-java-sdk)分发。 若要开始，请通过在`gradle`或`maven`中进行安装来添加为依赖项：

>[!BEGINTABS]

>[!TAB Gradle]

```javascript {line-numbers="true"}
compile 'com.adobe.target:java-sdk:1.0'
```

>[!TAB Maven]

```javascript {line-numbers="true"}
<dependency>
    <groupId>com.adobe.target</groupId>
    <artifactId>java-sdk</artifactId>
    <version>2.0</version>
</dependency>
```

>[!ENDTABS]

可在<https://github.com/adobe/target-java-sdk>中找到开放源代码。
