---
title: Analyzing Application Quality by Using Code Analysis Tools | Microsoft Docs
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
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 8b85bbad909a05bacab361a49cc7e029482ad606
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74291198"
---
# <a name="analyzing-application-quality-by-using-code-analysis-tools"></a>使用代码分析工具分析应用程序质量
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

In This Section [Analyzing Managed Code Quality](../code-quality/analyzing-managed-code-quality-by-using-code-analysis.md) Visual Studio code analysis for managed code provides information about managed assemblies, such as violations of the programming and design rules set forth in the Microsoft .NET Framework Design Guidelines. 警告消息标识任何相关的编程和设计问题，如有可能，还提供有关如何修复问题的信息。

 [Analyzing C/C++ Code Quality by Using Code Analysis](../code-quality/analyzing-c-cpp-code-quality-by-using-code-analysis.md) The C/C++ Code Analysis tool provides information to developers about possible defects in their C/C++ source code. 该工具报告的常见编码错误包括缓冲区溢出、内存未初始化、null 指针取消引用，以及内存和资源泄漏。

 [Using Rule Sets to Group Code Analysis Rules](../code-quality/using-rule-sets-to-group-code-analysis-rules.md) Select and create *rule sets* to apply to your project.

 [Code Analysis Application Errors](../code-quality/code-analysis-application-errors.md) Fix errors in the code analysis functionality.

 [Enhancing Code Quality with Team Project Check-in Policies](../code-quality/enhancing-code-quality-with-team-project-check-in-policies.md) When you use Team Foundation Version Control (TFVC), you can create check-in policies for your team projects that enforce practices that lead to better code and more efficient group development. 签入策略是在团队项目级别设置的，并在允许代码签入之前在开发人员计算机上强制实施的规则。

### <a name="code-analysis-for-drivers"></a>驱动程序的代码分析
 通过系统地分析驱动程序源代码，代码分析工具可以帮助提高驱动程序的稳定性和可靠性。

 [Analyzing Driver Quality by Using Code Analysis Tools](/windows-hardware/drivers/devtest/tools-for-verifying-drivers) Code Analysis for Drivers is a compile-time static verification tool that detects basic coding errors in C and C++ programs and includes a specialized module that is designed to detect errors in (primarily) kernel-mode driver code. Static Driver Verifier (SDV) 是一个静态验证工具，可以系统分析 Windows 内核模式驱动程序的源代码。 SDV 确定驱动程序是否与 Windows 操作系统内核正确交互。

 [Code Analysis for Drivers Warnings](https://go.microsoft.com/fwlink/?LinkId=225920) Describes the warnings that the Code Analysis for Drivers reports when it detects a possible error in driver code.

## <a name="related-tasks"></a>相关任务
 [Measuring Complexity and Maintainability of Managed Code](../code-quality/measuring-complexity-and-maintainability-of-managed-code.md) Insert description here.

 [Unit Test Your Code](../test/unit-test-your-code.md) Insert description here.
