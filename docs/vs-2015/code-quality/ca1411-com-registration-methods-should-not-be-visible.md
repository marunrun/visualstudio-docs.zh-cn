---
title: CA1411： COM 注册方法应该是不可见的 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1411
- ComRegistrationMethodsShouldNotBeVisible
helpviewer_keywords:
- ComRegistrationMethodsShouldNotBeVisible
- CA1411
ms.assetid: a59f96f1-1f38-4596-b656-947df5c55311
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: f001a2bb4920ebfb3f5cff3745639bd346a0a920
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85540136"
---
# <a name="ca1411-com-registration-methods-should-not-be-visible"></a>CA1411:COM 注册方法应该是不可见的
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|ComRegistrationMethodsShouldNotBeVisible|
|CheckId|CA1411|
|类别|Microsoft. 互操作性|
|是否重大更改|重大|

## <a name="cause"></a>原因
 用或特性标记的方法 <xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute?displayProperty=fullName> <xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute?displayProperty=fullName> 在外部可见。

## <a name="rule-description"></a>规则描述
 当向组件对象模型（COM）注册程序集时，会将项添加到程序集中每个 COM 可见类型的注册表中。 标记有和特性的方法 <xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute> <xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute> 将分别在注册和注销过程中调用，以运行特定于这些类型的注册/注销的用户代码。 不应在这些进程外调用此代码。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将方法的可访问性更改为 `private` 或 `internal` （ `Friend` 在中为 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] ）。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示了违反规则的两种方法。

 [!code-csharp[FxCop.Interoperability.ComRegistration2#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.ComRegistration2/cs/FxCop.Interoperability.ComRegistration2.cs#1)]
 [!code-vb[FxCop.Interoperability.ComRegistration2#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.ComRegistration2/vb/FxCop.Interoperability.ComRegistration2.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA1410:应对 COM 注册方法进行匹配](../code-quality/ca1410-com-registration-methods-should-be-matched.md)

## <a name="see-also"></a>另请参阅
 <xref:System.Runtime.InteropServices.RegistrationServices?displayProperty=fullName>将[程序集注册到 COM](https://msdn.microsoft.com/library/87925795-a3ae-4833-b138-125413478551) [Regasm.exe （程序集注册工具）](https://msdn.microsoft.com/library/e190e342-36ef-4651-a0b4-0e8c2c0281cb)
