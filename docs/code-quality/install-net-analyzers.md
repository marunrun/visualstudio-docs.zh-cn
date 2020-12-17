---
title: 启用或安装第一方 .NET 分析器
ms.date: 08/03/2018
description: 了解如何从 .NET SDK 启用第一方 .NET 分析器，或将这些分析器安装为 NuGet 包。
ms.custom: SEO-VS-2020
ms.topic: how-to
helpviewer_keywords:
- .NET analyzers
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: ea13fde64f6214cf3c219de45c79458b75e1caf8
ms.sourcegitcommit: d485b18e46ec4cf08704b5a8d0657bc716ec8393
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/17/2020
ms.locfileid: "97615520"
---
# <a name="enable-or-install-first-party-net-analyzers"></a>启用或安装第一方 .NET 分析器

## <a name="overview"></a>概述

.NET Compiler Platform (Roslyn) 分析器会检查 C# 或 Visual Basic 代码的代码质量和代码样式问题。 第一方 .NET 分析器与 **目标平台无关**。 也就是说，你的项目不需要面向特定的 .NET 平台。 分析器适用于目标为的项目以及 `net5.0` 更早的 .net 版本，如 `netcoreapp` 、 `netstandard` 和 `net472` 。

可以通过以下方式之一启用或安装第一方 .NET 分析器：

- **从 .NET Sdk 启用：从** Visual Studio 2019 16.8 和 .Net 5.0 开始， [.net sdk 随附](/dotnet/fundamentals/code-analysis/overview)了这些分析器。 默认情况下，对于面向 .NET 5.0 或更高版本的项目，分析处于启用状态。 通过将属性设置为，可以对面向早期 .NET 版本的项目启用代码分析 `EnableNETAnalyzers` `true` 。 你还可以通过将设置为来对你的项目禁用代码分析 `EnableNETAnalyzers` `false` 。

- **以 NuGet 包的形式安装**：如果不想移到 .net 5 + SDK，或者想要使用基于 NuGet 包的模型，则可以在 `Microsoft.CodeAnalysis.NetAnalyzers` Visual Studio 2019 上的 [NuGet 包](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers) 中使用该分析器。  对于按需版本更新，你可能更倾向于使用基于包的模型。 如果你在 Visual Studio 2017 上，请改为安装最新 `2.9.x` 版本的 `Microsoft.CodeAnalysis.FxCopAnalyzers` [NuGet 包](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/) 。

> [!NOTE]
> 建议从 .NET SDK 启用分析器，而不是安装 `Microsoft.CodeAnalysis.NetAnalyzers` [NuGet 包](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers)（如果可能）。 通过从 .NET SDK 启用分析器，可以确保在更新 SDK 后，立即自动获取分析器 bug 修复和新分析器。 在 NuGet 模型中，每次需要最新的 bug 修复时，都需要更新 NuGet 包。 NuGet 包会更频繁地更新。

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的代码分析器概述](roslyn-analyzers-overview.md)
- [在 Visual Studio 中使用代码分析器](use-roslyn-analyzers.md)
- [从旧版分析迁移到 .NET 分析器](migrate-from-legacy-analysis-to-net-analyzers.md)
- [从 FxCop 分析器迁移到 .NET 分析器](migrate-from-fxcop-analyzers-to-net-analyzers.md)
