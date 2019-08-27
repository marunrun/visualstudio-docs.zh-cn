---
title: 分析器规则严重性和禁止显示
ms.date: 03/26/2019
ms.topic: conceptual
helpviewer_keywords:
- code analysis, managed code
- analyzers
- Roslyn analyzers
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 6362d3f14065aaf9661e85266753642e4201ca48
ms.sourcegitcommit: 209ed0fcbb8daa1685e8d6b9a97f3857a4ce1152
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2019
ms.locfileid: "69548036"
---
# <a name="use-code-analyzers"></a>使用代码分析器

.NET Compiler Platform ("Roslyn") 代码分析器在你C#键入时分析或 Visual Basic 代码。 每个*诊断*或规则都有一个默认严重性和隐含状态, 可以覆盖你的项目。 本文介绍如何设置规则严重性, 如何使用规则集和取消冲突。

## <a name="analyzers-in-solution-explorer"></a>解决方案资源管理器中的分析器

您可以从**解决方案资源管理器**中进行大多数的分析器诊断自定义。 如果以 NuGet 包的形式[安装分析器](../code-quality/install-roslyn-analyzers.md), 则**分析器**节点会出现在**解决方案资源管理器**中的 "**引用**" 或 "**依赖项**" 节点下。 如果你展开分析器, 然后展开一个分析器程序集, 则会在程序集中看到所有诊断。

![解决方案资源管理器中的分析器节点](media/analyzers-expanded-in-solution-explorer.png)

您可以在 "**属性**" 窗口中查看诊断的属性, 包括其说明和默认严重性。 若要查看属性, 请右键单击规则, 然后选择 "**属性**", 或选择规则, 并按**Alt**+**enter**。

![属性窗口中的诊断属性](media/analyzer-diagnostic-properties.png)

若要查看诊断的联机文档, 请右键单击该诊断, 然后选择 "**查看帮助**"。

**解决方案资源管理器**中的每个诊断旁边的图标对应于在编辑器中打开的规则集中显示的图标:

- 圆圈中的 "i" 表示**信息**的[严重性](#rule-severity)
- 三角形中的 "!" 表示[严重性](#rule-severity)为 "**警告**"
- 圆圈中的 "x" 表示[严重性](#rule-severity)为 "**错误**"
- 浅灰色背景上的圆圈中的 "i" 表示[严重性](#rule-severity)为**隐藏**
- 圆圈中的向下箭头表示诊断被取消

![解决方案资源管理器中的诊断图标](media/diagnostics-icons-solution-explorer.png)

## <a name="rule-sets"></a>规则集

[规则集](../code-quality/using-rule-sets-to-group-code-analysis-rules.md)是一个 XML 文件, 用于存储单独诊断的严重性和隐含状态。

> [!NOTE]
> 规则集可以包括来自旧分析和代码分析器的规则。

若要在规则集编辑器中编辑活动规则集, 请在**解决方案资源管理器**中右键单击 "**引用** > **分析器**" 节点, 然后选择 "**打开活动规则集**"。 如果这是你首次编辑规则集, 则 Visual Studio 会生成默认规则集文件的副本, 并将其 *\<* 命名为项目名称 ">", 并将其添加到你的项目中。 此自定义规则集还会成为项目的活动规则集。

若要更改项目的活动规则集, 请导航到项目属性的 "**代码分析**" 选项卡。 从 "**运行此规则集**" 下的列表中选择规则集。 若要打开规则集, 请选择 "**打开**"。

> [!NOTE]
> .NET Core 和 .NET Standard 项目不支持**解决方案资源管理器**中规则集的菜单命令, 例如,**打开活动规则集**。 若要为 .NET Core 或 .NET Standard 项目指定非默认规则集, 请手动[将**CodeAnalysisRuleSet**属性添加](using-rule-sets-to-group-code-analysis-rules.md#specify-a-rule-set-for-a-project)到项目文件。 你仍可以在 Visual Studio 规则集编辑器 UI 中配置规则集内的规则。

## <a name="rule-severity"></a>规则严重性

如果将分析器作为 NuGet 包进行[安装](../code-quality/install-roslyn-analyzers.md), 则可以配置分析器规则或*诊断*的严重性。 下表显示了用于诊断的严重性选项:

|Severity|生成时行为|编辑器行为|
|-|-|-|
|Error|冲突在**错误列表**和命令行生成输出中显示为*错误*, 并导致生成失败。|出现问题的代码带有红色的波浪下划线, 并由滚动条中的小小框标记。|
|警告|冲突在**错误列表**和命令行生成输出中显示为*警告*, 但不会导致生成失败。|出现问题的代码带有绿色的波浪下划线, 并由滚动条中的小绿色框标记。|
|T:System.Diagnostics.Switch|冲突显示为**错误列表**中的消息, 而不是命令行生成输出中的*消息*。|令人讨厌的代码带灰色的波浪下划线, 并由滚动条中的小灰色框标记。|
|Hidden|对用户不可见。|对用户不可见。 但会将诊断报告给 IDE 诊断引擎。|
|无|完全取消。|完全取消。|

此外, 还可以通过将规则的严重性设置为**默认值**来将其重置。 每个诊断的默认严重性都可以在 "**属性**" 窗口中查看。

下面的屏幕截图显示了代码编辑器中三个不同的诊断冲突, 具有三个不同的严重性。 请注意弯曲的颜色, 以及右侧滚动条中的小框。

![代码编辑器中的错误、警告和信息冲突](media/diagnostics-severity-colors.png)

以下屏幕截图显示的是**错误列表**中显示的三个冲突:

![错误列表中的错误、警告和信息冲突](media/diagnostics-severities-in-error-list.png)

你可以从 "**解决方案资源管理器**" 或 "  *\<项目名称" > 规则集*文件中更改规则的严重性, 在**解决方案资源管理器**中更改规则的严重性后, 该文件将添加到解决方案中。

![解决方案资源管理器中的规则集文件](media/ruleset-in-solution-explorer.png)

### <a name="set-rule-severity-from-solution-explorer"></a>设置解决方案资源管理器的规则严重性

1. 在**解决方案资源管理器**，展开**引用** > **分析器**(**依赖关系** > **分析器**有关.NET Core 项目)。

1. 展开包含要为其设置严重性的规则的程序集。

1. 右键单击该规则, 然后选择 "**设置规则集严重性**"。 在 "弹出" 菜单中, 选择 "严重性" 选项之一。

   规则的严重性保存在活动规则集文件中。

### <a name="set-rule-severity-in-the-rule-set-file"></a>设置规则集文件中的规则严重性

1. 通过在 "**分析器**" 节点的右键单击菜单上, 选择 "**打开活动规则集**", 或在 "**代码分析**" 属性页上选择 "**打开**", 以打开[规则集](analyzer-rule-sets.md)文件**解决方案资源管理器**项目。

1. 通过展开其包含的程序集, 浏览到该规则。

1. 在 "**操作**" 列中, 选择要打开下拉列表的值, 并从列表中选择所需的严重性。

   ![已在编辑器中打开规则集文件](media/ruleset-file-in-editor.png)

## <a name="suppress-violations"></a>禁止冲突

有多种方法可禁止规则冲突:

- 从 "**分析**" 菜单

  在菜单栏上选择 "**分析** > **运行代码分析" 和 "取消活动问题**", 禁止显示所有当前冲突。 这有时称为 "基线"。

- From**解决方案资源管理器**

  若要在**解决方案资源管理器**中禁止发生冲突, 请将规则的 "严重性" 设置为 "**无**"。

- 从**规则集编辑器**

  若要取消规则集编辑器中的冲突, 请取消选中其名称旁的框, 或将 "**操作**" 设置为 "**无**"。

- 从**代码编辑器**

  若要禁止显示代码编辑器中的冲突, 请将光标放在包含冲突的代码行中, 然后按**Ctrl**+键 **。** 打开 "**快速操作**" 菜单。 选择 **"在源/禁止显示文件中** **取消 CAXXXX** > "。

  ![禁止显示 "快速操作" 菜单中的诊断](media/suppress-diagnostic-from-editor.png)

- 从**错误列表**

  您可以通过选择要取消的**错误列表**, 然后右键单击并选择 "在**源/隐藏文件**中**取消** > ", 来取消一个或多个诊断。

  - 如果在 "**源" 中**取消显示, 则 "**预览更改**" 对话框将打开C# , 并显示[#pragma 警告](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-pragma-warning)或 Visual Basic 添加到源代码中[#Disable 警告](/dotnet/visual-basic/language-reference/directives/directives)指令的预览。

    ![在代码文件中添加 #pragma 警告的预览](media/pragma-warning-preview.png)

  - 如果选择 "**在禁止显示文件中**", 则将打开 "**预览更改**" 对话框<xref:System.Diagnostics.CodeAnalysis.SuppressMessageAttribute> , 并显示添加到全局禁止显示文件的属性的预览。

    ![向禁止显示文件添加 SuppressMessage 属性的预览](media/preview-changes-in-suppression-file.png)

  在 "**预览更改**" 对话框中, 选择 "**应用**"。

  > [!NOTE]
  > 如果在**解决方案资源管理器**中看不到 "**禁止显示**" 菜单选项, 则可能是由于冲突而导致生成, 而非实时分析。 **错误列表**显示来自实时代码分析和生成的诊断或规则冲突。 由于生成诊断可能已过时, 例如, 如果已编辑代码以修复冲突, 但未重新生成, 则无法从**错误列表**中取消这些诊断。 来自实时分析或 IntelliSense 的诊断对于当前源始终是最新的, 并且可以从**错误列表**中抑制。 若要从所选内容中排除*生成*诊断, 请将**错误列表**源筛选器从 "**生成**" 改为 "**仅**intellisense"。 然后, 选择要禁止显示的诊断, 并按照前面所述进行操作。
  >
  > ![在 Visual Studio 中错误列表源筛选器](media/error-list-filter.png)

## <a name="command-line-usage"></a>命令行用法

当你在命令行中生成项目时, 如果满足以下条件, 则会在生成输出中显示规则冲突:

- 分析器以 Nuget 包的形式安装, 而不是作为 VSIX 扩展。

- 项目的代码中违反了一个或多个规则。

- 违反规则的[严重性](#rule-severity)设置为 "**警告**", 在这种情况下, 冲突不会导致生成失败或**错误**, 在这种情况下, 冲突会导致生成失败。

生成输出的详细级别不会影响是否显示规则冲突。 即使是具有**安静**详细级别, 规则冲突也会出现在生成输出中。

> [!TIP]
> 如果你习惯于从命令行运行旧分析, 无论是使用*FxCopCmd*还是使用**RunCodeAnalysis**标志的 msbuild, 下面介绍了如何使用代码分析器完成此操作。

若要在使用 msbuild 生成项目时在命令行上查看分析器冲突, 请运行如下所示的命令:

```cmd
msbuild myproject.csproj /target:rebuild /verbosity:minimal
```

下图显示了生成包含分析器规则冲突的项目的命令行生成输出:

![带规则冲突的 MSBuild 输出](media/command-line-build-analyzers.png)

## <a name="dependent-projects"></a>依赖项目

在.NET Core 项目中，如果添加对具有 NuGet 分析器的项目的引用这些分析器将自动添加到依赖项目太。 若要禁用此行为, 例如, 如果依赖项目是单元测试项目, 请通过设置**PrivateAssets**属性, 在所引用项目的 *.csproj*或 *.vbproj*文件中将 NuGet 包标记为 private:

```xml
<PackageReference Include="Microsoft.CodeAnalysis.FxCopAnalyzers" Version="2.9.0" PrivateAssets="all" />
```

## <a name="see-also"></a>请参阅

- [Visual Studio 中的代码分析器概述](../code-quality/roslyn-analyzers-overview.md)
- [提交代码分析器 bug](https://github.com/dotnet/roslyn-analyzers/issues)
- [使用规则集](../code-quality/using-rule-sets-to-group-code-analysis-rules.md)
- [禁止显示代码分析警告](../code-quality/in-source-suppression-overview.md)
