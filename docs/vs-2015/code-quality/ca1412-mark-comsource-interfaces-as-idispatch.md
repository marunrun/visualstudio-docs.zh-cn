---
title: CA1412：将 ComSource 接口标记为 IDispatch |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- MarkComSourceInterfacesAsIDispatch
- CA1412
helpviewer_keywords:
- CA1412
- MarkComSourceInterfacesAsIDispatch
ms.assetid: 131a7563-0410-443c-a8f5-52104250cfb4
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 86dc7042a48faa200ef9c360829b1756bc261ab0
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72652732"
---
# <a name="ca1412-mark-comsource-interfaces-as-idispatch"></a>CA1412：将 ComSource 接口标记为 IDispatch
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|MarkComSourceInterfacesAsIDispatch|
|CheckId|CA1412|
|类别|Microsoft. 互操作性|
|是否重大更改|重大|

## <a name="cause"></a>原因
 类型带有 <xref:System.Runtime.InteropServices.ComSourceInterfacesAttribute> 特性标记，并且至少有一个指定接口未标记为 `InterfaceIsDispatch` 值的 <xref:System.Runtime.InteropServices.InterfaceTypeAttribute> 特性。

## <a name="rule-description"></a>规则说明
 <xref:System.Runtime.InteropServices.ComSourceInterfacesAttribute> 用于标识类向组件对象模型（COM）客户端公开的事件接口。 这些接口必须作为 `InterfaceIsIDispatch` 公开，以便使 Visual Basic 6 COM 客户端能够接收事件通知。 默认情况下，如果未使用 <xref:System.Runtime.InteropServices.InterfaceTypeAttribute> 特性标记接口，则该接口将公开为双重接口。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请添加或修改 <xref:System.Runtime.InteropServices.InterfaceTypeAttribute> 属性，使其值设置为使用 <xref:System.Runtime.InteropServices.ComSourceInterfacesAttribute> 属性指定的所有接口的 Cominterfacetype.interfaceisidispatch。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示一个类，其中其中一个接口违反规则。

 [!code-csharp[FxCop.Interoperability.MarkIDispatch#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.MarkIDispatch/cs/FxCop.Interoperability.MarkIDispatch.cs#1)]
 [!code-vb[FxCop.Interoperability.MarkIDispatch#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.MarkIDispatch/vb/FxCop.Interoperability.MarkIDispatch.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA1408：请不要使用 AutoDual ClassInterfaceType](../code-quality/ca1408-do-not-use-autodual-classinterfacetype.md)

## <a name="see-also"></a>请参阅
 [如何：引发 COM 接收器所处理的事件](https://msdn.microsoft.com/7c9944b2-e951-4c3e-a0a1-59b2ae37d7fd)[与非托管代码互](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)操作
