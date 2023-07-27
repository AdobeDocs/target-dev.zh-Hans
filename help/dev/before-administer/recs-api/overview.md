---
title: 什么是Adobe Recommendations API？
description: 本指南将指导开发人员使用Adobe Target Recommendations API配置和管理Recommendations目录和自定义标准以及使用交付API检索推荐内容的实践操作。
feature: APIs/SDKs, Recommendations, Administration & Configuration, Overview
kt: 3815
thumbnail: null
author: Judy Kim
exl-id: 0d03c650-0b00-44b8-a794-10e5d738e42c
source-git-commit: e5bae1ac9485c3e1d7c55e6386f332755196ffab
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 2%

---

# Adobe Recommendations API概述

与Recommendations相关的API包括 [管理员API](../../before-administer/target-api-overview.md) 该功能允许您：

* 管理您的推荐产品或内容目录
* 管理Recommendations算法和活动

使用Target [投放API](../../implement/delivery-api/overview.md) 通过Recommendations，您还可以：

* 检索JSON、HTML或XML对象中的推荐，以便这些推荐可在Web、移动设备、电子邮件、物联网(IOT)和其他渠道中显示。

## 描述

有关Recommendations API的本指南将指导开发人员使用Recommendations API配置和管理Recommendations目录和自定义标准以及使用交付API检索推荐内容的实践操作。 到最后，您将能够：

* 使用Recommendations API配置和管理实体
* 使用Recommendations API配置和管理自定义标准
* 了解如何将Recommendations与投放API结合使用，以在非HTML设备中使用推荐结果

## 受众

本指南面向不熟悉Target API或Recommendations API的开发人员。

## 先决条件 {#prerequisites}

Target管理员API需要 [Adobe身份验证设置](../configure-authentication.md). 在使用Recommendations API之前，请确保已配置此项。

## 资源

请注意以下资源，了解本指南并成功遵循本指南所必需的：

| 资源 | 详细信息 |
| --- | --- |
| Postman | 获取 [Postman应用程序](https://www.postman.com/downloads/) 适用于您的操作系统。 Postman basic可在创建帐户时免费使用。 虽然总体而言使用Adobe Target API不需要使用，但Postman简化了API工作流程，并且Adobe Target提供了多个Postman收藏集以帮助执行其API并了解其操作方式。 本指南的其余部分假定您了解Postman的工作知识。 如需帮助，请参考 [Postman文档](https://learning.getpostman.com/). |
| 引用 | 在本指南的其余部分中，均假定您已熟悉以下资源：<UL><li>[Adobe I/OGithub](https://github.com/adobeio)</li><li>[Target管理员和配置文件API文档](../../administer/admin-api/admin-api-overview-new.md)</li><li>[Recommendations API文档](https://developers.adobetarget.com/api/recommendations/)</li></UL> |
