---
title: CA1410:应对 COM 注册方法进行匹配 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: dd47aa57d128ec5f88f77036546476128aae39f5
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65692075"
---
# <a name="ca1410-com-registration-methods-should-be-matched"></a>CA1410:应对 COM 注册方法进行匹配
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|ComRegistrationMethodsShouldBeMatched|
|CheckId|CA1410|
|类别|Microsoft.Interoperability|
|是否重大更改|非换行|

## <a name="cause"></a>原因
 某个类型声明与标记的方法<xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute?displayProperty=fullName>属性，但不声明具有标记的方法<xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute?displayProperty=fullName>属性，反之亦然。

## <a name="rule-description"></a>规则说明
 若要创建的组件对象模型 (COM) 客户端的[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]类型，该类型必须首先注册。 如果可用，使用标记的方法<xref:System.Runtime.InteropServices.ComRegisterFunctionAttribute>在注册过程中运行用户指定的代码调用属性。 使用标记的相应方法<xref:System.Runtime.InteropServices.ComUnregisterFunctionAttribute>属性被称为在注销过程中要反转的注册方法的操作。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请添加相应的注册或注销方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例显示了违反了此规则的类型。 注释的代码显示了对冲突的修复。

 [!code-csharp[FxCop.Interoperability.ComRegistration#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.ComRegistration/cs/FxCop.Interoperability.ComRegistration.cs#1)]
 [!code-vb[FxCop.Interoperability.ComRegistration#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.ComRegistration/vb/FxCop.Interoperability.ComRegistration.vb#1)]

## <a name="related-rules"></a>相关的规则
 [CA1411:COM 注册方法应该是不可见](../code-quality/ca1411-com-registration-methods-should-not-be-visible.md)

## <a name="see-also"></a>请参阅
 <xref:System.Runtime.InteropServices.RegistrationServices?displayProperty=fullName> [向 COM 注册程序集](https://msdn.microsoft.com/library/87925795-a3ae-4833-b138-125413478551) [Regasm.exe （程序集注册工具）](https://msdn.microsoft.com/library/e190e342-36ef-4651-a0b4-0e8c2c0281cb)
