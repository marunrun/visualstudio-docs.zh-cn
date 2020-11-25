---
title: " ( .NET 分析器上从 FxCop 迁移到源分析) "
ms.custom: SEO-VS-2020
description: 了解如何首次分析代码或者如何从二进制分析迁移 (FxCop) 到使用源分析 ( .NET 分析器) 分析托管代码的新方式。
ms.date: 03/06/2020
ms.topic: conceptual
f1_keywords:
- vs.projectpropertypages.codeanalysis
helpviewer_keywords:
- FxCop, migration
- legacy analysis, migration
- source code analysis, migration
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 84acec58ed78884f0b037950fa25ce40f6adcbfc
ms.sourcegitcommit: 967c2f8c1b3f805cf42c0246389517689d971b53
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/25/2020
ms.locfileid: "96112156"
---
# <a name="migrate-from-legacy-analysis-fxcop-to-source-analysis-net-analyzers"></a>从旧分析 (FxCop) 迁移到 ( .NET 分析器的源分析) 

.NET Compiler Platform ( "Roslyn" 的源分析 ) 分析器替换托管代码的 [旧式分析](../code-quality/code-analysis-for-managed-code-overview.md) 。 对于更高版本的项目模板（如 .NET Core 和 .NET Standard 项目），旧版分析不可用。

许多旧分析 (FxCop) 规则已重写为 .NET 分析器（一组 Roslyn 代码分析器）。 Roslyn 分析器在编译器执行过程中运行基于源代码的分析。 报告分析器结果以及编译器结果。

有关旧分析与源分析之间的差异的详细信息，请参阅以下内容：

- [源代码分析与传统分析](../code-quality/net-analyzers-faq.md#whats-the-difference-between-legacy-fxcop-and-net-analyzers)

- [.NET 分析器常见问题](../code-quality/net-analyzers-faq.md)

## <a name="migration"></a>迁移

若要迁移到源分析，请 [启用或安装 .net 分析器](install-net-analyzers.md)。 与传统的分析规则冲突一样，源代码分析冲突会出现在 Visual Studio 的“错误列表”窗口中。 此外，源代码分析冲突也会在代码编辑器中显示，表现为违规代码下有波浪线。 规则的[严重性设置](../code-quality/use-roslyn-analyzers.md#configure-severity-levels)决定波浪线的颜色。 若要查看移植到新 .NET 分析器的规则的状态，请参阅 [移植和 unported 规则](../code-quality/fxcop-rule-port-status.md)。

> [!NOTE]
> 在 Visual Studio 2019 16.8 和 .NET 5.0 之前，这些分析器作为 `Microsoft.CodeAnalysis.FxCopAnalyzers` [NuGet 包](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers)提供。 从 Visual Studio 2019 16.8 和 .NET 5.0 开始， [.NET SDK 中提供](/dotnet/fundamentals/code-analysis/overview)了这些分析器。 它们也作为 `Microsoft.CodeAnalysis.NetAnalyzers` [NuGet 包](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers)提供。 有关详细信息，请参阅 [从 FxCop 分析器迁移到 .net 分析器](migrate-from-fxcop-analyzers-to-net-analyzers.md)。

## <a name="configuration"></a>配置

若要详细了解如何配置 .NET 分析器：

- 若要配置 .NET 分析器，请参阅 [配置 .net 分析器](/dotnet/fundamentals/code-analysis/code-quality-rule-options)。

- 若要了解如何使用预定义的规则和 EditorConfig 或规则集文件来配置分析器，请参阅 [启用规则类别](/dotnet/fundamentals/code-analysis/code-quality-rule-options)。

## <a name="see-also"></a>请参阅

- [从 FxCop 分析器迁移到 .NET 分析器](migrate-from-fxcop-analyzers-to-net-analyzers.md)
