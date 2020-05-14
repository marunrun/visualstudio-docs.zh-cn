---
title: 分析器规则严重性和抑制
ms.date: 03/04/2020
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
ms.openlocfilehash: 67fd157ad4db24acbc1676ea0a9a1d79e9eb34f9
ms.sourcegitcommit: 92361aac3665a934faa081e1d1ea89a067b01c5b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/17/2020
ms.locfileid: "79431405"
---
# <a name="use-code-analyzers"></a>使用代码分析器

.NET 编译器平台 （"Roslyn"） 代码分析器在键入时分析您的 C# 或可视化基本代码。 每个*诊断*或规则都有一个默认严重性和抑制状态，可以覆盖您的项目。 本文介绍设置规则严重性、使用规则集和禁止冲突。

## <a name="analyzers-in-solution-explorer"></a>解决方案资源管理器中的分析仪

你可以从**解决方案资源管理器**执行分析器诊断的自定义。 如果将[分析器安装](../code-quality/install-roslyn-analyzers.md)为 NuGet 包，则**分析器**节点将显示在**解决方案资源管理器**中的 **"参考"** 或**依赖项**节点下。 如果展开**分析器**，然后展开分析器程序集之一，则会看到程序集中的所有诊断。

![解决方案资源管理器中的分析器节点](media/analyzers-expanded-in-solution-explorer.png)

您可以在"**属性"** 窗口中查看诊断的属性，包括其描述和默认严重性。 要查看属性，请右键单击规则并选择 **"属性**"，或选择规则，然后按**Alt**+**Enter**。

![属性窗口中的诊断属性](media/analyzer-diagnostic-properties.png)

要查看诊断的在线文档，请右键单击诊断并选择"**查看帮助**"。

**解决方案资源管理器**中每个诊断器旁边的图标对应于您在编辑器中打开规则集时看到的图标：

- 圆圈中的"x"表示**错误**[的严重性](#rule-severity)
- 三角形中的"！ [severity](#rule-severity) **Warning**
- 圆圈中的"i"表示**信息**[的严重性](#rule-severity)
- 浅色背景上的圆圈中的"i"表示**隐藏**[的严重性](#rule-severity)
- 圆圈中的向下箭头表示诊断被抑制

![解决方案资源管理器中的诊断图标](media/diagnostics-icons-solution-explorer.png)

## <a name="rule-severity"></a>规则严重性

::: moniker range=">=vs-2019"

如果将[分析器](../code-quality/install-roslyn-analyzers.md)作为 NuGet 包安装，则可以配置分析器规则或*诊断*的严重性。 从 Visual Studio 2019 版本 16.3 开始，您可以在[Editor Config 文件中](#set-rule-severity-in-an-editorconfig-file)配置规则的严重性。 您还可以[从解决方案资源管理器](#set-rule-severity-from-solution-explorer)或[规则集文件中](#set-rule-severity-in-the-rule-set-file)更改规则的严重性。

::: moniker-end

::: moniker range="vs-2017"

如果将[分析器](../code-quality/install-roslyn-analyzers.md)作为 NuGet 包安装，则可以配置分析器规则或*诊断*的严重性。 可以从[解决方案资源管理器](#set-rule-severity-from-solution-explorer)或[规则集文件中](#set-rule-severity-in-the-rule-set-file)更改规则的严重性。

::: moniker-end

下表显示了不同的严重性选项：

| 严重性（解决方案资源管理器） | 严重性（编辑器配置文件） | 构建时间行为 | 编辑器行为 |
|-|-|-|
| 错误 | `error` | 冲突在错误列表和命令行生成输出中显示为*错误*，并导致生成失败。| 有问题的代码用红色波浪线下划线，并在滚动栏中用红色小框标记。 |
| 警告 | `warning` | 冲突在错误列表和命令行生成输出中显示为*警告*，但不会导致生成失败。 | 有问题的代码用绿色波浪线下划线，并在滚动栏中用绿色小框标记。 |
| 信息 | `suggestion` | 冲突在错误列表中显示为 *"消息*"，在命令行生成输出中根本不显示。 | 有问题的代码用灰色波浪线下划线，并在滚动栏中用一个小灰色框标记。 |
| Hidden | `silent` | 用户不可见。 | 用户不可见。 但是，诊断报告给 IDE 诊断引擎。 |
| 无 | `none` | 完全抑制。 | 完全抑制。 |
| 默认 | `default` | 对应于规则的默认严重性。 要确定规则的默认值是什么，请查看"属性"窗口。 | 对应于规则的默认严重性。 |

以下代码编辑器的屏幕截图显示了三个不同的冲突，其严重性不同。 请注意波浪形的颜色和右侧滚动栏中的小彩色方块。

![代码编辑器中的错误、警告和信息冲突](media/diagnostics-severity-colors.png)

以下屏幕截图显示了与错误列表中显示的三个冲突相同的冲突：

![错误列表中的错误、警告和信息冲突](media/diagnostics-severities-in-error-list.png)

::: moniker range=">=vs-2019"

### <a name="set-rule-severity-in-an-editorconfig-file"></a>在编辑器配置文件中设置规则严重性

（视觉工作室 2019 版本 16.3 及更高版本）

您可以使用以下语法在 Editor Config 文件中设置编译器警告或分析器规则的严重性：

`dotnet_diagnostic.<rule ID>.severity = <severity>`

在 Editor Config 文件中设置规则的严重性优先于规则集或解决方案资源管理器中设置的任何严重性。 您可以在 Editor Config 文件中[手动](#manually-configure-rule-severity)配置严重性，也可以通过冲突旁边的灯泡[自动](#automatically-configure-rule-severity)配置严重性。

### <a name="set-rule-severity-of-multiple-analyzer-rules-at-once-in-an-editorconfig-file"></a>在编辑器配置文件中一次设置多个分析器规则的规则严重性

（视觉工作室 2019 版本 16.5 及更高版本）

您可以使用 Editor Config 文件中的单个条目设置特定类别分析器规则或所有分析器规则的严重性。

- 为分析器规则类别设置规则严重性：

`dotnet_analyzer_diagnostic.category-<rule category>.severity = <severity>`

- 为所有分析器规则设置规则严重性：

`dotnet_analyzer_diagnostic.severity = <severity>`

如果您有多个适用于特定规则 ID 的条目，则以下是选择适用条目的优先级顺序：

- 按 ID 划分的单个规则的严重性条目优先于类别的严重性条目。
- 类别的严重性条目优先于所有分析器规则的严重性输入。

请考虑以下编辑器配置示例，其中[CA1822](https://docs.microsoft.com/visualstudio/code-quality/ca1822)具有"性能"类别：

   ```ini
   [*.cs]
   dotnet_diagnostic.CA1822.severity = error
   dotnet_analyzer_diagnostic.category-performance.severity = warning
   dotnet_analyzer_diagnostic.severity = suggestion
   ```

在前面的示例中，所有三个条目都适用于 CA1822。 但是，使用指定的优先级规则，第一个基于规则 ID 的严重性条目胜于下一个条目。 在此示例中，CA1822 将具有有效的严重性"错误"。 具有"性能"类别的所有其余规则都将具有严重性"警告"。 所有剩余的分析器规则（没有"性能"类别）都将具有严重性"建议"。

#### <a name="manually-configure-rule-severity"></a>手动配置规则严重性

1. 如果项目还没有编辑器配置文件，[请添加一个](../ide/create-portable-custom-editor-options.md#add-an-editorconfig-file-to-a-project)。

2. 为要在相应的文件扩展名下配置的每个规则添加一个条目。 例如，要将[CA1822](ca1822.md)的严重性设置为`error`C# 文件，该条目如下所示：

   ```ini
   [*.cs]
   dotnet_diagnostic.CA1822.severity = error
   ```

> [!NOTE]
> 对于 IDE 代码样式分析器，还可以使用不同的语法（例如），`dotnet_style_qualification_for_field = false:suggestion`在 Editor Config 文件中配置它们。 但是，如果使用`dotnet_diagnostic`语法设置严重性，则它优先。 有关详细信息，请参阅[编辑器配置的语言约定](../ide/editorconfig-language-conventions.md)。

#### <a name="convert-an-existing-ruleset-file-to-editorconfig-file"></a>将现有规则集文件转换为编辑器配置文件

从 Visual Studio 2019 版本 16.5 开始，规则集文件被弃用，转而使用 Editor Config 文件来分析器配置托管代码。 大多数用于分析器规则严重性配置的 Visual Studio 工具已更新为处理 Editor Config 文件而不是规则集文件。 编辑器配置文件允许您配置分析器规则分型和分析器选项，包括 Visual Studio IDE 代码样式选项。 强烈建议您将现有规则集文件转换为 Editor Config 文件。 还建议您将 Editor Config 文件保存在回购的根目录或解决方案文件夹中。 通过使用回购或解决方案文件夹的根目录，可以确保此文件中的严重性设置分别自动应用于整个回购或解决方案。

有几种方法可以将现有规则集文件转换为 EditorConfig 文件：

- 从可视化工作室的规则集编辑器（需要可视化工作室 2019 16.5 或更高版本）。 如果项目已使用特定的规则集文件作为其`CodeAnalysisRuleSet`，则可以将其转换为 Visual Studio 中规则集编辑器中的等效编辑器配置文件。

    1. 双击解决方案资源管理器中的规则集文件。

       规则集文件应在规则集编辑器中打开。 您应该在规则集编辑器的顶部看到一个可单击**的信息栏**。

       ![将规则集转换为规则集编辑器中的编辑器配置文件](media/convert-ruleset-to-editorconfig-file-ruleset-editor.png)

    2. **单击**信息栏链接。

       这将打开一个 **"保存为"** 对话框，允许您选择要生成 Editor Config 文件的目录。

    3. **单击**"**保存**"按钮以生成编辑器配置文件。

       生成的编辑器配置应在编辑器中打开。 此外，MSBuild 属性`CodeAnalysisRuleSet`在项目文件中得到更新，以便它不再引用原始规则集文件。

- 通过命令行：

    1. 安装 NuGet 包[Microsoft.代码分析.规则集到编辑器转换器](https://www.nuget.org/packages/Microsoft.CodeAnalysis.RulesetToEditorconfigConverter)。

    2. 从`RulesetToEditorconfigConverter.exe`已安装的包执行，将规则集文件和 Editor Config 文件的路径作为命令行参数。

   ```
   Usage: RulesetToEditorconfigConverter.exe <%ruleset_file%> [<%path_to_editorconfig%>]
   ```

下面是要转换的规则集文件示例：

```xml
<?xml version="1.0" encoding="utf-8"?>
<RuleSet Name="Rules for ConsoleApp" Description="Code analysis rules for ConsoleApp.csproj." ToolsVersion="16.0">
  <Rules AnalyzerId="Microsoft.Analyzers.ManagedCodeAnalysis" RuleNamespace="Microsoft.Rules.Managed">
    <Rule Id="CA1001" Action="Warning" />
    <Rule Id="CA1821" Action="Warning" />
    <Rule Id="CA2213" Action="Warning" />
    <Rule Id="CA2231" Action="Warning" />
  </Rules>
</RuleSet>
```

下面是转换后的编辑器配置文件：

```ini
# NOTE: Requires **VS2019 16.3** or later

# Rules for ConsoleApp
# Description: Code analysis rules for ConsoleApp.csproj.

# Code files
[*.{cs,vb}]


dotnet_diagnostic.CA1001.severity = warning

dotnet_diagnostic.CA1821.severity = warning

dotnet_diagnostic.CA2213.severity = warning

dotnet_diagnostic.CA2231.severity = warning
```

#### <a name="automatically-configure-rule-severity"></a>自动配置规则严重性

##### <a name="configure-from-light-bulb-menu"></a>从灯泡菜单配置

Visual Studio 提供了一种从["快速操作"](../ide/quick-actions.md)灯泡菜单中配置规则严重性的快速方法。

1. 发生违规后，将鼠标悬停在编辑器中的违规切换上，然后打开灯泡菜单。 或者，将光标放在行上，然后按**Ctrl**+**。** （句点）。

2. 从灯泡菜单中，选择 **"配置"或"禁止"配置**>**\<规则 ID>严重性**。

   ![在可视化工作室中从灯泡菜单配置规则严重性](media/configure-rule-severity.png)

3. 在此处，选择一个严重性选项。

   ![将规则严重性配置为建议](media/configure-rule-severity-suggestion.png)

   Visual Studio 向 Editor Config 文件添加一个条目，以将规则配置为请求的级别，如预览框中所示。

   > [!TIP]
   > 如果项目中还没有编辑器配置文件，Visual Studio 会为您创建一个。

##### <a name="configure-from-error-list"></a>从错误列表配置

Visual Studio 还提供一种从错误列表上下文菜单配置规则严重性操作的便捷方法。

1. 发生冲突后，右键单击错误列表中的诊断条目。

2. 在上下文菜单中，选择 **"设置严重性**"。

   ![在可视化工作室中从错误列表中配置规则严重性](media/configure-rule-severity-error-list.png)

3. 在此处，选择一个严重性选项。

   Visual Studio 向编辑器配置文件添加一个条目，以将规则配置为请求的级别。

   > [!TIP]
   > 如果项目中还没有编辑器配置文件，Visual Studio 会为您创建一个。

::: moniker-end

### <a name="set-rule-severity-from-solution-explorer"></a>从解决方案资源管理器设置规则严重性

1. 在解决方案资源管理器中，展开**引用** > **分析器**（或 .NET Core 项目**的依赖关系** > **分析器**）。

2. 展开包含要为其设置严重性的规则的程序集。

::: moniker range=">=vs-2019"
3. 右键单击规则并选择 **"设置严重性**"。 在上下文菜单中，选择其中一个严重性选项。

   Visual Studio 向编辑器配置文件添加一个条目，以将规则配置为请求的级别。 如果项目使用规则集文件而不是 Editor Config 文件，则严重性条目将添加到规则集文件中。

   > [!TIP]
   > 如果项目中还没有编辑器配置文件或规则集文件，Visual Studio 会为您创建新的编辑器配置文件。
::: moniker-end

::: moniker range="vs-2017"
3. 右键单击规则并选择 **"设置规则集严重性**"。 在上下文菜单中，选择其中一个严重性选项。

   规则的严重性保存在活动规则集文件中。
::: moniker-end

### <a name="set-rule-severity-in-the-rule-set-file"></a>在规则集文件中设置规则严重性

![解决方案资源管理器中的规则集文件](media/ruleset-in-solution-explorer.png)

1. 通过在**解决方案资源管理器**中双击活动规则集文件，在**引用** > **分析器**节点的右键单击菜单上选择 **"打开活动规则集"，** 或在项目**的代码分析**属性页上选择 **"打开"来打开**活动规则集文件。

   如果这是您第一次编辑规则集，Visual Studio 会复制默认规则集文件，将其*\<命名为>.ruleset，* 并将其添加到项目中。 此自定义规则集也将成为项目的活动规则集。

   > [!NOTE]
   > .NET Core 和 .NET 标准项目不支持**解决方案资源管理器**中规则集的菜单命令，例如，**打开活动规则集**。 要为 .NET Core 或 .NET 标准项目指定非默认规则集，请手动[将**代码分析规则集**属性添加到](using-rule-sets-to-group-code-analysis-rules.md#specify-a-rule-set-for-a-project)项目文件中。 您仍然可以在 Visual Studio 规则集编辑器 UI 中的规则集中配置规则。

1. 通过展开它包含的程序集浏览到规则。

1. 在"**操作"** 列中，选择要打开下拉列表的值，并从列表中选择所需的严重性。

   ![在编辑器中打开规则集文件](media/ruleset-file-in-editor.png)

## <a name="suppress-violations"></a>抑制违规行为

有多种方法可以禁止违反规则：

::: moniker range=">=vs-2019"

- 在**编辑器配置文件中**

  将严重性设置为`none`， 例如`dotnet_diagnostic.CA1822.severity = none`，

- 从 **"分析"** 菜单

  选择 **"分析** > **生成"和"抑制**菜单栏上的活动问题"以抑制所有当前冲突。 这有时称为"基线"。

::: moniker-end

::: moniker range="vs-2017"

- 从 **"分析"** 菜单

  选择 **"分析** > **运行代码分析"并抑制**菜单栏上的活动问题，以抑制所有当前冲突。 这有时称为"基线"。

::: moniker-end

- 从**解决方案资源管理器**

  将规则的严重性设置为 **"无**"。

- 从**规则集编辑器**

  取消选中其名称旁边的框或将 **"操作"** 设置为 **"无**"。

- 从**代码编辑器**

  将光标放在有冲突的代码行中，然后按**Ctrl**+**周期 （.）** 打开 **"快速操作"** 菜单。 在 **"源/在抑制文件"中选择****"抑制 CAXXXX"。** > 

  ![从快速操作菜单中抑制诊断](media/suppress-diagnostic-from-editor.png)

- 从**错误列表中**

  选择要禁止禁止的规则，然后右键单击并选择 **"在** > **源/抑制文件中"的"抑制"。**

  - 如果禁止在**源中**，则"**预览更改"** 对话框将打开并显示添加到源代码的 C# [#pragma警告](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-pragma-warning)或可视基本[#Disable警告](/dotnet/visual-basic/language-reference/directives/directives)指令的预览。

    ![在代码文件中添加#pragma警告的预览](media/pragma-warning-preview.png)

  - 如果选择 **"在禁止禁止文件"，** 则"**预览更改"** 对话框将打开并<xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute>显示添加到全局抑制文件中的属性的预览。

    ![将禁止抑制消息属性添加到抑制文件的预览](media/preview-changes-in-suppression-file.png)

  在 **"预览更改"** 对话框中，选择 **"应用**"。

  > [!NOTE]
  > 如果在**解决方案资源管理器**中看不到 **"抑制**"菜单选项，则冲突可能来自生成而不是实时分析。 **"错误列表**"显示实时代码分析和生成中的诊断或规则冲突。 由于生成诊断可能过时，例如，如果您已编辑代码以修复冲突但尚未重新生成，则无法从**错误列表**中禁止这些诊断。 来自实时分析（IntelliSense）的诊断始终与当前源处于最新状态，可以从**错误列表中**进行抑制。 要从所选内容中排除*生成*诊断，请将"**仅生成 + IntelliSense"** 的错误**列表**源筛选器切换到 **"仅 IntelliSense"。** 然后，选择要禁止的诊断并继续，如前面所述。
  >
  > ![可视化工作室中的错误列表源筛选器](media/error-list-filter.png)

## <a name="command-line-usage"></a>命令行使用

在命令行生成项目时，如果满足以下条件，则生成输出中将显示规则冲突：

- 分析仪作为 NuGet 包安装，而不是 VSIX 扩展。

- 项目代码中违反了一个或多个规则。

- 违反规则[的严重性](#rule-severity)设置为**警告**，在这种情况下，冲突不会导致生成失败，或者**错误**，在这种情况下，冲突会导致生成失败。

生成输出的详细程度不会影响是否显示规则冲突。 即使**具有安静的**详细程度，规则冲突也会出现在生成输出中。

> [!TIP]
> 如果您习惯于从命令行运行旧版分析，或者使用*FxCopd.exe*或通过 msbuild 使用**RunCodeAnalysis**标志，下面介绍如何使用代码分析器执行此操作。

要在使用 msbuild 生成项目时在命令行看到分析器冲突，请运行如下所示的命令：

```cmd
msbuild myproject.csproj /target:rebuild /verbosity:minimal
```

以下图像显示了生成包含分析器规则冲突的项目时的命令行生成输出：

![带规则冲突的 MSBuild 输出](media/command-line-build-analyzers.png)

## <a name="dependent-projects"></a>从属项目

在 .NET Core 项目中，如果向具有 NuGet 分析器的项目添加引用，则这些分析器也会自动添加到从属项目中。 要禁用此行为，例如，如果从属项目是单元测试项目，请通过设置私有资产属性，将 NuGet 包标记为引用项目的 *.csproj*或 *.vbproj*文件中的**私有：**

```xml
<PackageReference Include="Microsoft.CodeAnalysis.FxCopAnalyzers" Version="2.9.0" PrivateAssets="all" />
```

## <a name="see-also"></a>另请参阅

- [可视化工作室中的代码分析器概述](../code-quality/roslyn-analyzers-overview.md)
- [提交代码分析器错误](https://github.com/dotnet/roslyn-analyzers/issues)
- [使用规则集](../code-quality/using-rule-sets-to-group-code-analysis-rules.md)
- [禁止代码分析警告](../code-quality/in-source-suppression-overview.md)
