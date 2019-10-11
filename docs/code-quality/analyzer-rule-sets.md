---
title: FxCop 分析器规则集和 editorconfig 文件
ms.date: 10/08/2019
ms.topic: conceptual
helpviewer_keywords:
- analyzer packages, rule sets
- rule sets for analyzers
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c8602483554ebd311ab6eebb13ff8d2de00d7e09
ms.sourcegitcommit: b23d73c86ec7720c4cd9a58050860bc559623a3d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2019
ms.locfileid: "72172783"
---
# <a name="enable-a-category-of-rules"></a>启用规则类别

分析器包可能包含预定义的[EditorConfig](use-roslyn-analyzers.md#set-rule-severity-in-an-editorconfig-file)和[规则集](using-rule-sets-to-group-code-analysis-rules.md)文件，使你能够快速轻松地启用一类规则，如安全性或设计规则。 [CodeAnalysis. FxCopAnalyzers](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers/) NuGet 分析器包包括两个规则集（从版本2.6.2 开始）和 EditorConfig 文件（从版本2.9.5 开始）。 通过启用特定类别的规则，可以确定目标问题和特定条件。

> [!NOTE]
> 从 Visual Studio 2019 16.3 版开始，支持使用 EditorConfig 文件启用分析器规则并设置其严重性。

FxCop 分析器 NuGet 包包含以下规则类别的预定义规则集和 EditorConfig 文件：

- 所有规则
- 数据流
- 设计
- 文档
- 全球化
- 互操作性
- 易
- 命名
- 性能
- 从 FxCop 移植
- 可靠性
- 安全性
- 用法

每类规则都有一个 EditorConfig 或规则集文件，用于：

- 启用类别中的所有规则（并禁用所有其他规则）
- 使用每个规则的默认严重性和启用设置（并禁用所有其他规则）

> [!TIP]
> "所有规则" 类别具有一个附加的 EditorConfig 或规则集文件，用于禁用所有规则。 使用此文件可快速删除项目中的任何分析器警告或错误。

> [!TIP]
> 如果要从旧的 "FxCop" 分析迁移到基于 .NET Compiler Platform 的代码分析，则可以使用 EditorConfig 和规则集文件继续使用与[之前使用的](rule-set-reference.md)规则相同的规则配置。

## <a name="predefined-editorconfig-files"></a>预定义的 EditorConfig 文件

FxCopAnalyzers 分析器包的预定义 EditorConfig 文件位于 *% USERPROFILE% \\ 中。 nuget\packages\microsoft.codeanalysis.fxcopanalyzers @ no__t-2 @ no__t-3version @ no__t-4\editorconfig*目录。 例如，启用所有安全规则的 EditorConfig 文件位于 *% USERPROFILE% \\. nuget\packages\microsoft.codeanalysis.fxcopanalyzers @ no__t-2 @ no__t-3version @ no__t-4\editorconfig\SecurityRulesEnabled @ no__editorconfig*。

将所选的 editorconfig 文件复制到项目的根目录。

## <a name="predefined-rule-sets"></a>预定义规则集

CodeAnalysis. FxCopAnalyzers 分析器包的预定义规则集文件位于 *% USERPROFILE% \\. nuget\packages\microsoft.codeanalysis.fxcopanalyzers @ no__t-2 @ no__t-3version @ no__t-4\rulesets*文件夹. 例如，启用所有安全规则的规则集文件位于 *% USERPROFILE% @no__t-nuget\packages\microsoft.codeanalysis.fxcopanalyzers @ no__t-2 @ no__t-3version @ no__t-4\rulesets\SecurityRulesEnabled.ruleset*。

复制一个或多个规则集，并将其粘贴到包含你的 Visual Studio 项目或直接**解决方案资源管理器**的目录中。

你还可以[自定义预定义的规则集](how-to-create-a-custom-rule-set.md)，并将其设置为首选项。 例如，你可以更改一个或多个规则的严重性，使冲突在**错误列表**中显示为错误或警告。

### <a name="set-the-active-rule-set"></a>设置活动规则集

设置活动规则集的过程稍有不同，具体取决于你是否有 .NET Core/.net Standard 项目或 .NET Framework 项目。

#### <a name="net-core"></a>.NET Core

若要将规则设置为在 .NET Core 或 .NET Standard 项目中进行分析，请手动将**CodeAnalysisRuleSet**属性添加到项目文件。 例如，以下代码片段将 `HelloWorld.ruleset` 设置为活动规则集。

```xml
<PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|AnyCPU' ">
  ...
  <CodeAnalysisRuleSet>HelloWorld.ruleset</CodeAnalysisRuleSet>
</PropertyGroup>
```

#### <a name="net-framework"></a>.NET Framework

若要将规则设置为 .NET Framework 项目中的分析的活动规则集：

- 右键单击 "**解决方案资源管理器**中的项目，然后选择"**属性**"。

- 在项目属性页中，选择 "**代码分析**" 选项卡。

::: moniker range="vs-2017"

- 在 "**运行此规则集**" 下，选择 "**浏览**"，然后选择已复制到项目目录的所需规则集。

::: moniker-end

::: moniker range=">=vs-2019"

- 在 "**活动规则**" 下，选择 "**浏览**"，然后选择已复制到项目目录的所需规则集。

::: moniker-end

   现在，你只会看到在所选规则集中启用的那些规则的规则冲突。

## <a name="see-also"></a>请参阅

- [分析器常见问题解答](analyzers-faq.md)
- [.NET Compiler Platform 分析器概述](roslyn-analyzers-overview.md)
- [安装分析器](install-roslyn-analyzers.md)
- [配置分析器](use-roslyn-analyzers.md)
- [使用规则集对代码分析规则进行分组](using-rule-sets-to-group-code-analysis-rules.md)
