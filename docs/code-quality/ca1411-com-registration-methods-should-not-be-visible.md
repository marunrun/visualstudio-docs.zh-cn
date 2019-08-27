---
title: CA1411:COM 注册方法应该是不可见的
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1411
- ComRegistrationMethodsShouldNotBeVisible
helpviewer_keywords:
- ComRegistrationMethodsShouldNotBeVisible
- CA1411
ms.assetid: a59f96f1-1f38-4596-b656-947df5c55311
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 4f6f40308255e0496b2bcccddf4299e83ea93100
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68922043"
---
# <a name="ca1411-com-registration-methods-should-not-be-visible"></a>CA1411:COM 注册方法应该是不可见的

|||
|-|-|
|TypeName|ComRegistrationMethodsShouldNotBeVisible|
|CheckId|CA1411|
|类别|Microsoft.Interoperability|
|是否重大更改|重大|

## <a name="cause"></a>原因

<xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute?displayProperty=fullName> 用<xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute?displayProperty=fullName>或特性标记的方法在外部可见。

## <a name="rule-description"></a>规则说明
当向组件对象模型 (COM) 注册程序集时, 会将项添加到程序集中每个 COM 可见类型的注册表中。 标记有<xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute>和<xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute>特性的方法将分别在注册和注销过程中调用, 以运行特定于这些类型的注册/注销的用户代码。 不应在这些进程外调用此代码。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突, 请将方法的可访问`private`性`internal`更改为[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]或 (`Friend`在中为)。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。

## <a name="example"></a>示例
下面的示例演示了违反规则的两种方法。

[!code-csharp[FxCop.Interoperability.ComRegistration2#1](../code-quality/codesnippet/CSharp/ca1411-com-registration-methods-should-not-be-visible_1.cs)]
[!code-vb[FxCop.Interoperability.ComRegistration2#1](../code-quality/codesnippet/VisualBasic/ca1411-com-registration-methods-should-not-be-visible_1.vb)]

## <a name="related-rules"></a>相关规则
[CA1410应匹配 COM 注册方法](../code-quality/ca1410-com-registration-methods-should-be-matched.md)

## <a name="see-also"></a>请参阅

- <xref:System.Runtime.InteropServices.RegistrationServices?displayProperty=fullName>
- [向 COM 注册程序集](/dotnet/framework/interop/registering-assemblies-with-com)
- [Regasm.exe（程序集注册工具）](/dotnet/framework/tools/regasm-exe-assembly-registration-tool)