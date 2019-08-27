---
title: 使用代码分析工具分析应用程序质量 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: conceptual
f1_keywords:
- vs.codeanalysis.analysisresults
helpviewer_keywords:
- application quality, analyzing
- code analysis
- team-based development, analyzing application quality
ms.assetid: 21680516-ddb5-446d-90d4-19d94f6ec699
caps.latest.revision: 26
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 83fbe8b372d021e0cec4faccfd0b22fcaa8af30d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68157100"
---
# <a name="analyzing-application-quality-by-using-code-analysis-tools"></a>使用代码分析工具分析应用程序质量
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本节内容  
 [分析托管代码质量](../code-quality/analyzing-managed-code-quality-by-using-code-analysis.md)  
 针对托管代码的 Visual Studio 代码分析提供有关托管程序集的信息，例如 Microsoft .NET Framework 设计准则中规定的编程和设计规则的冲突。 警告消息标识任何相关的编程和设计问题，如有可能，还提供有关如何修复问题的信息。  
  
 [使用代码分析来分析 C/C++ 代码质量](../code-quality/analyzing-c-cpp-code-quality-by-using-code-analysis.md)  
 C/C++ 代码分析工具为开发人员提供有关其 C/C++ 源代码中可能存在的缺陷的信息。 该工具报告的常见编码错误包括缓冲区溢出、内存未初始化、null 指针取消引用，以及内存和资源泄漏。  
  
 [使用规则集对代码分析规则进行分组](../code-quality/using-rule-sets-to-group-code-analysis-rules.md)  
 选择并创建*规则集*要应用于你的项目。  
  
 [代码分析应用程序错误](../code-quality/code-analysis-application-errors.md)  
 修复代码分析功能中的错误。  
  
 [利用团队项目签入策略提高代码质量](../code-quality/enhancing-code-quality-with-team-project-check-in-policies.md)  
 使用 Team Foundation 版本控制 (TFVC) 时，可以为团队项目创建签入策略，以强制执行会产生更有效的代码并实现更高效的团队开发的实践。 签入策略是在团队项目级别设置的，并在允许代码签入之前在开发人员计算机上强制实施的规则。  
  
### <a name="code-analysis-for-drivers"></a>驱动程序的代码分析  
 通过系统地分析驱动程序源代码，代码分析工具可以帮助提高驱动程序的稳定性和可靠性。  
  
 [使用代码分析工具来分析驱动程序质量](/windows-hardware/drivers/devtest/tools-for-verifying-drivers)  
 驱动程序的代码分析是一个编译时静态验证工具，检测 C 中的基本编码错误和C++程序，并包括一个专用的模块，旨在检测 （主要） 内核模式驱动程序代码中的错误。 Static Driver Verifier (SDV) 是一个静态验证工具，可以系统分析 Windows 内核模式驱动程序的源代码。 SDV 确定驱动程序是否与 Windows 操作系统内核正确交互。  
  
 [代码分析驱动程序警告](http://go.microsoft.com/fwlink/?LinkId=225920)  
 介绍驱动程序代码分析在驱动程序代码中检测到可能的错误时报告的警告。  
  
## <a name="related-tasks"></a>Related Tasks  
 [测量托管代码的复杂性和可维护性](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md)  
 在此处插入说明。  
  
 [单元测试代码](../test/unit-test-your-code.md)  
 在此处插入说明。
