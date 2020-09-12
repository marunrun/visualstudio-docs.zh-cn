---
title: 使用 editorconfig 配置 .NET 代码质量分析器
ms.date: 09/01/2020
ms.topic: conceptual
helpviewer_keywords:
- .NET analyzers
- FxCop analyzers, configuring
- code quality
author: mikadumont
ms.author: midumont
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: bc237082ec1188d71241facead975db1df2cf3af
ms.sourcegitcommit: 4ae5e9817ad13edd05425febb322b5be6d3c3425
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90035425"
---
# <a name="configure-net-code-quality-analysis-with-editorconfig"></a>通过 EditorConfig 配置 .NET 代码质量分析

每个代码质量分析器 (其规则 Id 以) 开头的代码 `CA` ，可以通过可配置选项进行优化，以应用于基本代码部分。 每个选项都通过将键值对添加到 [EditorConfig](https://editorconfig.org) 文件来指定。 配置文件可以特定于文件、项目、解决方案或整个存储库。

> [!TIP]
> 在**解决方案资源管理器**中右键单击项目，然后选择 "**添加**  >  **新项**"，将 editorconfig 文件添加到项目。 在 " **添加新项** " 窗口中，在 "搜索" 框中输入 **editorconfig** 。 选择 **Editorconfig 文件 (默认) ** 模板，然后选择 " **添加**"。
>
> ![在 Visual Studio 中将 EditorConfig 文件添加到项目](media/add-editorconfig-file.png)

::: moniker range=">=vs-2019"

有关配置规则的严重性 (例如，是错误还是警告) 的信息，请参阅 [在 EditorConfig 文件中设置规则严重性](use-roslyn-analyzers.md#set-rule-severity-in-an-editorconfig-file)。 或者，可以选择一个内置的 [EditorConfig 文件或规则集](analyzer-rule-sets.md) 来快速启用或禁用一类规则。

::: moniker-end

本文的其余部分将讨论优化 .NET 代码质量分析器应用于的选项的常规语法。

## <a name="option-scopes"></a>选项作用域

每个优化选项可针对所有规则进行配置，适用于一类规则 (例如，安全或设计) 或特定规则。

### <a name="all-rules"></a>┮Τ砏玥

为 *所有* 规则配置选项的语法如下所示：

|语法|示例|
|-|-|
| dotnet_code_quality。OptionName = OptionValue | `dotnet_code_quality.api_surface = public` |

### <a name="category-of-rules"></a>规则类别

为规则 *类别* 配置选项的语法 (如命名、设计或性能) ，如下所示：

|语法|示例|
|-|-|
| dotnet_code_quality。RuleCategory. OptionName = OptionValue | `dotnet_code_quality.Naming.api_surface = public` |

### <a name="specific-rule"></a>特定规则

为 *特定* 规则配置选项的语法如下所示：

|语法|示例|
|-|-|
| dotnet_code_quality。RuleId. OptionName = OptionValue | `dotnet_code_quality.CA1040.api_surface = public` |

## <a name="enabling-editorconfig-based-configuration"></a>启用基于 EditorConfig 的配置

可以为以下作用域启用基于 EditorConfig 的分析器配置：

- 特定文档 (s) 
- 特定文件夹 (s) 
- 特定项目 (s) 
- 特定解决方案 (s) 
- 整个存储库

若要启用配置，请使用相应目录中的选项添加 *editorconfig* 文件。 此文件还可以包含基于 EditorConfig 的诊断严重性配置条目。 请参阅[此处](use-roslyn-analyzers.md#configure-severity-levels)了解详细信息。

## <a name="enable-a-category-of-rules"></a>启用一种类别的规则

分析器包可能包含预定义的 [EditorConfig](use-roslyn-analyzers.md#configure-severity-levels) 和/或 [规则集](using-rule-sets-to-group-code-analysis-rules.md) 文件，使你能够快速轻松地启用一类规则，如安全性或设计规则。 [CodeAnalysis. NetAnalyzers](https://github.com/dotnet/roslyn-analyzers#microsoftcodeanalysisnetanalyzers) NuGet 分析器包同时包含 EditorConfig 文件和规则集。 通过启用特定类别的规则，可以确定目标问题和特定条件。

> [!NOTE]
> 从 Visual Studio 2019 16.3 版开始，支持使用 EditorConfig 文件启用分析器规则并设置其严重性。

NetAnalyzers NuGet 包包含以下规则类别的预定义 EditorConfig 文件和规则集：

- ┮Τ砏玥
- 数据流
- 设计
- 文档
- 全球化
- 互操作性
- 可维护性
- 命名
- 性能
- 从 FxCop 移植
- 可靠性
- 安全性
- 使用情况

每类规则都有一个 EditorConfig 或规则集文件，用于：

- 启用类别 (中的所有规则，并禁用所有其他规则) 
- 使用每个规则的默认严重性并默认启用 (设置并禁用所有其他规则) 

> [!TIP]
> "所有规则" 类别具有一个附加的 EditorConfig 或规则集文件，用于禁用所有规则。 使用此文件可快速删除项目中的任何分析器警告或错误。

> [!TIP]
> 如果要从旧的 "FxCop" 分析迁移到基于 .NET Compiler Platform 的代码分析，则可以使用 EditorConfig 和规则集文件继续使用与 [之前使用的](rule-set-reference.md)规则相同的规则配置。

## <a name="predefined-editorconfig-files"></a>预定义的 EditorConfig 文件

NetAnalyzers 分析器包的预定义 EditorConfig 文件位于 *% USERPROFILE% \\ . nuget\packages\microsoft.codeanalysis.netanalyzers \\ \<version\> \editorconfig*目录中。 例如，启用所有安全规则的 EditorConfig 文件位于 *% USERPROFILE% \\ . nuget\packages\microsoft.codeanalysis.netanalyzers \\ \<version\> \editorconfig\SecurityRulesEnabled \\ . EditorConfig*。

将所选的 editorconfig 文件复制到项目的根目录。

## <a name="predefined-rule-sets"></a>预定义规则集

CodeAnalysis. NetAnalyzers 分析器包的预定义规则集文件位于 *% USERPROFILE% \\ . nuget\packages\microsoft.codeanalysis.netanalyzers \\ \<version\> \rulesets*目录中。 例如，启用所有安全规则的规则集文件位于 *% USERPROFILE% \\ . nuget\packages\microsoft.codeanalysis.netanalyzers \\ \<version\> \rulesets\SecurityRulesEnabled.ruleset*。

复制一个或多个规则集，并将其粘贴到包含你的 Visual Studio 项目或直接 **解决方案资源管理器**的目录中。

你还可以 [自定义预定义的规则集](how-to-create-a-custom-rule-set.md) ，并将其设置为首选项。 例如，你可以更改一个或多个规则的严重性，使冲突在 **错误列表**中显示为错误或警告。


## <a name="rule-scope-options-for-net-code-quality-analyzers"></a>.NET 代码质量分析器的规则作用域选项

可以在 [EditorConfig 文件](../ide/create-portable-custom-editor-options.md#add-an-editorconfig-file-to-a-project)中指定选项。 例如，可以指定以下选项。

> [!TIP]
> 若要查看可用选项的完整列表，请参阅此 [分析器 Configuration.md 文件](https://github.com/dotnet/roslyn-analyzers/blob/master/docs/Analyzer%20Configuration.md)。 下面是一个示例，说明如何在 *Analyzer Configuration.md* 文件中记录一个选项：
>
> 选项名称： `sufficient_IterationCount_for_weak_KDF_algorithm`\
> 选项值：整数值 \
> 默认值：默认情况下，每个可配置规则 ( "100000"，默认情况下，大多数规则) \
> 示例： `dotnet_code_quality.CA5387.sufficient_IterationCount_for_weak_KDF_algorithm = 100000`

## <a name="api_surface"></a>api_surface

| 描述 | 允许的值 | 默认值 | 可配置规则 |
| - | - | - | - |
| 要分析的 API 面部分 | `public`<br/>`internal` 或 `friend`<br/>`private`<br/>`all`<br/><br/>使用逗号 ( 分隔多个值，)  | `public` | [CA1000](ca1000.md) [CA1003](ca1003.md) [CA1008](ca1008.md) [CA1010](ca1010.md)<br/>[CA1012](ca1012.md) [CA1024](ca1024.md) [CA1027](ca1027.md) [CA1028](ca1028.md)<br/>[CA1030](ca1030.md) [CA1036](ca1036.md) [CA1040](ca1040.md) [CA1041](ca1041.md)<br/>[CA1043](ca1043.md) [CA1044](ca1044.md) [CA1051](ca1051.md) [CA1052](ca1052.md)<br/>[CA1054](ca1054.md) [CA1055](ca1055.md) [CA1056](ca1056.md) [CA1058](ca1058.md)<br/>[CA1063](ca1063.md) [CA1708](ca1708.md) [CA1710](ca1710.md) [CA1711](ca1711.md)<br/>[CA1714](ca1714.md) [CA1715](ca1715.md) [CA1716](ca1716.md) [CA1717](ca1717.md)<br/>[CA1720](ca1720.md) [CA1721](ca1721.md) [CA1725](ca1725.md) [CA1801](ca1801.md)<br/>[CA1802](ca1802.md) [CA1815](ca1815.md) [CA1819](ca1819.md) [CA2217](ca2217.md)<br/>[CA2225](ca2225.md) [CA2226](ca2226.md) [CA2231](ca2231.md) [CA2234](ca2234.md)<br/>|

## <a name="exclude_async_void_methods"></a>exclude_async_void_methods

| 描述 | 允许的值 | 默认值 | 可配置规则 |
| - | - | - | - |
| 是否忽略未返回值的异步方法 | `true`<br/>`false` | `false` | [CA2007](ca2007.md) |

> [!NOTE]
> 在版本2.6.3 和更早版本的分析器包中，此选项名为 `skip_async_void_methods` 。

## <a name="exclude_single_letter_type_parameters"></a>exclude_single_letter_type_parameters

| 描述 | 允许的值 | 默认值 | 可配置规则 |
| - | - | - | - |
| 是否从规则中排除单字符 [类型参数](/dotnet/csharp/programming-guide/generics/generic-type-parameters) ， `S` 例如， `Collection<S>` | `true`<br/>`false` | `false` | [CA1715](ca1715.md) |

> [!NOTE]
> 在版本2.6.3 和更早版本的分析器包中，此选项名为 `allow_single_letter_type_parameters` 。

## <a name="output_kind"></a>output_kind

| 描述 | 允许的值 | 默认值 | 可配置规则 |
| - | - | - | - |
| 指定应分析生成此类程序集的项目中的代码 | 枚举的一个或多个字段 <xref:Microsoft.CodeAnalysis.OutputKind><br/><br/>使用逗号 ( 分隔多个值，)  | 所有输出类型 | [CA2007](ca2007.md) |

## <a name="required_modifiers"></a>required_modifiers

| 描述 | 允许的值 | 默认值 | 可配置规则 |
| - | - | - | - |
| 为应分析的 Api 指定必需的修饰符 | 以下允许的修饰符表中的一个或多个值<br/><br/>使用逗号 ( 分隔多个值，)  | 取决于每个规则 | [CA1802](ca1802.md) |

| 允许的修饰符 | 总结 |
| --- | --- |
| `none` | 无修饰符要求 |
| `static` 或 `Shared` | 必须在 Visual Basic 中声明为 "static" ( "Shared")  |
| `const` | 必须声明为 "const" |
| `readonly` | 必须声明为 "readonly" |
| `abstract` | 必须声明为 "abstract" |
| `virtual` | 必须声明为 "virtual" |
| `override` | 必须声明为 "override" |
| `sealed` | 必须声明为 "sealed" |
| `extern` | 必须声明为 "extern" |
| `async` | 必须声明为 "async" |

## <a name="exclude_extension_method_this_parameter"></a>exclude_extension_method_this_parameter

| 描述 | 允许的值 | 默认值 | 可配置规则 |
| - | - | - | - |
| 是否跳过 `this` 扩展方法的参数分析 | `true`<br/>`false` | `false` | [CA1062](ca1062.md) |

## <a name="null_check_validation_methods"></a>null_check_validation_methods

| 描述 | 允许的值 | 默认值 | 可配置规则 |
| - | - | - | - |
| 验证传递给方法的参数的 null 检查验证方法的名称为非 null。 | 允许的方法名称格式 (用 `|`) 分隔：<br/> -方法名称仅 (包含名称的所有方法，而不考虑包含类型或命名空间) <br/> -符号的 [文档 ID 格式](https://github.com/dotnet/csharplang/blob/master/spec/documentation-comments.md#id-string-format)的完全限定名称，带有可选 `M:` 前缀 | 无 | [CA1062](ca1062.md) |

## <a name="additional_string_formatting_methods"></a>additional_string_formatting_methods

| 描述 | 允许的值 | 默认值 | 可配置规则 |
| - | - | - | - |
| 其他字符串格式设置方法的名称 | 允许的方法名称格式 (用 `|`) 分隔：<br/> -方法名称仅 (包含名称的所有方法，而不考虑包含类型或命名空间) <br/> -符号的 [文档 ID 格式](https://github.com/dotnet/csharplang/blob/master/spec/documentation-comments.md#id-string-format)的完全限定名称，带有可选 `M:` 前缀 | 无 | [CA2241](ca2241.md) |

## <a name="excluded_type_names_with_derived_types"></a>excluded_type_names_with_derived_types

| 描述 | 允许的值 | 默认值 | 可配置规则 |
| - | - | - | - |
| 类型的名称，因此不包括类型及其所有派生类型进行分析 | 允许的符号名称格式 (由 `|`) 分隔：<br/> -Type name 仅 (包含名称的所有类型，而不考虑包含类型或命名空间) <br/> -符号的 [文档 ID 格式](https://github.com/dotnet/csharplang/blob/master/spec/documentation-comments.md#id-string-format)的完全限定名称，带有可选 `T:` 前缀 | 无 | [CA1303](ca1303.md) |

## <a name="excluded_symbol_names"></a>excluded_symbol_names

| 描述 | 允许的值 | 默认值 | 可配置规则 |
| - | - | - | - |
| 排除用于分析的符号的名称 | 允许的符号名称格式 (由 `|`) 分隔：<br/> -仅限符号名称 (包含名称的所有符号，而不考虑包含类型或命名空间) <br/> -符号的 [文档 ID 格式](https://github.com/dotnet/csharplang/blob/master/spec/documentation-comments.md#id-string-format)的完全限定名称。 每个符号名称都需要符号类型前缀，如方法的 "M：" 前缀、类型的 "T：" 前缀、命名空间的 "N：" 前缀等。<br/> - `.ctor` 对于构造函数和 `.cctor` 静态构造函数 | 无 | [CA1062](ca1062.md) [CA1303](ca1303.md) [CA2000](ca2000.md) [CA2100](ca2100.md) [CA2301](ca2301.md) [CA2302](ca2302.md)<br/>[CA2311](ca2311.md) [CA2312](ca2312.md) [CA2321](ca2321.md) [CA2322](ca2322.md) [CA2327](ca2327.md) [CA2328](ca2328.md)<br/>[CA2329](ca2329.md) [CA2330](ca2330.md) [CA3001](ca3001.md) [CA3002](ca3002.md) [CA3003](ca3003.md) [CA3004](ca3004.md)<br/>[CA3005](ca3005.md) [CA3006](ca3006.md) [CA3007](ca3007.md) [CA3008](ca3008.md) [CA3009](ca3009.md) [CA3010](ca3010.md)<br/>[CA3011](ca3011.md) [CA3012](ca3012.md) [CA5361](ca5361.md) CA5376 CA5377 [CA5378](ca5378.md)<br/>[CA5380](ca5380.md) [CA5381](ca5381.md) CA5382 CA5383 CA5384 CA5387<br/>CA5388 [CA5389](ca5389.md) CA5390 |

## <a name="disallowed_symbol_names"></a>disallowed_symbol_names

| 描述 | 允许的值 | 默认值 | 可配置规则 |
| - | - | - | - |
| 分析上下文中不允许的符号的名称 | 允许的符号名称格式 (由 `|`) 分隔：<br/> -仅限符号名称 (包含名称的所有符号，而不考虑包含类型或命名空间) <br/> -符号的 [文档 ID 格式](https://github.com/dotnet/csharplang/blob/master/spec/documentation-comments.md#id-string-format)的完全限定名称。 每个符号名称都需要符号类型前缀，如方法的 "M：" 前缀、类型的 "T：" 前缀、命名空间的 "N：" 前缀等。<br/> - `.ctor` 对于构造函数和 `.cctor` 静态构造函数 | 无 | [CA1031](ca1031.md) |

## <a name="see-also"></a>另请参阅

- [分析器配置](https://github.com/dotnet/roslyn-analyzers/blob/master/docs/Analyzer%20Configuration.md)
- [适用于 EditorConfig 的 .NET 编码约定](../ide/editorconfig-code-style-settings-reference.md)
