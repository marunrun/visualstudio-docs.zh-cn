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
ms.openlocfilehash: 8db6ad7bed4b1526d87112f33d3586728728d7f5
ms.sourcegitcommit: 92361aac3665a934faa081e1d1ea89a067b01c5b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/17/2020
ms.locfileid: "79431392"
---
# <a name="how-to-disable-source-code-analysis-for-managed-code"></a>如何禁用托管代码的源代码分析

::: moniker range=">=vs-2019"

此页面可帮助您在 Visual Studio 中禁用代码分析。 可以禁用的内容有限制，关闭代码分析的过程因以下几个因素而异：

- 项目类型（.NET 核心/标准与 .NET 框架）

  .NET Core 和 .NET 标准项目在其代码分析属性页上具有选项，允许您关闭作为 NuGet 包安装的分析器的代码分析。 有关详细信息，请参阅[.NET 核心和 .NET 标准项目](#net-core-and-net-standard-projects)。 要关闭 .NET 框架项目的源代码分析，请参阅[.NET 框架项目](#net-framework-projects)。

- 源分析与旧分析

  本主题适用于源代码分析，不适用于遗留（二进制）分析。 有关禁用旧版分析的信息，请参阅[如何：启用和禁用旧代码分析](how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)。

## <a name="net-core-and-net-standard-projects"></a>.NET 核心和 .NET 标准项目

从 Visual Studio 2019 版本 16.3 开始，代码分析属性页中有两个复选框，用于控制分析器在生成时间和设计时间是否运行。 这些选项特定于项目。

![在可视化工作室中启用或禁用实时代码分析或构建](media/run-on-build-run-live-analysis.png)

要打开此页面，请右键单击**解决方案资源管理器**中的项目节点并选择 **"属性**"。 选择 **"代码分析**"选项卡。

- 要在生成时禁用源分析，请取消选中 **"在生成时运行**"选项。
- 要禁用实时源分析，请取消选中 **"运行实时分析**"选项。

> [!NOTE]
> 从 Visual Studio 2019 版本 16.5 开始，如果您更喜欢按需代码分析执行工作流，则可以在实时分析和/或生成期间禁用分析器执行，并在项目或解决方案上按需手动触发代码分析一次。 有关手动运行代码分析的信息，请参阅[如何：手动运行托管代码的代码分析](how-to-run-code-analysis-manually-for-managed-code.md)。  

## <a name="net-framework-projects"></a>.NET 框架项目

要关闭分析器的源代码分析，请向[项目文件](../ide/solutions-and-projects-in-visual-studio.md#project-file)添加以下一个或多个 MSBuild 属性。

| MSBuild 属性 | 说明 | 默认 |
| - | - | - |
| `RunAnalyzersDuringBuild` | 控制分析器是否在生成时运行。 | `true` |
| `RunAnalyzersDuringLiveAnalysis` | 控制分析器是否在设计时实时分析代码。 | `true` |
| `RunAnalyzers` | 在生成和设计时间禁用分析器。 此属性优先于`RunAnalyzersDuringBuild`和`RunAnalyzersDuringLiveAnalysis`。 | `true` |

示例：

```xml
<RunAnalyzersDuringBuild>false</RunAnalyzersDuringBuild>
<RunAnalyzersDuringLiveAnalysis>false</RunAnalyzersDuringLiveAnalysis>
<RunAnalyzers>false</RunAnalyzers>
```

::: moniker-end

::: moniker range="vs-2017"

## <a name="source-analysis"></a>源分析

您不能在 Visual Studio 2017 中关闭[源分析](roslyn-analyzers-overview.md)。 如果要从错误列表中清除分析器错误，可以通过选择菜单栏上的 **"分析** > **运行代码分析"和"禁止活动问题"** 来抑制所有当前冲突。 有关详细信息，请参阅[禁止冲突](use-roslyn-analyzers.md#suppress-violations)。

从 Visual Studio 2019 版本 16.3 开始，您可以关闭源代码分析或按需执行。 考虑升级到视觉工作室 2019。

## <a name="legacy-analysis"></a>旧版分析

您可以在 **"代码分析"** 属性页上禁用旧版本时分析。 有关详细信息，请参阅[如何：启用和禁用旧代码分析](how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)。

::: moniker-end

## <a name="see-also"></a>另请参阅

- [抑制违规行为](use-roslyn-analyzers.md#suppress-violations)
- [如何：启用和禁用旧代码分析](how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)
