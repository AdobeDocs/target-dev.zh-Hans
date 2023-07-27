---
title: 安装.NET SDK
description: 了解如何安装 [!DNL Adobe Target] .NET SDK.
feature: APIs/SDKs
exl-id: 3cc84775-4692-4d14-9e82-db2873140835
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '60'
ht-degree: 0%

---

# 安装.NET SDK

.NET SDK的分发方 [NuGet](https://www.nuget.org/packages/Adobe.Target.Client). 要开始使用此功能，请通过安装将其添加为依赖项 `Package Manage` 或 `.NET CLI`：

## 包管理器

>[!BEGINTABS]

>[!TAB 包管理器]

```csharp {line-numbers="true"}
Install-Package Adobe.Target.Client
```

>[!TAB .NET CLI]

```csharp {line-numbers="true"}
dotnet add package Adobe.Target.Client
```

>[!ENDTABS]

开源代码位于 [https://github.com/adobe/target-dotnet-sdk](https://github.com/adobe/target-dotnet-sdk).
