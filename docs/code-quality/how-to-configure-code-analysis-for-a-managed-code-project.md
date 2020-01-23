---
title: 配置代码分析
ms.date: 04/04/2018
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.propertypages.csvb
- vs.codeanalysis.propertypages.solution
helpviewer_keywords:
- code analysis, selecting rule sets
- code analysis, rule sets
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: fe144e8de67264c9d89f6a240ef815afac9a4655
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75587558"
---
# <a name="how-to-configure-legacy-analysis-for-managed-code"></a>如何：为托管代码配置旧分析

在 Visual Studio 中，可以从要应用于托管代码项目的代码分析[规则集](../code-quality/rule-set-reference.md)列表中进行选择。 默认情况下**Microsoft 最少量建议规则**选择规则集，但可以应用不同的规则，如果所需的设置。 可以将规则集应用到解决方案中的一个或多个项目。

> [!NOTE]
> 本文适用于传统分析，不适用于[基于 .NET Compiler Platform 的代码分析器](use-roslyn-analyzers.md)。

## <a name="configure-a-rule-set-for-a-net-framework-project"></a>为 .NET Framework 项目配置规则集

1. 打开**代码分析**项目的属性页上的选项卡。 可以通过下列任一方法完成此操作：

   - 在中**解决方案资源管理器**，选择的项目。 在菜单栏上，选择**分析** > **配置代码分析** > **对于\<项目名称 >** 。

   - 右键单击该项目中的**解决方案资源管理器**，然后选择**属性**，然后选择**代码分析**选项卡。

2. 在中**配置**并**平台**列表中，选择生成配置和目标平台。

::: moniker range="vs-2017"

3. 若要在每次使用所选配置生成项目时运行代码分析，请选择 "**生成时启用代码分析**"。 您可以还手动运行代码分析通过选择**分析** > **运行代码分析** > **上运行代码分析\<项目名称 >** .

::: moniker-end

::: moniker range=">=vs-2019"

3. 若要在每次使用所选配置生成项目时运行代码分析，请在**二进制分析器**部分中选择 "**生成时运行**"。 您可以还手动运行代码分析通过选择**分析** > **运行代码分析** > **上运行代码分析\<项目名称 >** .

::: moniker-end

4. 若要查看生成的代码，请清除**禁止显示生成代码的结果**复选框。

    > [!NOTE]
    > 当生成的代码所产生的代码分析错误和警告出现在窗体和模板中时，此选项不会取消显示它们。 您可以查看和维护窗体或模板的源代码，而不会被覆盖。

::: moniker range="vs-2017"

5. 在中**运行此规则集**列表中，执行下列操作之一：

::: moniker-end

::: moniker range=">=vs-2019"

5. 在 "**活动规则**" 列表中，执行下列操作之一：

::: moniker-end

   - 选择你想要使用的规则集。

   - 选择 **\<浏览 >** 查找不在列表中的现有自定义规则集。

   - 定义[自定义规则集](../code-quality/how-to-create-a-custom-rule-set.md)。

## <a name="specify-rule-sets-for-multiple-projects-in-a-solution"></a>在解决方案中指定多个项目的规则集

默认情况下，分配的解决方案的所有托管的项目*Microsoft 最少量建议规则*代码分析规则集。 您可以更改分配给项目的解决方案中的规则集**属性**解决方案的对话框。

1. 在 Visual Studio 中打开解决方案。

2. 上**分析**菜单中，选择**为解决方案配置代码分析**。

3. 如有必要，展开**常见属性**，然后选择**代码分析设置**。

4. 您可以指定的一个或多个项目设置的规则：

    - 若要指定规则集为单个项目，选择项目名称。

    - 若要指定多个项目设置的规则，请按住**Ctrl** ，然后选择项目名称。

    - 若要在解决方案中指定的所有项目，按住**Shift**项目列表中单击。

5. 选择**规则集**规则的名称字段的一个项目，并选择设置你想要应用。

## <a name="see-also"></a>另请参阅

- [代码分析规则集参考](../code-quality/rule-set-reference.md)
