---
title: CA2104:不要声明只读可变引用类型 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotDeclareReadOnlyMutableReferenceTypes
- CA2104
helpviewer_keywords:
- CA2104
- DoNotDeclareReadOnlyMutableReferenceTypes
ms.assetid: 81b83ee5-4db5-4be0-9f8d-90b53894ec3b
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: a4c6619bc5803c1b44e1c6b0516987c3110bbd30
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65687420"
---
# <a name="ca2104-do-not-declare-read-only-mutable-reference-types"></a>CA2104:不要声明只读可变引用类型
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DoNotDeclareReadOnlyMutableReferenceTypes|
|CheckId|CA2104|
|类别|Microsoft.Security|
|是否重大更改|非换行|

## <a name="cause"></a>原因
 外部可见类型包含外部可见的只读字段，该字段为可变的引用类型。

## <a name="rule-description"></a>规则说明
 可变类型是实例数据可被修改的类型。 <xref:System.Text.StringBuilder?displayProperty=fullName>类是可变引用类型的一个示例。 它包含可以更改的类的实例值的成员。 不可变的引用类型的一个示例是<xref:System.String?displayProperty=fullName>类。 已实例化后，其值可能永远不会更改。

 只读修饰符 ([readonly](https://msdn.microsoft.com/library/2f8081f6-0de2-4903-898d-99696c48d2f4)中C#， [ReadOnly](https://msdn.microsoft.com/library/e868185d-6142-4359-a2fd-a7965cadfce8)中[!INCLUDE[vbprvb](../includes/vbprvb-md.md)]，和[const](https://msdn.microsoft.com/library/b21c0271-1ad0-40a0-b21c-5e812bba0318)中C++) 的引用类型字段上 (指针在C++)防止字段替换为引用类型的不同实例。 但是，修饰符不会阻止通过引用类型进行修改的字段的实例数据。

 只读数组字段不受此规则，但是会导致违反了[CA2105:不应仅读取数组字段](../code-quality/ca2105-array-fields-should-not-be-read-only.md)规则。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请删除只读修饰符，或接受一项重大更改时，该字段将替换为不可变类型。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 它可以安全地禁止显示此规则的警告，如果字段类型是不可变。

## <a name="example"></a>示例
 下面的示例演示了一个导致该规则的冲突的字段声明。

 [!code-cpp[FxCop.Security.MutableReferenceTypes#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Security.MutableReferenceTypes/cpp/FxCop.Security.MutableReferenceTypes.cpp#1)]
 [!code-csharp[FxCop.Security.MutableReferenceTypes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.MutableReferenceTypes/cs/FxCop.Security.MutableReferenceTypes.cs#1)]
 [!code-vb[FxCop.Security.MutableReferenceTypes#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Security.MutableReferenceTypes/vb/FxCop.Security.MutableReferenceTypes.vb#1)]
