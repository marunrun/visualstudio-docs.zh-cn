---
title: CA2104:不要声明只读可变引用类型
ms.date: 11/01/2018
ms.topic: reference
f1_keywords:
- DoNotDeclareReadOnlyMutableReferenceTypes
- CA2104
helpviewer_keywords:
- CA2104
- DoNotDeclareReadOnlyMutableReferenceTypes
ms.assetid: 81b83ee5-4db5-4be0-9f8d-90b53894ec3b
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 40fdeefc2d664b80bb6e17c109349cb5912b0516
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62545350"
---
# <a name="ca2104-do-not-declare-read-only-mutable-reference-types"></a>CA2104:不要声明只读可变引用类型

|||
|-|-|
|TypeName|DoNotDeclareReadOnlyMutableReferenceTypes|
|CheckId|CA2104|
|类别|Microsoft.Security|
|是否重大更改|非换行|

> [!NOTE]
> 规则 CA2104 已过时，将 Visual Studio 的未来版本中删除。 不将作为实现[分析器](roslyn-analyzers-overview.md)由于所需确定一种类型的实际不变性的复杂分析。

## <a name="cause"></a>原因

外部可见类型包含外部可见的只读字段，该字段为可变的引用类型。

## <a name="rule-description"></a>规则说明

可变类型是实例数据可被修改的类型。 <xref:System.Text.StringBuilder?displayProperty=fullName>类是可变引用类型的一个示例。 它包含可以更改的类的实例值的成员。 不可变的引用类型的一个示例是<xref:System.String?displayProperty=fullName>类。 已实例化后，其值可能永远不会更改。

只读修饰符 ([readonly](/dotnet/csharp/language-reference/keywords/readonly)中C#， [ReadOnly](/dotnet/visual-basic/language-reference/modifiers/readonly)在 Visual Basic 中，和[const](/cpp/cpp/const-cpp)在C++) 的引用类型字段上 (或指针中的C++)防止字段替换为引用类型的不同实例。 但是，修饰符不会阻止通过引用类型进行修改的字段的实例数据。

此规则可能会无意中显示一种类型的冲突的是，实际上，不可变。 在这种情况下，则可以安全地禁止显示警告。

只读数组字段不受此规则，但是会导致违反了[CA2105:不应仅读取数组字段](../code-quality/ca2105-array-fields-should-not-be-read-only.md)规则。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复此规则的冲突，请删除只读修饰符，或接受一项重大更改时，该字段将替换为不可变类型。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

它可以安全地禁止显示此规则的警告，如果字段类型是不可变。

## <a name="example"></a>示例

下面的示例演示了一个导致该规则的冲突的字段声明：

[!code-cpp[FxCop.Security.MutableReferenceTypes#1](../code-quality/codesnippet/CPP/ca2104-do-not-declare-read-only-mutable-reference-types_1.cpp)]
[!code-csharp[FxCop.Security.MutableReferenceTypes#1](../code-quality/codesnippet/CSharp/ca2104-do-not-declare-read-only-mutable-reference-types_1.cs)]
[!code-vb[FxCop.Security.MutableReferenceTypes#1](../code-quality/codesnippet/VisualBasic/ca2104-do-not-declare-read-only-mutable-reference-types_1.vb)]