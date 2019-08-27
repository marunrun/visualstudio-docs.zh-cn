---
title: CA1041:提供 ObsoleteAttribute 消息 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: fe14ca0c0e917896a2ed5a31a03a8c1a7057d613
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62559814"
---
# <a name="ca1041-provide-obsoleteattribute-message"></a>CA1041:提供 ObsoleteAttribute 消息
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|ProvideObsoleteAttributeMessage|
|CheckId|CA1041|
|类别|Microsoft.Design|
|是否重大更改|非换行|

## <a name="cause"></a>原因
 通过使用标记的类型或成员<xref:System.ObsoleteAttribute?displayProperty=fullName>属性不具有其<xref:System.ObsoleteAttribute.Message%2A?displayProperty=fullName>指定属性。

## <a name="rule-description"></a>规则说明
 <xref:System.ObsoleteAttribute> 用于标记不推荐使用的库类型和成员。 库的使用者应避免使用任何类型或成员标记为已过时。 这是库的因为它可能不受支持并最终将从更高版本中删除。 类型或成员使用的标记时<xref:System.ObsoleteAttribute>进行编译，<xref:System.ObsoleteAttribute.Message%2A>显示特性的属性。 这将为用户提供有关已过时的类型或成员的信息。 此信息通常包括多长时间的已过时的类型或成员将支持的库设计器并使用首选的替代。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请添加`message`参数<xref:System.ObsoleteAttribute>构造函数。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 因为不禁止显示此规则的警告<xref:System.ObsoleteAttribute.Message%2A>属性提供有关已过时的类型或成员的关键信息。

## <a name="example"></a>示例
 下面的示例显示了过时的成员具有正确声明<xref:System.ObsoleteAttribute>。

 [!code-cpp[FxCop.Design.ObsoleteAttributeOnMember#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.ObsoleteAttributeOnMember/cpp/FxCop.Design.ObsoleteAttributeOnMember.cpp#1)]
 [!code-csharp[FxCop.Design.ObsoleteAttributeOnMember#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.ObsoleteAttributeOnMember/cs/FxCop.Design.ObsoleteAttributeOnMember.cs#1)]
 [!code-vb[FxCop.Design.ObsoleteAttributeOnMember#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.ObsoleteAttributeOnMember/vb/FxCop.Design.ObsoleteAttributeOnMember.vb#1)]

## <a name="see-also"></a>请参阅
 <xref:System.ObsoleteAttribute?displayProperty=fullName>
