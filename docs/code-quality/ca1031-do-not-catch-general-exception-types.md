---
title: CA1031:不要捕捉一般异常类型
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1031
- DoNotCatchGeneralExceptionTypes
helpviewer_keywords:
- CA1031
- DoNotCatchGeneralExceptionTypes
ms.assetid: cbc283ae-2a46-4ec0-940e-85aa189b118f
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: c1dc1e5ed18ddcd42d42c96f3f853808c58ade48
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71236070"
---
# <a name="ca1031-do-not-catch-general-exception-types"></a>CA1031:不要捕捉一般异常类型

|||
|-|-|
|TypeName|DoNotCatchGeneralExceptionTypes|
|CheckId|CA1031|
|类别|Microsoft.Design|
|重大更改|不间断|

## <a name="cause"></a>原因
一般异常（ <xref:System.Exception?displayProperty=fullName>如或<xref:System.SystemException?displayProperty=fullName> ）在`catch`语句中捕获`catch()` ，或者使用的是常规 catch 子句。

## <a name="rule-description"></a>规则说明
不应捕捉一般异常。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突，请捕获更具体的异常，或者再次引发一般异常作为`catch`块中的最后一条语句。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。 捕获一般异常类型可以隐藏库用户的运行时问题，并且可能会使调试变得更加困难。

> [!NOTE]
> 从 .NET Framework 4 开始，公共语言运行时（CLR）不再提供操作系统和托管代码（如中[!INCLUDE[TLA#tla_mswin](../code-quality/includes/tlasharptla_mswin_md.md)]的访问冲突）中发生的损坏状态异常，以由托管代码进行处理。 如果要在 .NET Framework 4 或更高版本中编译应用程序并维护对损坏状态异常的处理，可将<xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute>属性应用于处理损坏状态异常的方法。

## <a name="example"></a>示例
下面的示例显示一个与此规则冲突的类型和一个正确实现`catch`该块的类型。

[!code-cpp[FxCop.Design.ExceptionAndSystemException#1](../code-quality/codesnippet/CPP/ca1031-do-not-catch-general-exception-types_1.cpp)]
[!code-vb[FxCop.Design.ExceptionAndSystemException#1](../code-quality/codesnippet/VisualBasic/ca1031-do-not-catch-general-exception-types_1.vb)]
[!code-csharp[FxCop.Design.ExceptionAndSystemException#1](../code-quality/codesnippet/CSharp/ca1031-do-not-catch-general-exception-types_1.cs)]

## <a name="related-rules"></a>相关规则
[CA2200再次引发以保留堆栈详细信息](../code-quality/ca2200-rethrow-to-preserve-stack-details.md)