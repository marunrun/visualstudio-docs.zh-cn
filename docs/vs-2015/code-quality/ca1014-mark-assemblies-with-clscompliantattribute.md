---
title: CA1014：用 CLSCompliantAttribute 标记程序集 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1014
- MarkAssembliesWithClsCompliant
helpviewer_keywords:
- CA1014
- MarkAssembliesWithClsCompliant
ms.assetid: 4fe57449-cf45-4745-bcd2-6345f1ed266d
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 9408a7b55c800a7979c39075afdf8e9e6e4c7cdb
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72663151"
---
# <a name="ca1014-mark-assemblies-with-clscompliantattribute"></a>CA1014：用 CLSCompliantAttribute 标记程序集
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|MarkAssembliesWithClsCompliant|
|CheckId|CA1014|
|类别|Microsoft. Design|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 程序集未应用 <xref:System.CLSCompliantAttribute?displayProperty=fullName> 特性。

## <a name="rule-description"></a>规则说明
 公共语言规范 (CLS) 定义了程序集在跨编程语言使用时必须符合的命名限制、数据类型和规则。 良好的设计规定，所有程序集都明确指示与 <xref:System.CLSCompliantAttribute> 的 CLS 符合性。 如果该特性不存在于程序集，则该程序集不兼容。

 符合 CLS 的程序集可能包含不符合的类型或类型成员。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将特性添加到程序集。 应确定不符合的类型或类型成员，并将这些元素标记为不相容，而不是将整个程序集标记为不相容。 如果可能，应为不符合要求的成员提供符合 CLS 的替代项，以便尽可能最广泛的受众可以访问程序集的所有功能。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。 如果你不希望程序集符合，请应用属性，并将其值设置为 `false`。

## <a name="example"></a>示例
 下面的示例演示一个应用了 <xref:System.CLSCompliantAttribute?displayProperty=fullName> 特性的程序集，该特性将声明为符合 CLS。

 [!code-cpp[FxCop.Design.AssembliesCls#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.AssembliesCls/cpp/FxCop.Design.AssembliesCls.cpp#1)]
 [!code-csharp[FxCop.Design.AssembliesCls#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.AssembliesCls/cs/FxCop.Design.AssembliesCls.cs#1)]
 [!code-vb[FxCop.Design.AssembliesCls#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.AssembliesCls/vb/FxCop.Design.AssembliesCls.vb#1)]

## <a name="see-also"></a>请参阅
 <xref:System.CLSCompliantAttribute?displayProperty=fullName>[语言独立性和与语言无关的组件](https://msdn.microsoft.com/library/4f0b77d0-4844-464f-af73-6e06bedeafc6)
