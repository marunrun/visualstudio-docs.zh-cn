---
title: CA1003:使用泛型事件处理程序实例 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- UseGenericEventHandlerInstances
- CA1003
helpviewer_keywords:
- CA1003
- UseGenericEventHandlerInstances
ms.assetid: 402101b6-555d-4cf7-b223-1d9fdfaaf1cd
caps.latest.revision: 24
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 25c96abd08f9d6c5f519c5f897c43aaf28bc231b
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65682263"
---
# <a name="ca1003-use-generic-event-handler-instances"></a>CA1003:使用泛型事件处理程序实例
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|UseGenericEventHandlerInstances|
|CheckId|CA1003|
|类别|Microsoft.Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 一种类型包含一个委托，它返回 void，其签名包含两个参数 （一个的对象的第一个和第二个是分配给 EventArgs 的类型） 和包含程序集针对[!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)]。

## <a name="rule-description"></a>规则说明
 之前[!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)]，以便将自定义信息传递给事件处理程序，一个新委托，必须指定派生自的类声明<xref:System.EventArgs?displayProperty=fullName>类。 这已不再是在实际[!INCLUDE[dnprdnlong](../includes/dnprdnlong-md.md)]，它引入了<xref:System.EventHandler%601?displayProperty=fullName>委托。 此泛型委托允许的任何类都派生自<xref:System.EventArgs>来与事件处理程序一起使用。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此规则的冲突，移除了该委托，并将其用途为通过使用<xref:System.EventHandler%601?displayProperty=fullName>委托。 如果该委托将自动生成[!INCLUDE[vbprvb](../includes/vbprvb-md.md)]编译器，更改要使用的事件声明的语法<xref:System.EventHandler%601?displayProperty=fullName>委托。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例显示了一个委托，它违反了此规则。 在[!INCLUDE[vbprvb](../includes/vbprvb-md.md)]示例中，注释说明了如何修改示例以满足该规则。 对于 C# 示例，以下是一个示例显示修改后的代码。

 [!code-csharp[FxCop.Design.CustomEventHandler#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.CustomEventHandler/cs/FxCop.Design.CustomEventHandler.cs#1)]
 [!code-vb[FxCop.Design.CustomEventHandler#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.CustomEventHandler/vb/FxCop.Design.CustomEventHandler.vb#1)]

## <a name="example"></a>示例
 以下示例从上一示例中，满足该规则，并将在中的使用它删除委托声明`ClassThatRaisesEvent`并`ClassThatHandlesEvent`方法通过使用<xref:System.EventHandler%601?displayProperty=fullName>委托。

 [!code-csharp[FxCop.Design.GenericEventHandler#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.GenericEventHandler/cs/FxCop.Design.GenericEventHandler.cs#1)]

## <a name="related-rules"></a>相关的规则
 [CA1005:避免泛型类型参数过多](../code-quality/ca1005-avoid-excessive-parameters-on-generic-types.md)

 [CA1010:集合应实现泛型接口](../code-quality/ca1010-collections-should-implement-generic-interface.md)

 [CA1000:不要在泛型类型中声明静态成员](../code-quality/ca1000-do-not-declare-static-members-on-generic-types.md)

 [CA1002:不要公开泛型列表](../code-quality/ca1002-do-not-expose-generic-lists.md)

 [CA1006:不要将嵌套在成员签名中的泛型类型](../code-quality/ca1006-do-not-nest-generic-types-in-member-signatures.md)

 [CA1004:泛型方法应提供类型参数](../code-quality/ca1004-generic-methods-should-provide-type-parameter.md)

 [CA1007： 在适用处在适用处使用泛型](../code-quality/ca1007-use-generics-where-appropriate.md)

## <a name="see-also"></a>请参阅
 [泛型](https://msdn.microsoft.com/library/75ea8509-a4ea-4e7a-a2b3-cf72482e9282)
