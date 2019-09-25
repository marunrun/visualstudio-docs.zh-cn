---
title: CA2149:透明方法不得调入本机代码
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2149
ms.assetid: 28951bd7-f3db-4871-99aa-bad68d1ead80
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- cplusplus
ms.openlocfilehash: 8e75b12b820b3ff3ac5a26f83148a49ca87c12ad
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71231955"
---
# <a name="ca2149-transparent-methods-must-not-call-into-native-code"></a>CA2149:透明方法不得调入本机代码

|||
|-|-|
|TypeName|TransparentMethodsMustNotCallNativeCode|
|CheckId|CA2149|
|类别|Microsoft.Security|
|重大更改|重大|

## <a name="cause"></a>原因
方法通过方法存根（如 P/Invoke）调用本机函数。

## <a name="rule-description"></a>规则说明
此规则对通过 P/Invoke 直接调用本机代码的任何透明方法引发。 违反此规则会导致级别 2 <xref:System.MethodAccessException>透明度模型中出现，并<xref:System.Security.Permissions.SecurityPermissionAttribute.UnmanagedCode%2A>在1级透明度模型中提供完全要求。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突，请使用<xref:System.Security.SecurityCriticalAttribute>或<xref:System.Security.SecuritySafeCriticalAttribute>特性标记调用本机代码的方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。

## <a name="example"></a>示例
[!code-csharp[FxCop.Security.CA2149.TransparentMethodsMustNotCallNativeCode#1](../code-quality/codesnippet/CSharp/ca2149-transparent-methods-must-not-call-into-native-code_1.cs)]