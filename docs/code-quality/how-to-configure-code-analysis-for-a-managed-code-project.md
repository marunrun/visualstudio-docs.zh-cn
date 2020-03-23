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
ms.openlocfilehash: 98db7cda02495d207d6e9387341173ea2efe22ca
ms.sourcegitcommit: 92361aac3665a934faa081e1d1ea89a067b01c5b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/17/2020
ms.locfileid: "79431347"
---
# <a name="how-to-configure-legacy-analysis-for-managed-code"></a>如何：为托管代码配置旧版分析

在 Visual Studio 中，您可以从代码分析[规则集](../code-quality/rule-set-reference.md)列表中选择以应用于托管代码项目。 默认情况下，选择**Microsoft 最小建议规则**集，但如果需要，可以应用其他规则集。 规则集可以应用于解决方案中的一个或多个项目。

> [!NOTE]
> 本文适用于旧分析，不适用于[基于 .NET 编译器平台的代码分析器](use-roslyn-analyzers.md)。

## <a name="configure-a-rule-set-for-a-net-framework-project"></a>为 .NET 框架项目配置规则集

1. 打开项目属性页上的代码**分析**选项卡。 可以通过下列任一方法完成此操作：

   - 在**解决方案资源管理器中**，选择项目。 在菜单栏上，选择 **"分析** > **配置代码分析** > **"以进行\<项目名称>**。

   - 右键单击**解决方案资源管理器**中的项目并选择 **"属性**"，然后选择 **"代码分析**"选项卡。

2. 在 **"配置**和**平台**"列表中，选择生成配置和目标平台。

::: moniker range="vs-2017"

3. 要每次使用所选配置生成项目时运行代码分析，请选择 **"在生成启用代码分析**"。 还可以通过在**项目\<名称>上**选择**分析** > **运行代码分析** > 运行代码分析来手动运行代码分析。

::: moniker-end

::: moniker range=">=vs-2019"

3. 要在每次使用所选配置生成项目时运行代码分析，请在**Binary 分析器**部分中选择 **"在生成时运行**"。 您还可以手动运行旧代码分析，[请参阅如何：为托管代码手动运行旧代码分析](how-to-run-legacy-code-analysis-manually-for-managed-code.md)，了解更多详细信息。

::: moniker-end

4. 要查看来自生成的代码的警告，请清除 **"从生成的代码中抑制结果**"复选框。

    > [!NOTE]
    > 当生成的代码所产生的代码分析错误和警告出现在窗体和模板中时，此选项不会取消显示它们。 您可以查看和维护窗体或模板的源代码，并且不会被覆盖。

::: moniker range="vs-2017"

5. 在 **"运行此规则集**"列表中，执行以下操作之一：

::: moniker-end

::: moniker range=">=vs-2019"

5. 在 **"活动规则"** 列表中，执行以下操作之一：

::: moniker-end

   - 选择要使用的规则集。

   - 选择**\<"浏览>** 以查找不在列表中的现有自定义规则集。

   - 定义[自定义规则集](../code-quality/how-to-create-a-custom-rule-set.md)。

## <a name="specify-rule-sets-for-multiple-projects-in-a-solution"></a>为解决方案中的多个项目指定规则集

默认情况下，解决方案的所有托管项目都分配了*Microsoft 最小建议规则*代码分析规则集。 您可以在解决方案的 **"属性"** 对话框中更改分配给解决方案项目的规则集。

1. 在 Visual Studio 中打开解决方案。

2. 在 **"分析"** 菜单上，选择 **"为解决方案配置代码分析**"。

3. 如有必要，请展开**公共属性**，然后选择**代码分析设置**。

4. 您可以为一个或多个项目指定规则集：

    - 要为单个项目指定规则集，请选择项目名称。

    - 要为多个项目指定规则集，请按住**Ctrl**并选择项目名称。

    - 要指定解决方案中的所有项目，请按住**Shift**并单击项目列表中。

5. 选择项目**的规则集**字段，然后选择要应用的规则集的名称。

## <a name="see-also"></a>另请参阅

- [代码分析规则集参考](../code-quality/rule-set-reference.md)
