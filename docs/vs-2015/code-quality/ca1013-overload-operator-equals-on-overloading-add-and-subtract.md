---
title: CA1013：重载加法和减法时重载相等运算符 |Microsoft Docs
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
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: dd1c144f04150e3965e2c0264b80147cbd9b8f19
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72663201"
---
# <a name="ca1013-overload-operator-equals-on-overloading-add-and-subtract"></a>CA1013：重载加法方法和减法方法时重载相等运算符
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|OverloadOperatorEqualsOnOverloadingAddAndSubtract|
|CheckId|CA1013|
|类别|Microsoft. Design|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 公共或受保护类型实现加或减运算符时没有实现相等运算符。

## <a name="rule-description"></a>规则说明
 如果可以使用加法和减法等运算组合类型的实例，则几乎应始终定义相等性，以便为具有相同构成值的任意两个实例返回 `true`。

 不能在相等运算符的重载实现中使用默认的相等运算符。 这样做将导致堆栈溢出。 若要实现相等运算符，请在实现中使用对象 Equals 方法。 请参见以下示例。

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
 若要修复与此规则的冲突，请实现相等运算符，使其在数学上与加法和减法运算符保持一致。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果相等运算符的默认实现为类型提供了正确的行为，则可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例定义了违反此规则的类型（`BadAddableType`）。 此类型应实现相等运算符，以使具有相同字段值的任意两个实例测试 `true` 是否相等。 类型 `GoodAddableType` 显示已更正的实现。 请注意，此类型还实现不等运算符，并覆盖 <xref:System.Object.Equals%2A> 以满足其他规则。 完整的实现还将实现 <xref:System.Object.GetHashCode%2A>。

 [!code-csharp[FxCop.Design.AddAndSubtract#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.AddAndSubtract/cs/FxCop.Design.AddAndSubtract.cs#1)]

## <a name="example"></a>示例
 下面的示例通过使用之前在本主题中定义的类型的实例来测试相等性，以说明相等运算符的默认行为和正确行为。

 [!code-csharp[FxCop.Design.TestAddAndSubtract#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.TestAddAndSubtract/cs/FxCop.Design.TestAddAndSubtract.cs#1)]

 本示例生成以下输出。

 **错误的类型： {2,2} {2,2} 是否相同？无**
**良好类型： {3,3} {3,3} 是否相等？是**
**好类型： {3,3} 0 为 = =？  是**1**错误类型： 3 4 是否相同？无**5**良好类型： 7 8 为 = =？  否**
## <a name="see-also"></a>请参阅
 [相等运算符](https://msdn.microsoft.com/library/bc496a91-fefb-4ce0-ab4c-61f09964119a)
