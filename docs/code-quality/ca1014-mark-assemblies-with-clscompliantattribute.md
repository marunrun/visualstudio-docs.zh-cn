---
title: CA1014:用 CLSCompliantAttribute 标记程序集
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1014
- MarkAssembliesWithClsCompliant
helpviewer_keywords:
- CA1014
- MarkAssembliesWithClsCompliant
ms.assetid: 4fe57449-cf45-4745-bcd2-6345f1ed266d
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 387eb464959fba522e31f9586998335cb306d844
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71236329"
---
# <a name="ca1014-mark-assemblies-with-clscompliantattribute"></a>CA1014:用 CLSCompliantAttribute 标记程序集

|||
|-|-|
|TypeName|MarkAssembliesWithClsCompliant|
|CheckId|CA1014|
|类别|Microsoft.Design|
|重大更改|不间断|

## <a name="cause"></a>原因
没有对程序集应用<xref:System.CLSCompliantAttribute?displayProperty=fullName>属性。

## <a name="rule-description"></a>规则说明
公共语言规范 (CLS) 定义了程序集在跨编程语言使用时必须符合的命名限制、数据类型和规则。 良好的设计规定，所有程序集都明确指示<xref:System.CLSCompliantAttribute>与的 CLS 符合性。 如果该特性不存在于程序集，则该程序集不兼容。

符合 CLS 的程序集可能包含不符合的类型或类型成员。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突，请将特性添加到程序集。 应确定不符合的类型或类型成员，并将这些元素标记为不相容，而不是将整个程序集标记为不相容。 如果可能，应为不符合要求的成员提供符合 CLS 的替代项，以便尽可能最广泛的受众可以访问程序集的所有功能。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。 如果你不希望程序集符合，请应用属性并将其值设置为`false`。

## <a name="example"></a>示例
下面的示例演示一个已应用特性的<xref:System.CLSCompliantAttribute?displayProperty=fullName>程序集，该特性将声明为符合 CLS。

[!code-csharp[FxCop.Design.AssembliesCls#1](../code-quality/codesnippet/CSharp/ca1014-mark-assemblies-with-clscompliantattribute_1.cs)]
[!code-cpp[FxCop.Design.AssembliesCls#1](../code-quality/codesnippet/CPP/ca1014-mark-assemblies-with-clscompliantattribute_1.cpp)]
[!code-vb[FxCop.Design.AssembliesCls#1](../code-quality/codesnippet/VisualBasic/ca1014-mark-assemblies-with-clscompliantattribute_1.vb)]

## <a name="see-also"></a>请参阅

- <xref:System.CLSCompliantAttribute?displayProperty=fullName>
- [语言独立性和与语言无关的组件](/dotnet/standard/language-independence-and-language-independent-components)