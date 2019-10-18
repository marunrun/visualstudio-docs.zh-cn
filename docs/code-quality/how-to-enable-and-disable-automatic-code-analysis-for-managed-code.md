---
title: 禁用旧代码分析
ms.date: 10/04/2019
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 656b36e6d0a90bb44eaa5745312f1a57e1ea3474
ms.sourcegitcommit: 485ffaedb1ade71490f11cf05962add1718945cc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72448936"
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
