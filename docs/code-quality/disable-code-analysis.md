---
title: 关闭代码分析
ms.date: 10/03/2019
ms.topic: conceptual
helpviewer_keywords:
- code analysis, disable
- disable code analysis
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d25254cabecd88c6e876646c3c276503aadf7eb7
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75587662"
---
# <a name="how-to-disable-source-code-analysis-for-managed-code"></a>如何禁用托管代码的源代码分析

::: moniker range=">=vs-2019"

此页可帮助你在 Visual Studio 中禁用代码分析。 您可以禁用的内容有限制，而关闭代码分析的过程会因几个因素而异：

- 项目类型（.NET Core/Standard 与 .NET Framework）

  .NET Core 和 .NET Standard 项目具有其 "代码分析属性" 页上的选项，可让你从安装为 NuGet 包的分析器关闭代码分析。 有关详细信息，请参阅[.Net Core 和 .NET Standard 项目](#net-core-and-net-standard-projects)。 若要关闭 .NET Framework 项目的源代码分析，请参阅[.NET Framework 项目](#net-framework-projects)。

- NuGet 分析器包与 VSIX 或内置分析器

  目前，无法为内置分析器禁用实时代码分析，例如，规则 ID IDE0067。 同样，你不能为作为 Visual Studio 扩展（VSIX）的一部分安装的分析器禁用实时代码分析。 若要取消内置和基于 VSIX 的分析器中的错误和警告，请选择 "**分析** > **生成和取消显示**菜单栏上的活动问题"。 您*可以*对作为 NuGet 包的一部分安装的分析器禁用实时分析和生成时分析。

- 源分析与传统分析

  本主题适用于源代码分析，不适用于旧版（二进制）分析。 有关禁用旧分析的信息，请参阅[如何：启用和禁用旧代码分析](how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)。

## <a name="net-core-and-net-standard-projects"></a>.NET Core 和 .NET Standard 项目

从 Visual Studio 2019 版本16.3 开始，"代码分析属性" 页中提供了两个复选框，可用于控制在生成时和设计时是否运行基于 NuGet 的分析器。 这些选项是项目特定的。

![在 Visual Studio 中启用或禁用实时代码分析或生成](media/run-on-build-run-live-analysis.png)

若要打开此页，请在**解决方案资源管理器**中右键单击项目节点，然后选择 "**属性**"。 选择 "**代码分析**" 选项卡。

- 若要在生成时禁用源分析，请取消选中 "**在生成上运行**" 选项。
- 若要禁用实时源分析，请取消选中 "**在实时分析上运行**" 选项。

> [!NOTE]
> 即使未选择 **"在实时分析上运行"** ，内置和基于 VSIX 的分析器也将继续提供代码的实时分析。 如果要禁止显示这些分析器中的错误和警告，请选择 "**分析** > **生成和取消显示**菜单栏上的活动问题。

## <a name="net-framework-projects"></a>.NET Framework 项目

若要关闭作为 NuGet 包的一部分安装的分析器的源代码分析，请将以下一个或多个 MSBuild 属性添加到[项目文件](../ide/solutions-and-projects-in-visual-studio.md#project-file)。

| MSBuild 属性 | 描述 | 默认值 |
| - | - | - |
| `RunAnalyzersDuringBuild` | 控制基于 NuGet 的分析器是否在生成时运行。 | `true` |
| `RunAnalyzersDuringLiveAnalysis` | 控制基于 NuGet 的分析器是否在设计时实时分析代码。 | `true` |
| `RunAnalyzers` | 在生成和设计时禁用基于 NuGet 的分析器。 此属性优先于 `RunAnalyzersDuringBuild` 和 `RunAnalyzersDuringLiveAnalysis`。 | `true` |

例如：

```xml
<RunAnalyzersDuringBuild>false</RunAnalyzersDuringBuild>
<RunAnalyzersDuringLiveAnalysis>false</RunAnalyzersDuringLiveAnalysis>
<RunAnalyzers>false</RunAnalyzers>
```

::: moniker-end

::: moniker range="vs-2017"

## <a name="source-analysis"></a>源分析

你无法在 Visual Studio 2017 中关闭[源分析](roslyn-analyzers-overview.md)。 如果要从错误列表中清除分析器错误，则可以通过选择 "**分析** > **运行代码分析并取消**菜单栏上的活动问题来禁止所有当前冲突。 有关详细信息，请参阅[取消冲突](use-roslyn-analyzers.md#suppress-violations)。

从 Visual Studio 2019 版本16.3 开始，你可以禁用基于 NuGet 的源代码分析。 请考虑升级到 Visual Studio 2019。

## <a name="legacy-analysis"></a>旧版分析

您可以在 "**代码分析**" 属性页上禁用旧的生成时分析。 有关详细信息，请参阅[如何：启用和禁用旧代码分析](how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)。

::: moniker-end

## <a name="see-also"></a>另请参阅

- [禁止冲突](use-roslyn-analyzers.md#suppress-violations)
- [如何：启用和禁用旧代码分析](how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)
