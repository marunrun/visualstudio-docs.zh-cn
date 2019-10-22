---
title: CA1410：应匹配 COM 注册方法 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1410
- ComRegistrationMethodsShouldBeMatched
helpviewer_keywords:
- CA1410
- ComRegistrationMethodsShouldBeMatched
ms.assetid: f3b2e62d-fd66-4093-9f0c-dba01ad995fd
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 30f507f07de858dc222b4824ac6da633c76812ab
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72652748"
---
# <a name="ca1410-com-registration-methods-should-be-matched"></a>CA1410：应对 COM 注册方法进行匹配
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|ComRegistrationMethodsShouldBeMatched|
|CheckId|CA1410|
|类别|Microsoft. 互操作性|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 类型声明一个用 <xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute?displayProperty=fullName> 特性标记的方法，但不声明用 <xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute?displayProperty=fullName> 特性标记的方法，反之亦然。

## <a name="rule-description"></a>规则说明
 要使组件对象模型（COM）客户端创建 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 类型，必须先注册该类型。 如果可用，则在注册过程中将调用标记为 <xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute> 特性的方法，以运行用户指定的代码。 在注销过程中，将调用标记为 <xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute> 特性的相应方法，以撤消注册方法的操作。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请添加相应的注册或注销方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示违反规则的类型。 带批注的代码显示了冲突的修复。

 [!code-csharp[FxCop.Interoperability.ComRegistration#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.ComRegistration/cs/FxCop.Interoperability.ComRegistration.cs#1)]
 [!code-vb[FxCop.Interoperability.ComRegistration#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.ComRegistration/vb/FxCop.Interoperability.ComRegistration.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA1411：COM 注册方法应该是不可见的](../code-quality/ca1411-com-registration-methods-should-not-be-visible.md)

## <a name="see-also"></a>请参阅
 <xref:System.Runtime.InteropServices.RegistrationServices?displayProperty=fullName>[用 COM Regasm 注册程序集](https://msdn.microsoft.com/library/87925795-a3ae-4833-b138-125413478551) [（程序集注册工具）](https://msdn.microsoft.com/library/e190e342-36ef-4651-a0b4-0e8c2c0281cb)
