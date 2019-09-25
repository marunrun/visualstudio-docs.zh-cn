---
title: CA1406:避免对 Visual Basic 6 客户端使用 Int64 参数
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- AvoidInt64ArgumentsForVB6Clients
- CA1406
helpviewer_keywords:
- AvoidInt64ArgumentsForVB6Clients
- CA1406
ms.assetid: d5d0d3fc-f105-43da-be5b-923ab023309c
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 82a8b1ea389c37dc63a9fe7366208a2a3028efb8
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71234800"
---
# <a name="ca1406-avoid-int64-arguments-for-visual-basic-6-clients"></a>CA1406:避免对 Visual Basic 6 客户端使用 Int64 参数

|||
|-|-|
|TypeName|AvoidInt64ArgumentsForVB6Clients|
|CheckId|CA1406|
|类别|Microsoft.Interoperability|
|重大更改|重大|

## <a name="cause"></a>原因
特别标记为对组件对象模型（COM）可见的类型会声明采用<xref:System.Int64?displayProperty=fullName>参数的成员。

## <a name="rule-description"></a>规则说明
Visual Basic 6 COM 客户端不能访问 64 位整数。

默认情况下，以下是对 COM 可见的：程序集、公共类型、公共类型中的公共实例成员以及公共值类型的所有成员。 但是，若要减少误报，此规则需要显式声明类型的 COM 可见性;必须用<xref:System.Runtime.InteropServices.ComVisibleAttribute?displayProperty=fullName>设置为`false`的将包含程序集标记为，且类型<xref:System.Runtime.InteropServices.ComVisibleAttribute>必须`true`标记为。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复其值始终可表示为32位整数的参数的此规则的冲突，请将参数类型更改为<xref:System.Int32?displayProperty=fullName>。 如果参数的值可能大于可以表示为32位整数的值，请将参数类型更改为<xref:System.Decimal?displayProperty=fullName>。 请注意， <xref:System.Single?displayProperty=fullName>和<xref:System.Double?displayProperty=fullName>都不会在<xref:System.Int64>数据类型的上限范围内丢失精度。 如果成员不是要对 COM 可见，请<xref:System.Runtime.InteropServices.ComVisibleAttribute>将其标记为。 `false`

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
如果确信 Visual Basic 6 个 COM 客户端将无法访问该类型，则可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例
下面的示例演示违反规则的类型。

[!code-csharp[FxCop.Interoperability.LongArgument#1](../code-quality/codesnippet/CSharp/ca1406-avoid-int64-arguments-for-visual-basic-6-clients_1.cs)]
[!code-vb[FxCop.Interoperability.LongArgument#1](../code-quality/codesnippet/VisualBasic/ca1406-avoid-int64-arguments-for-visual-basic-6-clients_1.vb)]

## <a name="related-rules"></a>相关规则
[CA1413避免在 COM 可见值类型中出现非公共字段](../code-quality/ca1413-avoid-non-public-fields-in-com-visible-value-types.md)

[CA1407避免在 COM 可见类型中出现静态成员](../code-quality/ca1407-avoid-static-members-in-com-visible-types.md)

[CA1017用 ComVisibleAttribute 标记程序集](../code-quality/ca1017-mark-assemblies-with-comvisibleattribute.md)

## <a name="see-also"></a>请参阅

- [与非托管代码交互操作](/dotnet/framework/interop/index)
- [Long 数据类型](/dotnet/visual-basic/language-reference/data-types/long-data-type)