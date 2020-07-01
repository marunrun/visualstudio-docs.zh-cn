---
title: CA1408：不要使用 AutoDual ClassInterfaceType |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotUseAutoDualClassInterfaceType
- CA1408
helpviewer_keywords:
- CA1408
- DoNotUseAutoDualClassInterfaceType
ms.assetid: 60ca5e02-3c51-42dd-942b-4f950eecfa0f
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: b953a97d557e28cce50f554acc03797d4be38220
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85534870"
---
# <a name="ca1408-do-not-use-autodual-classinterfacetype"></a>CA1408:请不要使用 AutoDual ClassInterfaceType
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|DoNotUseAutoDualClassInterfaceType|
|CheckId|CA1408|
|类别|Microsoft. 互操作性|
|是否重大更改|重大|

## <a name="cause"></a>原因
 组件对象模型（COM）可见类型被标记为 <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> 属性设置为的 `AutoDual` 值 <xref:System.Runtime.InteropServices.ClassInterfaceType> 。

## <a name="rule-description"></a>规则描述
 使用双重接口的类型使客户端可以绑定到特定的接口布局。 如果在将来的版本中对该类型或任何基类型的布局进行更改，将中断绑定到该接口的 COM 客户端。 默认情况下，如果 <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> 未指定属性，则使用仅调度接口。

 除非另行标记，否则所有公共非泛型类型都对 COM 可见;所有非公共和泛型类型对 COM 都不可见。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将属性的值更改 <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> 为的 `None` 值， <xref:System.Runtime.InteropServices.ClassInterfaceType> 并显式定义接口。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 请勿禁止显示此规则发出的警告，除非确定类型及其基类型的布局在未来版本中将不会更改。

## <a name="example"></a>示例
 下面的示例演示一个与规则冲突的类，以及一个用于使用显式接口的类的重新声明。

 [!code-csharp[FxCop.Interoperability.AutoDual#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.AutoDual/cs/FxCop.Interoperability.AutoDual.cs#1)]
 [!code-vb[FxCop.Interoperability.AutoDual#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.AutoDual/vb/FxCop.Interoperability.AutoDual.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA1403:自动布局类型不应对 COM 可见](../code-quality/ca1403-auto-layout-types-should-not-be-com-visible.md)

 [CA1412:将 ComSource 接口标记为 IDispatch](../code-quality/ca1412-mark-comsource-interfaces-as-idispatch.md)

## <a name="see-also"></a>另请参阅
 [介绍类接口](https://msdn.microsoft.com/733c0dd2-12e5-46e6-8de1-39d5b25df024)[为互操作进行互操作的 .Net 类型的符合](https://msdn.microsoft.com/library/4b8afb52-fb8d-4e65-b47c-fd82956a3cdd) [Interoperating with Unmanaged Code](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)性
