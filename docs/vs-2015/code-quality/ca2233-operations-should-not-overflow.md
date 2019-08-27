---
title: CA2233:运算不应溢出 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 0531a739ec00c3e6224ef5caa7b1c0bf71f0e4e4
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65697951"
---
# <a name="ca2233-operations-should-not-overflow"></a>CA2233:运算不应溢出
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|OperationsShouldNotOverflow|
|CheckId|CA2233|
|类别|Microsoft.Usage|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 某方法执行的算术运算，并且不会验证事先操作数以防止溢出。

## <a name="rule-description"></a>规则说明
 不应在没有首先验证操作数以确保操作的结果不涉及的数据类型的可能值的范围之外执行算术运算。 根据执行上下文和涉及的数据类型，算术溢出可能导致在<xref:System.OverflowException?displayProperty=fullName>或放弃结果的最高有效位。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请验证操作数之前执行该操作。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 它可以安全地禁止显示此规则的警告，如果操作数的可能的值将永远不会导致算术运算溢出。

## <a name="example-of-a-violation"></a>冲突的示例

### <a name="description"></a>描述
 下面的示例中的方法可操作违反了此规则的整数。 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 需要**删除**整数溢出选项禁用此激发。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Usage.OperationOverflow#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.OperationOverflow/cs/FxCop.Usage.OperationOverflow.cs#1)]
 [!code-vb[FxCop.Usage.OperationOverflow#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.OperationOverflow/vb/FxCop.Usage.OperationOverflow.vb#1)]

### <a name="comments"></a>注释
 如果在此示例中该方法传递<xref:System.Int32.MinValue?displayProperty=fullName>，则操作将下溢。 这会导致要放弃的结果的最高有效位。 下面的代码演示如何发生这种情况。

 [C#]

```
public static void Main()
{
    int value = int.MinValue;    // int.MinValue is -2147483648
    value = Calculator.Decrement(value);
    Console.WriteLine(value);
}
```

 [VB]

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

## <a name="fix-with-input-parameter-validation"></a>使用输入的参数验证修复

### <a name="description"></a>描述
 下面的示例通过验证输入的值来修复了上一冲突。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Usage.OperationOverflowFixed#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.OperationOverflowFixed/cs/FxCop.Usage.OperationOverflowFixed.cs#1)]
 [!code-vb[FxCop.Usage.OperationOverflowFixed#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Usage.OperationOverflowFixed/vb/FxCop.Usage.OperationOverflowFixed.vb#1)]

## <a name="fix-with-a-checked-block"></a>Checked 块修复

### <a name="description"></a>描述
 下面的示例通过选中块中包装操作修复了上一冲突。 如果该操作会导致溢出时，<xref:System.OverflowException?displayProperty=fullName>将引发。

 请注意选中的块中不支持[!INCLUDE[vbprvb](../includes/vbprvb-md.md)]。

### <a name="code"></a>代码
 [!code-csharp[FxCop.Usage.OperationOverflowChecked#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Usage.OperationOverflowChecked/cs/FxCop.Usage.OperationOverflowChecked.cs#1)]

## <a name="turn-on-checked-arithmetic-overflowunderflow"></a>开启检查算术上溢/下溢
 如果您打开已检查算术上溢/下溢 C# 中，相当于选中块中包装每个整数操作。

 **若要启用检查算术上溢/下溢 C# 中**

1. 在中**解决方案资源管理器**，右键单击项目，然后选择**属性**。

2. 选择“生成”选项卡，然后单击“高级”。

3. 选择**检查算术上溢/下溢**然后单击**确定**。

## <a name="see-also"></a>请参阅
 <xref:System.OverflowException?displayProperty=fullName> [C# 运算符](https://msdn.microsoft.com/library/0301e31f-22ad-49af-ac3c-d5eae7f0ac43) [Checked 和 Unchecked](https://msdn.microsoft.com/library/a84bc877-2c7f-4396-8735-1ce97c42f35e)
