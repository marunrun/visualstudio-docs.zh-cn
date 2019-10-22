---
title: CA1413：避免在 COM 可见值类型中出现非公共字段 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1413
- AvoidNonpublicFieldsInComVisibleValueTypes
helpviewer_keywords:
- CA1413
- AvoidNonpublicFieldsInComVisibleValueTypes
ms.assetid: 1352e7eb-fefc-4239-8847-25edc7804a54
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 7d66c2c52b6ee7f7d1d2fbbd461ca8c1251ce13d
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72652702"
---
# <a name="ca1413-avoid-non-public-fields-in-com-visible-value-types"></a>CA1413：避免在 COM 可见值类型中使用非公共字段
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|AvoidNonpublicFieldsInComVisibleValueTypes|
|CheckId|CA1413|
|类别|Microsoft. 互操作性|
|是否重大更改|重大|

## <a name="cause"></a>原因
 特别标记为对组件对象模型（COM）可见的值类型声明非公共实例字段。

## <a name="rule-description"></a>规则说明
 对 COM 可见的值类型的非公共实例字段对 COM 客户端可见。 请查看字段的内容，以了解不应公开的信息，或者可能会产生意外的设计或安全影响的信息。

 默认情况下，所有公共值类型对 COM 都可见。 但是，若要减少误报，此规则需要显式声明类型的 COM 可见性。 必须将包含程序集标记为 <xref:System.Runtime.InteropServices.ComVisibleAttribute?displayProperty=fullName> 设置为 `false`，并且必须将该类型标记为 <xref:System.Runtime.InteropServices.ComVisibleAttribute> 设置为 `true`。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突并使字段保持隐藏状态，请将值类型更改为引用类型或从类型中删除 <xref:System.Runtime.InteropServices.ComVisibleAttribute> 特性。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果可以接受此字段的公开泄露，则可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示违反规则的类型。

 [!code-csharp[FxCop.Interoperability.NonpublicField#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.NonpublicField/cs/FxCop.Interoperability.NonpublicField.cs#1)]
 [!code-vb[FxCop.Interoperability.NonpublicField#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.NonpublicField/vb/FxCop.Interoperability.NonpublicField.vb#1)]

## <a name="related-rules"></a>相关规则
 [CA1407：避免在 COM 可见类型中使用静态成员](../code-quality/ca1407-avoid-static-members-in-com-visible-types.md)

 [CA1017：用 ComVisibleAttribute 标记程序集](../code-quality/ca1017-mark-assemblies-with-comvisibleattribute.md)

## <a name="see-also"></a>请参阅
 [与非托管代码](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)的互操作性，[为互操作提供 .net 类型](https://msdn.microsoft.com/library/4b8afb52-fb8d-4e65-b47c-fd82956a3cdd)
