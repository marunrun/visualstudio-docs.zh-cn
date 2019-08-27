---
title: CA1009:正确声明事件处理程序 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1009
- DeclareEventHandlersCorrectly
helpviewer_keywords:
- CA1009
- DeclareEventHandlersCorrectly
ms.assetid: ab65c471-1449-49d2-9896-7b9af74284b4
caps.latest.revision: 21
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 51b04b4c081bd7961ef26657dd3cb526652df568
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65704253"
---
# <a name="ca1009-declare-event-handlers-correctly"></a>CA1009:正确声明事件处理程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DeclareEventHandlersCorrectly|
|CheckId|CA1009|
|类别|Microsoft.Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 处理公共或受保护的事件的委托没有返回类型或参数名称的正确签名。

## <a name="rule-description"></a>规则说明
 事件处理程序方法采用两个参数。 第一个是类型的<xref:System.Object?displayProperty=fullName>和名为发件人。 它是引发事件的对象。 第二个参数的类型是<xref:System.EventArgs?displayProperty=fullName>和名为 e。 这是与该事件关联的数据。 例如，如果打开文件时，将引发事件，事件数据通常包含的文件的名称。

 事件处理程序方法不应返回一个值。 在 C# 编程语言中，这会由返回类型中指示`void`。 事件处理程序可以调用多个对象中的多个方法。 如果允许这些方法返回一个值，多个返回值会发生的每个事件，且仅调用时的最后一个方法的值将可用。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请更正签名、 返回类型或委托的参数名称。 有关详细信息，请参阅下面的示例。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示一个适合于处理事件的委托。 可以通过此事件处理程序调用的方法符合设计指南中指定的签名。 `AlarmEventHandler` 是委托的类型名称。 `AlarmEventArgs` 从事件数据类的基类派生<xref:System.EventArgs>，它包含警报的事件数据。

 [!code-cpp[FxCop.Design.EventsTwoParams#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.EventsTwoParams/cpp/FxCop.Design.EventsTwoParams.cpp#1)]
 [!code-csharp[FxCop.Design.EventsTwoParams#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.EventsTwoParams/cs/FxCop.Design.EventsTwoParams.cs#1)]
 [!code-vb[FxCop.Design.EventsTwoParams#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.EventsTwoParams/vb/FxCop.Design.EventsTwoParams.vb#1)]

## <a name="related-rules"></a>相关的规则
 [CA2109:检查可见的事件处理程序](../code-quality/ca2109-review-visible-event-handlers.md)

## <a name="see-also"></a>请参阅
 <xref:System.EventArgs?displayProperty=fullName> <xref:System.Object?displayProperty=fullName>
 [NIB：事件和委托](https://msdn.microsoft.com/d98fd58b-fa4f-4598-8378-addf4355a115)
