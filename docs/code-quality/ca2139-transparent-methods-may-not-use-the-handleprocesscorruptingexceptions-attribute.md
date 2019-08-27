---
title: CA2139:透明方法不能使用 HandleProcessCorruptingExceptions 特性
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2139
ms.assetid: 45a0328a-add7-40f9-8934-dff59beb02b3
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: f6808c5e9b5d35ab6ec8d4012f08e15cba9a159d
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68920571"
---
# <a name="ca2139-transparent-methods-may-not-use-the-handleprocesscorruptingexceptions-attribute"></a>CA2139:透明方法不能使用 HandleProcessCorruptingExceptions 特性

|||
|-|-|
|TypeName|TransparentMethodsMustNotHandleProcessCorruptingExceptions|
|CheckId|CA2139|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
透明方法用<xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute>特性标记。

## <a name="rule-description"></a>规则说明
此规则将触发任何透明的方法, 并使用<xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute>属性尝试处理进程损坏异常。 进程损坏异常是 CLR 版本4.0 异常分类 (例如) <xref:System.AccessViolationException>。 HandleProcessCorruptedStateExceptionsAttribute 特性只由安全关键方法使用，并且如果应用于透明的方法，则将被忽略。 若要处理进程损坏异常, 此方法必须成为安全关键的或安全可靠关键的。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复<xref:System.Security.SecurityCriticalAttribute>与此规则的冲突, 请<xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute>删除特性, 或使用或<xref:System.Security.SecuritySafeCriticalAttribute>特性标记方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。

## <a name="example"></a>示例
在此示例中, 透明方法标记有<xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute>属性, 并将导致规则失败。 还应将方法标记<xref:System.Security.SecurityCriticalAttribute>为<xref:System.Security.SecuritySafeCriticalAttribute>或属性。

[!code-csharp[FxCop.Security.CA2139.TransparentMethodsMustNotHandleProcessCorruptingExceptions#1](../code-quality/codesnippet/CSharp/ca2139-transparent-methods-may-not-use-the-handleprocesscorruptingexceptions-attribute_1.cs)]