---
title: 代码分析规则集
ms.date: 04/02/2018
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.rulesets.learnmore
helpviewer_keywords:
- code analysis, rule sets
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 13a49f208fe3c60dfb8b9e20c83675cc43f1efb1
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75587168"
---
# <a name="use-rule-sets-to-group-code-analysis-rules"></a>使用规则集对代码分析规则进行分组

在 Visual Studio 中配置代码分析时，可以从内置*规则集*列表中进行选择。 规则集是一组代码分析规则，用于标识目标问题和该项目的特定条件。 例如，你可以应用一个规则集，设计用于扫描代码以实现公开可用的 Api。 还可以应用包含所有可用规则的规则集。

你可以通过添加或删除规则或将规则严重性更改为在**错误列表**中显示为警告或错误来自定义规则集。 自定义规则集可以满足特定开发环境的需求。 自定义规则集时，规则集编辑器会提供搜索和筛选工具，以帮助您在此过程中使用。

规则集可用于[托管代码分析](analyzer-rule-sets.md)、对[托管代码的传统分析](how-to-configure-code-analysis-for-a-managed-code-project.md)和[ C++代码分析](using-rule-sets-to-specify-the-cpp-rules-to-run.md)。

## <a name="rule-set-format"></a>规则集格式

规则集是以 XML 格式*指定的规则集文件。* 由 ID 和*操作*组成的规则按文件中的分析器 ID 和命名空间分组。

*规则集*文件的内容类似于以下 XML：

```xml
<RuleSet Name="Rules for Hello World project" Description="These rules focus on critical issues for the Hello World app." ToolsVersion="10.0">
  <Localization ResourceAssembly="Microsoft.VisualStudio.CodeAnalysis.RuleSets.Strings.dll" ResourceBaseName="Microsoft.VisualStudio.CodeAnalysis.RuleSets.Strings.Localized">
    <Name Resource="HelloWorldRules_Name" />
    <Description Resource="HelloWorldRules_Description" />
  </Localization>
  <Rules AnalyzerId="Microsoft.Analyzers.ManagedCodeAnalysis" RuleNamespace="Microsoft.Rules.Managed">
    <Rule Id="CA1001" Action="Warning" />
    <Rule Id="CA1009" Action="Warning" />
    <Rule Id="CA1016" Action="Warning" />
    <Rule Id="CA1033" Action="Warning" />
  </Rules>
  <Rules AnalyzerId="Microsoft.CodeQuality.Analyzers" RuleNamespace="Microsoft.CodeQuality.Analyzers">
    <Rule Id="CA1802" Action="Error" />
    <Rule Id="CA1814" Action="Info" />
    <Rule Id="CA1823" Action="None" />
    <Rule Id="CA2217" Action="Warning" />
  </Rules>
</RuleSet>
```

> [!TIP]
> 在图形**规则集编辑器**中[编辑规则集](../code-quality/working-in-the-code-analysis-rule-set-editor.md)比使用手动更容易。

## <a name="specify-a-rule-set-for-a-project"></a>为项目指定规则集

项目的规则集由 Visual Studio 项目文件中的**CodeAnalysisRuleSet**属性指定。 例如：

```xml
<PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|AnyCPU' ">
  ...
  <CodeAnalysisRuleSet>HelloWorld.ruleset</CodeAnalysisRuleSet>
</PropertyGroup>
```

## <a name="see-also"></a>另请参阅

- [代码分析规则集参考](../code-quality/rule-set-reference.md)
