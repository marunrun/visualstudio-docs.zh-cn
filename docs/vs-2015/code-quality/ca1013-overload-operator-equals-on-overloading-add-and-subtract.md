---
title: CA1013:重载相等运算符，加法和减法 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- OverrideOperatorEqualsOnOverridingAddAndSubtract
- OverrideOperatorEqualsOnOverloadingAddAndSubtract
- CA1013
- OverloadOperatorEqualsOnOverloadingAddAndSubtract
helpviewer_keywords:
- OverrideOperatorEqualsOnOverloadingAddAndSubtract
- OverrideOperatorEqualsOnOverridingAddAndSubtract
- CA1013
- OverloadOperatorEqualsOnOverloadingAddAndSubtract
ms.assetid: 5bd28d68-c179-49ff-af47-5250b8b18a10
caps.latest.revision: 24
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 1b70085c83d842ccb5f8addc661af9109b5a5976
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65695625"
---
# <a name="ca1013-overload-operator-equals-on-overloading-add-and-subtract"></a>CA1013:重载加法方法和减法方法时重载相等运算符
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|OverloadOperatorEqualsOnOverloadingAddAndSubtract|
|CheckId|CA1013|
|类别|Microsoft.Design|
|是否重大更改|非换行|

## <a name="cause"></a>原因
 公共或受保护类型实现加或减运算符时没有实现相等运算符。

## <a name="rule-description"></a>规则说明
 类型的实例可以使用加法和减法运算来组合时应几乎始终定义相等，以便返回`true`的任何具有相同的构成值的两个实例。

 相等运算符的重载实现中，不能使用默认的相等运算符。 执行此操作将导致堆栈溢出。 若要实现相等运算符，请在实现中使用 Object.Equals 方法。 请参见以下示例。

```vb
If (Object.ReferenceEquals(left, Nothing)) Then
    Return Object.ReferenceEquals(right, Nothing)
Else
    Return left.Equals(right)
End If
```

```csharp
if (Object.ReferenceEquals(left, null))
    return Object.ReferenceEquals(right, null);
return left.Equals(right);
```

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请实现相等运算符，这样就与加法和减法运算符从数学上保持一致。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 它可以安全地禁止显示此规则的警告时的默认实现相等运算符的类型提供正确的行为。

## <a name="example"></a>示例
 以下示例定义一个类型 (`BadAddableType`) 这违反了此规则。 此类型应实现相等运算符，使任何具有测试相同的字段值的两个实例`true`是否相等。 类型`GoodAddableType`显示了已更正的实现。 请注意，此类型还实现是否不相等运算符，重写<xref:System.Object.Equals%2A>以满足其他规则。 完整的实现中还将实现<xref:System.Object.GetHashCode%2A>。

 [!code-csharp[FxCop.Design.AddAndSubtract#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.AddAndSubtract/cs/FxCop.Design.AddAndSubtract.cs#1)]

## <a name="example"></a>示例
 下面的示例为确定相等性测试，通过使用以前已在本主题阐释相等运算符的默认值和正确的行为中定义的类型的实例。

 [!code-csharp[FxCop.Design.TestAddAndSubtract#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.TestAddAndSubtract/cs/FxCop.Design.TestAddAndSubtract.cs#1)]

 本示例生成以下输出。

 **错误的类型： {2,2} {2,2}相等？否**
**很好的类型： {3,3} {3,3}相等？是**
**很好的类型： {3,3} {3,3}包括 = =？ 是**
**错误的类型： {2,2} {9,9}相等？否**
**很好的类型： {3,3} {9,9}包括 = =？ 不**
## <a name="see-also"></a>请参阅
 [相等运算符](https://msdn.microsoft.com/library/bc496a91-fefb-4ce0-ab4c-61f09964119a)
