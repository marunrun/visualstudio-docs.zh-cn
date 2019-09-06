---
title: 使用 editorconfig 配置 FxCop 分析器
ms.date: 03/11/2019
ms.topic: conceptual
helpviewer_keywords:
- FxCop analyzers, configuring
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 68c175a55c9e60e870a5466a831aaae50d62dced
ms.sourcegitcommit: 9c07ae6fb18204ea080c8248994a683fa12e5c82
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2019
ms.locfileid: "70293451"
---
# <a name="configure-fxcop-analyzers"></a>配置 FxCop 分析器

[FxCop 分析器](install-fxcop-analyzers.md)包含来自旧分析的最重要的 "FxCop" 规则，转换为基于 .NET Compiler Platform 的代码分析器。 可以通过两种方式配置 FxCop 代码分析器：

- 使用[规则集](#fxcop-analyzer-rule-sets)，可以启用或禁用规则并设置各个规则冲突的严重性。

- 从[CodeAnalysis FxCopAnalyzers](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers) NuGet 包的版本2.6.3 开始，通过[editorconfig 文件](#editorconfig-file)。 [可配置选项](fxcop-analyzer-options.md)使你可以优化基本代码的哪些部分进行分析。

> [!TIP]
> 有关旧版分析和 FxCop 分析器之间的差异的信息，请参阅[FxCop 分析器常见问题解答](fxcop-analyzers-faq.md)。

## <a name="fxcop-analyzer-rule-sets"></a>FxCop 分析器规则集

配置 FxCop 分析器的一种方法是使用 XML*规则集*。 规则集是用于标识目标问题和特定条件的代码分析规则的分组。 规则集使你可以启用或禁用规则并设置各个规则冲突的严重性。

FxCop 分析器 NuGet 包包含以下规则类别的预定义规则集：

- 设计
- 文档
- 可维护性
- 命名
- 性能
- 可靠性
- 安全性
- 用法

有关详细信息，请参阅[代码分析器的规则集](analyzer-rule-sets.md)。

## <a name="editorconfig-file"></a>EditorConfig 文件

可以通过将键值对添加到[editorconfig](https://editorconfig.org)文件来配置 FxCop 分析器规则。 配置文件可以[特定于项目，](#per-project-configuration)也可以在两个或多个项目之间[共享](#shared-configuration)。

> [!NOTE]
> 不能通过使用 editorconfig 文件来配置旧的 FxCop 规则。

### <a name="per-project-configuration"></a>每项目配置

若要为特定项目启用基于 editorconfig 的分析器配置，请将*editorconfig*文件添加到项目的根目录。

> [!TIP]
> 可以通过在**解决方案资源管理器**中右键单击项目，然后选择 "**添加** > **新项**"，将 editorconfig 文件添加到项目。 在 "**添加新项**" 窗口中，在 "搜索" 框中输入**editorconfig** 。 选择 " **Editorconfig 文件（默认）** " 模板，然后选择 "**添加**"。
>
> ![在 Visual Studio 中将 editorconfig 项添加到项目](media/add-editorconfig-file.png)

目前，对于在不同目录级别（例如，解决方案和项目级别）存在的 "组合" editorconfig 文件，不提供分层支持。

### <a name="shared-configuration"></a>共享配置

可以在两个或多个项目之间共享用于 FxCop 分析器配置的 editorconfig 文件，但需要执行一些附加步骤。

1. 将*editorconfig*文件保存到常见位置。

2. 创建具有以下内容的*属性*文件：

   ```xml
   <Project DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
     <PropertyGroup>
       <SkipDefaultEditorConfigAsAdditionalFile>true</SkipDefaultEditorConfigAsAdditionalFile>
     </PropertyGroup>
     <ItemGroup Condition="Exists('<your path>\.editorconfig')" >
       <AdditionalFiles Include="<your path>\.editorconfig" />
     </ItemGroup>
   </Project>
   ```

3. 向 *.csproj*或 *.vbproj*文件添加一行，以导入在上一步中创建的*属性*文件。 必须将此行置于导入 FxCop*属性*文件的任何行之前。 例如，如果你的属性文件命名为*editorconfig。属性*：

   ```xml
   ...
   <Import Project="..\..\editorconfig.props" Condition="Exists('..\..\editorconfig.props')" />
   <Import Project="..\packages\Microsoft.CodeAnalysis.FxCopAnalyzers.2.6.3\build\Microsoft.CodeAnalysis.FxCopAnalyzers.props" Condition="Exists('..\packages\Microsoft.CodeAnalysis.FxCopAnalyzers.2.6.3\build\Microsoft.CodeAnalysis.FxCopAnalyzers.props')" />
   ...
   ```

4. 重新加载项目。

> [!NOTE]
> 此处所述的 EditorConfig 文件的任意共享位置仅适用于配置 FxCop 分析器。 对于其他设置，如缩进和代码样式，EditorConfig 文件必须始终放置在项目文件夹或父文件夹中。

## <a name="option-scopes"></a>选项作用域

每个选项均可针对规则的类别（例如，命名或设计）或特定规则进行配置。

### <a name="all-rules"></a>所有规则

为所有规则配置选项的语法如下所示：

|语法|示例|
|-|-|
| dotnet_code_quality.OptionName = OptionValue | `dotnet_code_quality.api_surface = public` |

### <a name="category-of-rules"></a>规则类别

为规则*类别*（如命名、设计或性能）配置选项的语法如下所示：

|语法|示例|
|-|-|
| dotnet_code_quality.RuleCategory. OptionName = OptionValue | `dotnet_code_quality.Naming.api_surface = public` |

### <a name="specific-rule"></a>特定规则

为特定规则配置选项的语法如下所示：

|语法|示例|
|-|-|
| dotnet_code_quality.RuleId. OptionName = OptionValue | `dotnet_code_quality.CA1040.api_surface = public` |

## <a name="see-also"></a>请参阅

- [分析器配置](https://github.com/dotnet/roslyn-analyzers/blob/master/docs/Analyzer%20Configuration.md)
- [FxCop 分析器](install-fxcop-analyzers.md)
- [适用于 EditorConfig 的 .NET 编码约定](../ide/editorconfig-code-style-settings-reference.md)
