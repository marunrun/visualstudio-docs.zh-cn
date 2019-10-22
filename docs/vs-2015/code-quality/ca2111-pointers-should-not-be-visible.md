---
title: CA2111：指针不应为 visible |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- PointersShouldNotBeVisible
- CA2111
helpviewer_keywords:
- CA2111
- PointersShouldNotBeVisible
ms.assetid: b3a8d466-895b-43bc-a2df-5d7058fe915f
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: a0d5546c6f6a2f5dbd0c6063f4a1dfd40ce1d7bb
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72658741"
---
# <a name="ca2111-pointers-should-not-be-visible"></a>CA2111：指针应为不可见
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|PointersShouldNotBeVisible|
|CheckId|CA2111|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 公共或受保护的 <xref:System.IntPtr?displayProperty=fullName> 或 <xref:System.UIntPtr?displayProperty=fullName> 字段不是只读的。

## <a name="rule-description"></a>规则说明
 <xref:System.IntPtr> 和 <xref:System.UIntPtr> 是用于访问非托管内存的指针类型。 如果指针不是私有、内部或只读，则恶意代码可以更改指针的值，这可能会允许访问内存中的任意位置或导致应用程序或系统故障。

 如果要保护对包含指针字段的类型的访问，请参阅[CA2112：受保护的类型不应公开字段](../code-quality/ca2112-secured-types-should-not-expose-fields.md)。

## <a name="how-to-fix-violations"></a>如何解决冲突
 通过使指针成为只读的、内部的或私有的，使其安全。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果不依赖指针的值，则禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的代码显示了违反和满足规则的指针。 请注意，非私有指针也违反规则[CA1051： "不要声明可见实例字段](../code-quality/ca1051-do-not-declare-visible-instance-fields.md)"。

 [!code-csharp[FxCop.Security.PointersArePrivate#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.PointersArePrivate/cs/FxCop.Security.PointersArePrivate.cs#1)]

## <a name="related-rules"></a>相关规则
 [CA2112：受保护的类型不应公开字段](../code-quality/ca2112-secured-types-should-not-expose-fields.md)

 [CA1051：不要声明可见实例字段](../code-quality/ca1051-do-not-declare-visible-instance-fields.md)

## <a name="see-also"></a>请参阅
 <xref:System.IntPtr?displayProperty=fullName> <xref:System.UIntPtr?displayProperty=fullName>
