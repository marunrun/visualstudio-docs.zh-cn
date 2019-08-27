---
title: CA1413:避免在 COM 可见值类型中使用非公共字段
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1413
- AvoidNonpublicFieldsInComVisibleValueTypes
helpviewer_keywords:
- CA1413
- AvoidNonpublicFieldsInComVisibleValueTypes
ms.assetid: 1352e7eb-fefc-4239-8847-25edc7804a54
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 3eb216af1b6cd742aff83b248b6752adea292345
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68921843"
---
# <a name="ca1413-avoid-non-public-fields-in-com-visible-value-types"></a>CA1413:避免在 COM 可见值类型中使用非公共字段

|||
|-|-|
|TypeName|AvoidNonpublicFieldsInComVisibleValueTypes|
|CheckId|CA1413|
|类别|Microsoft.Interoperability|
|是否重大更改|重大|

## <a name="cause"></a>原因
特别标记为对组件对象模型 (COM) 可见的值类型声明非公共实例字段。

## <a name="rule-description"></a>规则说明
对 COM 可见的值类型的非公共实例字段对 COM 客户端可见。 请查看字段的内容, 以了解不应公开的信息, 或者可能会产生意外的设计或安全影响的信息。

默认情况下, 所有公共值类型对 COM 都可见。 但是, 若要减少误报, 此规则需要显式声明类型的 COM 可见性。 必须用<xref:System.Runtime.InteropServices.ComVisibleAttribute?displayProperty=fullName>设置为`false`的将包含程序集标记为, 且类型<xref:System.Runtime.InteropServices.ComVisibleAttribute>必须`true`标记为。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突并使字段保持隐藏状态, 请将值类型更改为引用类型或<xref:System.Runtime.InteropServices.ComVisibleAttribute>从类型中删除该属性。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
如果可以接受此字段的公开泄露, 则可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例
下面的示例演示违反规则的类型。

[!code-csharp[FxCop.Interoperability.NonpublicField#1](../code-quality/codesnippet/CSharp/ca1413-avoid-non-public-fields-in-com-visible-value-types_1.cs)]
[!code-vb[FxCop.Interoperability.NonpublicField#1](../code-quality/codesnippet/VisualBasic/ca1413-avoid-non-public-fields-in-com-visible-value-types_1.vb)]

## <a name="related-rules"></a>相关规则
[CA1407避免在 COM 可见类型中出现静态成员](../code-quality/ca1407-avoid-static-members-in-com-visible-types.md)

[CA1017用 ComVisibleAttribute 标记程序集](../code-quality/ca1017-mark-assemblies-with-comvisibleattribute.md)

## <a name="see-also"></a>请参阅

- [与非托管代码交互操作](/dotnet/framework/interop/index)
- [为互操作限定 .NET 类型](/dotnet/framework/interop/qualifying-net-types-for-interoperation)