---
title: 使用 editorconfig 配置 .NET 代码质量分析器
ms.date: 09/23/2019
ms.topic: conceptual
helpviewer_keywords:
- .NET analyzers
- FxCop analyzers, configuring
- code quality
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: fbd30859c5ee3dbbea80c6d88d68c0211da62c88
ms.sourcegitcommit: de98ed7edc81383e47b87ae6e61143fbbbe7bc56
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/21/2020
ms.locfileid: "88706576"
---
# <a name="configure-net-code-quality-analyzers"></a>配置 .NET 代码质量分析器

对于某些 .NET 代码质量分析器 (其规则 Id 以) 开头的分析器 `CA` ，你可以通过 [可配置的选项](fxcop-analyzer-options.md)来优化应应用的基本代码部分。 每个选项都通过将键值对添加到 [EditorConfig](https://editorconfig.org) 文件来指定。 配置文件可以特定于文件、项目、解决方案或整个存储库。

> [!TIP]
> 在**解决方案资源管理器**中右键单击项目，然后选择 "**添加**  >  **新项**"，将 editorconfig 文件添加到项目。 在 " **添加新项** " 窗口中，在 "搜索" 框中输入 **editorconfig** 。 选择 **Editorconfig 文件 (默认) ** 模板，然后选择 " **添加**"。
>
> ![在 Visual Studio 中将 editorconfig 文件添加到项目](media/add-editorconfig-file.png)

::: moniker range=">=vs-2019"

有关配置规则的严重性 (例如，是错误还是警告) 的信息，请参阅 [在 EditorConfig 文件中设置规则严重性](use-roslyn-analyzers.md#set-rule-severity-in-an-editorconfig-file)。 或者，可以选择一个内置的 [EditorConfig 文件或规则集](analyzer-rule-sets.md) 来快速启用或禁用一类规则。

::: moniker-end

本文的其余部分将讨论优化 .NET 代码质量分析器应用于的 [选项](fxcop-analyzer-options.md) 的常规语法。

## <a name="option-scopes"></a>选项作用域

每个优化选项可针对所有规则进行配置，适用于一类规则 (例如，命名或设计) 或特定规则。

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

## <a name="enabling-editorconfig-based-configuration"></a>启用基于 Editorconfig 的配置

可以为以下作用域启用基于 EditorConfig 的分析器配置：

- 特定文档 (s) 
- 特定文件夹 (s) 
- 特定项目 (s) 
- 特定解决方案 (s) 
- 整个存储库

若要启用配置，请使用相应目录中的选项添加 *editorconfig* 文件。 此文件还可以包含基于 EditorConfig 的诊断严重性配置条目。 请参阅[此处](use-roslyn-analyzers.md#rule-severity)了解详细信息。

## <a name="see-also"></a>另请参阅

- [.NET 代码质量分析器的规则作用域选项](fxcop-analyzer-options.md)
- [分析器配置](https://github.com/dotnet/roslyn-analyzers/blob/master/docs/Analyzer%20Configuration.md)
- [适用于 EditorConfig 的 .NET 编码约定](../ide/editorconfig-code-style-settings-reference.md)
