---
title: 使用 Roslyn 分析器进行代码分析
ms.date: 03/26/2018
ms.topic: overview
helpviewer_keywords:
- code analysis, managed code
- analyzers
- Roslyn analyzers
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 2d4a9bfca972f9c57688b19bd872b31ee5997f76
ms.sourcegitcommit: 209ed0fcbb8daa1685e8d6b9a97f3857a4ce1152
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2019
ms.locfileid: "69550761"
---
# <a name="overview-of-net-compiler-platform-code-analyzers"></a>.NET Compiler Platform 代码分析器概述

.NET 编译器平台 ("Roslyn") 分析器分析代码的样式、质量和可维护性、设计和其他问题。 Visual Studio 包括一系列内置的分析器，这些分析器在用户键入时分析 C# 或 Visual Basic 代码。 在[文本编辑器选项](../ide/code-styles-and-code-cleanup.md)页上或在 [.editorconfig 文件](../ide/editorconfig-code-style-settings-reference.md)中配置这些内置分析器的首选项。 可以将其他分析器作为 Visual Studio 扩展或 NuGet 包安装。

如果分析器发现规则冲突，将在代码编辑器（违规代码下方有波浪线）和“错误列表”窗口中报告   。

许多分析器规则或诊断都有一个或多个相关的代码修复程序，可以应用它们来纠正问题   。 Visual Studio 中内置的每个分析器诊断都有关联的代码修复。 代码修复以及其他类型的[快速操作](../ide/quick-actions.md)显示在灯泡图标菜单中。 有关这些代码修复的信息，请参阅[常见快速操作](../ide/common-quick-actions.md)。

![分析器冲突和快速操作代码修复](../code-quality/media/built-in-analyzer-code-fix.png)

## <a name="net-compiler-platform-based-analysis-versus-legacy-analysis"></a>基于 .NET Compiler Platform 的分析与传统分析

.NET Compiler Platform（“Roslyn”）代码分析最终将替换托管代码的[传统分析](../code-quality/code-analysis-for-managed-code-overview.md)。 许多传统分析规则已重写为基于 .NET Compiler Platform 的代码分析器。

与传统的分析规则冲突一样，基于 .NET Compiler Platform 的代码分析冲突会出现在 Visual Studio 的错误列表窗口中。 此外，基于 .NET Compiler Platform 的代码分析冲突还会在代码编辑器中以波浪线的形式显示在违规代码下方  。 规则的[严重性设置](../code-quality/use-roslyn-analyzers.md#rule-severity)决定波浪线的颜色。 以下屏幕截图显示了三个冲突 &mdash; 一个为红色、一个绿色为以及一个为灰色：

![代码编辑器中的波浪线](media/diagnostics-severity-colors.png)

基于 .NET Compiler Platform 的代码分析器在生成时分析代码，如果启了用传统分析，传统分析也是如此，但代码分析器在你键入时也处于活动状态。 如果启用[完整的解决方案分析](../code-quality/how-to-enable-and-disable-full-solution-analysis-for-managed-code.md#to-toggle-full-solution-analysis)，代码分析器还提供未在编辑器中打开的代码文件的设计时分析。

> [!TIP]
> 仅当分析器作为 NuGet 包安装时，才会显示来自代码分析器的生成时错误和警告。

基于 .NET Compiler Platform 的代码分析器不仅报告与传统分析相同类型的问题，而且让你能够轻松地修复文件或项目中的一处或全部冲突。 这些操作称为代码修复  。 代码修复是特定于 IDE 的；在 Visual Studio 中，它们以[快速操作](../ide/quick-actions.md)的方式实现。 并非所有分析器诊断都有相关联的代码修复。

> [!NOTE]
> 以下 UI 选项仅适用于传统分析：
>
> - “分析”   > “运行代码分析”  菜单选项。
> - 项目的属性页的“代码分析”选项卡上的“生成时启用代码分析”和“禁止显示所生成代码的结果”复选框    。

若在“错误列表”窗口中要区分来自代码分析器和传统分析的冲突，请查看“工具”列  。 如果“工具”值与“解决方案资源管理器”中的某个分析器程序集（例如 Microsoft.CodeQuality.Analyzers）匹配，则该冲突来自代码分析器   。 否则，冲突源自传统分析。

![错误列表中的工具列](media/code-analysis-tool-in-error-list.png)

> [!TIP]
> 项目文件中的 RunCodeAnalysis msbuild 属性仅适用于传统分析  。 如果安装分析器，请在项目文件中将 RunCodeAnalysis 设置为 false，以防止生成后运行传统分析   。
>
> ```xml
> <RunCodeAnalysis>false</RunCodeAnalysis>
> ```

## <a name="nuget-package-versus-vsix-extension"></a>NuGet 包与 VSIX 扩展

.NET Compiler Platform 分析器可以通过 NuGet 包按项目安装，也可以作为 Visual Studio 扩展安装在 Visual Studio 内。 这两种[安装分析器](../code-quality/install-roslyn-analyzers.md)方法之间存在一些关键行为差异。

### <a name="scope"></a>范围

如果将分析器安装为 Visual Studio 扩展，则它们将在解决方案级别应用于 Visual Studio 的所有实例。 如果将分析器安装为 NuGet 包（这是首选方法），它们仅适用于安装了 NuGet 软件包的项目。 在团队环境中，作为 NuGet 包安装的分析器适用于处理该项目的所有开发人员  。

### <a name="build-errors"></a>生成错误

要在生成时强制执行规则，包括通过命令行执行或作为持续集成 (CI) 生成的一部分来执行，请将分析器安装为 NuGet 包。 如果将分析器作为扩展安装，则分析器警告和错误不会显示在生成报告中。

以下屏幕截图显示了生成包含分析器规则冲突的项目时的命令行生成输出：

![带规则冲突的 MSBuild 输出](media/command-line-build-analyzers.png)

### <a name="rule-severity"></a>规则严重性

无法设置作为 Visual Studio 扩展安装的分析器的规则严重性。 若要配置[规则严重性](../code-quality/use-roslyn-analyzers.md#rule-severity)，则应将分析器安装为 NuGet 包。

## <a name="categories"></a>类别

下面介绍有助于分析代码的不同分析器类型：

- Microsoft 建议的分析器：[FxCop 分析器](../code-quality/fxcop-analyzers.yml)
- Visual Studio IDE 分析器：[配置](../ide/code-styles-and-code-cleanup.md)
- 第三方分析器：[StyleCop](https://www.nuget.org/packages/StyleCop.Analyzers/)、[Roslynator](https://www.nuget.org/packages/Roslynator/)、[XUnit 分析器](https://www.nuget.org/packages/xunit.analyzers/)、[Sonar 分析器](https://www.nuget.org/packages/SonarAnalyzer.CSharp/)

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [在 Visual Studio 中安装代码分析器](../code-quality/install-roslyn-analyzers.md)

> [!div class="nextstepaction"]
> [在 Visual Studio 中使用代码分析器](../code-quality/use-roslyn-analyzers.md)

## <a name="see-also"></a>请参阅

- [分析器常见问题解答](analyzers-faq.md)
- [编写自己的代码分析器](../extensibility/getting-started-with-roslyn-analyzers.md)
- [.NET Compiler Platform SDK](/dotnet/csharp/roslyn-sdk/)
