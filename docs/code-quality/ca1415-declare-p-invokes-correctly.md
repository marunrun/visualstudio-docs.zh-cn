---
title: CA1415:正确声明 P-Invoke
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1415
- DeclarePInvokesCorrectly
helpviewer_keywords:
- CA1415
- DeclarePInvokesCorrectly
ms.assetid: 42a90796-0264-4460-bf97-2fb4a093dfdc
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 99274abee2c05a1bd33e34c9eb02cc928c1b54b0
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71234617"
---
# <a name="ca1415-declare-pinvokes-correctly"></a>CA1415:正确声明 P/Invoke

|||
|-|-|
|TypeName|DeclarePInvokesCorrectly|
|CheckId|CA1415|
|类别|Microsoft.Interoperability|
|重大更改|无间断-如果在程序集外部不能出现声明参数的 P/Invoke。 如果在程序集外部显示声明参数的 P/Invoke，则为。|

## <a name="cause"></a>原因
平台调用方法的声明不正确。

## <a name="rule-description"></a>规则说明
平台调用方法访问非托管代码，并通过使用或`Declare` <xref:System.Runtime.InteropServices.DllImportAttribute?displayProperty=fullName>中[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]的关键字定义。 目前，此规则查找目标 Win32 函数的平台调用方法声明，这些函数具有指向重叠结构参数的指针，并且相应的托管参数不是指向<xref:System.Threading.NativeOverlapped?displayProperty=fullName>结构的指针。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突，请正确声明平台调用方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。

## <a name="example"></a>示例
下面的示例演示违反规则并满足规则的平台调用方法。

[!code-csharp[FxCop.Interoperability.DeclarePInvokes#1](../code-quality/codesnippet/CSharp/ca1415-declare-p-invokes-correctly_1.cs)]

## <a name="see-also"></a>请参阅
[与非托管代码交互操作](/dotnet/framework/interop/index)