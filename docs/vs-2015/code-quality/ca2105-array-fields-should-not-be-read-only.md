---
title: CA2105:不应仅读取数组字段 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 4741b30d1429a1a179328c8fb4b150fc4f920612
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68154388"
---
# <a name="ca2105-array-fields-should-not-be-read-only"></a>CA2105:数组字段不应为只读
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|ArrayFieldsShouldNotBeReadOnly|
|CheckId|CA2105|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 保存数组的公共或受保护字段是只读的声明的。

## <a name="rule-description"></a>规则说明
 当应用`readonly`(`ReadOnly`中[!INCLUDE[vbprvb](../includes/vbprvb-md.md)]) 不能更改为包含一个数组，该字段的字段修饰符来指代不同的数组。 但是，可以更改在只读字段中存储的数组的元素。 制定决策或执行基于可以公开访问的只读数组的元素的操作的代码可能包含可利用的安全漏洞。

 请注意，具有公共字段也违反了设计规则[CA1051:不要声明可见实例字段](../code-quality/ca1051-do-not-declare-visible-instance-fields.md)。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决由该规则标识的安全漏洞，不要依赖于可公开访问的只读数组的内容。 强烈建议你使用以下过程之一：

- 将不能更改的强类型集合替换为数组。 有关详细信息，请参阅 <xref:System.Collections.ReadOnlyCollectionBase?displayProperty=fullName> 。

- 使用返回私有数组副本的方法替换公共字段。 你的代码不依赖于克隆，因为如果，则不存在风险修改元素。

  如果你选择第二种方法，请不该字段将替换为属性;属性返回数组造成负面影响性能。 有关详细信息，请参阅[CA1819:属性不应返回数组](../code-quality/ca1819-properties-should-not-return-arrays.md)。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 强烈建议不要使用此规则的警告中排除。 几乎在任何情况下发生其中只读字段的内容并不重要。 如果与你的方案的情况，请删除`readonly`修饰符而不是排除警告消息。

## <a name="example"></a>示例
 此示例演示了违反此规则的危险。 第一部分显示了一个示例库，它有一个类型， `MyClassWithReadOnlyArrayField`，，其中包含两个字段 (`grades`和`privateGrades`) 的不安全。 该字段`grades`是公共的而且因此容易受到任何调用方。 该字段`privateGrades`是私有的但是仍易受攻击，因为它将返回到调用方通过`GetPrivateGrades`方法。 `securePrivateGrades`以通过安全方式公开字段`GetSecurePrivateGrades`方法。 它声明为私有，应遵循良好的设计做法。 第二部分演示中存储的值更改的代码`grades`和`privateGrades`成员。

 示例类库显示在下面的示例。

 [!code-csharp[FxCop.Security.ArrayFieldsNotReadOnly#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.ArrayFieldsNotReadOnly/cs/FxCop.Security.ArrayFieldsNotReadOnly.cs#1)]

## <a name="example"></a>示例
 以下代码使用示例类库演示只读数组安全问题。

 [!code-csharp[FxCop.Security.TestArrayFieldsRead#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.TestArrayFieldsRead/cs/FxCop.Security.TestArrayFieldsRead.cs#1)]

 此示例的输出是：

 **之前篡改：等级：90，90，90 专用年级：90，90，90 保护等级，90，90，90**
**后篡改：等级：90、 555，90 专用年级：90、 555、 90 保护等级，90，90，90**
## <a name="see-also"></a>请参阅
 <xref:System.Array?displayProperty=fullName> <xref:System.Collections.ReadOnlyCollectionBase?displayProperty=fullName>
