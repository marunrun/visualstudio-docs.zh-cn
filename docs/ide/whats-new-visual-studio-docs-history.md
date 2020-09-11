---
title: 'Visual Studio 文档：新增功能历史记录 '
titleSuffix: ''
description: Visual Studio 中的新增功能历史记录文档
ms.date: 09/01/2020
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
ms.openlocfilehash: 9f5fc25f6bb25c9471b1de1d464fa6afc4c80b3b
ms.sourcegitcommit: 703c68667261df5985a73282c1cbb0541118989c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89410738"
---
# <a name="history-of-whats-new-in-visual-studio-docs"></a>Visual Studio 中的新增功能历史记录文档

欢迎了解 Visual Studio 文档中的新增功能历史记录。本主题包含 2020 年 8 月之前（从 2020 年 7 月开始）对文档所做的主要更改。 有关最新的新增功能，请参阅 [Visual Studio 文档：文档中的新增功能](whats-new-visual-studio-docs.md)。

## <a name="july-2020"></a>2020 年 7 月
### <a name="code-quality"></a>代码质量

**新文章**

- [CA1417：避免在 P/Invokes 的字符串参数上使用 `OutAttribute`](/visualstudio/code-quality/ca1417) - 添加 CA1417 的文档
- [CA1805：避免进行不必要的初始化。](/visualstudio/code-quality/ca1805) - 添加 CA1805 的文档
- [CA1836：可用时最好使用 IsEmpty（而不是 Count）](/visualstudio/code-quality/ca1836) - 添加 CA1836 的文档（最好使用“IsEmpty”(而不是“Count”)）
- [CA2016：将 CancellationToken 参数转发到采用一个该参数的方法](/visualstudio/code-quality/ca2016) - 文档 CA2016 - 将 CancellationToken 参数转发到采用一个该参数的方法
- [CA2350：确保 DataTable.ReadXml() 的输入受信任](/visualstudio/code-quality/ca2350) - 初始数据集/数据表反序列化规则文档
- [CA2351：确保 DataSet.ReadXml() 的输入受信任](/visualstudio/code-quality/ca2351) - 初始数据集/数据表反序列化规则文档
- [CA2352：可序列化类型中不安全的数据集或数据表易受远程代码执行攻击](/visualstudio/code-quality/ca2352) - 初始数据集/数据表反序列化规则文档
- [CA2353：可序列化类型中不安全的数据集或数据表](/visualstudio/code-quality/ca2353) - 初始数据集/数据表反序列化规则文档
- [CA2354：反序列化对象图中的不安全数据集或数据表可能容易受到远程代码执行攻击](/visualstudio/code-quality/ca2354) - 初始数据集/数据表反序列化规则文档
- [CA2355：反序列化对象图中的不安全数据集或数据表](/visualstudio/code-quality/ca2355) - 初始数据集/数据表反序列化规则文档
- [CA2356：Web 反序列化对象图中的不安全数据集或数据表类型](/visualstudio/code-quality/ca2356) - 初始数据集/数据表反序列化规则文档

### <a name="containers"></a>容器

**新文章**

- [配置 Kubernetes 本地进程](/visualstudio/containers/configure-local-process-with-kubernetes) - Kubernetes 本地进程：YAML 配置
- [使用 Kubernetes 本地进程（预览版）](/visualstudio/containers/local-process-kubernetes) - Dev Spaces 迁移
- [Local Process with Kubernetes 的工作原理](/visualstudio/containers/overview-local-process-kubernetes)
  - Kubernetes 本地进程：添加路由部分
  - Dev Spaces 迁移

### <a name="cross-platform"></a>跨平台

**更新的文章**

- [更改日志（Visual Studio Tools for Unity、Windows）](/visualstudio/cross-platform/change-log-visual-studio-tools-for-unity)- 将 VSTU 更改日志升级到 4.7.1.0
- [更改日志（Visual Studio Tools for Unity、Mac）](/visualstudio/cross-platform/change-log-visual-studio-tools-for-unity-mac)- 将 VSTUM 更改日志升级到 2.7.1.0

### <a name="get-started"></a>入门

**新文章**

- [教程：扩展简单的 C# 控制台应用](/visualstudio/get-started/csharp/tutorial-console-part-2) - 版本扩展人行道教程第一版

### <a name="ide"></a>IDE

**新文章**

- [开发者社区指南](/visualstudio/ide/developer-community-guidelines) - 添加了 DevCom 指南
- [针对未导入类型和扩展方法的 IntelliSense 完成](/visualstudio/ide/reference/intellisense-completion-unimported-types-extension-methods)

### <a name="install"></a>安装

**新文章**

- [使用最小脱机布局更新 Visual Studio](/visualstudio/install/update-minimal-layout) - 文档最小布局功能
- [Visual Studio enterprise 指南](/visualstudio/install/visual-studio-enterprise-guide) - Enterprise 指南

### <a name="javascript"></a>JavaScript

**新文章**

- [编译 TypeScript 代码 (Node.js)](/visualstudio/javascript/compile-typescript-code-npm) - TypeScript 编译和生成
- [编译 TypeScript 代码 (ASP.NET Core)](/visualstudio/javascript/compile-typescript-code-nuget) - TypeScript 编译和生成

### <a name="msbuild"></a>MSBuild

**新文章**

- [通用 MSBuild 项元数据](/visualstudio/msbuild/common-msbuild-item-metadata) - MSBuild：添加包含 Link 和 LinkBase 的可选元数据的表
- [MSBuild 中的解决方案筛选器](/visualstudio/msbuild/solution-filters) - MSBuild 解决方案筛选器

### <a name="test"></a>测试

**新文章**

- [使用测试资源管理器调试和分析单元测试](/visualstudio/test/debug-unit-tests-with-test-explorer) - 测试资源管理器性能

**更新的文章**

- [使用 .runsettings 文件配置单元测试](/visualstudio/test/configure-unit-tests-by-using-a-dot-runsettings-file)
  - 进行了更新以使用 runsettings 文件配置单元测试
  - 已更改责任选项说明，并添加了示例。