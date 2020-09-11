---
title: 'Visual Studio 文档：2020 年 8 月新增功能 '
titleSuffix: ''
description: 2020 年 8 月 Visual Studio 文档中的新增功能。
ms.date: 09/02/2020
helpviewer_keywords:
- Visual Studio, what's new, docs
- what's new [Visual Studio]
ms.assetid: 89844796-621B-4EF5-9D76-197084B011CB
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.topic: conceptual
ms.workload:
- multiple
ms.openlocfilehash: 4364bd62ac19be958632b8cb2dbbe907013e8a70
ms.sourcegitcommit: 703c68667261df5985a73282c1cbb0541118989c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89402239"
---
# <a name="visual-studio-docs-whats-new-for-august-2020"></a>Visual Studio 文档：2020 年 8 月新增功能

欢迎了解 2020 年 8 月 Visual Studio 文档中的新增功能。 本文列出了 7 月份对文档进行的一些重大更改。 有关前几月新增功能的信息，请参阅[新增功能历史记录](whats-new-visual-studio-docs-history.md)主题。

## <a name="azure"></a>Azure

**新文章**

- [使用 Visual Studio 连接服务添加 Azure Application Insights](/visualstudio/azure/azure-app-insights-add-connected-service) - 用于 VS 2019 16.7 的连接服务
- [使用 Visual Studio 连接服务添加 Azure Cache for Redis](/visualstudio/azure/azure-cache-for-redis-add-connected-service) - 用于 VS 2019 16.7 的连接服务
- [使用 Visual Studio 连接服务将 Azure Cosmos DB 添加到你的应用](/visualstudio/azure/azure-cosmosdb-add-connected-service) - 用于 VS 2019 16.7 的连接服务
- [使用 Visual Studio 连接服务添加 Azure SignalR](/visualstudio/azure/azure-signalr-add-connected-service) - 用于 VS 2019 16.7 的连接服务
- [添加与 Azure SQL 数据库的连接](/visualstudio/azure/azure-sql-database-add-connected-service) - 用于 VS 2019 16.7 的连接服务

**更新的文章**

- [使用 Visual Studio 连接服务添加 Azure 存储](/visualstudio/azure/vs-azure-tools-connected-services-storage)
  - 用于 VS 2019 16.7 的连接服务
  - Azure 存储连接服务文章：支持更新 UI 和项目类型

## <a name="code-quality"></a>代码质量

**新文章**

- [CA1310：为了确保正确，请指定 StringComparison](/visualstudio/code-quality/ca1310) - 添加 CA1310 的文档并更新 CA1307 的文档
- [CA1837：使用 Environment.ProcessId 而不是 Process.GetCurrentProcess().Id](/visualstudio/code-quality/ca1837) - CA1837 的文档
- [CA1838：避免 P/Invokes 的 `StringBuilder` 参数](/visualstudio/code-quality/ca1838) - 添加 CA1838 的文档
- [CA2008：不要在未传递 TaskScheduler 的情况下创建任务](/visualstudio/code-quality/ca2008) - 添加 CA2008 的文档
- [CA2249：请考虑使用 String.Contains 而不是 String.IndexOf](/visualstudio/code-quality/ca2249) - CA2249 的文档
- [CA2361：请确保包含 DataSet.ReadXml() 的自动生成的类没有与不受信任的数据一起使用](/visualstudio/code-quality/ca2361) - 更多数据集/数据表规则
- [CA2362：自动生成的可序列化类型中不安全的数据集或数据表易受远程代码执行攻击](/visualstudio/code-quality/ca2362) - 更多数据集/数据表规则
- [IL3000：当发布为单个文件时，避免使用访问程序集文件路径](/visualstudio/code-quality/il3000) - 添加 IL3000 的文档
- [IL3001：当发布为单个文件时，避免使用访问程序集文件路径](/visualstudio/code-quality/il3001) - 添加 IL3001 的文档

**已更新**

- [CA1002：不要公开泛型列表](/visualstudio/code-quality/ca1002) - 添加可配置性 - API Surface 部分
- [CA1046：不要对引用类型重载同等运算符](/visualstudio/code-quality/ca1046) - 添加可配置性 - API Surface 部分
- [CA1307：为了清晰起见，请指定 StringComparison](/visualstudio/code-quality/ca1307) - 添加 CA1310 的文档并更新 CA1307 的文档
- [CA1700：不要命名“Reserved”枚举值](/visualstudio/code-quality/ca1700) - 添加可配置性 - API Surface 部分
- [CA1707：标识符不应包含下划线](/visualstudio/code-quality/ca1707) - 添加可配置性 - API Surface 部分
- [CA1822：将成员标记为 static](/visualstudio/code-quality/ca1822) - 添加可配置性 - API Surface 部分
- [CA2351：确保 DataSet.ReadXml() 的输入受信任](/visualstudio/code-quality/ca2351) - 更多数据集/数据表规则
- [安装第三方分析器](/visualstudio/code-quality/install-roslyn-analyzers) - 已更改代码分析文档的结构和标题

## <a name="containers"></a>容器

**更新的文章**

- [使用 Visual Studio 将 ASP.NET 容器部署到容器注册表](/visualstudio/containers/hosting-web-apps-in-docker) - Visual Studio 16.7 发布 UI 的容器工具更新
- [Visual Studio Kubernetes 工具入门](/visualstudio/containers/tutorial-kubernetes-tools) - Kubernetes 教程：添加要删除的步骤

## <a name="deployment"></a>部署

**新文章**

- [Visual Studio 安装程序项目扩展和 NET Core 3.1](/visualstudio/deployment/installer-projects-net-core) - 为安装程序项目 .NET Core 3.1 功能创建新帮助页

**更新的文章**

- [将应用部署到文件夹、IIS、Azure 或其他目标](/visualstudio/deployment/deploying-applications-services-and-components-resources) - 部署更新
- [Visual Studio 中的部署](/visualstudio/deployment/index) - 部署更新

## <a name="extensibility"></a>扩展性

**更新的文章**
- [项目子类型](/visualstudio/extensibility/internals/project-subtypes) - 修复列表项缩进
- [Visual Studio 的颜色值参考](/visualstudio/extensibility/ux-guidelines/color-value-reference-for-visual-studio) - AB#1759333 修复缺少的列标题

## <a name="get-started"></a>入门

**更新的文章**

- [步骤 5：将 ASP.NET Core 应用部署到 Azure](/visualstudio/get-started/csharp/tutorial-aspnet-core-ef-step-05) - 新连接服务 UI 的视频教程更新

## <a name="ide"></a>IDE

**新文章**

- [在 Visual Studio 中更改 F1 帮助键](/visualstudio/ide/not-in-toc/change-f1-help-key) - 重构默认 F1 帮助页
- [文本编辑器的 F1 帮助](/visualstudio/ide/not-in-toc/default-f1-text-editor) - 重构默认 F1 帮助页
- [将 `typeof` 转换为 `nameof`](/visualstudio/ide/reference/convert-typeof-to-nameof) - 将 typeof 转换为 nameof 重构
- [简化 LINQ 表达式](/visualstudio/ide/reference/simplify-linq-expression) - 简化 LINQ 表达式重构

**更新的文章**

- [在 Visual Studio 中自定义窗口布局](/visualstudio/ide/customizing-window-layouts-in-visual-studio) - 将已标记的竖排文档选项卡信息添加到“自定义窗口布局”主题
- [如何报告 Visual Studio 或 Visual Studio 安装程序的问题](/visualstudio/ide/how-to-report-a-problem-with-visual-studio)
  - 向 NMI 添加详细信息
  - 重做整个“报告问题”页
- [F1 帮助](/visualstudio/ide/not-in-toc/default) - 重构默认 F1 帮助页
- [“选项”对话框 ->“环境”->“自动恢复”](/visualstudio/ide/reference/autorecover-environment-options-dialog-box) - 添加有关更新的自动保存文件位置的信息
- [“选项”>“文本编辑器”>“基本(Visual Basic)”>“高级”](/visualstudio/ide/reference/options-text-editor-basic-visual-basic) - 添加内联参数名称提示的基本文档
- [“选项”->“文本编辑器”->“C#”->“高级”](/visualstudio/ide/reference/options-text-editor-csharp-advanced) - 添加内联参数名称提示的基本文档
- [Visual Studio 性能提示和技巧](/visualstudio/ide/visual-studio-performance-tips-and-tricks) - 添加“禁用地图模式”和“禁用自动换行”信息
- [Visual Studio 2019 中的新增功能](/visualstudio/ide/whats-new-visual-studio-2019) - 使用 16.7 GA 信息更新 Visual Studio 2019 中的新增功能

## <a name="rtvs"></a>RTVS

**更新的文章**

- [使用 SQL Server 和 R](/visualstudio/rtvs/integrating-sql-server-with-r) - 包括列标题的更正的表

## <a name="community-contributors"></a>社区参与者

在此期间，以下人员为 Visual Studio 文档做出了贡献。 谢谢！ 按照[参与者指南](https://docs.microsoft.com/contribute/)中的指导操作，了解如何参与 Visual Studio 文档。

- [AlexB-SheldonMFG](https://github.com/AlexB-SheldonMFG) - Alex Black (11)
- [Youssef1313](https://github.com/Youssef1313) - Youssef Victor (8)
- [hyoshioka0128](https://github.com/hyoshioka0128) - Hiroshi Yoshioka (3)
- [AstroChoco](https://github.com/AstroChoco) - Qian Lu (Chocolate) (1)
- [athyunnath](https://github.com/athyunnath) - Athyunnath Eleti (1)
- [caro-oviedo](https://github.com/caro-oviedo) - Caro Oviedo  (1)
- [Evangelink](https://github.com/Evangelink) - Amaury Levé (1)
- [jethas-bennettjones](https://github.com/jethas-bennettjones) - Shafiq Jetha (1)
- [nebuk89](https://github.com/nebuk89) - Ben De St Paer-Gotch (1)
- [pcartwright81](https://github.com/pcartwright81) (1)
- [pkulikov](https://github.com/pkulikov) - Petr Kulikov (1)
- [riQQ](https://github.com/riQQ) (1)
- [tcmetzger](https://github.com/tcmetzger) - Timo Cornelius Metzger (1)
- [weitzhandler](https://github.com/weitzhandler) - Shimmy (1)