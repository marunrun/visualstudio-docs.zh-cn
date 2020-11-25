---
title: 从 FxCop 分析器迁移到 .NET 分析器
ms.custom: SEO-VS-2020
description: 了解如何从 FxCop 分析器迁移到 .NET 分析器
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
ms.openlocfilehash: b62f99b296c0f9624079423d850029f804e5ebe4
ms.sourcegitcommit: 967c2f8c1b3f805cf42c0246389517689d971b53
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/25/2020
ms.locfileid: "96112161"
---
# <a name="migrate-from-fxcop-analyzers-to-net-analyzers"></a>从 FxCop 分析器迁移到 .NET 分析器

.NET Compiler Platform ( "Roslyn" 的源分析 ) 分析器替换托管代码的 [旧式分析](code-analysis-for-managed-code-overview.md) 。 许多旧分析 (FxCop) 规则已经重新编写为源分析器。

在 Visual Studio 2019 16.8 和 .NET 5.0 之前，这些分析器作为 `Microsoft.CodeAnalysis.FxCopAnalyzers` [NuGet 包](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers)提供。

从 Visual Studio 2019 16.8 和 .NET 5.0 开始， [.NET SDK 中提供](/dotnet/fundamentals/code-analysis/overview)了这些分析器。 它们也作为 `Microsoft.CodeAnalysis.NetAnalyzers` [NuGet 包](https://www.nuget.org/packages/Microsoft.CodeAnalysis.NetAnalyzers)提供。 `Microsoft.CodeAnalysis.FxCopAnalyzers` NuGet 包即将弃用。

## <a name="migration-steps"></a>迁移步骤

请按照以下步骤将你的项目或解决方案从迁移 `Microsoft.CodeAnalysis.FxCopAnalyzers` 到 .net 分析器：

1. 卸载 `Microsoft.CodeAnalysis.FxCopAnalyzers` NuGet 包

2. [启用或安装 .NET 分析器](install-net-analyzers.md)

3. 启用其他规则： `Microsoft.CodeAnalysis.NetAnalyzers` 与相比，更保守 `Microsoft.CodeAnalysis.FxCopAnalyzers` 。 与 FxCopAnalyzers 包不同，它仅有几个在 [默认情况下启用为生成警告](/dotnet/fundamentals/code-analysis/overview#enabled-rules)的正确性规则。 可以通过自定义[AnalysisMode](/dotnet/core/project-sdk/msbuild-props#analysismode) MSBuild 属性来[启用其他规则](/dotnet/fundamentals/code-analysis/overview#enable-additional-rules)。 例如，如果将属性设置为，则 `AllEnabledByDefault` 默认情况下会启用所有适用的 CA 规则作为生成警告。

   ```xml
   <PropertyGroup>
     <AnalysisMode>AllEnabledByDefault</AnalysisMode>
   </PropertyGroup>
   ```

## <a name="see-also"></a>请参阅

- [源代码分析与传统分析](net-analyzers-faq.md#whats-the-difference-between-legacy-fxcop-and-net-analyzers)
- [从旧分析迁移到 .NET 分析器](migrate-from-legacy-analysis-to-net-analyzers.md)
- [启用或安装 .NET 分析器](install-net-analyzers.md)
- [.NET 分析器常见问题](net-analyzers-faq.md)
- [配置 .NET 分析器](/dotnet/fundamentals/code-analysis/code-quality-rule-options)
