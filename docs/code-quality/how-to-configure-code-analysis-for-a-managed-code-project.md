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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: a1b09b77eb051d32a3aabb929e9058786215cfb4
ms.sourcegitcommit: 209ed0fcbb8daa1685e8d6b9a97f3857a4ce1152
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2019
ms.locfileid: "69551047"
---
# <a name="how-to-configure-legacy-analysis-for-managed-code"></a>如何：为托管代码配置旧分析

在 Visual Studio 中, 可以从要应用于托管代码项目的代码分析[规则集](../code-quality/rule-set-reference.md)列表中进行选择。 默认情况下**Microsoft 最少量建议规则**选择规则集，但可以应用不同的规则，如果所需的设置。 可以将规则集应用到解决方案中的一个或多个项目。

有关如何为 ASP.NET web 应用程序配置规则集的信息, 请参阅[如何:为 ASP.NET web 应用程序](../code-quality/how-to-configure-code-analysis-for-an-aspnet-web-application.md)配置代码分析。

> [!NOTE]
> 本文适用于传统分析, 不适用于[基于 .NET Compiler Platform 的代码分析器](use-roslyn-analyzers.md), 不在生成后运行代码分析。

## <a name="configure-a-rule-set-for-a-net-framework-project"></a>为 .NET Framework 项目配置规则集

1. 打开**代码分析**项目的属性页上的选项卡。 可以在以下两种方式来执行此操作：

   - 在中**解决方案资源管理器**，选择的项目。 在菜单栏上，选择**分析** > **配置代码分析** > **对于\<项目名称 >** 。

   - 右键单击该项目中的**解决方案资源管理器**，然后选择**属性**，然后选择**代码分析**选项卡。

1. 在中**配置**并**平台**列表中，选择生成配置和目标平台。

1. 若要运行代码分析，每次使用所选的配置生成项目，选择**生成时启用代码分析**复选框。 您可以还手动运行代码分析通过选择**分析** > **运行代码分析** > **上运行代码分析\<项目名称 >** .

1. 默认情况下，代码分析不报告由外部工具自动生成的代码所产生的警告。 若要查看生成的代码，请清除**禁止显示生成代码的结果**复选框。

    > [!NOTE]
    > 当生成的代码所产生的代码分析错误和警告出现在窗体和模板中时，此选项不会取消显示它们。 您可以查看和维护窗体或模板的源代码，而无需再对其覆盖。

1. 在中**运行此规则集**列表中，执行下列操作之一：

    - 选择你想要使用的规则集。

    - 选择 **\<浏览...>** 若要查找的现有的自定义规则集不在列表中。

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

## <a name="see-also"></a>请参阅

- [代码分析规则集参考](../code-quality/rule-set-reference.md)
- [如何：为 ASP.NET web 应用程序配置代码分析](../code-quality/how-to-configure-code-analysis-for-an-aspnet-web-application.md)
