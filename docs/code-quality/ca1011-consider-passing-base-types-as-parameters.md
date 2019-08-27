---
title: CA1011:考虑将基类型作为参数传递
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- ConsiderPassingBaseTypesAsParameters
- CA1011
helpviewer_keywords:
- CA1011
- ConsiderPassingBaseTypesAsParameters
ms.assetid: ce1e1241-dcf4-419b-9363-1d5bc4989279
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 644c581757a559311b6660a77c4d9190a7361314
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62779542"
---
# <a name="ca1011-consider-passing-base-types-as-parameters"></a>CA1011:考虑将基类型作为参数传递

|||
|-|-|
|TypeName|ConsiderPassingBaseTypesAsParameters|
|CheckId|CA1011|
|类别|Microsoft.Design|
|是否重大更改|重大|

## <a name="cause"></a>原因

方法声明中包含的形参是一个派生的类型，且该方法调用只有参数的基类型的成员。

## <a name="rule-description"></a>规则说明

在方法声明中将基类型指定为参数时，可以将派生自基类型的任何类型作为相应的参数传递给方法。 在方法体中使用参数时，执行的特定方法取决于自变量的类型。 如果不需要提供的派生类型的其他功能，则使用的基类型可以得到更广泛使用的方法。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复此规则的冲突，请更改与其基类型的参数类型。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

则可以安全地禁止显示此规则的警告

- 如果该方法需要提供的派生类型的特定功能

     \- 或 -

- 若要强制实施仅派生的类型或派生程度更大的类型，传递给方法。

在这些情况下，代码将由于强类型检查由编译器和运行时提供更可靠。

## <a name="example"></a>示例

下面的示例演示一种方法， `ManipulateFileStream`，，可仅与<xref:System.IO.FileStream>对象，与此规则冲突。 第二种方法， `ManipulateAnyStream`，通过替换来满足该规则<xref:System.IO.FileStream>通过使用参数<xref:System.IO.Stream>。

[!code-csharp[FxCop.Design.ConsiderPassingBaseTypes#1](../code-quality/codesnippet/CSharp/ca1011-consider-passing-base-types-as-parameters_1.cs)]
[!code-cpp[FxCop.Design.ConsiderPassingBaseTypes#1](../code-quality/codesnippet/CPP/ca1011-consider-passing-base-types-as-parameters_1.cpp)]
[!code-vb[FxCop.Design.ConsiderPassingBaseTypes#1](../code-quality/codesnippet/VisualBasic/ca1011-consider-passing-base-types-as-parameters_1.vb)]

## <a name="related-rules"></a>相关的规则

[CA1059:成员不应公开某些具体类型](../code-quality/ca1059-members-should-not-expose-certain-concrete-types.md)