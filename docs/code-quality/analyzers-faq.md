---
title: 编辑器配置与分析器
ms.date: 03/11/2019
ms.topic: conceptual
helpviewer_keywords:
- analyzers, faq
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 680d52ff04553d399b6abeb53919d8aafd4fa792
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79300923"
---
# <a name="code-analysis-faq"></a>代码分析常见问题解答

此页包含有关 Visual Studio 中有关 .NET 编译器平台代码分析的一些常见问题的解答。

## <a name="code-analysis-versus-editorconfig"></a>代码分析与编辑器配置

**问**：我应该使用代码分析或编辑器配置来检查代码样式吗？

**A**： 代码分析和编辑器分析文件是手牵手工作的。 当您[在 EditorConfig 文件](../ide/editorconfig-code-style-settings-reference.md)或[文本编辑器选项](../ide/code-styles-and-code-cleanup.md)页上定义代码样式时，实际上是在配置可视化工作室中内置的代码分析器。 编辑器配置文件可用于启用或禁用分析器规则，以及配置一些 NuGet 分析器包，如[FxCop 分析器](configure-fxcop-analyzers.md)。

## <a name="editorconfig-versus-rule-sets"></a>编辑器配置与规则集

**问**：我是否应该使用规则集或编辑器配置文件配置分析器？

**A**： 规则集和编辑器配置文件可以共存，并且都可用于配置分析器。 编辑器配置文件和规则集都允许您启用和禁用规则并设置其严重性。

但是，EditorConfig 文件提供了配置规则的其他方法：

- 对于 FxCop 分析器，EditorConfig 文件允许您[定义要分析的代码类型](fxcop-analyzer-options.md)。
- 对于内置于 Visual Studio 中的代码样式分析器，Editor Config 文件允许您为代码库[定义首选的代码样式](../ide/editorconfig-code-style-settings-reference.md)。

除了规则集和 EditorConfig 文件之外，某些分析器还通过使用标记为 C# 和 VB 编译器[的其他文件](../ide/build-actions.md#build-action-values)的文本文件进行配置。

> [!NOTE]
> - EditorConfig 文件只能在 Visual Studio 2019 版本 16.3 及更高版本中启用规则并设置其严重性。
> - 编辑器配置文件不能用于配置旧版分析，而规则集可以。

## <a name="code-analysis-in-ci-builds"></a>CI 生成中的代码分析

**问**：基于 .NET 编译器平台的代码分析在持续集成 （CI） 生成中是否正常工作？

**答**：是的。 对于从 NuGet 包安装的分析器，这些规则在[生成时（](roslyn-analyzers-overview.md#build-errors)包括在 CI 生成期间）强制执行。 CI 中使用的分析器从规则集和编辑器配置文件生成尊重规则配置。 目前，Visual Studio 中内置的代码分析器不能作为 NuGet 包提供，因此这些规则在 CI 生成中不可执行。

## <a name="ide-analyzers-versus-stylecop"></a>IDE 分析仪与 StyleCop

**问**：Visual Studio IDE 代码分析器和 StyleCop 分析器之间的区别是什么？

**答**： Visual Studio IDE 包括内置分析器，可同时查找代码样式和质量问题。 这些规则可帮助您在引入新语言功能时使用这些功能，并提高代码的可维护性。 IDE 分析器会随每个可视化工作室版本不断更新。

[StyleCop 分析器](https://github.com/DotNetAnalyzers/StyleCopAnalyzers)是作为 NuGet 包安装的第三方分析器，用于检查代码中的样式一致性。 通常，StyleCop 规则允许您为代码库设置个人首选项，而无需将一种样式推荐到另一种样式。

## <a name="code-analyzers-versus-legacy-analysis"></a>代码分析器与旧分析

**问**：旧版分析和基于 .NET 编译器平台的代码分析有何区别？

**A**： .NET 编译器平台代码分析实时和编译期间分析源代码，而旧分析在生成完成后分析二进制文件。 有关详细信息，请参阅[.NET 编译器平台分析与旧分析和](roslyn-analyzers-overview.md#source-code-analysis-versus-legacy-analysis) [FxCop 分析器常见问题解答](fxcop-analyzers-faq.md)。

## <a name="treat-warnings-as-errors"></a>视警告为错误

**问**：我的项目使用生成选项将警告视为错误。 从旧分析迁移到源代码分析后，所有代码分析警告现在都显示为错误。 我怎样才能防止这种情况？

**为**防止代码分析警告被视为错误，请按照以下步骤操作：

  1. 创建包含以下内容的 .props 文件：

     ```xml
     <Project>
        <PropertyGroup>
           <CodeAnalysisTreatWarningsAsErrors>false</CodeAnalysisTreatWarningsAsErrors>
        </PropertyGroup>
     </Project>
     ```

  2. 向 .csproj 或 .vbproj 项目文件添加行以导入您在上一步中创建的 .props 文件。 此行必须放置在导入 FxCop 分析器 .props 文件的任何行之前。 例如，如果您的 .props 文件名为代码分析.props：

     ```xml
     ...
     <Import Project="..\..\codeanalysis.props" Condition="Exists('..\..\codeanalysis.props')" />
     <Import Project="..\packages\Microsoft.CodeAnalysis.FxCopAnalyzers.2.6.5\build\Microsoft.CodeAnalysis.FxCopAnalyzers.props" Condition="Exists('..\packages\Microsoft.CodeAnalysis.FxCopAnalyzers.2.6.5\build\Microsoft.CodeAnalysis.FxCopAnalyzers.props')" />
     ...
     ```

## <a name="see-also"></a>另请参阅

- [分析仪概述](roslyn-analyzers-overview.md)
- [EditorConfig 的 .NET 编码约定设置](../ide/editorconfig-code-style-settings-reference.md)
