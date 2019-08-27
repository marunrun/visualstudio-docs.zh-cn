---
title: CA2138:透明方法不得调用具有 SuppressUnmanagedCodeSecurity 特性的方法
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2138
ms.assetid: a14c4d32-f079-4f3a-956c-a1657cde0f66
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: 316aef3b0f1f715857fde8eaf2a6e74b1a49e40f
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68920576"
---
# <a name="ca2138-transparent-methods-must-not-call-methods-with-the-suppressunmanagedcodesecurity-attribute"></a>CA2138:透明方法不得调用具有 SuppressUnmanagedCodeSecurity 特性的方法

|||
|-|-|
|TypeName|TransparentMethodsMustNotCallSuppressUnmanagedCodeSecurityMethods|
|CheckId|CA2138|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
安全透明方法调用使用<xref:System.Security.SuppressUnmanagedCodeSecurityAttribute>特性标记的方法。

## <a name="rule-description"></a>规则说明
此规则对直接调用本机代码的任何透明方法 (例如通过使用 P/Invoke (平台调用) 调用) 引发。 使用<xref:System.Security.SuppressUnmanagedCodeSecurityAttribute>特性标记的 P/Invoke 和 COM 互操作方法将导致针对调用方法执行的 LinkDemand。 由于安全透明代码不能满足 Linkdemand, 此代码也无法调用用 SuppressUnmanagedCodeSecurity 特性标记的方法, 也无法调用用 SuppressUnmanagedCodeSecurity 特性标记的类的方法。 方法将失败, 或者要求将转换为完全请求。

违反此规则会导致在级别<xref:System.MethodAccessException> 2 安全透明度模型中出现, 并<xref:System.Security.Permissions.SecurityPermissionAttribute.UnmanagedCode%2A>在1级透明度模型中提供完全要求。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复<xref:System.Security.SecurityCriticalAttribute>与此规则的冲突, 请<xref:System.Security.SuppressUnmanagedCodeSecurityAttribute>删除特性, 并使用或<xref:System.Security.SecuritySafeCriticalAttribute>特性标记该方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。

## <a name="example"></a>示例
[!code-csharp[FxCop.Security.CA2138.TransparentMethodsMustNotCallSuppressUnmanagedCodeSecurityMethods#1](../code-quality/codesnippet/CSharp/ca2138-transparent-methods-must-not-call-methods-with-the-suppressunmanagedcodesecurity-attribute_1.cs)]