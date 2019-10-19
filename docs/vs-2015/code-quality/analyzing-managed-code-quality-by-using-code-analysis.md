---
title: 使用代码分析来分析托管代码质量 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
helpviewer_keywords:
- code analysis,managed code
- managed code analyis
ms.assetid: 68510a55-da51-4381-81a5-0feba76b8b4f
caps.latest.revision: 26
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 0d5f0646f26226e9895414db512681e0a7a71faa
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72671115"
---
# <a name="analyzing-managed-code-quality-by-using-code-analysis"></a>使用代码分析来分析托管代码质量
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以在 Visual Studio 中使用代码分析工具发现代码中的潜在问题，如不安全的数据访问、使用冲突和设计问题。 代码分析适用于 .NET Framework、本机（C 和C++）和数据库应用程序。 托管代码的代码分析在面向特定编码问题的*规则集中*组织规则。

## <a name="common-tasks"></a>常规任务

|常规任务|支持内容|
|------------------|------------------------|
|**获取动手实践：** 通过更正简单 .NET Framework 应用程序中的缺陷来了解代码分析的基础知识。|-   [演练：对托管代码进行代码缺陷分析](../code-quality/walkthrough-analyzing-managed-code-for-code-defects.md)|
|**为项目配置代码分析：** 托管代码的规则组织成针对特定领域（如安全性和设计）的规则集。 您可以使用 Microsoft 标准规则集之一或创建自己的规则集。|[针对托管代码的 -    代码分析概述](../code-quality/code-analysis-for-managed-code-overview.md)<br />-   [使用规则集对代码分析规则进行分组](../code-quality/using-rule-sets-to-group-code-analysis-rules.md)<br />-   [使用 SuppressMessage 特性禁止显示警告](../code-quality/suppress-warnings-by-using-the-suppressmessage-attribute.md)|
|**运行代码分析：** 您可以指定每次生成项目配置时自动运行代码分析，还可以在项目上手动运行代码分析。|-   [如何：启用和禁用自动代码分析](../code-quality/how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)<br />-   [如何：手动运行代码分析](../code-quality/how-to-run-code-analysis-manually-for-managed-code.md)|
|**分析代码分析结果：** 代码分析窗口中列出了代码分析警告和错误。 可以选择警告或错误的标题以显示有关该警告的其他信息，同时突出显示引发规则的源代码行。 可以选择警告 ID 以显示 MSDN Library 的详细信息，其中包含关于如何解决问题的信息和示例。|-   [如何：查看托管代码缺陷](../code-quality/how-to-view-managed-code-defects.md)<br />[针对托管代码的 -    代码分析警告](../code-quality/code-analysis-for-managed-code-warnings.md)<br />[按 CheckId -    警告](../code-quality/code-analysis-warnings-for-managed-code-by-checkid.md)<br />-   [匿名方法和代码分析](../code-quality/anonymous-methods-and-code-analysis.md)|
|**将代码分析与开发生命周期进行集成：** 中的签入策略 [!INCLUDE[esprscc](../includes/esprscc-md.md)] 允许开发团队确保所有代码签入都符合一组通用的代码分析标准。 为代码分析规则冲突创建工作项是可在 "错误列表" 窗口中执行的简单过程。|-   [利用团队项目签入策略提高代码质量](../code-quality/enhancing-code-quality-with-team-project-check-in-policies.md)<br />-   [如何：将代码项目规则集与团队项目签入策略同步](../code-quality/how-to-synchronize-code-project-rule-sets-with-team-project-check-in-policy.md)<br />-   [如何：为托管代码缺陷创建工作项](../code-quality/how-to-create-a-work-item-for-a-managed-code-defect.md)|
