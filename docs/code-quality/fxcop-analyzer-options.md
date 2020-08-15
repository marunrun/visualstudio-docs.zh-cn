---
title: FxCop 分析器配置选项
ms.date: 09/23/2019
ms.topic: reference
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 7d6b56bec2174ca71cc66f5424b7bdc309330d95
ms.sourcegitcommit: 577c905de52057a741e68c2ed168ea527813fda5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2020
ms.locfileid: "88248802"
---
# <a name="rule-scope-options-for-fxcop-analyzers"></a>FxCop 分析器的规则作用域选项

某些 FxCop 分析器规则使你可以优化它们应应用到的基本代码部分。 此页列出可用的范围配置选项、其允许的值以及可应用这些选项的规则。 若要使用这些选项，请在 [EditorConfig 文件](../ide/create-portable-custom-editor-options.md#add-an-editorconfig-file-to-a-project)中指定它们。

从 [FxCopAnalyzers](https://www.nuget.org/packages/Microsoft.CodeAnalysis.FxCopAnalyzers) NuGet 包的版本2.6.3 开始提供这些配置选项。

> [!TIP]
> 若要查看可用于给定版本的 FxCopAnalyzers 包的选项的完整列表，请查看包的*文档*文件夹中的*Analyzer Configuration.md*文件。 文件位于 *% USERPROFILE% \\ . nuget\packages\microsoft.codeanalysis.fxcopanalyzers \\ \<version\> \documentation\Analyzer Configuration.md*。 此配置文档文件包含在包的每个版本中，从版本2.6.5 开始。 下面是一个示例，说明如何在 *Analyzer Configuration.md* 文件中记录一个选项：
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

| 允许的修饰符 | 摘要 |
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
