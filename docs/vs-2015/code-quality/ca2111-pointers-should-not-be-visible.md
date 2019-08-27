---
title: CA2111:指针不应是可见 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 8497433088e4c49868a76dd3281d02a5e79babe5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68154366"
---
# <a name="ca2111-pointers-should-not-be-visible"></a>CA2111:指针应为不可见
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|PointersShouldNotBeVisible|
|CheckId|CA2111|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 公共或受保护<xref:System.IntPtr?displayProperty=fullName>或<xref:System.UIntPtr?displayProperty=fullName>字段不是只读的。

## <a name="rule-description"></a>规则说明
 <xref:System.IntPtr> 和<xref:System.UIntPtr>是用于访问非托管的内存的指针类型。 如果指针不是私有、 内部或只读的恶意代码可以更改指针，有可能允许访问内存中的任意位置或导致应用程序或系统故障的值。

 如果你想要对包含指针字段的类型的安全访问，请参阅[CA2112:受保护的类型不应公开字段](../code-quality/ca2112-secured-types-should-not-expose-fields.md)。

## <a name="how-to-fix-violations"></a>如何解决冲突
 通过使只读的、 内部或私有来保护指针。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果您不依赖于指针的值，禁止显示此规则的警告。

## <a name="example"></a>示例
 下面的代码演示与冲突，并满足该规则的指针。 请注意，非私有指针还违反规则[CA1051:不要声明可见实例字段](../code-quality/ca1051-do-not-declare-visible-instance-fields.md)。

 [!code-csharp[FxCop.Security.PointersArePrivate#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.PointersArePrivate/cs/FxCop.Security.PointersArePrivate.cs#1)]

## <a name="related-rules"></a>相关的规则
 [CA2112:受保护的类型不应公开字段](../code-quality/ca2112-secured-types-should-not-expose-fields.md)

 [CA1051:不要声明可见实例字段](../code-quality/ca1051-do-not-declare-visible-instance-fields.md)

## <a name="see-also"></a>请参阅
 <xref:System.IntPtr?displayProperty=fullName> <xref:System.UIntPtr?displayProperty=fullName>
