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
ms.openlocfilehash: d738cf15ebe734cb74e553f38f6eb26af17e8cfd
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85542306"
---
# <a name="ca1041-provide-obsoleteattribute-message"></a>CA1041:提供 ObsoleteAttribute 消息
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|ProvideObsoleteAttributeMessage|
|CheckId|CA1041|
|类别|Microsoft. Design|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 使用 <xref:System.ObsoleteAttribute?displayProperty=fullName> 未指定属性的特性标记类型或成员 <xref:System.ObsoleteAttribute.Message%2A?displayProperty=fullName> 。

## <a name="rule-description"></a>规则描述
 <xref:System.ObsoleteAttribute>用于标记不推荐使用的库类型和成员。 库使用者应避免使用任何标记为过时的类型或成员。 这是因为它可能不受支持，最终将从库的更高版本中删除。 在编译使用标记的类型或成员时 <xref:System.ObsoleteAttribute> ，将 <xref:System.ObsoleteAttribute.Message%2A> 显示该特性的属性。 这将为用户提供有关已过时的类型或成员的信息。 此信息通常包括库设计器支持过时的类型或成员的时间，以及要使用的首选替换。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将 `message` 参数添加到 <xref:System.ObsoleteAttribute> 构造函数。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 请勿禁止显示此规则发出的警告，因为 <xref:System.ObsoleteAttribute.Message%2A> 属性提供有关已过时的类型或成员的重要信息。

## <a name="example"></a>示例
 下面的示例显示一个已正确声明的过时成员 <xref:System.ObsoleteAttribute> 。

 [!code-cpp[FxCop.Design.ObsoleteAttributeOnMember#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.ObsoleteAttributeOnMember/cpp/FxCop.Design.ObsoleteAttributeOnMember.cpp#1)]
 [!code-csharp[FxCop.Design.ObsoleteAttributeOnMember#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ObsoleteAttributeOnMember/cs/FxCop.Design.ObsoleteAttributeOnMember.cs#1)]
 [!code-vb[FxCop.Design.ObsoleteAttributeOnMember#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.ObsoleteAttributeOnMember/vb/FxCop.Design.ObsoleteAttributeOnMember.vb#1)]

## <a name="see-also"></a>另请参阅
 <xref:System.ObsoleteAttribute?displayProperty=fullName>
