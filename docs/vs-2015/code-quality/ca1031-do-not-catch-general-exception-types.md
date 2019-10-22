---
title: CA1031：不要捕获一般异常类型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1031
- DoNotCatchGeneralExceptionTypes
helpviewer_keywords:
- CA1031
- DoNotCatchGeneralExceptionTypes
ms.assetid: cbc283ae-2a46-4ec0-940e-85aa189b118f
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 2696446ee2b257b78559909c0cba672cded39943
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72661900"
---
# <a name="ca1031-do-not-catch-general-exception-types"></a>CA1031：不要捕捉一般异常类型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DoNotCatchGeneralExceptionTypes|
|CheckId|CA1031|
|类别|Microsoft. Design|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 一般异常（如 <xref:System.Exception?displayProperty=fullName> 或 <xref:System.SystemException?displayProperty=fullName>）在 `catch` 语句中捕获，或者使用 `catch()` 等常规 catch 子句。

## <a name="rule-description"></a>规则说明
 不应捕捉一般异常。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请捕获更具体的异常，或者再次引发一般异常作为 `catch` 块中的最后一条语句。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。 捕获一般异常类型可以隐藏库用户的运行时问题，并且可能会使调试变得更加困难。

> [!NOTE]
> 从 [!INCLUDE[net_v40_long](../includes/net-v40-long-md.md)] 开始，公共语言运行时 (CLR) 不再提供操作系统和托管代码中发生的损坏状态异常（例如，[!INCLUDE[TLA#tla_mswin](../includes/tlasharptla-mswin-md.md)] 中的访问冲突），然后由托管代码来处理。 如果要在 [!INCLUDE[net_v40_short](../includes/net-v40-short-md.md)] 或更高版本中编译应用程序并维护对损坏状态异常的处理，则可以将 <xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute> 属性应用于处理损坏状态异常的方法。

## <a name="example"></a>示例
 下面的示例显示一个与此规则冲突的类型和一个正确实现 `catch` 块的类型。

 [!code-cpp[FxCop.Design.ExceptionAndSystemException#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.ExceptionAndSystemException/cpp/FxCop.Design.ExceptionAndSystemException.cpp#1)]
 [!code-csharp[FxCop.Design.ExceptionAndSystemException#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ExceptionAndSystemException/cs/FxCop.Design.ExceptionAndSystemException.cs#1)]
 [!code-vb[FxCop.Design.ExceptionAndSystemException#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.ExceptionAndSystemException/vb/FxCop.Design.ExceptionAndSystemException.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA2200：再次引发以保留堆栈详细信息](../code-quality/ca2200-rethrow-to-preserve-stack-details.md)
