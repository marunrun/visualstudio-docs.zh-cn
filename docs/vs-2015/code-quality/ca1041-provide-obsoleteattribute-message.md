---
title: CA1041：提供 ObsoleteAttribute 消息 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1041
- ProvideObsoleteAttributeMessage
helpviewer_keywords:
- ProvideObsoleteAttributeMessage
- CA1041
ms.assetid: be5bee69-d2d2-44e1-be2e-3ea451969003
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: dd1799f67036ab55de5b136d746ce938835de87f
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72668327"
---
# <a name="ca1041-provide-obsoleteattribute-message"></a>CA1041：提供 ObsoleteAttribute 消息
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|ProvideObsoleteAttributeMessage|
|CheckId|CA1041|
|类别|Microsoft. Design|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 使用未指定其 <xref:System.ObsoleteAttribute.Message%2A?displayProperty=fullName> 属性的 <xref:System.ObsoleteAttribute?displayProperty=fullName> 特性标记类型或成员。

## <a name="rule-description"></a>规则说明
 <xref:System.ObsoleteAttribute> 用于标记不推荐使用的库类型和成员。 库使用者应避免使用任何标记为过时的类型或成员。 这是因为它可能不受支持，最终将从库的更高版本中删除。 当编译使用 <xref:System.ObsoleteAttribute> 标记的类型或成员时，将显示该属性的 <xref:System.ObsoleteAttribute.Message%2A> 属性。 这将为用户提供有关已过时的类型或成员的信息。 此信息通常包括库设计器支持过时的类型或成员的时间，以及要使用的首选替换。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将 `message` 参数添加到 <xref:System.ObsoleteAttribute> 构造函数。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 请勿禁止显示此规则发出的警告，因为 <xref:System.ObsoleteAttribute.Message%2A> 属性提供有关已过时的类型或成员的重要信息。

## <a name="example"></a>示例
 下面的示例显示了一个已正确声明 <xref:System.ObsoleteAttribute> 的过时成员。

 [!code-cpp[FxCop.Design.ObsoleteAttributeOnMember#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.ObsoleteAttributeOnMember/cpp/FxCop.Design.ObsoleteAttributeOnMember.cpp#1)]
 [!code-csharp[FxCop.Design.ObsoleteAttributeOnMember#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ObsoleteAttributeOnMember/cs/FxCop.Design.ObsoleteAttributeOnMember.cs#1)]
 [!code-vb[FxCop.Design.ObsoleteAttributeOnMember#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.ObsoleteAttributeOnMember/vb/FxCop.Design.ObsoleteAttributeOnMember.vb#1)]

## <a name="see-also"></a>请参阅
 <xref:System.ObsoleteAttribute?displayProperty=fullName>
