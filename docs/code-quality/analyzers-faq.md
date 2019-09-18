---
title: EditorConfig 与分析器
ms.date: 03/11/2019
ms.topic: conceptual
helpviewer_keywords:
- analyzers, faq
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 26e48664c40db018df60f2b6d600fab0767a7b72
ms.sourcegitcommit: 2db01751deeee7b2bdb1db25419ea6706e6fcdf8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2019
ms.locfileid: "71062169"
---
# <a name="code-analysis-faq"></a>代码分析常见问题解答

本页包含有关 Visual Studio 中基于 .NET Compiler Platform 代码分析的一些常见问题的解答。

## <a name="code-analysis-versus-editorconfig"></a>代码分析与 EditorConfig

**问**:是否应该使用代码分析或 EditorConfig 来检查代码样式？

**答**：代码分析和 EditorConfig 文件工作。 在[EditorConfig 文件](../ide/editorconfig-code-style-settings-reference.md)或 "[文本编辑器" 选项](../ide/code-styles-and-code-cleanup.md)页上定义代码样式时，实际上是在配置 Visual Studio 中内置的代码分析器。 EditorConfig 文件还可用于配置一些 NuGet 分析器包，例如[FxCop 分析器](configure-fxcop-analyzers.md)。

## <a name="editorconfig-versus-rule-sets"></a>EditorConfig 与规则集

**问**:我应该使用规则集还是 EditorConfig 文件配置分析器？

**答**：规则集和 EditorConfig 文件可以共存，并可同时用于配置分析器。 [规则集](analyzer-rule-sets.md)使你可以启用和禁用规则并设置其严重性。 EditorConfig 文件提供了其他配置规则的方法。 对于 FxCop 分析器，EditorConfig 文件允许[定义要分析的代码类型](fxcop-analyzer-options.md)。 对于内置于 Visual Studio 中的代码样式分析器，EditorConfig 文件允许你为基本代码[定义首选代码样式](../ide/editorconfig-code-style-settings-reference.md)。

除了规则集和 EditorConfig 文件外，某些分析器还通过使用标记为C#和 VB 编译器的[附加文件](../ide/build-actions.md#build-action-values)的文本文件进行配置。

> [!NOTE]
> 不能使用 EditorConfig 文件来配置旧分析，而规则集也可以。

## <a name="code-analysis-in-ci-builds"></a>CI 生成中的代码分析

**问**:在持续集成（CI）版本中，基于 .NET Compiler Platform 的代码分析是否起作用？

**答**：可以。 对于从 NuGet 包安装的分析器，将[在生成时强制执行](roslyn-analyzers-overview.md#build-errors)这些规则，包括在 CI 生成过程中。 CI 生成中使用的分析器遵循[规则集](analyzer-rule-sets.md)和[editorconfig 文件](configure-fxcop-analyzers.md)中的规则配置。 目前，Visual Studio 中内置的代码分析器不作为 NuGet 包提供，因此在 CI 生成中无法强制执行这些规则。

## <a name="ide-analyzers-versus-stylecop"></a>IDE 分析器与 StyleCop

**问**:Visual Studio IDE 代码分析器和 StyleCop 分析器之间的区别是什么？

**答**：Visual Studio IDE 包含内置分析器，用于查找代码样式和质量问题。 这些规则可帮助你在引入新语言功能时使用它们，并改进代码的可维护性。 IDE 分析器随每个 Visual Studio 版本不断地进行更新。

[StyleCop 分析器](https://github.com/DotNetAnalyzers/StyleCopAnalyzers)是作为 NuGet 包安装的第三方分析器，用于检查代码中的样式一致性。 通常，StyleCop 规则允许你为基本代码设置个人首选项，而无需对另一种样式进行建议。

## <a name="code-analyzers-versus-legacy-analysis"></a>代码分析器与传统分析

**问**:传统分析和基于 .NET Compiler Platform 的代码分析之间有何区别？

**答**：基于 .NET Compiler Platform 的代码分析实时分析源代码，并在编译期间分析二进制文件。 有关详细信息，请参阅[基于 .NET Compiler Platform 的分析与传统分析](roslyn-analyzers-overview.md#net-compiler-platform-based-analysis-versus-legacy-analysis)和[FxCop 分析器常见问题解答](fxcop-analyzers-faq.md)。

## <a name="see-also"></a>请参阅

- [分析器概述](roslyn-analyzers-overview.md)
- [EditorConfig 的 .NET 编码约定设置](../ide/editorconfig-code-style-settings-reference.md)
