---
title: 使用 editorconfig 配置 FxCop 分析器
ms.date: 09/23/2019
ms.topic: conceptual
helpviewer_keywords:
- FxCop analyzers, configuring
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 182042db9a744d037e295a8448f8c49a9c7b3a97
ms.sourcegitcommit: d20ce855461c240ac5eee0fcfe373f166b4a04a9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2020
ms.locfileid: "84184791"
---
# <a name="configure-fxcop-analyzers"></a>配置 FxCop 分析器

[FxCop 分析器包](install-fxcop-analyzers.md)包含从旧分析转换为基于 .NET Compiler Platform 的代码分析器的最重要的 "FxCop" 规则。 对于某些 FxCop 规则，你可以通过[可配置的选项](fxcop-analyzer-options.md)来优化应应用的基本代码部分。 每个选项都通过将键值对添加到[EditorConfig](https://editorconfig.org)文件来指定。 配置文件可以[特定于项目，](#per-project-configuration)也可以在两个或多个项目之间[共享](#shared-configuration)。

> [!TIP]
> 在**解决方案资源管理器**中右键单击项目，然后选择 "**添加**  >  **新项**"，将 editorconfig 文件添加到项目。 在 "**添加新项**" 窗口中，在 "搜索" 框中输入**editorconfig** 。 选择 " **Editorconfig 文件（默认）** " 模板，然后选择 "**添加**"。
>
> ![在 Visual Studio 中将 editorconfig 文件添加到项目](media/add-editorconfig-file.png)

::: moniker range=">=vs-2019"

有关配置规则的严重性（例如，是错误还是警告）的信息，请参阅[在 EditorConfig 文件中设置规则严重性](use-roslyn-analyzers.md#set-rule-severity-in-an-editorconfig-file)。 或者，可以选择一个内置的[EditorConfig 文件或规则集](analyzer-rule-sets.md)来快速启用或禁用一类规则。

::: moniker-end

本文的其余部分将讨论优化 FxCop 规则应用位置的[选项](fxcop-analyzer-options.md)的常规语法。

> [!NOTE]
> 不能通过使用 EditorConfig 文件来配置旧的 FxCop 规则。 有关旧版分析和 FxCop 分析器之间的差异的信息，请参阅[FxCop 分析器常见问题解答](fxcop-analyzers-faq.md)。

## <a name="option-scopes"></a>选项作用域

每个优化选项均可针对规则的类别（例如，命名或设计）或特定规则配置。

### <a name="all-rules"></a>┮Τ砏玥

为*所有*规则配置选项的语法如下所示：

|语法|示例|
|-|-|
| dotnet_code_quality。OptionName = OptionValue | `dotnet_code_quality.api_surface = public` |

### <a name="category-of-rules"></a>规则类别

为规则*类别*（如命名、设计或性能）配置选项的语法如下所示：

|语法|示例|
|-|-|
| dotnet_code_quality。RuleCategory. OptionName = OptionValue | `dotnet_code_quality.Naming.api_surface = public` |

### <a name="specific-rule"></a>特定规则

为*特定*规则配置选项的语法如下所示：

|语法|示例|
|-|-|
| dotnet_code_quality。RuleId. OptionName = OptionValue | `dotnet_code_quality.CA1040.api_surface = public` |

## <a name="enabling-editorconfig-based-configuration"></a>启用基于 Editorconfig 的配置

### <a name="vs2019-163-and-later--fxcopanalyzers-package-version-33x-and-later"></a>VS2019 16.3 及更高版本 + FxCopAnalyzers 包版本 3.3. x 和更高版本

可以为以下作用域启用基于 EditorConfig 的分析器配置：

- 特定文档
- 特定文件夹
- 特定项目
- 特定解决方案
- 整个存储库

若要启用配置，请使用相应目录中的选项添加*editorconfig*文件。 此文件还可以包含基于 EditorConfig 的诊断严重性配置条目。 请参阅[此处](use-roslyn-analyzers.md#rule-severity)提供的更多详细信息。

### <a name="prior-to-vs2019-163-or-using-an-fxcopanalyzers-package-version-prior-to-33x"></a>在 VS2019 16.3 之前，或使用 3.3. x 之前的 FxCopAnalyzers 包版本

#### <a name="per-project-configuration"></a>每项目配置

若要为特定项目启用基于 EditorConfig 的分析器配置，请将*EditorConfig*文件添加到项目的根目录。

#### <a name="shared-configuration"></a>共享配置

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
> 此处所述的 EditorConfig 文件的任意共享位置仅适用于配置某些 FxCop 分析器规则的作用域。 对于其他设置，如 "规则严重性"、"常规编辑器设置" 和 "代码样式"，EditorConfig 文件必须始终放置在项目文件夹或父文件夹中。

## <a name="see-also"></a>请参阅

- [FxCop 分析器的规则作用域选项](fxcop-analyzer-options.md)
- [分析器配置](https://github.com/dotnet/roslyn-analyzers/blob/master/docs/Analyzer%20Configuration.md)
- [FxCop 分析器](install-fxcop-analyzers.md)
- [适用于 EditorConfig 的 .NET 编码约定](../ide/editorconfig-code-style-settings-reference.md)
