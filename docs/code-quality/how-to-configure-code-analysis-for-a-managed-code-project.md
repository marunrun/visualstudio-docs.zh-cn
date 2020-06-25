---
title: 配置代码分析
ms.date: 04/04/2018
ms.topic: how-to
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
ms.openlocfilehash: a8c922f0fc952cede53b9961e2e772e71a19cbb9
ms.sourcegitcommit: 48e93538f1e352fc1f972b642bb5fcce2f6834a2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2020
ms.locfileid: "85371945"
---
# <a name="how-to-configure-legacy-analysis-for-managed-code"></a>如何：为托管代码配置旧分析

在 Visual Studio 中，可以从要应用于托管代码项目的代码分析[规则集](../code-quality/rule-set-reference.md)列表中进行选择。 默认情况下，选择 " **Microsoft 建议的最低规则**" 规则集，但你可以根据需要应用不同的规则集。 规则集可应用于解决方案中的一个或多个项目。

> [!NOTE]
> 本文适用于传统分析，不适用于[基于 .NET Compiler Platform 的代码分析器](use-roslyn-analyzers.md)。

## <a name="configure-a-rule-set-for-a-net-framework-project"></a>为 .NET Framework 项目配置规则集

1. 在项目的属性页上打开 "**代码分析**" 选项卡。 可以通过下列任一方法完成此操作：

   - 在**解决方案资源管理器**中，选择项目。 在菜单栏上，选择 "**分析**  >  **为**  >  ** \<projectname> **配置代码分析"。

   - 右键单击 "**解决方案资源管理器**中的项目，选择"**属性**"，然后选择"**代码分析**"选项卡。

2. 在 "**配置**" 和 "**平台**" 列表中，选择生成配置和目标平台。

::: moniker range="vs-2017"

3. 若要在每次使用所选配置生成项目时运行代码分析，请选择 "**生成时启用代码分析**"。 您还可以通过选择 "**分析**  >  **运行代码分析**  >  **" "运行代码分析" \<projectname> **来手动运行代码分析。

::: moniker-end

::: moniker range=">=vs-2019"

3. 若要在每次使用所选配置生成项目时运行代码分析，请在**二进制分析器**部分中选择 "**生成时运行**"。 还可以手动运行旧版代码分析，请参阅[如何：手动运行托管代码的旧版代码分析](how-to-run-legacy-code-analysis-manually-for-managed-code.md)了解更多详细信息。

::: moniker-end

4. 若要查看生成的代码中的警告，请清除 "**禁止显示生成代码的结果**" 复选框。

    > [!NOTE]
    > 当生成的代码所产生的代码分析错误和警告出现在窗体和模板中时，此选项不会取消显示它们。 您可以查看和维护窗体或模板的源代码，而不会被覆盖。

::: moniker range="vs-2017"

5. 在 "**运行此规则集**" 列表中，执行下列操作之一：

::: moniker-end

::: moniker range=">=vs-2019"

5. 在 "**活动规则**" 列表中，执行下列操作之一：

::: moniker-end

   - 选择要使用的规则集。

   - 选择 **\<Browse>** 此项可查找列表中不存在的现有自定义规则集。

   - 定义[自定义规则集](../code-quality/how-to-create-a-custom-rule-set.md)。

## <a name="specify-rule-sets-for-multiple-projects-in-a-solution"></a>为解决方案中的多个项目指定规则集

默认情况下，将为解决方案的所有托管项目分配 " *Microsoft 最低建议规则*" 代码分析规则集。 可以在解决方案的 "**属性**" 对话框中更改分配给解决方案项目的规则集。

1. 在 Visual Studio 中打开解决方案。

2. 在 "**分析**" 菜单上，选择 "**为解决方案配置代码分析**"。

3. 如有必要，展开 "**通用属性**"，然后选择 "**代码分析设置**"。

4. 你可以为一个或多个项目指定规则集：

    - 若要为单个项目指定规则集，请选择项目名称。

    - 若要为多个项目指定规则集，请按住**Ctrl**并选择项目名称。

    - 若要指定解决方案中的所有项目，请按住**Shift** ，并单击项目列表。

5. 选择项目的 "**规则集**" 字段，然后选择要应用的规则集的名称。

## <a name="see-also"></a>请参阅

- [代码分析规则集参考](../code-quality/rule-set-reference.md)
