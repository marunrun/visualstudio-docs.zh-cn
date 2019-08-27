---
title: CA2233:运算不应溢出
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- OperationsShouldNotOverflow
- CA2233
helpviewer_keywords:
- OperationsShouldNotOverflow
- CA2233
ms.assetid: 3a2b06ba-6d1b-4666-9eaf-e053ef47ffaa
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 7c07dde4c3b992db30c9fc72a0dfa01f0f13b31e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62806597"
---
# <a name="ca2233-operations-should-not-overflow"></a>CA2233:运算不应溢出

|||
|-|-|
|TypeName|OperationsShouldNotOverflow|
|CheckId|CA2233|
|类别|Microsoft.Usage|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因

某方法执行的算术运算，并且不会验证事先操作数以防止溢出。

## <a name="rule-description"></a>规则说明

请不要在没有首先验证操作数以确保操作的结果不涉及的数据类型的可能值的范围之外执行算术运算。 根据执行上下文和涉及的数据类型，算术溢出可能导致在<xref:System.OverflowException?displayProperty=fullName>或放弃结果的最高有效位。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复此规则的冲突，请验证操作数之前执行该操作。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

它可以安全地禁止显示此规则的警告，如果操作数的可能的值将永远不会导致算术运算溢出。

## <a name="example-of-a-violation"></a>冲突的示例

下面的示例中的方法可操作违反了此规则的整数。 [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 需要**删除**整数溢出选项禁用此激发。

[!code-vb[FxCop.Usage.OperationOverflow#1](../code-quality/codesnippet/VisualBasic/ca2233-operations-should-not-overflow_1.vb)]
[!code-csharp[FxCop.Usage.OperationOverflow#1](../code-quality/codesnippet/CSharp/ca2233-operations-should-not-overflow_1.cs)]

如果在此示例中该方法传递<xref:System.Int32.MinValue?displayProperty=fullName>，则操作将下溢。 这会导致要放弃的结果的最高有效位。 下面的代码演示如何发生这种情况。

```csharp
public static void Main()
{
    int value = int.MinValue;    // int.MinValue is -2147483648
    value = Calculator.Decrement(value);
    Console.WriteLine(value);
}
```

```vb
Public Shared Sub Main()
    Dim value = Integer.MinValue    ' Integer.MinValue is -2147483648
    value = Calculator.Decrement(value)
    Console.WriteLine(value)
End Sub
```

输出：

```text
2147483647
```

## <a name="fix-with-input-parameter-validation"></a>使用输入的参数验证修复

下面的示例通过验证输入的值来修复了上一冲突。

[!code-csharp[FxCop.Usage.OperationOverflowFixed#1](../code-quality/codesnippet/CSharp/ca2233-operations-should-not-overflow_2.cs)]
[!code-vb[FxCop.Usage.OperationOverflowFixed#1](../code-quality/codesnippet/VisualBasic/ca2233-operations-should-not-overflow_2.vb)]

## <a name="fix-with-a-checked-block"></a>Checked 块修复

下面的示例通过选中块中包装操作修复了上一冲突。 如果该操作会导致溢出时，<xref:System.OverflowException?displayProperty=fullName>将引发。

Checked 的块中不支持[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]。

[!code-csharp[FxCop.Usage.OperationOverflowChecked#1](../code-quality/codesnippet/CSharp/ca2233-operations-should-not-overflow_3.cs)]

## <a name="turn-on-checked-arithmetic-overflowunderflow"></a>开启检查算术上溢/下溢

如果您打开已检查算术上溢/下溢 C# 中，相当于选中块中包装每个整数操作。

若要启用检查算术上溢/下溢 C# 中：

1. 在中**解决方案资源管理器**，右键单击项目，然后选择**属性**。

2. 选择“生成”选项卡，然后单击“高级”。

3. 选择**检查算术上溢/下溢**然后单击**确定**。

## <a name="see-also"></a>请参阅

- <xref:System.OverflowException?displayProperty=fullName>
- [C# 运算符](/dotnet/csharp/language-reference/operators/index)
- [Checked and Unchecked](/dotnet/csharp/language-reference/keywords/checked-and-unchecked)