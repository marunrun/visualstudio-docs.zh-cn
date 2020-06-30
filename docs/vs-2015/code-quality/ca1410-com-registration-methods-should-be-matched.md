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
ms.openlocfilehash: 43767ce04b32440a5c6753f5bfcabb91487c1232
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546700"
---
# <a name="ca1410-com-registration-methods-should-be-matched"></a>CA1410:应对 COM 注册方法进行匹配
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|ComRegistrationMethodsShouldBeMatched|
|CheckId|CA1410|
|Category|Microsoft. 互操作性|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 类型声明用特性标记的方法 <xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute?displayProperty=fullName> ，但不声明用特性标记的方法 <xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute?displayProperty=fullName> ，反之亦然。

## <a name="rule-description"></a>规则描述
 要使组件对象模型（COM）客户端创建 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 类型，必须先注册类型。 如果可用，则在注册过程中将调用标记为属性的方法， <xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute> 以运行用户指定的代码。 在注销过程中，将调用使用特性标记的相应方法， <xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute> 以撤消注册方法的操作。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请添加相应的注册或注销方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示违反规则的类型。 带批注的代码显示了冲突的修复。

 [!code-csharp[FxCop.Interoperability.ComRegistration#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.ComRegistration/cs/FxCop.Interoperability.ComRegistration.cs#1)]
 [!code-vb[FxCop.Interoperability.ComRegistration#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.ComRegistration/vb/FxCop.Interoperability.ComRegistration.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA1411:COM 注册方法应该是不可见的](../code-quality/ca1411-com-registration-methods-should-not-be-visible.md)

## <a name="see-also"></a>另请参阅
 <xref:System.Runtime.InteropServices.RegistrationServices?displayProperty=fullName>将[程序集注册到 COM](https://msdn.microsoft.com/library/87925795-a3ae-4833-b138-125413478551) [Regasm.exe （程序集注册工具）](https://msdn.microsoft.com/library/e190e342-36ef-4651-a0b4-0e8c2c0281cb)
