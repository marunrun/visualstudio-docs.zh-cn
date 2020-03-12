---
title: 分析器规则严重性和禁止显示
ms.date: 09/23/2019
ms.topic: conceptual
helpviewer_keywords:
- code analysis, managed code
- analyzers
- Roslyn analyzers
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: c24164f31ca444d17035f145a1783c69dfb2585b
ms.sourcegitcommit: 3154387056160bf4c36ac8717a7fdc0cd9faf3f9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2020
ms.locfileid: "78408475"
---
# <a name="use-code-analyzers"></a>使用代码分析器

.NET Compiler Platform（“Roslyn”）代码分析器可随键入分析 C# 或 Visual Basic 代码。 每个“诊断”或规则都有一个默认的严重性和禁止显示状态，可以在你的项目中覆盖它们  。 本文将介绍设置规则严重性、使用规则集和禁止显示冲突。

## <a name="analyzers-in-solution-explorer"></a>解决方案资源管理器中的分析器

可以在“解决方案资源管理器”中自定义分析器诊断  。 如果以 NuGet 包的形式[安装分析器](../code-quality/install-roslyn-analyzers.md)，则“解决方案资源管理器”中的“引用”或“依赖项”节点下会出现“分析器”节点     。 如果展开“分析器”，然后展开其中一个分析器程序集，你将看到该程序集中的所有诊断  。

![解决方案资源管理器中的分析器节点](media/analyzers-expanded-in-solution-explorer.png)

可以在“属性”窗口中查看诊断的属性，包括其描述和默认严重性  。 若要查看属性，请右键单击规则并选择“属性”，或者选择规则然后按 Alt+Enter    。

![属性窗口中的诊断属性](media/analyzer-diagnostic-properties.png)

若要查看诊断的联机文档，请右键单击诊断并选择“查看帮助”  。

**解决方案资源管理器**中每个诊断旁边的图标对应于在编辑器中打开规则集时在其中看到的图标：

- 圆圈中的“x”表示[严重性](#rule-severity)为“错误” 
- 三角形中的“!”表示[严重性](#rule-severity)为“警告” 
- 圆圈中的“i”表示[严重性](#rule-severity)为“信息” 
- 浅色背景上圆圈中的“i”表示[严重性](#rule-severity)为“隐藏” 
- 圆圈中的向下箭头表示已禁止显示该诊断

![解决方案资源管理器中的诊断图标](media/diagnostics-icons-solution-explorer.png)

## <a name="rule-severity"></a>规则严重性

::: moniker range=">=vs-2019"

如果以 NuGet 包的形式[安装分析器](../code-quality/install-roslyn-analyzers.md)，可以配置分析器规则或诊断的严重性  。 从 Visual Studio 2019 版本 16.3 开始，可以[在 EditorConfig 文件中](#set-rule-severity-in-an-editorconfig-file)配置规则的严重性。 还可以[从解决方案资源管理器](#set-rule-severity-from-solution-explorer)或[在规则集文件中](#set-rule-severity-in-the-rule-set-file)更改规则的严重性。

::: moniker-end

::: moniker range="vs-2017"

如果以 NuGet 包的形式[安装分析器](../code-quality/install-roslyn-analyzers.md)，可以配置分析器规则或诊断的严重性  。 可以[从解决方案资源管理器](#set-rule-severity-from-solution-explorer)或[在规则集文件中](#set-rule-severity-in-the-rule-set-file)更改规则的严重性。

::: moniker-end

下表显示了不同的严重性选项：

| 严重性（解决方案资源管理器） | 严重性（EditorConfig 文件） | 生成时行为 | 编辑器行为 |
|-|-|-|
| 错误 | `error` | 此类冲突在错误列表和命令行生成输出中显示为“错误”，并导致生成失败  。| 违规代码用红色波浪下划线表示，并用滚动条中的红色小框标记。 |
| 警告 | `warning` | 此类冲突在错误列表和命令行生成输出中显示为“警告”，但不会导致生成失败  。 | 违规代码用绿色波浪下划线表示，并用滚动条中的绿色小框标记。 |
| T:System.Diagnostics.Switch | `suggestion` | 此类冲突在错误列表中显示为“消息”，而不会在命令行生成输出中显示  。 | 违规代码用灰色波浪下划线表示，并用滚动条中的灰色小框标记。 |
| Hidden | `silent` | 对用户不可见。 | 对用户不可见。 但是，诊断会报告给 IDE 诊断引擎。 |
| None | `none` | 完全禁止显示。 | 完全禁止显示。 |
| 默认 | `default` | 对应于规则的默认严重性。 若要确定规则的默认值，请查看“属性”窗口。 | 对应于规则的默认严重性。 |

下面的代码编辑器屏幕截图显示了三个严重性各异的冲突。 注意波浪线和右侧滚动条上彩色小方块的颜色。

![代码编辑器中的错误、警告和信息冲突](media/diagnostics-severity-colors.png)

以下屏幕截图显示了相同的三个冲突在错误列表中的样子：

![错误列表中的错误、警告和信息冲突](media/diagnostics-severities-in-error-list.png)

::: moniker range=">=vs-2019"

### <a name="set-rule-severity-in-an-editorconfig-file"></a>在 EditorConfig 文件中设置规则严重性

（Visual Studio 2019 版本 16.3 及更高版本）

在 EditorConfig 文件中指定规则严重性的一般语法如下：

`dotnet_diagnostic.<rule ID>.severity = <severity>`

在 EditorConfig 文件中设置规则的严重性优先于在规则集或解决方案资源管理器中设置的任何严重性。 你可以在 EditorConfig 文件中[手动](#manually-configure-rule-severity)配置严重性，或者通过出现在冲突旁边的灯泡[自动](#automatically-configure-rule-severity)配置。

#### <a name="manually-configure-rule-severity"></a>手动配置规则严重性

1. 如果你的项目还没有 EditorConfig 文件，请[添加一个](../ide/create-portable-custom-editor-options.md#add-an-editorconfig-file-to-a-project)。

2. 在相应的文件扩展名下为要配置的每个规则添加一个条目。 例如，若要将 C# 文件的 [CA1822](ca1822.md) 的严重性设置为 `error`，条目如下所示：

   ```ini
   [*.cs]
   dotnet_diagnostic.CA1822.severity = error
   ```

> [!NOTE]
> 对于 IDE 代码样式分析器，还可以使用不同的语法（例如 `dotnet_style_qualification_for_field = false:suggestion`）在 EditorConfig 文件中配置它们。 但是，如果使用 `dotnet_diagnostic` 语法设置严重性，则优先使用该严重性。 有关详细信息，请参阅 [EditorConfig 适用的 .NET 语言约定](../ide/editorconfig-language-conventions.md)。

#### <a name="automatically-configure-rule-severity"></a>自动配置规则严重性

Visual Studio 提供了一种从[快速操作](../ide/quick-actions.md)灯泡菜单配置规则严重性的方便方法。

1. 发生冲突后，将鼠标悬停在编辑器中表示冲突的波浪线上，然后打开灯泡菜单。 或者，将光标放在该行上并按 Ctrl+.   （句点）。

2. 从灯泡菜单中，选择“配置或禁止显示问题”>“配置 \<规则 ID> 的严重性”   。

   ![从 Visual Studio 的灯泡菜单配置规则严重性](media/configure-rule-severity.png)

3. 从此处选择一个严重性选项。

   ![将规则严重性配置为“建议”](media/configure-rule-severity-suggestion.png)

   Visual Studio 会在 EditorConfig 文件中添加一个条目，以将规则配置为请求的级别，如预览框中所示。

   > [!TIP]
   > 如果项目中还没有 EditorConfig 文件，Visual Studio 将为你创建一个。

::: moniker-end

### <a name="set-rule-severity-from-solution-explorer"></a>从解决方案资源管理器设置规则严重性

1. 在“解决方案资源管理器”中，展开“引用” > “分析器”（如果是 .NET Core 项目，则为“依赖项” > “分析器”）      。

1. 展开包含待设置严重性的规则的程序集。

1. 右键单击规则并选择“设置规则集严重性”  。 在弹出菜单中，选择其中一个严重性选项。

   规则的严重性保存在活动规则集文件中。

### <a name="set-rule-severity-in-the-rule-set-file"></a>在规则集文件中设置规则严重性

![解决方案资源管理器中的规则集文件](media/ruleset-in-solution-explorer.png)

1. 在“解决方案资源管理器”中双击活动规则集文件，在“引用” > “分析器”节点的右键菜单上选择“打开活动规则集”，或者在项目的“代码分析”属性页上选择“打开”       。

   如果这是你第一次编辑规则集，则 Visual Studio 将复制默认规则集文件，将其命名为 \<projectname>.ruleset，并将其添加到项目中  。 此自定义规则集也将成为项目的活动规则集。

   > [!NOTE]
   > .NET Core 和 .NET Standard 项目不支持“解决方案资源管理器”中规则集的菜单命令，例如“打开活动规则集”   。 若要为 .NET Core 或 .NET Standard 项目指定非默认规则集，请在项目文件中手动[添加 CodeAnalysisRuleSet 属性](using-rule-sets-to-group-code-analysis-rules.md#specify-a-rule-set-for-a-project)  。 你仍可以在 Visual Studio 规则集编辑器 UI 中的规则集内配置规则。

1. 展开包含规则的程序集并浏览到该规则。

1. 在“操作”列中，选择值以打开下拉列表，然后从列表中选择所需的严重性  。

   ![在编辑器中打开规则集文件](media/ruleset-file-in-editor.png)

## <a name="suppress-violations"></a>禁止显示冲突

可通过多种方法禁止显示规则冲突：

::: moniker range=">=vs-2019"

- 在“编辑 EditorConfig 文件”中 

  将严重性设置为 `none`，例如 `dotnet_diagnostic.CA1822.severity = none`。

- 从“分析”菜单中 

  在菜单栏上选择“分析” > “生成并禁止显示活动问题”，以禁止显示所有当前冲突   。 有时这称为“基线”。

::: moniker-end

::: moniker range="vs-2017"

- 从“分析”菜单中 

  在菜单栏上选择“分析” > “运行代码分析并禁止显示活动问题”，以禁止显示所有当前冲突   。 有时这称为“基线”。

::: moniker-end

- 从“解决方案资源管理器”中 

  将规则的严重性设置为“无”  。

- 从“规则集编辑器”中 

  取消选中其名称旁边的框，或将“操作”设置为“无”   。

- 从“代码编辑器”中 

  将光标放在有冲突的代码行中，然后按 Ctrl+句点 (.) 打开“快速操作”菜单    。 选择“禁止显示 CAXXXX” > “在源中”/“在禁止显示文件中”   。

  ![从“快速操作”菜单中禁止显示诊断](media/suppress-diagnostic-from-editor.png)

- 从“错误列表”中 

  选择要禁止显示的规则，然后右键单击并选择“禁止显示” > “在源中”/“在禁止显示文件中”   。

  - 如果“在源中”禁止显示，将打开“预览更改”对话框，并显示添加到源代码中的 C# [#pragma warning](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-pragma-warning) 或 Visual Basic [#Disable warning](/dotnet/visual-basic/language-reference/directives/directives) 指令的预览   。

    ![在代码文件中添加 #pragma warning 的预览](media/pragma-warning-preview.png)

  - 如果选择“在禁止显示文件中”，将打开“预览更改”对话框，并显示添加到全局禁止显示文件的 <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 属性的预览   。

    ![向禁止显示文件添加 SuppressMessage 属性的预览](media/preview-changes-in-suppression-file.png)

  在“预览更改”对话框中，选择“应用”   。

  > [!NOTE]
  > 如果在“解决方案资源管理器”中没有看到“禁止显示”菜单选项，则冲突可能来自生成而非实时分析   。 “错误列表”显示来自实时代码分析和生成的诊断或规则冲突  。 由于生成诊断可能已过时（例如已编辑代码以修复冲突，但尚未重新生成），无法从“错误列表”中禁止显示这些诊断  。 来自实时分析或 IntelliSense 的诊断始终是当前源的最新诊断，可以从“错误列表”中禁止显示  。 若要从所选内容中排除“生成”诊断，请将“错误列表”源筛选器从“生成 + IntelliSense”切换到“仅 IntelliSense”     。 然后，选择要禁止显示的诊断并按前面所述继续操作。
  >
  > ![Visual Studio 中的错误列表源筛选器](media/error-list-filter.png)

## <a name="command-line-usage"></a>命令行用法

在命令行生成项目时，如果满足以下条件，则生成输出中将显示规则冲突：

- 分析器是作为 Nuget 包安装的，而不是作为 VSIX 扩展安装的。

- 项目的代码中违反了一个或多个规则。

- 代码所违反规则的[严重性](#rule-severity)设置为“警告”（在这种情况下，违规不会导致生成失败）或“错误”（在这种情况下，违规会导致生成失败）   。

生成输出的详细程度不影响是否显示规则冲突。 即使有“相当级别”的详细程度，规则冲突也会出现在生成输出中  。

> [!TIP]
> 如果你习惯于使用 FxCopCmd.exe 或通过 msbuild 使用“RunCodeAnalysis”标志从命令行运行旧版分析，下面介绍了如何对代码分析器执行该操作，供你参考   。

若要在使用 msbuild 生成项目时在命令行中查看分析器冲突，请运行以下命令：

```cmd
msbuild myproject.csproj /target:rebuild /verbosity:minimal
```

以下图像显示了生成包含分析器规则冲突的项目时的命令行生成输出：

![带规则冲突的 MSBuild 输出](media/command-line-build-analyzers.png)

## <a name="dependent-projects"></a>依赖项目

在 .NET Core 项目中，如果添加对具有 NuGet 分析器的项目的引用，则这些分析器也会自动添加到依赖项目中。 若要禁用此行为（例如当依赖项目是单元测试项目时），请通过设置“PrivateAssets”属性，在引用项目的 .csproj 或 .vbproj 文件中将 NuGet 包标记为专用    ：

```xml
<PackageReference Include="Microsoft.CodeAnalysis.FxCopAnalyzers" Version="2.9.0" PrivateAssets="all" />
```

## <a name="see-also"></a>请参阅

- [Visual Studio 中的代码分析器概述](../code-quality/roslyn-analyzers-overview.md)
- [提交代码分析器 bug](https://github.com/dotnet/roslyn-analyzers/issues)
- [使用规则集](../code-quality/using-rule-sets-to-group-code-analysis-rules.md)
- [禁止显示代码分析警告](../code-quality/in-source-suppression-overview.md)
