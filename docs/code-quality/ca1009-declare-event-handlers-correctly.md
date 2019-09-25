---
title: CA1009:正确声明事件处理程序
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1009
- DeclareEventHandlersCorrectly
helpviewer_keywords:
- CA1009
- DeclareEventHandlersCorrectly
ms.assetid: ab65c471-1449-49d2-9896-7b9af74284b4
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: e923730213ca31a4429d8547fdaaf980692f9a96
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71236479"
---
# <a name="ca1009-declare-event-handlers-correctly"></a>CA1009:正确声明事件处理程序

|||
|-|-|
|TypeName|DeclareEventHandlersCorrectly|
|CheckId|CA1009|
|类别|Microsoft.Design|
|重大更改|重大|

## <a name="cause"></a>原因
处理公共或受保护事件的委托不具有正确的签名、返回类型或参数名称。

## <a name="rule-description"></a>规则说明
事件处理程序方法采用两个参数。 第一种类型<xref:System.Object?displayProperty=fullName>为，名称为 "sender"。 它是引发事件的对象。 第二个参数的类型<xref:System.EventArgs?displayProperty=fullName>为，名称为 "e"。 这是与该事件关联的数据。 例如，如果在打开文件时引发事件，则事件数据通常包含文件的名称。

事件处理程序方法不应返回值。 在C#编程语言中，这由返回类型`void`指示。 事件处理程序可以在多个对象中调用多个方法。 如果允许方法返回值，则每个事件将会出现多个返回值，并且只有调用的最后一个方法的值可用。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突，请更正该委托的签名、返回类型或参数名称。 有关详细信息，请参阅以下示例。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。

## <a name="example"></a>示例
下面的示例演示适合处理事件的委托。 此事件处理程序可调用的方法符合设计准则中指定的签名。 `AlarmEventHandler`委托的类型名称。 `AlarmEventArgs`从事件数据<xref:System.EventArgs>的基类派生，并保存警报事件数据。

[!code-cpp[FxCop.Design.EventsTwoParams#1](../code-quality/codesnippet/CPP/ca1009-declare-event-handlers-correctly_1.cpp)]
[!code-csharp[FxCop.Design.EventsTwoParams#1](../code-quality/codesnippet/CSharp/ca1009-declare-event-handlers-correctly_1.cs)]
[!code-vb[FxCop.Design.EventsTwoParams#1](../code-quality/codesnippet/VisualBasic/ca1009-declare-event-handlers-correctly_1.vb)]

## <a name="related-rules"></a>相关规则
[CA2109检查可见的事件处理程序](../code-quality/ca2109-review-visible-event-handlers.md)

## <a name="see-also"></a>请参阅

- <xref:System.EventArgs?displayProperty=fullName>
- <xref:System.Object?displayProperty=fullName>
- [处理和引发事件](/dotnet/standard/events/index)