---
title: 'Visual Studio 文档：新增功能历史记录 '
titleSuffix: ''
description: Visual Studio 中的新增功能历史记录文档
ms.date: 09/30/2020
helpviewer_keywords:
- Visual Studio, what's new, docs
- what's new [Visual Studio]
ms.assetid: 511DAFC7-896E-449A-BFF7-0E8F7BBA8A78
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.topic: conceptual
ms.workload:
- multiple
ms.openlocfilehash: b9aba6b9c4be882498535ab96020461f22722c10
ms.sourcegitcommit: c025a5e2013c4955ca685092b13e887ce64aaf64
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2020
ms.locfileid: "91659298"
---
# <a name="history-of-whats-new-in-visual-studio-docs"></a>Visual Studio 中的新增功能历史记录文档

欢迎了解 Visual Studio 文档中的新增功能历史记录。本主题包含 2020 年 9 月之前（从 2020 年 7 月开始）对文档所做的主要更改。 有关最新的新增功能，请参阅 [Visual Studio 文档：文档中的新增功能](whats-new-visual-studio-docs.md)。

## <a name="august-2020"></a>2020 年 8 月
### <a name="azure"></a>Azure

**新文章**

- [使用 Visual Studio 连接服务添加 Azure Application Insights](../azure/azure-app-insights-add-connected-service.md) - 用于 VS 2019 16.7 的连接服务
- [使用 Visual Studio 连接服务添加 Azure Cache for Redis](../azure/azure-cache-for-redis-add-connected-service.md) - 用于 VS 2019 16.7 的连接服务
- [使用 Visual Studio 连接服务将 Azure Cosmos DB 添加到你的应用](../azure/azure-cosmosdb-add-connected-service.md) - 用于 VS 2019 16.7 的连接服务
- [使用 Visual Studio 连接服务添加 Azure SignalR](../azure/azure-signalr-add-connected-service.md) - 用于 VS 2019 16.7 的连接服务
- [添加与 Azure SQL 数据库的连接](../azure/azure-sql-database-add-connected-service.md) - 用于 VS 2019 16.7 的连接服务

**更新的文章**

- [使用 Visual Studio 连接服务添加 Azure 存储](../azure/vs-azure-tools-connected-services-storage.md)
  - 用于 VS 2019 16.7 的连接服务
  - Azure 存储连接服务文章：支持更新 UI 和项目类型

### <a name="code-quality"></a>代码质量

**新文章**

- [CA1310：为了确保正确，请指定 StringComparison](/dotnet/fundamentals/code-analysis/quality-rules/ca1310) - 添加 CA1310 的文档并更新 CA1307 的文档
- [CA1837：使用 Environment.ProcessId 而不是 Process.GetCurrentProcess().Id](/dotnet/fundamentals/code-analysis/quality-rules/ca1837) - CA1837 的文档
- [CA1838：避免 P/Invokes 的 `StringBuilder` 参数](/dotnet/fundamentals/code-analysis/quality-rules/ca1838) - 添加 CA1838 的文档
- [CA2008：不要在未传递 TaskScheduler 的情况下创建任务](/dotnet/fundamentals/code-analysis/quality-rules/ca2008) - 添加 CA2008 的文档
- [CA2249：请考虑使用 String.Contains 而不是 String.IndexOf](/dotnet/fundamentals/code-analysis/quality-rules/ca2249) - CA2249 的文档
- [CA2361：请确保包含 DataSet.ReadXml() 的自动生成的类没有与不受信任的数据一起使用](/dotnet/fundamentals/code-analysis/quality-rules/ca2361) - 更多数据集/数据表规则
- [CA2362：自动生成的可序列化类型中不安全的数据集或数据表易受远程代码执行攻击](/dotnet/fundamentals/code-analysis/quality-rules/ca2362) - 更多数据集/数据表规则
- [IL3000：当发布为单个文件时，避免使用访问程序集文件路径](/dotnet/fundamentals/code-analysis/quality-rules/il3000) - 添加 IL3000 的文档
- [IL3001：当发布为单个文件时，避免使用访问程序集文件路径](/dotnet/fundamentals/code-analysis/quality-rules/il3001) - 添加 IL3001 的文档

**已更新**

- [CA1002：不要公开泛型列表](/dotnet/fundamentals/code-analysis/quality-rules/ca1002) - 添加可配置性 - API Surface 部分
- [CA1046：不要对引用类型重载同等运算符](/dotnet/fundamentals/code-analysis/quality-rules/ca1046) - 添加可配置性 - API Surface 部分
- [CA1307：为了清晰起见，请指定 StringComparison](/dotnet/fundamentals/code-analysis/quality-rules/ca1307) - 添加 CA1310 的文档并更新 CA1307 的文档
- [CA1700：不要命名“Reserved”枚举值](/dotnet/fundamentals/code-analysis/quality-rules/ca1700) - 添加可配置性 - API Surface 部分
- [CA1707：标识符不应包含下划线](/dotnet/fundamentals/code-analysis/quality-rules/ca1707) - 添加可配置性 - API Surface 部分
- [CA1822：将成员标记为 static](/dotnet/fundamentals/code-analysis/quality-rules/ca1822) - 添加可配置性 - API Surface 部分
- [CA2351：确保 DataSet.ReadXml() 的输入受信任](/dotnet/fundamentals/code-analysis/quality-rules/ca2351) - 更多数据集/数据表规则
- [安装第三方分析器](../code-quality/install-roslyn-analyzers.md) - 已更改代码分析文档的结构和标题

### <a name="containers"></a>容器

**更新的文章**

- [使用 Visual Studio 将 ASP.NET 容器部署到容器注册表](../containers/hosting-web-apps-in-docker.md) - Visual Studio 16.7 发布 UI 的容器工具更新
- [Visual Studio Kubernetes 工具入门](../containers/bridge-to-kubernetes.md) - Kubernetes 教程：添加要删除的步骤

### <a name="deployment"></a>部署

**新文章**

- [Visual Studio 安装程序项目扩展和 NET Core 3.1](../deployment/installer-projects-net-core.md) - 为安装程序项目 .NET Core 3.1 功能创建新帮助页

**更新的文章**

- [将应用部署到文件夹、IIS、Azure 或其他目标](../deployment/deploying-applications-services-and-components-resources.md) - 部署更新
- [Visual Studio 中的部署](../deployment/index.yml) - 部署更新

### <a name="extensibility"></a>扩展性

**更新的文章**
- [项目子类型](../extensibility/internals/project-subtypes.md) - 修复列表项缩进
- [Visual Studio 的颜色值参考](../extensibility/ux-guidelines/color-value-reference-for-visual-studio.md) - AB#1759333 修复缺少的列标题

### <a name="get-started"></a>入门

**更新的文章**

- [步骤 5：将 ASP.NET Core 应用部署到 Azure](../get-started/csharp/tutorial-aspnet-core-ef-step-05.md) - 新连接服务 UI 的视频教程更新

### <a name="ide"></a>IDE

**新文章**

- [在 Visual Studio 中更改 F1 帮助键](./not-in-toc/change-f1-help-key.md) - 重构默认 F1 帮助页
- [文本编辑器的 F1 帮助](./not-in-toc/default-f1-text-editor.md) - 重构默认 F1 帮助页
- [将 `typeof` 转换为 `nameof`](./reference/convert-typeof-to-nameof.md) - 将 typeof 转换为 nameof 重构
- [简化 LINQ 表达式](./reference/simplify-linq-expression.md) - 简化 LINQ 表达式重构

**更新的文章**

- [在 Visual Studio 中自定义窗口布局](./customizing-window-layouts-in-visual-studio.md) - 将已标记的竖排文档选项卡信息添加到“自定义窗口布局”主题
- [如何报告 Visual Studio 或 Visual Studio 安装程序的问题](./how-to-report-a-problem-with-visual-studio.md)
  - 向 NMI 添加详细信息
  - 重做整个“报告问题”页
- [F1 帮助](./not-in-toc/default.md) - 重构默认 F1 帮助页
- [“选项”对话框 ->“环境”->“自动恢复”](./reference/autorecover-environment-options-dialog-box.md) - 添加有关更新的自动保存文件位置的信息
- [“选项”>“文本编辑器”>“基本(Visual Basic)”>“高级”](./reference/options-text-editor-basic-visual-basic.md) - 添加内联参数名称提示的基本文档
- [“选项”->“文本编辑器”->“C#”->“高级”](./reference/options-text-editor-csharp-advanced.md) - 添加内联参数名称提示的基本文档
- [Visual Studio 性能提示和技巧](./visual-studio-performance-tips-and-tricks.md) - 添加“禁用地图模式”和“禁用自动换行”信息
- [Visual Studio 2019 中的新增功能](./whats-new-visual-studio-2019.md) - 使用 16.7 GA 信息更新 Visual Studio 2019 中的新增功能

### <a name="rtvs"></a>RTVS

**更新的文章**

- [使用 SQL Server 和 R](../rtvs/integrating-sql-server-with-r.md) - 包括列标题的更正的表

## <a name="july-2020"></a>2020 年 7 月
### <a name="code-quality"></a>代码质量

**新文章**

- [CA1417：避免在 P/Invokes 的字符串参数上使用 `OutAttribute`](/dotnet/fundamentals/code-analysis/quality-rules/ca1417) - 添加 CA1417 的文档
- [CA1805：避免进行不必要的初始化。](/dotnet/fundamentals/code-analysis/quality-rules/ca1805) - 添加 CA1805 的文档
- [CA1836：可用时最好使用 IsEmpty（而不是 Count）](/dotnet/fundamentals/code-analysis/quality-rules/ca1836) - 添加 CA1836 的文档（最好使用“IsEmpty”(而不是“Count”)）
- [CA2016：将 CancellationToken 参数转发到采用一个该参数的方法](/dotnet/fundamentals/code-analysis/quality-rules/ca2016) - 文档 CA2016 - 将 CancellationToken 参数转发到采用一个该参数的方法
- [CA2350：确保 DataTable.ReadXml() 的输入受信任](/dotnet/fundamentals/code-analysis/quality-rules/ca2350) - 初始数据集/数据表反序列化规则文档
- [CA2351：确保 DataSet.ReadXml() 的输入受信任](/dotnet/fundamentals/code-analysis/quality-rules/ca2351) - 初始数据集/数据表反序列化规则文档
- [CA2352：可序列化类型中不安全的数据集或数据表易受远程代码执行攻击](/dotnet/fundamentals/code-analysis/quality-rules/ca2352) - 初始数据集/数据表反序列化规则文档
- [CA2353：可序列化类型中不安全的数据集或数据表](/dotnet/fundamentals/code-analysis/quality-rules/ca2353) - 初始数据集/数据表反序列化规则文档
- [CA2354：反序列化对象图中的不安全数据集或数据表可能容易受到远程代码执行攻击](/dotnet/fundamentals/code-analysis/quality-rules/ca2354) - 初始数据集/数据表反序列化规则文档
- [CA2355：反序列化对象图中的不安全数据集或数据表](/dotnet/fundamentals/code-analysis/quality-rules/ca2355) - 初始数据集/数据表反序列化规则文档
- [CA2356：Web 反序列化对象图中的不安全数据集或数据表类型](/dotnet/fundamentals/code-analysis/quality-rules/ca2356) - 初始数据集/数据表反序列化规则文档

### <a name="containers"></a>容器

**新文章**

- [配置 Kubernetes 本地进程](../containers/configure-bridge-to-kubernetes.md) - Kubernetes 本地进程：YAML 配置
- [使用 Kubernetes 本地进程（预览版）](../containers/bridge-to-kubernetes.md) - Dev Spaces 迁移
- [Local Process with Kubernetes 的工作原理](../containers/overview-bridge-to-kubernetes.md)
  - Kubernetes 本地进程：添加路由部分
  - Dev Spaces 迁移

### <a name="cross-platform"></a>跨平台

**更新的文章**

- [更改日志（Visual Studio Tools for Unity、Windows）](../cross-platform/change-log-visual-studio-tools-for-unity.md)- 将 VSTU 更改日志升级到 4.7.1.0
- [更改日志（Visual Studio Tools for Unity、Mac）](../cross-platform/change-log-visual-studio-tools-for-unity-mac.md)- 将 VSTUM 更改日志升级到 2.7.1.0

### <a name="get-started"></a>入门

**新文章**

- [教程：扩展简单的 C# 控制台应用](../get-started/csharp/tutorial-console-part-2.md) - 版本扩展人行道教程第一版

### <a name="ide"></a>IDE

**新文章**

- [开发者社区指南](./developer-community-guidelines.md) - 添加了 DevCom 指南
- [针对未导入类型和扩展方法的 IntelliSense 完成](./reference/intellisense-completion-unimported-types-extension-methods.md)

### <a name="install"></a>安装

**新文章**

- [使用最小脱机布局更新 Visual Studio](../install/update-minimal-layout.md) - 文档最小布局功能
- [Visual Studio enterprise 指南](../install/visual-studio-enterprise-guide.md) - Enterprise 指南

### <a name="javascript"></a>JavaScript

**新文章**

- [编译 TypeScript 代码 (Node.js)](../javascript/compile-typescript-code-npm.md) - TypeScript 编译和生成
- [编译 TypeScript 代码 (ASP.NET Core)](../javascript/compile-typescript-code-nuget.md) - TypeScript 编译和生成

### <a name="msbuild"></a>MSBuild

**新文章**

- [通用 MSBuild 项元数据](../msbuild/common-msbuild-item-metadata.md) - MSBuild：添加包含 Link 和 LinkBase 的可选元数据的表
- [MSBuild 中的解决方案筛选器](../msbuild/solution-filters.md) - MSBuild 解决方案筛选器

### <a name="test"></a>测试

**新文章**

- [使用测试资源管理器调试和分析单元测试](../test/debug-unit-tests-with-test-explorer.md) - 测试资源管理器性能

**更新的文章**

- [使用 .runsettings 文件配置单元测试](../test/configure-unit-tests-by-using-a-dot-runsettings-file.md)
  - 进行了更新以使用 runsettings 文件配置单元测试
  - 已更改责任选项说明，并添加了示例。