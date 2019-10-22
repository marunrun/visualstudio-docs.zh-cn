---
title: CA1051：不要声明可见实例字段 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1051
- DoNotDeclareVisibleInstanceFields
helpviewer_keywords:
- CA1051
- DoNotDeclareVisibleInstanceFields
ms.assetid: 2805376c-824c-462c-81d1-c51aaf7cabe7
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 41332ab7d729f7b2187ccace6b05fe2d17763a0d
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72672520"
---
# <a name="ca1051-do-not-declare-visible-instance-fields"></a>CA1051：不要声明可见实例字段
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DoNotDeclareVisibleInstanceFields|
|CheckId|CA1051|
|类别|Microsoft. Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 外部可见类型包含外部可见的实例字段。

## <a name="rule-description"></a>规则说明
 字段的主要用途应是作为实现的详细信息。 字段应 `private` 或 `internal` 并且应使用属性公开。 在访问某个字段时，可以轻松访问该属性，而属性访问器中的代码可以在扩展类型功能时更改，而不会引入重大更改。 仅返回私有字段或内部字段的值的属性，经过优化，可在与访问字段相同的情况上执行：性能提升极少与属性上的外部可见字段的使用相关联。

 外部可见指的是 `public`、`protected` 和 `protected internal` （`Public`、`Protected` 和 `Protected Friend`）可访问性级别。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将该字段 `private` 或 `internal`，并使用外部可见的属性将其公开。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。 外部可见字段不提供属性无法使用的任何权益。 此外，公共字段不能通过[链接要求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)进行保护。 请参阅[CA2112：受保护的类型不应公开字段](../code-quality/ca2112-secured-types-should-not-expose-fields.md)。

## <a name="example"></a>示例
 下面的示例演示了违反此规则的类型（`BadPublicInstanceFields`）。 `GoodPublicInstanceFields` 显示更正后的代码。

 [!code-csharp[FxCop.Design.TypesPublicInstanceFields#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.TypesPublicInstanceFields/cs/FxCop.Design.TypesPublicInstanceFields.cs#1)]

## <a name="related-rules"></a>相关规则
 [CA2112：受保护的类型不应公开字段](../code-quality/ca2112-secured-types-should-not-expose-fields.md)

## <a name="see-also"></a>请参阅
 [链接需求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)
