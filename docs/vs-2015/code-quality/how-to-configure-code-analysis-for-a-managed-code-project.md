---
title: 如何：为托管代码项目配置代码分析 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.propertypages.csvb
helpviewer_keywords:
- code analysis, selecting rule sets
- code analysis, rule sets
ms.assetid: 618f6ff3-db0e-46cb-b08d-dfa35e62c9e7
caps.latest.revision: 35
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 1ac04a3d8834e3fc24f148fc36327d101e43720a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72658848"
---
# <a name="how-to-configure-code-analysis-for-a-managed-code-project"></a>如何：配置托管代码项目的代码分析
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)] 中，[!INCLUDE[vsPreLong](../includes/vsprelong-md.md)] 和 [!INCLUDE[vsPro](../includes/vspro-md.md)]，你可以从要应用于托管代码项目的代码分析*规则集*列表中进行选择。 默认规则集是 Microsoft 建议的最低规则。 可以将另一个规则集应用于一个项目，也可以应用于解决方案中的所有项目。

> [!NOTE]
> 有关如何为 ASP.NET Web 应用程序配置规则集的信息，请参阅[如何：为 ASP.NET Web 应用程序配置代码分析](../code-quality/how-to-configure-code-analysis-for-an-aspnet-web-application.md)。

### <a name="to-configure-a-rule-set-for-a-net-framework-project"></a>为 .NET Framework 项目配置规则集

1. 在**解决方案资源管理器**中，单击该项目。

2. 在 "**分析**" 菜单上，单击 "为*项目名称***配置代码分析**"。

3. 在 "**配置**" 和 "**平台**" 列表中，单击 "生成配置" 和 "目标平台"。

4. 若要在每次使用所选配置生成项目时运行代码分析，请选中 "**生成时启用代码分析（定义 CODE_ANALYSIS 常量）** " 复选框。 还可以通过打开 "**分析**" 菜单，并单击 "在*项目名称***上运行代码分析"** 来手动运行代码分析。

5. 默认情况下，代码分析不报告由外部工具自动生成的代码所产生的警告。 若要查看生成的代码中的警告，请清除 "**禁止显示生成代码的结果**" 复选框。

    > [!NOTE]
    > 当生成的代码所产生的代码分析错误和警告出现在窗体和模板中时，此选项不会取消显示它们。 可以查看和维护窗体或模板的源代码。

6. 在 "**运行此规则集**" 列表中，执行下列操作之一：

    - 单击要使用的规则集。

    - 单击 **\<Browse .。。>** 指定列表中不存在的现有自定义规则集。

    - 定义自定义规则集。

         有关详细信息，请参阅[创建自定义规则集](../code-quality/creating-custom-code-analysis-rule-sets.md)。

## <a name="see-also"></a>请参阅
 [演练：配置和使用自定义规则集](../code-quality/walkthrough-configuring-and-using-a-custom-rule-set.md)
