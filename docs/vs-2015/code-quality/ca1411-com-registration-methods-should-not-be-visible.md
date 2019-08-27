---
title: CA1411:COM 注册方法应该是不可见 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 2d7bcaf5637be70174a3a337343d92b7b3705b46
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65692032"
---
# <a name="ca1411-com-registration-methods-should-not-be-visible"></a>CA1411:COM 注册方法应该是不可见的
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|ComRegistrationMethodsShouldNotBeVisible|
|CheckId|CA1411|
|类别|Microsoft.Interoperability|
|是否重大更改|重大|

## <a name="cause"></a>原因
 使用标记的方法<xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute?displayProperty=fullName>或<xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute?displayProperty=fullName>属性是外部可见。

## <a name="rule-description"></a>规则说明
 程序集注册时使用组件对象模型 (COM)，条目添加到注册表中的程序集中每个 COM 可见类型。 使用标记的方法<xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute>和<xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute>属性在注册和注销过程中，分别称为，若要运行的是特定于注册/注销这些类型的用户代码。 此代码不应在这些进程外部调用。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请更改到方法的可访问性`private`或`internal`(`Friend`中[!INCLUDE[vbprvb](../includes/vbprvb-md.md)])。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例显示与该规则冲突的两种方法。

 [!code-csharp[FxCop.Interoperability.ComRegistration2#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.ComRegistration2/cs/FxCop.Interoperability.ComRegistration2.cs#1)]
 [!code-vb[FxCop.Interoperability.ComRegistration2#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.ComRegistration2/vb/FxCop.Interoperability.ComRegistration2.vb#1)]

## <a name="related-rules"></a>相关的规则
 [CA1410:应对 COM 注册方法进行匹配](../code-quality/ca1410-com-registration-methods-should-be-matched.md)

## <a name="see-also"></a>请参阅
 <xref:System.Runtime.InteropServices.RegistrationServices?displayProperty=fullName> [向 COM 注册程序集](https://msdn.microsoft.com/library/87925795-a3ae-4833-b138-125413478551) [Regasm.exe （程序集注册工具）](https://msdn.microsoft.com/library/e190e342-36ef-4651-a0b4-0e8c2c0281cb)
