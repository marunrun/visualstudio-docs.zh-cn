---
title: CA1009：正确声明事件处理程序 |Microsoft Docs
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
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 6a4a4e2e6990772b50568043c4d18ff29248571d
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547883"
---
# <a name="ca1009-declare-event-handlers-correctly"></a>CA1009:正确声明事件处理程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|DeclareEventHandlersCorrectly|
|CheckId|CA1009|
|Category|Microsoft. Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 处理公共或受保护事件的委托不具有正确的签名、返回类型或参数名称。

## <a name="rule-description"></a>规则描述
 事件处理程序方法采用两个参数。 第一种类型为 <xref:System.Object?displayProperty=fullName> ，名称为 "sender"。 它是引发事件的对象。 第二个参数的类型为 <xref:System.EventArgs?displayProperty=fullName> ，名称为 "e"。 这是与该事件关联的数据。 例如，如果在打开文件时引发事件，则事件数据通常包含文件的名称。

 事件处理程序方法不应返回值。 在 c # 编程语言中，这由返回类型指示 `void` 。 事件处理程序可以在多个对象中调用多个方法。 如果允许方法返回值，则每个事件将会出现多个返回值，并且只有调用的最后一个方法的值可用。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请更正该委托的签名、返回类型或参数名称。 有关详细信息，请参阅以下示例。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示适合处理事件的委托。 此事件处理程序可调用的方法符合设计准则中指定的签名。 `AlarmEventHandler`委托的类型名称。 `AlarmEventArgs`从事件数据的基类派生， <xref:System.EventArgs> 并保存警报事件数据。

 [!code-cpp[FxCop.Design.EventsTwoParams#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.EventsTwoParams/cpp/FxCop.Design.EventsTwoParams.cpp#1)]
 [!code-csharp[FxCop.Design.EventsTwoParams#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.EventsTwoParams/cs/FxCop.Design.EventsTwoParams.cs#1)]
 [!code-vb[FxCop.Design.EventsTwoParams#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.EventsTwoParams/vb/FxCop.Design.EventsTwoParams.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA2109:检查可见的事件处理程序](../code-quality/ca2109-review-visible-event-handlers.md)

## <a name="see-also"></a>另请参阅
 <xref:System.EventArgs?displayProperty=fullName> <xref:System.Object?displayProperty=fullName>
 [钢笔尖：事件和委托](https://msdn.microsoft.com/d98fd58b-fa4f-4598-8378-addf4355a115)
