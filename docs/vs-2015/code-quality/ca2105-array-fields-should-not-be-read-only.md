---
title: CA2105：数组字段不应为只读 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2105
- ArrayFieldsShouldNotBeReadOnly
helpviewer_keywords:
- ArrayFieldsShouldNotBeReadOnly
- CA2105
ms.assetid: 0bdc3421-3ceb-4182-b30c-a992fbfcc35d
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: db52bf869642a5bdcc28eeb0792b295ae314a508
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85538666"
---
# <a name="ca2105-array-fields-should-not-be-read-only"></a>CA2105:数组字段不应为只读
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|ArrayFieldsShouldNotBeReadOnly|
|CheckId|CA2105|
|Category|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 保存数组的公共或受保护字段声明为只读。

## <a name="rule-description"></a>规则描述
 `readonly` `ReadOnly` [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 向包含数组的字段应用（in）修饰符时，无法将该字段更改为引用其他数组。 但是，可以更改在只读字段中存储的数组的元素。 根据可公开访问的只读数组元素进行决策或执行操作的代码可能包含可利用的安全漏洞。

 请注意，拥有公共字段也会违反设计规则[CA1051：不要声明可见实例字段](../code-quality/ca1051-do-not-declare-visible-instance-fields.md)。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则标识的安全漏洞，请不要依赖于可公开访问的只读数组的内容。 强烈建议使用以下过程之一：

- 将数组替换为无法更改的强类型集合。 有关详细信息，请参阅 <xref:System.Collections.ReadOnlyCollectionBase?displayProperty=fullName>。

- 使用返回私有数组的克隆的方法替换公共字段。 由于你的代码不依赖于克隆，因此，如果修改了这些元素，则没有任何风险。

  如果选择第二种方法，请不要将该字段替换为属性;返回数组的属性会对性能产生负面影响。 有关详细信息，请参阅[CA1819：属性不应返回数组](../code-quality/ca1819-properties-should-not-return-arrays.md)。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 强烈建议排除此规则发出的警告。 几乎不会出现只读字段内容不重要的情况。 如果是这种情况，请删除该修饰符， `readonly` 而不是排除消息。

## <a name="example"></a>示例
 此示例演示违反此规则的危险。 第一部分显示一个具有类型的示例库，该类型 `MyClassWithReadOnlyArrayField` 包含不安全的两个字段（ `grades` 和 `privateGrades` ）。 此字段 `grades` 是公共的，因此很容易受到任何调用方的攻击。 该字段 `privateGrades` 是私有的，但仍有漏洞，因为它通过方法返回给调用方 `GetPrivateGrades` 。 此 `securePrivateGrades` 字段通过方法以安全的方式公开 `GetSecurePrivateGrades` 。 它被声明为私有，以遵循良好的设计做法。 第二个部分显示更改存储在和成员中的值的代码 `grades` `privateGrades` 。

 示例类库在下面的示例中显示。

 [!code-csharp[FxCop.Security.ArrayFieldsNotReadOnly#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.ArrayFieldsNotReadOnly/cs/FxCop.Security.ArrayFieldsNotReadOnly.cs#1)]

## <a name="example"></a>示例
 下面的代码使用示例类库来说明只读数组安全问题。

 [!code-csharp[FxCop.Security.TestArrayFieldsRead#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TestArrayFieldsRead/cs/FxCop.Security.TestArrayFieldsRead.cs#1)]

 此示例的输出为：

 **在篡改之前：成绩：90、90、90 Private 成绩：90、90、90安全等级、90、90、90** 
**篡改后：成绩：90、555、90 Private 成绩：90、555、90安全等级、90、90、90**
## <a name="see-also"></a>另请参阅
 <xref:System.Array?displayProperty=fullName> <xref:System.Collections.ReadOnlyCollectionBase?displayProperty=fullName>
