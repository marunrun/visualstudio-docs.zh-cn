---
title: CA1051:不要声明可见实例字段 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 96e518977e12f2ae061d5ab73803d51dad733149
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65686825"
---
# <a name="ca1051-do-not-declare-visible-instance-fields"></a>CA1051:不要声明可见实例字段
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DoNotDeclareVisibleInstanceFields|
|CheckId|CA1051|
|类别|Microsoft.Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 外部可见的类型具有一个外部可见实例字段。

## <a name="rule-description"></a>规则说明
 字段的主要用途应是作为实现的详细信息。 字段应`private`或`internal`和应通过使用属性公开。 很容易访问的属性是要访问的字段和属性访问器中的代码可以更改随着类型的功能扩展，而不会引入重大更改。 只需返回私有或内部字段的值的属性进行了优化来执行与相媲美访问字段;很少的性能提升是通过属性与外部可见字段的使用相关联。

 外部可见指`public`， `protected`，并`protected internal`(`Public`， `Protected`，并`Protected Friend`在 Visual Basic 中) 可访问性级别。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此规则的冲突，使字段`private`或`internal`并将其公开使用的外部可见的属性。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。 外部可见字段不提供对属性不可用的任何权益。 此外，不能由保护公共字段[链接要求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)。 请参阅[CA2112:受保护的类型不应公开字段](../code-quality/ca2112-secured-types-should-not-expose-fields.md)。

## <a name="example"></a>示例
 下面的示例演示一种类型 (`BadPublicInstanceFields`) 这违反了此规则。 `GoodPublicInstanceFields` 显示了更正后的代码。

 [!code-csharp[FxCop.Design.TypesPublicInstanceFields#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.TypesPublicInstanceFields/cs/FxCop.Design.TypesPublicInstanceFields.cs#1)]

## <a name="related-rules"></a>相关的规则
 [CA2112:受保护的类型不应公开字段](../code-quality/ca2112-secured-types-should-not-expose-fields.md)

## <a name="see-also"></a>请参阅
 [链接需求](https://msdn.microsoft.com/library/a33fd5f9-2de9-4653-a4f0-d9df25082c4d)
