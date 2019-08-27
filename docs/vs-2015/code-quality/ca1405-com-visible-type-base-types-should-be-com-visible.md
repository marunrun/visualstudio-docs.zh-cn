---
title: CA1405:COM 可见类型的基类型应对 COM 可见 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1405
- ComVisibleTypeBaseTypesShouldBeComVisible
helpviewer_keywords:
- CA1405
- ComVisibleTypeBaseTypesShouldBeComVisible
ms.assetid: a762ea2f-5285-4f73-bfb9-9eb10aea4290
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: f284c0e6e57a2ca359e765992db3f2d599fec328
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65705751"
---
# <a name="ca1405-com-visible-type-base-types-should-be-com-visible"></a>CA1405:COM 可见类型的基类型应对 COM 可见
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|ComVisibleTypeBaseTypesShouldBeComVisible|
|CheckId|CA1405|
|类别|Microsoft.Interoperability|
|是否重大更改|DependsOnFix|

## <a name="cause"></a>原因
 组件对象模型 (COM) 可见类型派生自不是 COM 可见类型。

## <a name="rule-description"></a>规则说明
 当 COM 可见类型中的新版本中添加成员时，它必须遵守严格的指导原则，以避免中断绑定到当前版本的 COM 客户端。 对 COM 不可见的类型会假定它不需要添加新成员时，请遵循这些 COM 版本控制规则。 但是，如果 COM 可见类型派生自 COM 不可见类型中，公开的类接口<xref:System.Runtime.InteropServices.ClassInterfaceType?displayProperty=fullName>或<xref:System.Runtime.InteropServices.ClassInterfaceType>（默认值） 的基类型的所有公共成员 （除非它们专门标记为 COM 不可见，这是冗余）向 COM 公开 如果基类型在后续版本中添加新成员，可能会中断将绑定到派生类型的类接口的任何 COM 客户端。 COM 可见类型应该派生 COM 可见类型，以降低中断 COM 客户端的可能性。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此规则的冲突，则使 COM 可见的基类型或派生的类型对于 COM 不可见。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例显示了违反了此规则的类型。

 [!code-csharp[FxCop.Interoperability.ComBaseTypes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.ComBaseTypes/cs/FxCop.Interoperability.ComBaseTypes.cs#1)]
 [!code-vb[FxCop.Interoperability.ComBaseTypes#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.ComBaseTypes/vb/FxCop.Interoperability.ComBaseTypes.vb#1)]

## <a name="see-also"></a>请参阅
 <xref:System.Runtime.InteropServices.ClassInterfaceAttribute?displayProperty=fullName> [类接口简介](https://msdn.microsoft.com/733c0dd2-12e5-46e6-8de1-39d5b25df024)[与进行互操作非托管代码](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)
