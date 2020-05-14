---
title: 使用 Roslyn 分析器进行代码分析
ms.date: 10/03/2019
ms.topic: overview
helpviewer_keywords:
- code analysis, managed code
- analyzers
- Roslyn analyzers
- code analyzers
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 78a47cb2a5aefd7d20e0b8087f5f3ad735716175
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2020
ms.locfileid: "79431275"
---
# <a name="overview-of-source-code-analyzers"></a>源代码分析器概述

.NET Compiler Platform（“Roslyn”）代码分析器检查 C# 或 Visual Basic 代码的样式、质量和可维护性、设计及其他问题。

- 某些分析器内置于 Visual Studio 中。 对于这些分析器，诊断 ID 或代码的格式为 IDExxxx，如 IDE0067。 大多数这些内置分析器会检查[代码样式](../ide/code-styles-and-code-cleanup.md)，并且你可以在[文本编辑器选项](../ide/code-styles-and-code-cleanup.md)页上或在 [EditorConfig 文件](../ide/editorconfig-code-style-settings-reference.md)中配置首选项。 一小部分内置分析器会检查代码质量。

- 可以将其他分析器作为 NuGet 包或 Visual Studio 扩展进行安装。 例如：

  - [FxCop 分析器](../code-quality/install-fxcop-analyzers.md)，Microsoft 的推荐代码质量分析器
  - 第三方分析器，例如 [StyleCop](https://www.nuget.org/packages/StyleCop.Analyzers/)、[Roslynator](https://www.nuget.org/packages/Roslynator.Analyzers/)、[XUnit Analyzers](https://www.nuget.org/packages/xunit.analyzers/) 和 [Sonar Analyzer](https://www.nuget.org/packages/SonarAnalyzer.CSharp/)

如果分析器发现规则冲突，将在代码编辑器（违规代码下方有波浪线）和“错误列表”窗口中报告  。

许多分析器规则或诊断都有一个或多个相关的代码修复程序，可以应用它们来纠正问题   。 Visual Studio 中内置的每个分析器诊断都有关联的代码修复。 代码修复以及其他类型的[快速操作](../ide/quick-actions.md)显示在灯泡图标菜单中。 有关这些代码修复的信息，请参阅[常见快速操作](../ide/common-quick-actions.md)。

![分析器冲突和快速操作代码修复](../code-quality/media/built-in-analyzer-code-fix.png)

## <a name="source-code-analysis-versus-legacy-analysis"></a>源代码分析与传统分析

Roslyn 分析器进行的源分析会替换针对托管代码的[传统分析](../code-quality/code-analysis-for-managed-code-overview.md)。 许多传统代码分析规则都已被重新编写为 Roslyn 代码分析器。 对于更新的项目模板（如 .NET Core 和 .NET Standard 项目），传统分析甚至不可用。

与传统的分析规则冲突一样，源代码分析冲突会出现在 Visual Studio 的“错误列表”窗口中。 此外，源代码分析冲突也会在代码编辑器中显示，表现为违规代码下有波浪线  。 规则的[严重性设置](../code-quality/use-roslyn-analyzers.md#rule-severity)决定波浪线的颜色。 以下图像显示了三个冲突&mdash;一个为红色，一个为绿色，一个为灰色：

![Visual Studio 中代码编辑器中的波浪线](media/diagnostics-severity-colors.png)

代码分析器在生成时检查代码，比如传统分析（如果启用），但还可在你键入时保持运行状态。 你可配置实时代码分析的范围，以仅对当前文档执行、对所有打开的文档执行或对整个解决方案执行。 请参阅[如何：配置实时代码分析范围](./configure-live-code-analysis-scope-managed-code.md)。

> [!TIP]
> 仅当分析器作为 NuGet 包安装时，才会显示来自代码分析器的生成时错误和警告。 内置分析器（例如 IDE0067 和 IDE0068）不会在生成期间运行。

Roslyn 代码分析器不仅会报告传统分析也会报告的相同类型的问题，而且还可以用于轻松修复文件或项目中一次冲突或所有。 这些操作称为代码修复  。 代码修复是特定于 IDE 的；在 Visual Studio 中，它们以[快速操作](../ide/quick-actions.md)的方式实现。 并非所有分析器诊断都有相关联的代码修复。

> [!NOTE]
> 在 Visual Studio 2019 16.5 版本之前，“分析” > “运行代码分析”菜单选项会执行旧式分析   。 从 Visual Studio 2019 16.5 开始，“运行代码分析”菜单选项会针对所选项目或解决方案执行基于 Roslyn 的分析器  。

若在“错误列表”中要区分来自代码分析器和传统分析的冲突，请查看“工具”列  。 如果“工具”值与“解决方案资源管理器”中的某个分析器程序集（例如 Microsoft.CodeQuality.Analyzers）匹配，则该冲突来自代码分析器   。 否则，冲突源自传统分析。

![错误列表中的工具列](media/code-analysis-tool-in-error-list.png)

> [!TIP]
> 项目文件中的 RunCodeAnalysis MSBuild 属性仅适用于传统分析  。 如果安装分析器，请在项目文件中将 RunCodeAnalysis 设置为 false，以防止生成后运行传统分析   。
>
> ```xml
> <RunCodeAnalysis>false</RunCodeAnalysis>
> ```

## <a name="nuget-package-versus-vsix-extension"></a>NuGet 包与 VSIX 扩展

可以通过 NuGet 包为每个项目安装 Roslyn 代码分析器。 有些分析器还可用作 Visual Studio 扩展，在这种情况下，它们适用于在 Visual Studio 中打开的任何解决方案。 这两种[安装分析器](../code-quality/install-roslyn-analyzers.md)方法之间存在一些关键行为差异。

### <a name="scope"></a>范围

如果将分析器安装为 Visual Studio 扩展，则它们将在解决方案级别应用于 Visual Studio 的所有实例。 如果将分析器安装为 NuGet 包（这是首选方法），它们仅适用于安装了 NuGet 软件包的项目。 在团队环境中，作为 NuGet 包安装的分析器适用于处理该项目的所有开发人员  。

### <a name="build-errors"></a>生成错误

要在生成时强制执行规则，包括通过命令行执行或作为持续集成 (CI) 生成的一部分来执行，请将分析器安装为 NuGet 包。 如果将分析器作为扩展安装，则分析器警告和错误不会显示在生成报告中。

以下图像显示了生成包含分析器规则冲突的项目时的命令行生成输出：

![带规则冲突的 MSBuild 输出](media/command-line-build-analyzers.png)

### <a name="rule-severity"></a>规则严重性

无法配置作为 Visual Studio 扩展安装的分析器的规则严重性。 若要配置[规则严重性](../code-quality/use-roslyn-analyzers.md#rule-severity)，则应将分析器安装为 NuGet 包。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [在 Visual Studio 中安装代码分析器](../code-quality/install-roslyn-analyzers.md)

> [!div class="nextstepaction"]
> [在 Visual Studio 中使用代码分析器](../code-quality/use-roslyn-analyzers.md)

## <a name="see-also"></a>请参阅

- [分析器常见问题解答](analyzers-faq.md)
- [编写自己的代码分析器](../extensibility/getting-started-with-roslyn-analyzers.md)
- [.NET Compiler Platform SDK](/dotnet/csharp/roslyn-sdk/)
