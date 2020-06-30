---
title: CA1406：避免 Visual Basic 6 个客户端的 Int64 参数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- AvoidInt64ArgumentsForVB6Clients
- CA1406
helpviewer_keywords:
- AvoidInt64ArgumentsForVB6Clients
- CA1406
ms.assetid: d5d0d3fc-f105-43da-be5b-923ab023309c
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: b6ab93c24cd97d498ae886c7a9184fd4a5f111f1
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85534909"
---
# <a name="ca1406-avoid-int64-arguments-for-visual-basic-6-clients"></a>CA1406:避免对 Visual Basic 6 客户端使用 Int64 参数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|AvoidInt64ArgumentsForVB6Clients|
|CheckId|CA1406|
|Category|Microsoft. 互操作性|
|是否重大更改|重大|

## <a name="cause"></a>原因
 特别标记为对组件对象模型（COM）可见的类型会声明采用参数的成员 <xref:System.Int64?displayProperty=fullName> 。

## <a name="rule-description"></a>规则描述
 Visual Basic 6 COM 客户端不能访问 64 位整数。

 默认情况下，以下是对 COM 可见的：程序集、公共类型、公共类型中的公共实例成员以及公共值类型的所有成员。 但是，若要减少误报，此规则需要显式声明类型的 COM 可见性;必须用设置为的将包含程序集标记为 <xref:System.Runtime.InteropServices.ComVisibleAttribute?displayProperty=fullName> `false` ，且类型必须标记为 <xref:System.Runtime.InteropServices.ComVisibleAttribute> `true` 。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复其值始终可表示为32位整数的参数的此规则的冲突，请将参数类型更改为 <xref:System.Int32?displayProperty=fullName> 。 如果参数的值可能大于可以表示为32位整数的值，请将参数类型更改为 <xref:System.Decimal?displayProperty=fullName> 。 请注意， <xref:System.Single?displayProperty=fullName> 和都不 <xref:System.Double?displayProperty=fullName> 会在数据类型的上限范围内丢失精度 <xref:System.Int64> 。 如果成员不是要对 COM 可见，请将其标记 <xref:System.Runtime.InteropServices.ComVisibleAttribute> 为 `false` 。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果确信 Visual Basic 6 个 COM 客户端将无法访问该类型，则可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示违反规则的类型。

 [!code-csharp[FxCop.Interoperability.LongArgument#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.LongArgument/cs/FxCop.Interoperability.LongArgument.cs#1)]
 [!code-vb[FxCop.Interoperability.LongArgument#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.LongArgument/vb/FxCop.Interoperability.LongArgument.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA1413:避免在 COM 可见值类型中使用非公共字段](../code-quality/ca1413-avoid-non-public-fields-in-com-visible-value-types.md)

 [CA1407:避免在 COM 可见类型中使用静态成员](../code-quality/ca1407-avoid-static-members-in-com-visible-types.md)

 [CA1017:用 ComVisibleAttribute 标记程序集](../code-quality/ca1017-mark-assemblies-with-comvisibleattribute.md)

## <a name="see-also"></a>另请参阅
 [与非托管代码](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)[长数据类型](https://msdn.microsoft.com/library/b4770c34-1804-4f8c-b512-c10b0893e516)互操作
