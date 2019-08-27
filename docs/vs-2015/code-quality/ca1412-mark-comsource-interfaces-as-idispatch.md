---
title: CA1412:将 ComSource 接口标记为 IDispatch |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: d72dd7e143720ce4ef2fce364a7e5ed3529ff9f3
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65691997"
---
# <a name="ca1412-mark-comsource-interfaces-as-idispatch"></a>CA1412:将 ComSource 接口标记为 IDispatch
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|MarkComSourceInterfacesAsIDispatch|
|CheckId|CA1412|
|类别|Microsoft.Interoperability|
|是否重大更改|重大|

## <a name="cause"></a>原因
 类型将标有<xref:System.Runtime.InteropServices.ComSourceInterfacesAttribute>属性和至少一个指定的接口未标有<xref:System.Runtime.InteropServices.InterfaceTypeAttribute>属性设置为`InterfaceIsDispatch`值。

## <a name="rule-description"></a>规则说明
 <xref:System.Runtime.InteropServices.ComSourceInterfacesAttribute> 用于标识向组件对象模型 (COM) 客户端公开类的事件接口。 必须将这些接口公开为`InterfaceIsIDispatch`使 Visual Basic 6 COM 客户端可以接收事件通知。 默认情况下，如果接口未标有<xref:System.Runtime.InteropServices.InterfaceTypeAttribute>属性，公开为双重接口。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请添加或修改<xref:System.Runtime.InteropServices.InterfaceTypeAttribute>属性，以便其值设为使用指定的所有接口 InterfaceIsIDispatch<xref:System.Runtime.InteropServices.ComSourceInterfacesAttribute>属性。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示了一个接口与该规则冲突的类。

 [!code-csharp[FxCop.Interoperability.MarkIDispatch#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.MarkIDispatch/cs/FxCop.Interoperability.MarkIDispatch.cs#1)]
 [!code-vb[FxCop.Interoperability.MarkIDispatch#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.MarkIDispatch/vb/FxCop.Interoperability.MarkIDispatch.vb#1)]

## <a name="related-rules"></a>相关的规则
 [CA1408:不要使用 AutoDual ClassInterfaceType](../code-quality/ca1408-do-not-use-autodual-classinterfacetype.md)

## <a name="see-also"></a>请参阅
 [如何：引发 COM 接收器所处理的事件](https://msdn.microsoft.com/7c9944b2-e951-4c3e-a0a1-59b2ae37d7fd)[与进行互操作非托管代码](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)
