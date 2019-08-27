---
title: CA1034:嵌套的类型不应是可见 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 915b5807f7b14269acf4b7509ffceaecfb13af47
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62536394"
---
# <a name="ca1034-nested-types-should-not-be-visible"></a>CA1034:嵌套类型不应是可见的
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|NestedTypesShouldNotBeVisible|
|CheckId|CA1034|
|类别|Microsoft.Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 外部可见类型包含的外部可见的类型声明。 嵌套的枚举和受保护的类型不受此规则。

## <a name="rule-description"></a>规则说明
 嵌套的类型是另一种类型的范围内声明的类型。 嵌套的类型可用于封装包含类型的私有实现详细信息。 如果用于此用途，则嵌套类型不应是外部可见的。

 不使用外部可见的嵌套的类型的逻辑分组或以避免名称冲突;相反，使用命名空间。

 嵌套的类型包括成员可访问性，其中一些程序员不清楚地了解这一概念。

 子类和高级自定义方案中的嵌套的类型中，可以使用受保护的类型。

## <a name="how-to-fix-violations"></a>如何解决冲突
 如果你确实想要从外部可见的嵌套的类型，更改类型的可访问性。 否则，删除从其父级的嵌套的类型。 如果嵌套的目的是进行分类的嵌套的类型，使用命名空间改为创建层次结构。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例显示了违反了此规则的类型。

 [!code-cpp[FxCop.Design.NestedTypes#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Design.NestedTypes/cpp/FxCop.Design.NestedTypes.cpp#1)]
 [!code-csharp[FxCop.Design.NestedTypes#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.NestedTypes/cs/FxCop.Design.NestedTypes.cs#1)]
 [!code-vb[FxCop.Design.NestedTypes#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Design.NestedTypes/vb/FxCop.Design.NestedTypes.vb#1)]
