---
title: 使用规则集对代码分析规则进行分组 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.rulesets.learnmore
helpviewer_keywords:
- code analysis, rule sets
ms.assetid: ed0f3a2a-1516-42e2-92de-b8986dc75d42
caps.latest.revision: 38
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 30bd2e53531d9abc7d27adba05c3b724c88d61c3
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72603481"
---
# <a name="using-rule-sets-to-group-code-analysis-rules"></a>使用规则集对代码分析规则进行分组
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)]、[!INCLUDE[vsPreLong](../includes/vsprelong-md.md)] 或 [!INCLUDE[vsPro](../includes/vspro-md.md)] 中配置代码分析时，可以从 Microsoft 内置*规则集*列表中进行选择。 规则集是代码分析规则的逻辑分组，用于标识目标问题和特定条件。 例如，你可以应用一个规则集，用于扫描公开可用 Api 的代码，也可以应用只包括最小建议规则的规则集。 还可以应用包含所有规则的规则集。

 您可以通过添加或删除规则，或通过更改规则作为警告或错误出现在 "**错误列表**" 窗口中，自定义规则集。 自定义规则集可以满足特定开发环境的需求。 自定义规则集时，"规则集" 页提供了搜索和筛选工具，可帮助您在此过程中使用。

## <a name="common-tasks"></a>常规任务

|任务|相关内容|
|----------|---------------------|
|**获取动手实践：** 使用代码分析工具指定自定义规则集，以便在简单的 .NET Framework 应用程序中查找和修复问题。|-   [演练：配置和使用自定义规则集](../code-quality/walkthrough-configuring-and-using-a-custom-rule-set.md)|
|**为项目配置代码分析：** 为项目、网站或解决方案选择现有规则集。|-   [如何：配置托管代码项目的代码分析](../code-quality/how-to-configure-code-analysis-for-a-managed-code-project.md)<br />[使用规则集指定要运行的C++规则](../code-quality/using-rule-sets-to-specify-the-cpp-rules-to-run.md)-   <br />-   [如何：为 ASP.NET Web 应用程序配置代码分析](../code-quality/how-to-configure-code-analysis-for-an-aspnet-web-application.md)<br />-   [如何：为解决方案中的多个项目指定规则集](../code-quality/how-to-specify-managed-code-rule-sets-for-multiple-projects-in-a-solution.md)|
|**自定义规则集：** 指定要应用于项目的规则。|-   [创建自定义规则集](../code-quality/creating-custom-code-analysis-rule-sets.md)|
|**了解内置规则集：** 查看组成内置规则集的代码分析规则。|-   [代码分析规则集引用](../code-quality/code-analysis-rule-set-reference.md)|
|将**代码分析与 Team Foundation Server 集成：** [!INCLUDE[esprtfs](../includes/esprtfs-md.md)] 签入策略使开发团队能够确保所有代码签入都符合一组通用的代码分析标准。|-   [如何：将代码项目规则集与团队项目签入策略同步](../code-quality/how-to-synchronize-code-project-rule-sets-with-team-project-check-in-policy.md)|
