---
title: CA1014:用 CLSCompliantAttribute 标记程序集 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 324f52eaac86a6ff48b71a98714b866dfca8b239
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65704270"
---
# <a name="ca1014-mark-assemblies-with-clscompliantattribute"></a>CA1014:用 CLSCompliantAttribute 标记程序集
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|MarkAssembliesWithClsCompliant|
|CheckId|CA1014|
|类别|Microsoft.Design|
|是否重大更改|非换行|

## <a name="cause"></a>原因
 程序集不具有<xref:System.CLSCompliantAttribute?displayProperty=fullName>特性应用于它。

## <a name="rule-description"></a>规则说明
 公共语言规范 (CLS) 定义了程序集在跨编程语言使用时必须符合的命名限制、数据类型和规则。 好的设计要求所有程序集显式指示 CLS 遵从性与<xref:System.CLSCompliantAttribute>。 如果该属性不存在对程序集，该程序集不合规。

 很可能要包含的类型或类型不符合要求的成员的符合 cls 的程序集。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此规则的冲突，请将属性添加到该程序集。 而不是将标记为不符合要求的整个程序集，应确定哪些类型或类型成员将不符合策略，并将这种情况下，这些元素标记。 如果可能，应为不符合要求的成员提供符合 cls 的替代方法，以便尽可能多的受众可以访问您的程序集的所有功能。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。 如果不希望要符合要求的程序集，应用该特性并将其值设置为`false`。

## <a name="example"></a>示例
 下面的示例演示具有的程序集<xref:System.CLSCompliantAttribute?displayProperty=fullName>应用声明它符合 CLS 規格的属性。

 [!code-cpp[FxCop.Design.AssembliesCls#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.AssembliesCls/cpp/FxCop.Design.AssembliesCls.cpp#1)]
 [!code-csharp[FxCop.Design.AssembliesCls#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.AssembliesCls/cs/FxCop.Design.AssembliesCls.cs#1)]
 [!code-vb[FxCop.Design.AssembliesCls#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.AssembliesCls/vb/FxCop.Design.AssembliesCls.vb#1)]

## <a name="see-also"></a>请参阅
 <xref:System.CLSCompliantAttribute?displayProperty=fullName> [语言独立性和与语言无关的组件](https://msdn.microsoft.com/library/4f0b77d0-4844-464f-af73-6e06bedeafc6)
