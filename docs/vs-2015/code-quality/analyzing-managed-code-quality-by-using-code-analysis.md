---
title: 使用代码分析来分析托管的代码质量 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
helpviewer_keywords:
- code analysis,managed code
- managed code analyis
ms.assetid: 68510a55-da51-4381-81a5-0feba76b8b4f
caps.latest.revision: 26
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 5d8740b79b026ade7f3da19aa4a89cacd94df17d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68157122"
---
# <a name="analyzing-managed-code-quality-by-using-code-analysis"></a>使用代码分析来分析托管代码质量
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以在 Visual Studio 中使用代码分析工具发现代码中的潜在问题，如不安全的数据访问、使用冲突和设计问题。 代码分析适用于.NET Framework 中，本机 (C 和C++)，和数据库应用程序。 托管代码的代码分析将组织中的规则*规则集*面向特定编码问题。  
  
## <a name="common-tasks"></a>常规任务  
  
|常规任务|支持内容|  
|------------------|------------------------|  
|**进行动手实践：** 通过更正一个简单的.NET Framework 应用程序中存在的缺陷了解代码分析的基础知识。|-   [演练：分析托管代码的代码缺陷](../code-quality/walkthrough-analyzing-managed-code-for-code-defects.md)|  
|**配置项目的代码分析：** 托管代码的规则组织成针对特定领域，例如安全性和设计的规则集。 可以使用的 Microsoft 标准规则设置或创建你自己的一个。|-   [代码分析托管的代码概述](../code-quality/code-analysis-for-managed-code-overview.md)<br />-   [使用规则集对代码分析规则进行分组](../code-quality/using-rule-sets-to-group-code-analysis-rules.md)<br />-   [使用 SuppressMessage 特性禁止显示警告](../code-quality/suppress-warnings-by-using-the-suppressmessage-attribute.md)|  
|**运行代码分析：** 可以指定代码分析，以自动生成的项目配置，每次运行并且您可以手动运行代码分析项目。|-   [如何：启用和禁用自动代码分析](../code-quality/how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)<br />-   [如何：手动运行代码分析](../code-quality/how-to-run-code-analysis-manually-for-managed-code.md)|  
|**分析代码分析结果：** 在代码分析窗口中列出的代码分析警告和错误。 可以选择警告或错误的标题以显示有关该警告的其他信息，同时突出显示引发规则的源代码行。 可以选择警告 ID 以显示 MSDN Library 的详细信息，其中包含关于如何解决问题的信息和示例。|-   [如何：查看托管的代码缺陷](../code-quality/how-to-view-managed-code-defects.md)<br />-   [代码分析托管的代码警告](../code-quality/code-analysis-for-managed-code-warnings.md)<br />-   [按 checkid 排列的警告](../code-quality/code-analysis-warnings-for-managed-code-by-checkid.md)<br />-   [匿名方法和代码分析](../code-quality/anonymous-methods-and-code-analysis.md)|  
|**与在开发生命周期集成代码分析：** 在签入策略[!INCLUDE[esprscc](../includes/esprscc-md.md)]启用开发团队，以确保所有代码签入符合一组常用的代码分析标准。 创建代码分析规则冲突的工作项是可以在错误列表窗口中执行的简单过程。|-   [利用团队项目签入策略提高代码质量](../code-quality/enhancing-code-quality-with-team-project-check-in-policies.md)<br />-   [如何：将代码项目规则集与团队项目签入策略同步](../code-quality/how-to-synchronize-code-project-rule-sets-with-team-project-check-in-policy.md)<br />-   [如何：为托管的代码缺陷创建工作项](../code-quality/how-to-create-a-work-item-for-a-managed-code-defect.md)|
