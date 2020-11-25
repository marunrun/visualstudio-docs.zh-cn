---
title: 启用或安装 .NET 分析器
ms.date: 08/03/2018
description: 了解如何从 .NET SDK 启用 .NET 分析器，或将这些分析器安装为 NuGet 包。
ms.custom: SEO-VS-2020
ms.topic: how-to
helpviewer_keywords:
- .NET analyzers
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: a14d89caba498a07c2447f9df1109e4da9f6a466
ms.sourcegitcommit: 967c2f8c1b3f805cf42c0246389517689d971b53
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/25/2020
ms.locfileid: "96112157"
---
# <a name="enable-or-install-net-analyzers"></a>启用或安装 .NET 分析器

## <a name="overview"></a>概述

.NET Compiler Platform (Roslyn) 分析器会检查 C# 或 Visual Basic 代码的代码质量和代码样式问题。 可以通过以下方式之一来启用或安装这些分析器：

- **从 .NET Sdk 启用：从** Visual Studio 2019 16.8 和 .Net 5.0 开始， [.net sdk 随附](/dotnet/fundamentals/code-analysis/overview)了这些分析器。 默认情况下，对于面向 .NET 5.0 或更高版本的项目，分析处于启用状态。 通过将属性设置为，可以对面向早期 .NET 版本的项目启用代码分析 `EnableNETAnalyzers` `true` 。 你还可以通过将设置为来对你的项目禁用代码分析 `EnableNETAnalyzers` `false` 。

- **安装为 NuGet 包**：或者，你可以通过 `Microsoft.CodeAnalysis.NetAnalyzers` 在 Visual Studio 2019 上安装 [NuGet 包](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers) 来安装这些分析器。 如果你在 Visual Studio 2017 上，请安装最新 `2.9.x` 版本的 `Microsoft.CodeAnalysis.FxCopAnalyzers` [NuGet 包](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/)。

> [!NOTE]
> 建议从 .NET SDK 启用分析器，而不是安装 `Microsoft.CodeAnalysis.NetAnalyzers` [NuGet 包](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers)（如果可能）。 通过从 .NET SDK 启用分析器，可以确保在更新 SDK 后，立即自动获取分析器 bug 修复和新分析器。

## <a name="see-also"></a>请参阅

- [Visual Studio 中的代码分析器概述](roslyn-analyzers-overview.md)
- [在 Visual Studio 中使用代码分析器](use-roslyn-analyzers.md)
- [从旧分析迁移到 .NET 分析器](migrate-from-legacy-analysis-to-net-analyzers.md)
- [从 FxCop 分析器迁移到 .NET 分析器](migrate-from-fxcop-analyzers-to-net-analyzers.md)
