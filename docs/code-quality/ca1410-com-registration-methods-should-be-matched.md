---
title: CA1410:应对 COM 注册方法进行匹配
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1410
- ComRegistrationMethodsShouldBeMatched
helpviewer_keywords:
- CA1410
- ComRegistrationMethodsShouldBeMatched
ms.assetid: f3b2e62d-fd66-4093-9f0c-dba01ad995fd
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: bca9e06c861ab2bcaceead8bf8ee195b64e45c83
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71234738"
---
# <a name="ca1410-com-registration-methods-should-be-matched"></a>CA1410:应对 COM 注册方法进行匹配

|||
|-|-|
|TypeName|ComRegistrationMethodsShouldBeMatched|
|CheckId|CA1410|
|类别|Microsoft.Interoperability|
|重大更改|不间断|

## <a name="cause"></a>原因

类型声明用<xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute?displayProperty=fullName>特性标记的方法，但不声明<xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute?displayProperty=fullName>用特性标记的方法，反之亦然。

## <a name="rule-description"></a>规则说明

要使组件对象模型（COM）客户端创建 .NET 类型，必须先注册该类型。 如果可用，则在注册过程中将调用标记<xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute>为属性的方法，以运行用户指定的代码。 在注销过程中，将调用使用<xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute>特性标记的相应方法，以撤消注册方法的操作。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，请添加相应的注册或注销方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

不禁止显示此规则发出的警告。

## <a name="example"></a>示例

下面的示例演示违反规则的类型。 带批注的代码显示了冲突的修复。

[!code-csharp[FxCop.Interoperability.ComRegistration#1](../code-quality/codesnippet/CSharp/ca1410-com-registration-methods-should-be-matched_1.cs)]
[!code-vb[FxCop.Interoperability.ComRegistration#1](../code-quality/codesnippet/VisualBasic/ca1410-com-registration-methods-should-be-matched_1.vb)]

## <a name="related-rules"></a>相关规则

[CA1411COM 注册方法应该是不可见的](../code-quality/ca1411-com-registration-methods-should-not-be-visible.md)

## <a name="see-also"></a>请参阅

- <xref:System.Runtime.InteropServices.RegistrationServices?displayProperty=fullName>
- [向 COM 注册程序集](/dotnet/framework/interop/registering-assemblies-with-com)
- [Regasm.exe（程序集注册工具）](/dotnet/framework/tools/regasm-exe-assembly-registration-tool)