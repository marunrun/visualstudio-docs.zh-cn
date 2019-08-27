---
title: CA1031:不要捕捉一般异常类型 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 4588a949b4b6439c3f76270b0bcdab9cd52c23d9
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63431216"
---
# <a name="ca1031-do-not-catch-general-exception-types"></a>CA1031:不要捕捉一般异常类型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DoNotCatchGeneralExceptionTypes|
|CheckId|CA1031|
|类别|Microsoft.Design|
|是否重大更改|非换行|

## <a name="cause"></a>原因
 如一般异常<xref:System.Exception?displayProperty=fullName>或<xref:System.SystemException?displayProperty=fullName>陷入`catch`语句或常规 catch 子句，如`catch()`使用。

## <a name="rule-description"></a>规则说明
 不应捕捉一般异常。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此规则的冲突，捕获更具体的异常，或重新引发一般异常中的最后一个语句`catch`块。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。 捕捉一般异常类型可以隐藏运行时库用户问题，并且可能使调试更加困难。

> [!NOTE]
> 从 [!INCLUDE[net_v40_long](../includes/net-v40-long-md.md)] 开始，公共语言运行时 (CLR) 不再提供操作系统和托管代码中发生的损坏状态异常（例如，[!INCLUDE[TLA#tla_mswin](../includes/tlasharptla-mswin-md.md)] 中的访问冲突），然后由托管代码来处理。 如果你想要编译中的应用程序[!INCLUDE[net_v40_short](../includes/net-v40-short-md.md)]或更高版本和维护对损坏的状态异常的处理，您可以应用<xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute>属性为负责处理损坏的状态异常的方法。

## <a name="example"></a>示例
 下面的示例显示了违反此规则的类型，并正确实现的类型`catch`块。

 [!code-cpp[FxCop.Design.ExceptionAndSystemException#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.ExceptionAndSystemException/cpp/FxCop.Design.ExceptionAndSystemException.cpp#1)]
 [!code-csharp[FxCop.Design.ExceptionAndSystemException#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ExceptionAndSystemException/cs/FxCop.Design.ExceptionAndSystemException.cs#1)]
 [!code-vb[FxCop.Design.ExceptionAndSystemException#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.ExceptionAndSystemException/vb/FxCop.Design.ExceptionAndSystemException.vb#1)]

## <a name="related-rules"></a>相关的规则
 [CA2200:再次引发以保留堆栈详细信息](../code-quality/ca2200-rethrow-to-preserve-stack-details.md)
