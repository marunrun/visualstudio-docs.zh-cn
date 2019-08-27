---
title: 启用或禁用代码分析
ms.date: 10/25/2018
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: ec0a8a3f04830115d343fcef611cfbd338163395
ms.sourcegitcommit: 209ed0fcbb8daa1685e8d6b9a97f3857a4ce1152
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2019
ms.locfileid: "69551037"
---
# <a name="how-to-enable-and-disable-automatic-code-analysis-for-managed-code"></a>如何：为托管代码启用和禁用自动代码分析

可以配置 (静态) 代码分析, 使其在每次生成托管代码项目之后运行。 可以为每个生成配置 (例如, "调试" 和 "发布") 设置不同的代码分析属性。

本文仅适用于传统分析, 而不是使用[代码分析器](roslyn-analyzers-overview.md)进行实时代码分析。

## <a name="to-enable-or-disable-automatic-code-analysis"></a>启用或禁用自动代码分析

1. 在**解决方案资源管理器**中, 右键单击项目, 然后选择 "**属性**"。

1. 在项目的 "属性" 对话框中, 选择 "**代码分析**" 选项卡。

   > [!TIP]
   > 较新的项目类型 (如 .NET Core 和 .NET Standard 应用程序) 没有**代码分析**选项卡。传统分析不适用于这些项目类型, 但你可以使用[基于 .NET Compiler Platform 的代码分析器](roslyn-analyzers-overview.md)获取实时代码分析。 若要禁止显示代码分析器发出的警告, 请参阅本文末尾处的注释。

1. 在**配置**中指定生成类型, 并在**平台**中指定目标平台。

1. 若要启用或禁用自动代码分析, 请选中或清除 "**生成时启用代码分析**" 复选框。

> [!NOTE]
> "**生成时启用代码分析**" 复选框只影响旧分析。 它不会影响[基于 .NET Compiler Platform 的代码分析器](roslyn-analyzers-overview.md), 在将其作为 NuGet 包安装时, 该分析器始终在生成时执行。 如果要从**错误列表**中清除分析器错误, 则可以通过在菜单栏上选择 "**分析** > **运行代码分析" 和 "取消活动问题**" 来取消所有当前冲突。 有关详细信息, 请参阅[取消冲突](use-roslyn-analyzers.md#suppress-violations)。
