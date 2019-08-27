---
title: CA2145:不应使用 SuppressUnmanagedCodeSecurityAttribute 修饰透明方法
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2145
ms.assetid: 81970700-b438-4b3b-9239-16887e16f7b7
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a9269a0862dacf928cffb31f722f382271d5f0e7
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62542114"
---
# <a name="ca2145-transparent-methods-should-not-be-decorated-with-the-suppressunmanagedcodesecurityattribute"></a>CA2145:不应使用 SuppressUnmanagedCodeSecurityAttribute 修饰透明方法

|||
|-|-|
|TypeName|TransparentMethodsShouldNotUseSuppressUnmanagedCodeSecurity|
|CheckId|CA2145|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因

透明方法，使用标记的方法<xref:System.Security.SecuritySafeCriticalAttribute>方法或包含一种方法的类型将标有<xref:System.Security.SuppressUnmanagedCodeSecurityAttribute>属性。

## <a name="rule-description"></a>规则说明

使用修饰方法<xref:System.Security.SuppressUnmanagedCodeSecurityAttribute>属性具有调用它的任何方法隐式的 LinkDemand。 此 LinkDemand 要求调用代码是关键安全的。 标记使用 SuppressUnmanagedCodeSecurity 的方法<xref:System.Security.SecurityCriticalAttribute>属性会使此需求更明显的方法的调用方。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要解决此规则的冲突，标记该方法或类型具有<xref:System.Security.SecurityCriticalAttribute>属性。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

不禁止显示此规则发出的警告。

### <a name="code"></a>代码

[!code-csharp[FxCop.Security.CA2145.TransparentMethodsShouldNotUseSuppressUnmanagedCodeSecurity#1](../code-quality/codesnippet/CSharp/ca2145-transparent-methods-should-not-be-decorated-with-the-suppressunmanagedcodesecurityattribute_1.cs)]