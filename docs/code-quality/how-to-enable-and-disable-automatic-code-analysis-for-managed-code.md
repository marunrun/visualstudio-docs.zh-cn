---
title: 禁用旧代码分析
ms.date: 10/04/2019
ms.topic: how-to
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 532fe62ceee3ab32fc203976af58dd867b97b453
ms.sourcegitcommit: 48e93538f1e352fc1f972b642bb5fcce2f6834a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2020
ms.locfileid: "85371880"
---
# <a name="how-to-enable-and-disable-binary-code-analysis-for-managed-code"></a>如何：启用和禁用托管代码的二进制代码分析

你可以配置要在每次生成托管代码项目之后运行的旧代码分析（二进制分析）。 对于每个生成配置，也可以具有不同的设置，例如 "调试" 和 "发布"。

> [!NOTE]
> 旧版分析不适用于较新的项目类型，如 .NET Core 和 .NET Standard 应用。 这些项目使用[基于 .NET Compiler Platform 的代码分析器](roslyn-analyzers-overview.md)来分析活动和生成时的代码。 有关在这些项目中禁用源代码分析的信息，请参阅[如何禁用源代码分析](disable-code-analysis.md)。

启用或禁用旧代码分析：

1. 在**解决方案资源管理器**中，右键单击项目，然后选择 "**属性**"。

2. 在项目的 "属性" 对话框中，选择 "**代码分析**" 选项卡。

3. 在**配置**中指定生成类型，并在**平台**中指定目标平台。 （仅限 Non-.NET Core/.NET Standard 项目。）

::: moniker range="vs-2017"

4. 若要启用或禁用自动代码分析，请选中或清除 "**生成时启用代码分析**" 复选框。

::: moniker-end

::: moniker range=">=vs-2019"

4. 若要启用或禁用自动代码分析，请在**二进制分析器**部分中选中或清除 "**生成时运行**" 复选框。

   ![在 Visual Studio 中对生成选项运行二进制代码分析](media/run-on-build-binary-analyzers.png)

::: moniker-end

> [!NOTE]
> 如果在生成时禁用二进制代码分析，则不会影响[基于 .NET Compiler Platform 的代码分析器](roslyn-analyzers-overview.md)（如果将其安装为 NuGet 包，则该分析器始终在生成时执行）。 有关从这些分析器禁用分析的信息，请参阅[如何禁用源代码分析](disable-code-analysis.md)。
