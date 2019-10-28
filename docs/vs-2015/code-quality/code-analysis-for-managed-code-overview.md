---
title: 托管代码的代码分析概述 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: overview
f1_keywords:
- vs.projectpropertypages.codeanalysis
helpviewer_keywords:
- code analysis, managed code
- managed code, code analysis
ms.assetid: 12ec0dab-46a4-43d8-984a-440730ef37a9
caps.latest.revision: 37
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 33ab4a000fac75c51c32e8a6d37de62e006160b3
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72610064"
---
# <a name="code-analysis-for-managed-code-overview"></a>托管代码的代码分析概述
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

针对托管代码的代码分析用于分析托管程序集并报告有关程序集的信息，例如 Microsoft .NET Framework 设计准则中规定的编程和设计规则的冲突。

 分析工具将它在分析期间执行的检查表示为警告消息。 警告消息标识任何相关的编程和设计问题，如有可能，还提供有关如何修复问题的信息。

## <a name="ide-integrated-development-environment-integration"></a>IDE（集成开发环境）集成
 作为开发人员，你可以对项目自动运行代码分析，也可以手动运行代码分析。

 若要在每次生成项目时运行代码分析，请在该项目的属性页上选中“生成时启用代码分析(定义 CODE_ANALYSIS 常量)”  。 有关详细信息，请参阅[如何：启用和禁用自动代码分析](../code-quality/how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)。

 若要对项目手动运行代码分析，请在“分析”菜单上，单击“对 ProjectName 运行代码分析”    。 有关详细信息，请参阅[如何：启用和禁用自动代码分析](../code-quality/how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)。

## <a name="rule-sets"></a>规则集
 托管代码的代码分析规则划分到规则集中  。 可以使用某个 Microsoft 标准规则集，也可以创建自定义规则集以满足特定需求。 有关详细信息，请参阅[使用规则集对代码分析规则进行分组](../code-quality/using-rule-sets-to-group-code-analysis-rules.md)。

## <a name="in-source-suppression"></a>在源代码中禁止显示
 它通常用于指示警告不适用。 这样，便可以通知开发人员以及可能会在以后评审代码的其他人员：已调查了一个警告，且禁止显示或忽略了该警告。

 在源代码中禁止显示警告是通过自定义特性实现的。 若要禁止显示警告，请向源代码添加特性 `SuppressMessage`，如下面的示例所示：

 ```csharp
 [System.Diagnostics.CodeAnalysis.SuppressMessage("Microsoft.Design", "CA1039:ListsAreStrongTyped")]
 Public class MyClass
 {
     // code
 }
 ```

 有关详细信息，请参阅[使用 SuppressMessage 特性禁止显示警告](../code-quality/suppress-warnings-by-using-the-suppressmessage-attribute.md)。

## <a name="run-code-analysis-as-part-of-check-in-policy"></a>作为签入策略的一部分运行代码分析
 作为一个单位，可能希望所有签入行为满足特定的策略。 特别是希望确保遵从下列策略：

- 要签入的代码中没有生成错误。

- 在最近一次生成中运行了代码分析。

  可以通过指定签入策略来实现该任务。 有关详细信息，请参阅[利用团队项目签入策略提高代码质量](../code-quality/enhancing-code-quality-with-team-project-check-in-policies.md)。

## <a name="team-build-integration"></a>Team Build 集成
 你可以使用生成系统的集成功能在生成过程中运行分析工具。 有关详细信息，请参阅[生成应用程序](/azure/devops/pipelines/index)。

## <a name="see-also"></a>另请参阅
 [使用规则集对代码分析规则进行分组](../code-quality/using-rule-sets-to-group-code-analysis-rules.md)[操作方法：启用和禁用自动代码分析](../code-quality/how-to-enable-and-disable-automatic-code-analysis-for-managed-code.md)
