---
title: CA2105:数组字段不应为只读
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2105
- ArrayFieldsShouldNotBeReadOnly
helpviewer_keywords:
- ArrayFieldsShouldNotBeReadOnly
- CA2105
ms.assetid: 0bdc3421-3ceb-4182-b30c-a992fbfcc35d
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7407fcbe035d02992f414027114d69c257f5f390
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71232914"
---
# <a name="ca2105-array-fields-should-not-be-read-only"></a>CA2105:数组字段不应为只读

|||
|-|-|
|TypeName|ArrayFieldsShouldNotBeReadOnly|
|CheckId|CA2105|
|类别|Microsoft.Security|
|重大更改|重大|

## <a name="cause"></a>原因

保存数组的公共或受保护字段声明为只读。

## <a name="rule-description"></a>规则说明

向包含数组的`readonly`字段`ReadOnly`应用[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]（in）修饰符时，无法将该字段更改为引用其他数组。 但是，可以更改在只读字段中存储的数组的元素。 根据可公开访问的只读数组元素进行决策或执行操作的代码可能包含可利用的安全漏洞。

请注意，拥有公共字段也会违反设计规则[CA1051：不要声明可见实例字段](../code-quality/ca1051-do-not-declare-visible-instance-fields.md)。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复此规则标识的安全漏洞，请不要依赖于可公开访问的只读数组的内容。 强烈建议使用以下过程之一：

- 将数组替换为无法更改的强类型集合。 有关详细信息，请参阅 <xref:System.Collections.ReadOnlyCollectionBase?displayProperty=fullName> 。

- 使用返回私有数组的克隆的方法替换公共字段。 由于你的代码不依赖于克隆，因此，如果修改了这些元素，则没有任何风险。

如果选择第二种方法，请不要将该字段替换为属性;返回数组的属性会对性能产生负面影响。 有关详细信息，请[参阅 CA1819：属性不应返回数组](../code-quality/ca1819-properties-should-not-return-arrays.md)。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

强烈建议排除此规则发出的警告。 几乎不会出现只读字段内容不重要的情况。 如果是这种情况，请删除`readonly`该修饰符，而不是排除消息。

## <a name="example-1"></a>示例 1

此示例演示违反此规则的危险。 第一部分显示一个具有类型的示例库，该类型`MyClassWithReadOnlyArrayField`包含不安全的两个`grades`字段`privateGrades`（和）。 此字段`grades`是公共的，因此很容易受到任何调用方的攻击。 该字段`privateGrades`是私有的，但仍有漏洞，因为它`GetPrivateGrades`通过方法返回给调用方。 此`securePrivateGrades`字段`GetSecurePrivateGrades`通过方法以安全的方式公开。 它被声明为私有，以遵循良好的设计做法。 第二个部分显示更改存储在和`grades` `privateGrades`成员中的值的代码。

示例类库在下面的示例中显示。

[!code-csharp[FxCop.Security.ArrayFieldsNotReadOnly#1](../code-quality/codesnippet/CSharp/ca2105-array-fields-should-not-be-read-only_1.cs)]

## <a name="example-2"></a>示例 2

下面的代码使用示例类库来说明只读数组安全问题。

[!code-csharp[FxCop.Security.TestArrayFieldsRead#1](../code-quality/codesnippet/CSharp/ca2105-array-fields-should-not-be-read-only_2.cs)]

此示例的输出为：

```text
Before tampering: Grades: 90, 90, 90 Private Grades: 90, 90, 90  Secure Grades, 90, 90, 90
After tampering: Grades: 90, 555, 90 Private Grades: 90, 555, 90  Secure Grades, 90, 90, 90
```

## <a name="related-rules"></a>相关规则

- [CA2104不要声明只读可变引用类型](../code-quality/ca2104-do-not-declare-read-only-mutable-reference-types.md)

## <a name="see-also"></a>请参阅

- <xref:System.Array?displayProperty=fullName>
- <xref:System.Collections.ReadOnlyCollectionBase?displayProperty=fullName>
