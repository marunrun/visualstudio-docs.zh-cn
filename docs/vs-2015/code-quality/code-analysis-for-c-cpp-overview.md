---
title: C-C++ 代码分析概述 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: overview
helpviewer_keywords:
- annotations, code analysis
- build integration, code analysis
- C/C++ code analysis
- IDE, code analysis
- pragma directive, code analysis
- code analysis, C/C++
- code analysis tool
- command line, code analysis
- C++, code analysis
- check-in policies, code analysis
- '#pragma directives, code analysis'
- C, code analysis
ms.assetid: 81f0c9e8-f471-4de5-aac4-99db336a8809
caps.latest.revision: 27
author: corob-msft
ms.author: corob
manager: jillfra
ms.openlocfilehash: 1ce41cd1c0dabc94658b83aa5e2bcdc08d005fdb
ms.sourcegitcommit: 68f893f6e472df46f323db34a13a7034dccad25a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2020
ms.locfileid: "77275360"
---
# <a name="code-analysis-for-cc-overview"></a>C/C++ 代码分析概述
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

C/C++ 代码分析工具为开发人员提供有关其 C/C++ 源代码中可能存在的缺陷的信息。 该工具报告的常见编码错误包括缓冲区溢出、内存未初始化、null 指针取消引用，以及内存和资源泄漏。  
  
## <a name="ide-integrated-development-environment-integration"></a>IDE（集成开发环境）集成  
 为了方便开发人员可以自然地使用分析工具，将它完全集成在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] IDE 中。 在生成过程中，源代码产生的任何警告都显示在错误列表中。 你可以导航到导致该警告的源代码并查看更多信息，了解相关原因和找出问题可能的解决方案。  
  
## <a name="pragma-support"></a>#pragma 支持  
 开发人员可以使用 `#pragma` 指令将警告视为错误；启用或禁用警告，并禁止显示各代码的警告。 有关详细信息，请参阅[如何：为特定 C/C ++ 警告启用和禁用代码分析](https://msdn.microsoft.com/910b8518-71f1-4b2e-b012-70647795642a)。  
  
## <a name="annotation-support"></a>注释支持  
 注释可以提高代码分析的准确性。 注释可以提供有关函数参数和返回类型的先决条件和后置条件的其他信息。 有关详细信息，请参阅[如何：使用 _analysis_assume 指定其他代码信息](../code-quality/how-to-specify-additional-code-information-by-using-analysis-assume.md)  
  
## <a name="run-analysis-tool-as-part-of-check-in-policy"></a>根据签入策略运行代码分析  
 建议要求所有源代码签入均满足特定策略。 具体而言，建议确保在最近的本地生成过程中运行分析。 有关启用代码分析签入策略的详细信息，请参阅[创建和使用代码分析签入策略](../code-quality/creating-and-using-code-analysis-check-in-policies.md)  
  
## <a name="team-build-integration"></a>Team Build 集成  
 你可以使用生成系统的集成功能在 [!INCLUDE[esprtfs](../includes/esprtfs-md.md)] 生成过程中运行代码分析工具。 有关详细信息，请参阅[生成应用程序](/azure/devops/pipelines/index)。  
  
## <a name="command-line-support"></a>命令行支持  
 除了完全集成到开发环境中，开发人员还可以通过命令行使用分析工具，如以下示例所示：  
  
 `C:\>cl /analyze Sample.cpp`
