---
title: CA1413:避免在 COM 可见值类型中的非公共字段 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 59ca3c5f53dee43bdd73eb706f03792458e71698
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65691137"
---
# <a name="ca1413-avoid-non-public-fields-in-com-visible-value-types"></a>CA1413:避免在 COM 可见值类型中使用非公共字段
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|AvoidNonpublicFieldsInComVisibleValueTypes|
|CheckId|CA1413|
|类别|Microsoft.Interoperability|
|是否重大更改|重大|

## <a name="cause"></a>原因
 专门标记为可见到组件对象模型 (COM) 的值类型声明的非公共实例字段。

## <a name="rule-description"></a>规则说明
 对 COM 可见的值类型的非公共实例字段对 COM 客户端可见。 查看信息不应公开或将具有意外的设计或安全影响字段的内容。

 默认情况下，所有公共值类型都是对 COM 可见。 但是，若要减少误报，此规则要求显式声明的类型的 COM 可见性。 包含程序集必须使用标记<xref:System.Runtime.InteropServices.ComVisibleAttribute?displayProperty=fullName>设置为`false`和类型必须标有<xref:System.Runtime.InteropServices.ComVisibleAttribute>设置为`true`。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，并保持隐藏的字段，将值类型更改为引用类型或删除<xref:System.Runtime.InteropServices.ComVisibleAttribute>属性的类型。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 它可以安全地禁止显示此规则的警告，如果公开的字段是可接受。

## <a name="example"></a>示例
 下面的示例显示了违反了此规则的类型。

 [!code-csharp[FxCop.Interoperability.NonpublicField#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Interoperability.NonpublicField/cs/FxCop.Interoperability.NonpublicField.cs#1)]
 [!code-vb[FxCop.Interoperability.NonpublicField#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Interoperability.NonpublicField/vb/FxCop.Interoperability.NonpublicField.vb#1)]

## <a name="related-rules"></a>相关的规则
 [CA1407:避免在 COM 可见类型中的静态成员](../code-quality/ca1407-avoid-static-members-in-com-visible-types.md)

 [CA1017:用 ComVisibleAttribute 标记程序集](../code-quality/ca1017-mark-assemblies-with-comvisibleattribute.md)

## <a name="see-also"></a>请参阅
 [与进行互操作非托管代码](https://msdn.microsoft.com/library/ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258)[为互操作限定.NET 类型](https://msdn.microsoft.com/library/4b8afb52-fb8d-4e65-b47c-fd82956a3cdd)
