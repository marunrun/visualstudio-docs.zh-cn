---
title: EditorConfig 与分析器
ms.date: 03/11/2019
ms.topic: conceptual
helpviewer_keywords:
- analyzers, faq
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7b060ae550fd0188728c827cac01c12d51930b57
ms.sourcegitcommit: de98ed7edc81383e47b87ae6e61143fbbbe7bc56
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2020
ms.locfileid: "88711542"
---
# <a name="code-analysis-faq"></a>代码分析常见问题解答

本页包含有关 Visual Studio 中基于 .NET Compiler Platform 代码分析的一些常见问题的解答。

## <a name="code-analysis-versus-editorconfig"></a>代码分析与 EditorConfig

**问**：我是否应该使用代码分析或 EditorConfig 来检查代码样式？

**答**：代码分析和 EditorConfig 文件的工作方式非常好。 在 [EditorConfig 文件](../ide/editorconfig-code-style-settings-reference.md) 或 " [文本编辑器" 选项](../ide/code-styles-and-code-cleanup.md) 页上定义代码样式时，实际上是在配置 Visual Studio 中内置的代码分析器。 EditorConfig 文件可用于启用或禁用分析器规则，还可用于配置 NuGet 分析器包。

## <a name="editorconfig-versus-rule-sets"></a>EditorConfig 与规则集

**问**：我应该使用规则集还是 EditorConfig 文件配置分析器？

**答**：规则集和 EditorConfig 文件可以共存，并且可同时用于配置分析器。 EditorConfig 文件和规则集都允许您启用和禁用规则并设置其严重性。

但是，EditorConfig 文件还提供了其他配置规则的方法：

- 对于 .NET 代码质量分析器，EditorConfig 文件允许 [定义要分析的代码类型](fxcop-analyzer-options.md)。
- 对于内置于 Visual Studio 中的 .NET 代码样式分析器，EditorConfig 文件允许你为基本代码 [定义首选代码样式](../ide/editorconfig-code-style-settings-reference.md) 。

除了规则集和 EditorConfig 文件外，某些分析器还通过使用标记为 c # 和 VB 编译器的 [附加文件](../ide/build-actions.md#build-action-values) 的文本文件进行配置。

> [!NOTE]
> - EditorConfig 文件只能用于启用规则，并在 Visual Studio 2019 版本16.3 及更高版本中设置其严重性。
> - 不能使用 EditorConfig 文件来配置旧分析，而规则集也可以。

## <a name="code-analysis-in-ci-builds"></a>CI 生成中的代码分析

**问**：基于 .NET Compiler Platform 的代码分析是否在持续集成 (CI) 生成？

**答**：是的。 对于从 NuGet 包安装的分析器，将 [在生成时强制执行](roslyn-analyzers-overview.md#build-errors)这些规则，包括在 CI 生成过程中。 CI 生成中使用的分析器遵循规则集和 EditorConfig 文件中的规则配置。 目前，Visual Studio 中内置的代码分析器不作为 NuGet 包提供，因此在 CI 生成中无法强制执行这些规则。

## <a name="ide-analyzers-versus-stylecop"></a>IDE 分析器与 StyleCop

**问**： VISUAL Studio IDE 代码分析器和 StyleCop 分析器之间有何区别？

**答**： VISUAL Studio IDE 包含内置分析器，用于查找代码样式和质量问题。 这些规则可帮助你在引入新语言功能时使用它们，并改进代码的可维护性。 IDE 分析器随每个 Visual Studio 版本不断地进行更新。

[StyleCop 分析器](https://github.com/DotNetAnalyzers/StyleCopAnalyzers) 是作为 NuGet 包安装的第三方分析器，用于检查代码中的样式一致性。 通常，StyleCop 规则允许你为基本代码设置个人首选项，而无需对另一种样式进行建议。

## <a name="code-analyzers-versus-legacy-analysis"></a>代码分析器与传统分析

**问**：传统分析和基于 .NET Compiler Platform 的代码分析之间有何区别？

**答**：基于 .NET Compiler Platform 的代码分析实时分析源代码，并在编译期间分析二进制文件。 有关详细信息，请参阅 [基于 .NET Compiler Platform 的分析与传统分析](roslyn-analyzers-overview.md#source-code-analysis-versus-legacy-analysis) 和 [FxCop 分析器常见问题解答](fxcop-analyzers-faq.md)。

## <a name="treat-warnings-as-errors"></a>视警告为错误

**问**：我的项目使用 "生成" 选项将警告视为错误。 从旧分析迁移到源代码分析后，所有代码分析警告现在都将显示为错误。 如何防止出现这种情况？

**答**：若要防止代码分析警告被视为错误，请执行以下步骤：

  1. 创建具有以下内容的属性文件：

     ```xml
     <Project>
        <PropertyGroup>
           <CodeAnalysisTreatWarningsAsErrors>false</CodeAnalysisTreatWarningsAsErrors>
        </PropertyGroup>
     </Project>
     ```

  2. 向 .csproj 或 .vbproj 项目文件添加一行，以导入在上一步中创建的属性文件。 必须将此行置于导入 FxCop 属性文件的任何行之前。 例如，如果你的属性文件命名为 codeanalysis。属性：

     ```xml
     ...
     <Import Project="..\..\codeanalysis.props" Condition="Exists('..\..\codeanalysis.props')" />
     <Import Project="..\packages\Microsoft.CodeAnalysis.FxCopAnalyzers.2.6.5\build\Microsoft.CodeAnalysis.FxCopAnalyzers.props" Condition="Exists('..\packages\Microsoft.CodeAnalysis.FxCopAnalyzers.2.6.5\build\Microsoft.CodeAnalysis.FxCopAnalyzers.props')" />
     ...
     ```

## <a name="code-analysis-solution-property-page"></a>代码分析解决方案属性页

**问**：解决方案的 "代码分析" 属性页在哪里？

**答**：解决方案级别的 "代码分析" 属性页已删除，以支持更可靠的共享属性组。 对于在项目级别管理代码分析，"代码分析" 属性页仍可用。 对于托管项目 (，我们还建议从规则集迁移到 EditorConfig，以便进行规则配置。 ) 用于在解决方案或存储库中的多个/所有项目间共享规则集，我们建议使用共享属性/目标文件或属性/文件中的 CodeAnalysisRuleSet 属性定义属性组。 如果你没有任何项目导入的公共属性或目标，则应考虑 [将此类属性组添加到属性或顶级解决方案目录下的目录，该目录将自动导入到目录或其子目录中定义的所有项目文件中](https://docs.microsoft.com/visualstudio/msbuild/customize-your-build?directorybuildprops-and-directorybuildtargets)。

## <a name="see-also"></a>另请参阅

- [分析器概述](roslyn-analyzers-overview.md)
- [EditorConfig 的 .NET 编码约定设置](../ide/editorconfig-code-style-settings-reference.md)
