---
title: CA1408:不要使用 AutoDual ClassInterfaceType |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 88d23ee703b482813ad0a5401e9dea7adf9a063c
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65705707"
---
# <a name="ca1408-do-not-use-autodual-classinterfacetype"></a>CA1408:请不要使用 AutoDual ClassInterfaceType
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DoNotUseAutoDualClassInterfaceType|
|CheckId|CA1408|
|类别|Microsoft.Interoperability|
|是否重大更改|重大|

## <a name="cause"></a>原因
 组件对象模型 (COM) 可见类型将标有<xref:System.Runtime.InteropServices.ClassInterfaceAttribute>属性设置为`AutoDual`的值<xref:System.Runtime.InteropServices.ClassInterfaceType>。

## <a name="rule-description"></a>规则说明
 使用双重接口的类型使客户端可以绑定到特定的接口布局。 如果在将来的版本中对该类型或任何基类型的布局进行更改，将中断绑定到该接口的 COM 客户端。 默认情况下，如果<xref:System.Runtime.InteropServices.ClassInterfaceAttribute>属性未指定，则使用仅支持调度的接口。

 除非以其他方式标记，所有公共的非泛型类型都是对 COM 可见所有非公共和泛型类型是对 COM 不可见

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请更改的值<xref:System.Runtime.InteropServices.ClassInterfaceAttribute>归于`None`的值<xref:System.Runtime.InteropServices.ClassInterfaceType>显式定义接口。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 除非它是特定类型和其基类型的布局不会更改的未来版本中，不要禁止显示此规则的警告。

## <a name="example"></a>示例
 下面的示例显示了违反了规则和要使用显式接口的类重新声明的类。

 [!code-csharp[FxCop.Interoperability.AutoDual#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.AutoDual/cs/FxCop.Interoperability.AutoDual.cs#1)]
 [!code-vb[FxCop.Interoperability.AutoDual#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.AutoDual/vb/FxCop.Interoperability.AutoDual.vb#1)]

## <a name="related-rules"></a>相关的规则
 [CA1403:自动布局类型不应对 COM 可见](../code-quality/ca1403-auto-layout-types-should-not-be-com-visible.md)

 [CA1412:将 ComSource 接口标记为 IDispatch](../code-quality/ca1412-mark-comsource-interfaces-as-idispatch.md)

## <a name="see-also"></a>请参阅
 [类接口简介](https://msdn.microsoft.com/733c0dd2-12e5-46e6-8de1-39d5b25df024)[为互操作限定.NET 类型](https://msdn.microsoft.com/library/4b8afb52-fb8d-4e65-b47c-fd82956a3cdd)[与进行互操作非托管代码](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)
