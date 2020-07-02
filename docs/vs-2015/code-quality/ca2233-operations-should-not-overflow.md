---
title: CA2233：操作不应溢出 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- OperationsShouldNotOverflow
- CA2233
helpviewer_keywords:
- OperationsShouldNotOverflow
- CA2233
ms.assetid: 3a2b06ba-6d1b-4666-9eaf-e053ef47ffaa
caps.latest.revision: 21
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: eff09fb8f4423560c4681c94507d909f5864c69e
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545231"
---
# <a name="ca2233-operations-should-not-overflow"></a>CA2233:运算不应溢出
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|OperationsShouldNotOverflow|
|CheckId|CA2233|
|类别|Microsoft. 使用情况|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 方法执行算术运算，而不事先验证操作数以防止溢出。

## <a name="rule-description"></a>规则描述
 在未首先验证操作数的情况下，不应执行算术运算，以确保操作的结果不在涉及的数据类型的可能值范围之外。 根据执行上下文和所涉及的数据类型的不同，算术溢出会导致或结果的 <xref:System.OverflowException?displayProperty=fullName> 最高有效位被丢弃。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请在执行操作之前验证操作数。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果操作数的可能值永远不会导致算术运算溢出，则可以安全地禁止显示此规则发出的警告。

## <a name="example-of-a-violation"></a>冲突示例

### <a name="description"></a>描述
 下面的示例中的方法操作了违反此规则的整数。 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)]需要禁用**删除**整数溢出选项，此选项才会激发。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Usage.OperationOverflow#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.OperationOverflow/cs/FxCop.Usage.OperationOverflow.cs#1)]
 [!code-vb[FxCop.Usage.OperationOverflow#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.OperationOverflow/vb/FxCop.Usage.OperationOverflow.vb#1)]

### <a name="comments"></a>注释
 如果传递本示例中的方法 <xref:System.Int32.MinValue?displayProperty=fullName> ，则操作将下溢。 这会导致放弃结果的最高有效位。 下面的代码演示了这种情况。

 [C#]

```
public static void Main()
{
    int value = int.MinValue;    // int.MinValue is -2147483648
    value = Calculator.Decrement(value);
    Console.WriteLine(value);
}
```

 VB

```
Public Shared Sub Main()
    Dim value = Integer.MinValue    ' Integer.MinValue is -2147483648
    value = Calculator.Decrement(value)
    Console.WriteLine(value)
End Sub
```

### <a name="output"></a>Output

```
2147483647
```

## <a name="fix-with-input-parameter-validation"></a>修复了输入参数验证

### <a name="description"></a>描述
 下面的示例通过验证输入的值修复了之前的冲突。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Usage.OperationOverflowFixed#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.OperationOverflowFixed/cs/FxCop.Usage.OperationOverflowFixed.cs#1)]
 [!code-vb[FxCop.Usage.OperationOverflowFixed#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.OperationOverflowFixed/vb/FxCop.Usage.OperationOverflowFixed.vb#1)]

## <a name="fix-with-a-checked-block"></a>使用 Checked 块修复

### <a name="description"></a>描述
 下面的示例通过在已检查的块中包装操作来修复前面的冲突。 如果操作导致溢出， <xref:System.OverflowException?displayProperty=fullName> 将引发。

 请注意，中不支持选中的块 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Usage.OperationOverflowChecked#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.OperationOverflowChecked/cs/FxCop.Usage.OperationOverflowChecked.cs#1)]

## <a name="turn-on-checked-arithmetic-overflowunderflow"></a>打开选中的算术溢出/下溢
 如果打开 c # 中的选中算术溢出/下溢，则等效于在已检查的块中包装每个整数操作。

 **打开 C 中的选中算术溢出/下溢#**

1. 在**解决方案资源管理器**中，右键单击项目，然后选择 "**属性**"。

2. 选择“生成”选项卡，然后单击“高级”********。

3. 选择 "**检查算术溢出/下溢**" 并单击 **"确定"**。

## <a name="see-also"></a>另请参阅
 <xref:System.OverflowException?displayProperty=fullName>[C # 运算符](https://msdn.microsoft.com/library/0301e31f-22ad-49af-ac3c-d5eae7f0ac43) [Checked 和 Unchecked](https://msdn.microsoft.com/library/a84bc877-2c7f-4396-8735-1ce97c42f35e)
