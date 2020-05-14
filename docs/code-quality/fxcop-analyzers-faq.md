---
title: FxCop 代码分析和 FxCop 分析器
ms.date: 09/06/2018
ms.topic: conceptual
helpviewer_keywords:
- code analysis FAQ
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: bc04cbc6d46d8dc47a08d06c8c5949bb5d9107f3
ms.sourcegitcommit: 92361aac3665a934faa081e1d1ea89a067b01c5b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/17/2020
ms.locfileid: "79431360"
---
# <a name="frequently-asked-questions-about-fxcop-and-fxcop-analyzers"></a>有关 FxCop 和 FxCop 分析器的常见问题解答

理解旧版 FxCop 和 FxCop 分析器之间的差异可能有点令人困惑。 本文旨在解决你可能遇到的一些问题。

## <a name="whats-the-difference-between-legacy-fxcop-and-fxcop-analyzers"></a>旧版 FxCop 和 FxCop 分析器之间有什么区别？

旧版 FxCop 在已编译的程序集上运行生成后分析。 它作为单独的可执行文件运行，名为 FxCopCmd.exe****。 FxCopCmd.exe 加载已编译的程序集，运行代码分析，然后报告结果（或“诊断”）**。

FxCop 分析器基于 .NET Compiler Platform（“Roslyn”）。 [将它们安装 NuGet 包](install-fxcop-analyzers.md#nuget-package)，该包为项目或解决方案所引用。 FxCop 分析器在编译器执行期间运行基于源代码的分析。 FxCop 分析器托管在编译器进程（csc.exe 或 vbc.exe）中，并在生成项目时运行分析********。 报告分析器结果以及编译器结果。

> [!NOTE]
> 还可[将 FxCop 分析器安装为 Visual Studio 扩展](install-fxcop-analyzers.md#vsix)。 在这种情况下，当你在代码编辑器中键入时分析器将执行，但它们不会在生成时执行。 若要将 FxCop 分析器作为持续集成 (CI) 的一部分运行，请将它们安装为 NuGet 包。

## <a name="does-the-run-code-analysis-command-run-fxcop-analyzers"></a>“运行代码分析”命令是否运行 FxCop 分析器？

在 Visual Studio 2019 16.5 版本之前，当您选择 **"分析** > **运行代码分析**"时，它将执行旧版分析。 从 Visual Studio 2019 16.5 开始，**运行代码分析**菜单选项将执行基于 Roslyn 的基于 Roslyn 的分析器，用于所选项目或解决方案。 如果您安装了基于 Roslyn 的 FxCop 分析仪，它们也将被执行。 有关详细信息，请参阅[如何：手动运行托管代码的代码分析](how-to-run-code-analysis-manually-for-managed-code.md)。

## <a name="does-the-runcodeanalysis-msbuild-project-property-run-analyzers"></a>RunCodeAnalysis msbuild 项目属性是否运行分析器？

不是。 项目文件（例如 .csproj）中的 RunCodeAnalysis 属性仅用于执行旧版 FxCop******。 它将运行调用 FxCopCmd.exe 的生成后 msbuild 任务****。

## <a name="so-how-do-i-run-fxcop-analyzers-then"></a>那么我该如何运行 FxCop 分析器呢？

要运行 FxCop 分析器，首先请为它们[安装 NuGet 包](install-fxcop-analyzers.md)。 然后在 Visual Studio 中或使用 msbuild 生成项目或解决方案。 FxCop 分析器生成的警告和错误将显示在“错误列表”或命令窗口中****。

## <a name="i-get-warning-ca0507-even-after-ive-installed-the-fxcop-analyzers-nuget-package"></a>即使在安装了 FxCop 分析器 NuGet 包之后，我仍会收到 CA0507 警告

如果您已安装 FxCop 分析器，但继续收到警告 CA0507"**运行代码分析"已被弃用，转而使用在生成期间运行的 FxCop 分析器"，** 则可能需要将[项目文件中](../ide/solutions-and-projects-in-visual-studio.md#project-file)的**RunCodeAnalysis** msbuild 属性设置为**false**。 否则，遗留分析将在每次生成后执行。

```xml
<RunCodeAnalysis>false</RunCodeAnalysis>
```

## <a name="which-rules-have-been-ported-to-fxcop-analyzers"></a>哪些规则已移植到 FxCop 分析仪？

有关哪些旧版分析规则已移植到[FxCop 分析器](install-fxcop-analyzers.md)的信息，请参阅[Fxcop 规则端口状态](fxcop-rule-port-status.md)。

## <a name="code-analysis-warnings-are-treated-as-errors"></a>代码分析警告被视为错误

如果项目使用生成选项将警告视为错误，则 FxCop 分析器警告可能会显示为错误。 为防止将代码分析警告视为错误，请按照[代码分析常见问题 解答](../code-quality/analyzers-faq.md#treat-warnings-as-errors)中的步骤操作。

## <a name="see-also"></a>另请参阅

- [.NET Compiler Platform 分析器概述](roslyn-analyzers-overview.md)
- [迁移到 FxCop 分析仪](migrate-from-legacy-analysis-to-fxcop-analyzers.md)
- [安装 FxCop 分析器](install-fxcop-analyzers.md)
