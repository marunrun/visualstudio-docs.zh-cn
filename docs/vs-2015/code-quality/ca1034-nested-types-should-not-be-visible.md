---
title: CA1034：嵌套类型不应是可见的 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- NestedTypesShouldNotBeVisible
- CA1034
helpviewer_keywords:
- NestedTypesShouldNotBeVisible
- CA1034
ms.assetid: e9789a2c-2540-42a1-8705-ae7104011194
caps.latest.revision: 20
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 04a982c993ffbb04a3e7600dfb93a00e80727b84
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85542163"
---
# <a name="ca1034-nested-types-should-not-be-visible"></a>CA1034:嵌套类型不应是可见的
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|NestedTypesShouldNotBeVisible|
|CheckId|CA1034|
|Category|Microsoft. Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 外部可见类型包含外部可见的类型声明。 嵌套的枚举和受保护的类型不受此规则的保护。

## <a name="rule-description"></a>规则描述
 嵌套类型是在另一个类型的范围内声明的类型。 嵌套类型适用于封装包含类型的私有实现详细信息。 如果用于此用途，则嵌套类型不应是外部可见的。

 不要使用外部可见的嵌套类型进行逻辑分组或避免名称冲突;请改用命名空间。

 嵌套类型包括成员可访问性的概念，而某些程序员并不清楚清楚。

 在高级自定义方案中，可以在子类和嵌套类型中使用受保护的类型。

## <a name="how-to-fix-violations"></a>如何解决冲突
 如果不想让嵌套类型在外部可见，请更改类型的可访问性。 否则，请从其父级中删除嵌套类型。 如果嵌套的目的是对嵌套类型进行分类，请改用命名空间来创建层次结构。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示违反规则的类型。

 [!code-cpp[FxCop.Design.NestedTypes#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.NestedTypes/cpp/FxCop.Design.NestedTypes.cpp#1)]
 [!code-csharp[FxCop.Design.NestedTypes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.NestedTypes/cs/FxCop.Design.NestedTypes.cs#1)]
 [!code-vb[FxCop.Design.NestedTypes#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.NestedTypes/vb/FxCop.Design.NestedTypes.vb#1)]
