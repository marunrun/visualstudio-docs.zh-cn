---
title: 分析器规则严重性和禁止显示
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
ms.openlocfilehash: edb9cb30be9d62a533e6d011cbb8d0436ef898b1
ms.sourcegitcommit: a801ca3269274ce1de4f6b2c3f40b58bbaa3f460
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/25/2020
ms.locfileid: "88801602"
---
# <a name="use-code-analyzers"></a>使用代码分析器

.NET Compiler Platform ( "Roslyn" ) 代码分析器在你键入时分析 c # 或 Visual Basic 代码。 每个 *诊断* 或规则都有一个默认严重性和隐含状态，可以覆盖你的项目。 本文介绍如何设置规则严重性，如何使用规则集和取消冲突。

## <a name="analyzers-in-solution-explorer"></a>解决方案资源管理器中的分析器

您可以从 **解决方案资源管理器**中进行大多数的分析器诊断自定义。 如果以 NuGet 包的形式[安装分析器](../code-quality/install-roslyn-analyzers.md)，则**分析器**节点会出现在**解决方案资源管理器**中的 "**引用**" 或 "**依赖项**" 节点下。 如果你展开分析器，然后展开一个分析器程序 **集，则**会在程序集中看到所有诊断。

![解决方案资源管理器中的分析器节点](media/analyzers-expanded-in-solution-explorer.png)

您可以在 " **属性** " 窗口中查看诊断的属性，包括其说明和默认严重性。 若要查看属性，请右键单击 (或选择并按住规则) 并选择 "**属性**"，或选择规则，然后选择 " **Alt** + **Enter**"。

![属性窗口中的诊断属性](media/analyzer-diagnostic-properties.png)

若要查看诊断的联机文档，请右键单击 (或选择并按住诊断) ，然后选择 " **查看帮助**"。

**解决方案资源管理器**中的每个诊断旁边的图标对应于在编辑器中打开的规则集中显示的图标：

- 圆圈中的 "x" 表示[严重性](#rule-severity)为 "**错误**"
- 三角形中的 "！" 表示[严重性](#rule-severity)为 "**警告**"
- 圆圈中的 "i" 表示**信息**的[严重性](#rule-severity)
- 浅灰色背景上的圆圈中的 "i" 表示 [严重性](#rule-severity) 为 **隐藏**
- 圆圈中的向下箭头表示诊断被取消

![解决方案资源管理器中的诊断图标](media/diagnostics-icons-solution-explorer.png)

## <a name="rule-severity"></a>规则严重性

::: moniker range=">=vs-2019"

如果将分析器作为 NuGet 包进行[安装](../code-quality/install-roslyn-analyzers.md)，则可以配置分析器规则或*诊断*的严重性。 从 Visual Studio 2019 版本16.3 开始，你可以 [在 EditorConfig 文件中](#set-rule-severity-in-an-editorconfig-file)配置规则的严重性。 你还可以 [从解决方案资源管理器](#set-rule-severity-from-solution-explorer) 或 [规则集文件中](#set-rule-severity-in-the-rule-set-file)更改规则的严重性。

::: moniker-end

::: moniker range="vs-2017"

如果将分析器作为 NuGet 包进行[安装](../code-quality/install-roslyn-analyzers.md)，则可以配置分析器规则或*诊断*的严重性。 你可以 [从解决方案资源管理器](#set-rule-severity-from-solution-explorer) 或 [规则集文件中](#set-rule-severity-in-the-rule-set-file)更改规则的严重性。

::: moniker-end

下表显示了不同的严重性选项：

| 严重性 (解决方案资源管理器)  | 严重性 (EditorConfig 文件)  | 生成时行为 | 编辑器行为 |
|-|-|-|
| 错误 | `error` | 冲突在错误列表和命令行生成输出中显示为 *错误* ，并导致生成失败。| 令人讨厌的代码带有红色波形曲线，并由滚动条中的小红色框标记。 |
| 警告 | `warning` | 冲突在错误列表和命令行生成输出中显示为 *警告* ，但不会导致生成失败。 | 令人讨厌的代码带有绿色波形曲线，并由滚动条中的小绿色框标记。 |
| 信息 | `suggestion` | 冲突显示为错误列表中的消息，而不是命令行生成输出中的 *消息* 。 | 令人讨厌的代码带有灰色波形曲线，并由滚动条中的小灰色框标记。 |
| Hidden | `silent` | 对用户不可见。 | 对用户不可见。 但会将诊断报告给 IDE 诊断引擎。 |
| 无 | `none` | 完全取消。 | 完全取消。 |
| 默认 | `default` | 对应于规则的默认严重性。 若要确定规则的默认值是什么，请查看属性窗口。 | 对应于规则的默认严重性。 |

代码编辑器的以下屏幕截图显示了三个不同严重性的不同冲突。 请注意右侧滚动条中的波形曲线颜色和小的彩色正方形。

![代码编辑器中的错误、警告和信息冲突](media/diagnostics-severity-colors.png)

以下屏幕截图显示的是错误列表中显示的三个冲突：

![错误列表中的错误、警告和信息冲突](media/diagnostics-severities-in-error-list.png)

::: moniker range=">=vs-2019"

### <a name="set-rule-severity-in-an-editorconfig-file"></a>在 EditorConfig 文件中设置规则严重性

 (Visual Studio 2019 版本16.3 及更高版本) 

你可以使用以下语法为 EditorConfig 文件中的编译器警告或分析器规则设置严重性：

`dotnet_diagnostic.<rule ID>.severity = <severity>`

在 EditorConfig 文件中设置规则的严重性优先于在规则集中或解决方案资源管理器中设置的任何严重性。 您可以在 EditorConfig 文件中 [手动](#manually-configure-rule-severity) 配置严重性，也可以通过在冲突旁显示的灯泡 [自动](#automatically-configure-rule-severity) 进行配置。

### <a name="set-rule-severity-of-multiple-analyzer-rules-at-once-in-an-editorconfig-file"></a>在 EditorConfig 文件中同时设置多个分析器规则的规则严重性

 (Visual Studio 2019 版本16.5 及更高版本) 

您可以使用 EditorConfig 文件中的单个条目为特定类别的分析器规则或所有分析器规则设置严重性。

- 为分析器规则类别设置规则严重性：

`dotnet_analyzer_diagnostic.category-<rule category>.severity = <severity>`

- 为所有分析器规则设置规则严重性：

`dotnet_analyzer_diagnostic.severity = <severity>`

如果你有多个适用于特定规则 ID 的条目，则选择适用项的优先顺序如下：

- 单个规则按 ID 的严重性条目优先于类别的严重性条目。
- 对于所有分析器规则，类别的严重性项优先于严重性项。

请考虑以下 EditorConfig 示例，其中 [CA1822](https://docs.microsoft.com/visualstudio/code-quality/ca1822) 的类别为 "Performance"：

   ```ini
   [*.cs]
   dotnet_diagnostic.CA1822.severity = error
   dotnet_analyzer_diagnostic.category-performance.severity = warning
   dotnet_analyzer_diagnostic.severity = suggestion
   ```

在前面的示例中，所有三个条目都适用于 CA1822。 但是，使用指定的优先规则，基于第一个规则 ID 的严重性条目将在下一条目上入选。 在此示例中，CA1822 的严重严重性为 "错误"。 所有 "性能" 类别的其余规则都将具有严重性 "警告"。 所有剩余的分析器规则（没有 "性能" 类别）都将具有严重性 "建议"。

#### <a name="manually-configure-rule-severity"></a>手动配置规则严重性

1. 如果你的项目还没有 EditorConfig 文件，则 [添加一个](../ide/create-portable-custom-editor-options.md#add-an-editorconfig-file-to-a-project)。

2. 在相应的文件扩展名下为要配置的每个规则添加一个条目。 例如，若要将 [CA1822](ca1822.md) 的严重性设置为 `error` c # 文件，该条目如下所示：

   ```ini
   [*.cs]
   dotnet_diagnostic.CA1822.severity = error
   ```

> [!NOTE]
> 对于 IDE 代码样式分析器，还可以使用不同的语法（例如）在 EditorConfig 文件中配置它们 `dotnet_style_qualification_for_field = false:suggestion` 。 但是，如果使用语法设置了严重性 `dotnet_diagnostic` ，则优先使用该语法。 有关详细信息，请参阅 [EditorConfig 的语言约定](../ide/editorconfig-language-conventions.md)。

#### <a name="convert-an-existing-ruleset-file-to-editorconfig-file"></a>将现有的规则集文件转换为 EditorConfig 文件

从 Visual Studio 2019 版本16.5 开始，规则集文件已弃用，以支持托管代码的分析器配置的 EditorConfig 文件。 大多数用于 analyzer 的 Visual Studio 工具规则严重性配置已更新为在 EditorConfig 文件而不是规则集文件上运行。 EditorConfig 文件允许配置分析器规则严重性和分析器选项，包括 Visual Studio IDE 代码样式选项。 强烈建议将现有的规则集文件转换为 EditorConfig 文件。 此外，建议将 EditorConfig 文件保存到存储库的根目录或解决方案文件夹中。 通过使用存储库或解决方案文件夹的根，可以确保将此文件中的严重性设置分别自动应用于整个存储库或解决方案。

有几种方法可以将现有的规则集文件转换为 EditorConfig 文件：

- 在 Visual Studio 中的规则集编辑器中 (需要 Visual Studio 2019 16.5 或更高版本) 。 如果你的项目已使用特定规则集文件作为其 `CodeAnalysisRuleSet` ，则可以通过 Visual Studio 中的 "规则集编辑器" 将其转换为等效的 EditorConfig 文件。

    1. 双击解决方案资源管理器中的规则集文件。

       规则集文件应在规则集编辑器中打开。 "规则集编辑器" 顶部应该会显示一个可单击的 **信息栏** 。

       ![在规则集编辑器中将规则集转换为 EditorConfig 文件](media/convert-ruleset-to-editorconfig-file-ruleset-editor.png)

    2. 选择 " **信息栏** " 链接。

       这将打开 " **另存为** " 对话框，该对话框允许您选择要在其中生成 EditorConfig 文件的目录。

    3. 选择 " **保存** " 按钮以生成 EditorConfig 文件。

       生成的 EditorConfig 应在编辑器中打开。 此外，MSBuild 属性 `CodeAnalysisRuleSet` 在项目文件中进行了更新，使其不再引用原始规则集文件。

- 通过命令行：

    1. 安装 NuGet 包 [CodeAnalysis. RulesetToEditorconfigConverter](https://www.nuget.org/packages/Microsoft.CodeAnalysis.RulesetToEditorconfigConverter)。

    2. `RulesetToEditorconfigConverter.exe`从已安装的包执行，其中包含作为命令行参数的规则集文件和 EditorConfig 文件的路径。

   ```
   Usage: RulesetToEditorconfigConverter.exe <%ruleset_file%> [<%path_to_editorconfig%>]
   ```

下面是要转换的示例规则集文件：

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

下面是转换后的 EditorConfig 文件：

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

Visual Studio 提供了一种简便的方法，可用于在 " [快速操作](../ide/quick-actions.md) " 灯泡菜单中配置规则的严重性。

1. 发生冲突后，将鼠标悬停在编辑器中的冲突波形曲线上，并打开灯泡菜单。 或者，将光标放在行上，然后按**Ctrl**键 + **。** （句点）。

2. 在灯泡菜单中，选择 " **配置" 或 "禁止显示问题** > **配置 \<rule ID> 严重级别**"。

   ![在 Visual Studio 中配置灯泡菜单中的规则严重性](media/configure-rule-severity.png)

3. 从此处选择一个严重性选项。

   ![将规则严重性配置为建议](media/configure-rule-severity-suggestion.png)

   Visual Studio 将向 EditorConfig 文件中添加一个条目，以将规则配置为请求的级别，如 "预览" 框中所示。

   > [!TIP]
   > 如果项目中还没有 EditorConfig 文件，则 Visual Studio 会为你创建一个。

##### <a name="configure-from-error-list"></a>从错误列表配置

Visual Studio 还提供了一种简便的方法来配置 "错误列表" 上下文菜单中的规则严重性。

1. 发生冲突后，右键单击 (或选择并按住) "错误列表" 中的诊断条目。

2. 从上下文菜单中，选择 " **设置严重性**"。

   ![在 Visual Studio 中从错误列表配置规则严重性](media/configure-rule-severity-error-list.png)

3. 从此处选择一个严重性选项。

   Visual Studio 将向 EditorConfig 文件中添加一个条目，以将规则配置为请求的级别。

   > [!TIP]
   > 如果项目中还没有 EditorConfig 文件，则 Visual Studio 会为你创建一个。

::: moniker-end

### <a name="set-rule-severity-from-solution-explorer"></a>设置解决方案资源管理器的规则严重性

1. 在解决方案资源管理器中，选择 "**引用**  >  **分析器**" (或 "适用于 .net Core 项目的**依赖项**  >  **分析器**) "。

2. 展开包含要为其设置严重性的规则的程序集。

::: moniker range=">=vs-2019"
3. 右键单击 (或选择并按住规则) 并选择 " **设置严重性**"。 在上下文菜单中，选择 "严重性" 选项之一。

   Visual Studio 将向 EditorConfig 文件中添加一个条目，以将规则配置为请求的级别。 如果你的项目使用规则集文件而不是 EditorConfig 文件，则会将严重性条目添加到规则集文件中。

   > [!TIP]
   > 如果项目中还没有 EditorConfig 文件或规则集文件，Visual Studio 会为你创建一个新的 EditorConfig 文件。
::: moniker-end

::: moniker range="vs-2017"
3. 右键单击 (或选择并按住规则) 并选择 " **设置规则集严重性**"。 在上下文菜单中，选择 "严重性" 选项之一。

   规则的严重性保存在活动规则集文件中。
::: moniker-end

### <a name="set-rule-severity-in-the-rule-set-file"></a>设置规则集文件中的规则严重性

![解决方案资源管理器中的规则集文件](media/ruleset-in-solution-explorer.png)

1. 通过以下方式之一打开活动规则集文件：

- 在**解决方案资源管理器**中，双击该文件，右键单击 (或选择并按住) **引用**  >  **分析器**节点，然后选择 "**打开活动规则集**"。
- 在项目的 " **代码分析** " 属性页上，选择 " **打开** "。

  如果这是你第一次编辑规则集，则 Visual Studio 会生成默认规则集文件的副本，并将其命名为* \<projectname> 规则*集，并将其添加到你的项目中。 此自定义规则集还会成为项目的活动规则集。

   > [!NOTE]
   > .NET Core 和 .NET Standard 项目不支持 **解决方案资源管理器**中规则集的菜单命令，例如， **打开活动规则集**。 若要为 .NET Core 或 .NET Standard 项目指定非默认规则集，请手动 [将 **CodeAnalysisRuleSet** 属性添加](using-rule-sets-to-group-code-analysis-rules.md#specify-a-rule-set-for-a-project) 到项目文件。 你仍可以在 Visual Studio 规则集编辑器 UI 中配置规则集内的规则。

1. 通过展开其包含的程序集，浏览到该规则。

1. 在 " **操作** " 列中，选择要打开下拉列表的值，并从列表中选择所需的严重性。

   ![已在编辑器中打开规则集文件](media/ruleset-file-in-editor.png)

::: moniker range=">=vs-2019"

## <a name="configure-generated-code"></a>配置生成的代码

分析器运行于项目中的所有源文件上，并在其上报告冲突。 但是，这些冲突对生成的代码文件（如设计器生成的代码文件、生成系统生成的临时源文件等）不起作用。用户无法手动编辑这些文件，并且/或者不关心修复这类工具生成文件中的冲突。

默认情况下，analyzer 驱动程序执行分析器会将具有特定名称、文件扩展名或自动生成的文件头的文件视为生成的代码文件。 例如，以或结尾的文件名被 `.designer.cs` `.generated.cs` 视为生成的代码。 但是，这些试探法可能无法确定用户源代码中所有自定义生成的代码文件。

从 Visual Studio 2019 16.5 开始，最终用户可以将特定的文件和/或文件夹配置为在 [EditorConfig 文件](https://editorconfig.org/)中被视为生成的代码。 按照以下步骤添加这样的配置：

1. 如果你的项目还没有 EditorConfig 文件，则 [添加一个](../ide/create-portable-custom-editor-options.md#add-an-editorconfig-file-to-a-project)。

2. 添加 `generated_code = true | false` 特定文件和/或文件夹的条目。 例如，若要将名称以结尾的所有文件视为 `.MyGenerated.cs` 生成的代码，该条目应如下所示：

   ```ini
   [*.MyGenerated.cs]
   generated_code = true
   ```

::: moniker-end

## <a name="suppress-violations"></a>禁止冲突

有多种方法可禁止规则冲突：

::: moniker range=">=vs-2019"

- 在**EditorConfig 文件**中

  将严重性设置为 `none` ，例如 `dotnet_diagnostic.CA1822.severity = none` 。

- 从 " **分析** " 菜单

  **Analyze**  >  在菜单栏上选择 "分析**生成并取消活动问题**" 可禁止显示所有当前冲突。 这有时称为 "基线"。

::: moniker-end

::: moniker range="vs-2017"

- 从 " **分析** " 菜单

  **Analyze**  >  在菜单栏上选择 "分析**运行代码分析" 和 "取消活动问题**"，禁止显示所有当前冲突。 这有时称为 "基线"。

::: moniker-end

- From **解决方案资源管理器**

  将规则的 "严重性" 设置为 " **无**"。

- 从 **规则集编辑器**

  清除其名称旁边的复选框，或将 " **操作** " 设置为 " **无**"。

- 从 **代码编辑器**

  将光标放在包含冲突的代码行中，然后选择 " **Ctrl** + **Period )  (** " 以打开 "**快速操作**" 菜单。 选择**Suppress CAXXXX**  >  **"在源/禁止显示文件中**取消 CAXXXX"。

  ![禁止显示 "快速操作" 菜单中的诊断](media/suppress-diagnostic-from-editor.png)

- 从 **错误列表**

  选择要禁止显示的规则，然后右键单击 (或选择并按住) ，然后选择 "在**Suppress**  >  **源/隐藏文件**中取消"。

  - 如果在 " **源" 中**取消，则会打开 " **预览更改** " 对话框，并显示 c # [#pragma 警告](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-pragma-warning) 或 Visual Basic 添加到源代码中 [#Disable 警告](/dotnet/visual-basic/language-reference/directives/directives) 指令的预览。

    ![在代码文件中添加 #pragma 警告的预览](media/pragma-warning-preview.png)

  - 如果选择 " **在禁止显示文件中**"，则将打开 " **预览更改** " 对话框，并显示 <xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> 添加到全局禁止显示文件的属性的预览。

    ![向禁止显示文件添加 SuppressMessage 属性的预览](media/preview-changes-in-suppression-file.png)

  在 " **预览更改** " 对话框中，选择 " **应用**"。

  > [!NOTE]
  > 如果在**解决方案资源管理器**中看不到 "**禁止显示**" 菜单选项，则可能是由于冲突而导致生成，而非实时分析。 **错误列表**显示来自实时代码分析和生成的诊断或规则冲突。 由于生成诊断可能已过时，例如，如果已编辑代码以修复冲突，但未重新生成，则无法从 **错误列表**中取消这些诊断。 来自实时分析或 IntelliSense 的诊断对于当前源始终是最新的，并且可以从 **错误列表**中抑制。 若要从所选内容中排除 *生成* 诊断，请将 **错误列表** 源筛选器从 " **生成** " 改为 " **仅**intellisense"。 然后，选择要禁止显示的诊断，并按照前面所述进行操作。
  >
  > ![在 Visual Studio 中错误列表源筛选器](media/error-list-filter.png)

## <a name="command-line-usage"></a>命令行用法

当你在命令行中生成项目时，如果满足以下条件，则会在生成输出中显示规则冲突：

- 分析器以 NuGet 包的形式安装，而不是作为 VSIX 扩展。

- 项目的代码中违反了一个或多个规则。

- 违反规则的 [严重性](#rule-severity) 设置为 " **警告**"，在这种情况下，冲突不会导致生成失败或 **错误**，在这种情况下，冲突会导致生成失败。

生成输出的详细级别不会影响是否显示规则冲突。 即使是具有 **安静** 详细级别，规则冲突也会出现在生成输出中。

> [!TIP]
> 如果你习惯于从命令行运行旧分析，无论是使用 *FxCopCmd.exe* 还是通过 **RunCodeAnalysis** 标志的 msbuild，下面介绍了如何使用代码分析器完成此操作。

若要在使用 msbuild 生成项目时在命令行上查看分析器冲突，请运行如下所示的命令：

```cmd
msbuild myproject.csproj /target:rebuild /verbosity:minimal
```

以下图像显示了生成包含分析器规则冲突的项目时的命令行生成输出：

![带规则冲突的 MSBuild 输出](media/command-line-build-analyzers.png)

## <a name="dependent-projects"></a>依赖项目

在 .NET Core 项目中，如果添加对包含 NuGet 分析器的项目的引用，则这些分析器也会自动添加到依赖项目。 若要禁用此行为，例如，如果依赖项目是单元测试项目，请通过设置**PrivateAssets**属性，在所引用项目的 *.csproj*或 *.vbproj*文件中将 NuGet 包标记为 private：

```xml
<PackageReference Include="Microsoft.CodeAnalysis.FxCopAnalyzers" Version="2.9.0" PrivateAssets="all" />
```

## <a name="see-also"></a>请参阅

- [Visual Studio 中的代码分析器概述](../code-quality/roslyn-analyzers-overview.md)
- [提交代码分析器 bug](https://github.com/dotnet/roslyn-analyzers/issues)
- [使用规则集](../code-quality/using-rule-sets-to-group-code-analysis-rules.md)
- [禁止显示代码分析警告](../code-quality/in-source-suppression-overview.md)
