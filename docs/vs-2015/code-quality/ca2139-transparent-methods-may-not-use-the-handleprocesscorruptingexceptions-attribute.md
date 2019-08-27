---
title: CA2139:透明方法不能使用 HandleProcessCorruptingExceptions 特性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2139
ms.assetid: 45a0328a-add7-40f9-8934-dff59beb02b3
caps.latest.revision: 13
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: a05813d01a05c02455d43e74029251e96e4e4580
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68154278"
---
# <a name="ca2139-transparent-methods-may-not-use-the-handleprocesscorruptingexceptions-attribute"></a>CA2139:透明方法不能使用 HandleProcessCorruptingExceptions 特性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|TransparentMethodsMustNotHandleProcessCorruptingExceptions|
|CheckId|CA2139|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 透明方法标记为<xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute>属性。

## <a name="rule-description"></a>规则说明
 这是透明的尝试处理进程损坏异常通过任何方法将触发此规则<xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute>属性。 进程损坏异常属于此类异常的 CLR 版本 4.0 异常分类<xref:System.AccessViolationException>。 HandleProcessCorruptedStateExceptionsAttribute 特性只由安全关键方法使用，并且如果应用于透明的方法，则将被忽略。 若要处理进程损坏异常，此方法必须成为安全关键或安全可靠关键。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请删除<xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute>属性，或此方法标记<xref:System.Security.SecurityCriticalAttribute>或<xref:System.Security.SecuritySafeCriticalAttribute>属性。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 在此示例中，透明方法将标有<xref:System.Runtime.ExceptionServices.HandleProcessCorruptedStateExceptionsAttribute>属性，将不符合规则。 该方法还应标记为<xref:System.Security.SecurityCriticalAttribute>或<xref:System.Security.SecuritySafeCriticalAttribute>属性。

 [!code-csharp[FxCop.Security.CA2139.TransparentMethodsMustNotHandleProcessCorruptingExceptions#1](../snippets/csharp/VS_Snippets_CodeAnalysis/fxcop.security.ca2139.transparentmethodsmustnothandleprocesscorruptingexceptions/cs/ca2139 - transparentmethodsmustnothandleprocesscorruptingexceptions.cs#1)]
