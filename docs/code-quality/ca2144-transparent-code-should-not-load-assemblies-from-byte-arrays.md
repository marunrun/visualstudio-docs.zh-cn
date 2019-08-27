---
title: CA2144:透明代码不应从字节数组加载程序集
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2144
ms.assetid: 777b1310-6e16-4413-b4ee-5f3136304f82
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9ff77d02ef9778112f5229e8104e9a1c1a1cde87
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68920438"
---
# <a name="ca2144-transparent-code-should-not-load-assemblies-from-byte-arrays"></a>CA2144:透明代码不应从字节数组加载程序集

|||
|-|-|
|TypeName|TransparentMethodsShouldNotLoadAssembliesFromByteArrays|
|CheckId|CA2144|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
透明方法使用以下方法之一从字节数组加载程序集:

- <xref:System.Reflection.Assembly.Load%2A>

- <xref:System.Reflection.Assembly.Load%2A>

- <xref:System.Reflection.Assembly.Load%2A>

## <a name="rule-description"></a>规则说明
透明代码安全检查不像关键代码的安全检查一样全面，因为透明代码不能执行安全敏感的操作。 从字节数组中加载的程序集在不透明的代码中可能不会被注意到，并且该字节数组可能包含确实需要审核的关键或更重要的安全关键代码。 因此, 透明代码不应从字节数组加载程序集。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突, 请使用<xref:System.Security.SecurityCriticalAttribute> <xref:System.Security.SecuritySafeCriticalAttribute>或特性标记正在加载程序集的方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。

## <a name="example"></a>示例
由于透明方法从字节数组加载程序集, 因此将在以下代码上激发规则。

[!code-csharp[FxCop.Security.CA2144.TransparentMethodsShouldNotLoadAssembliesFromByteArrays#1](../code-quality/codesnippet/CSharp/ca2144-transparent-code-should-not-load-assemblies-from-byte-arrays_1.cs)]