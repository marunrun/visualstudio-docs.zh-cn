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
ms.openlocfilehash: dcb5937f58088684e7bfc204ab4143434b0684ae
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71236397"
---
# <a name="ca1011-consider-passing-base-types-as-parameters"></a>CA1011:考虑将基类型作为参数传递

|||
|-|-|
|TypeName|ConsiderPassingBaseTypesAsParameters|
|CheckId|CA1011|
|类别|Microsoft.Design|
|重大更改|重大|

## <a name="cause"></a>原因

方法声明包含一个派生类型的形参，而方法仅调用该参数的基类型的成员。

## <a name="rule-description"></a>规则说明

在方法声明中将基类型指定为参数时，可以将派生自基类型的任何类型作为相应的参数传递给方法。 在方法体中使用参数时，执行的特定方法取决于参数的类型。 如果派生类型提供的其他功能不是必需的，则使用基类型可以更广泛使用该方法。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，请将参数的类型更改为其基类型。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

可以安全地禁止显示此规则发出的警告

- 如果方法需要由派生类型提供的特定功能，

     \- 或 -

- 若要强制只将派生类型或派生程度更高的类型传递给方法。

在这些情况下，由于编译器和运行时提供的强类型检查，代码将更可靠。

## <a name="example"></a>示例

下面的示例演示一个方法， `ManipulateFileStream`该方法只能<xref:System.IO.FileStream>与与此规则冲突的对象一起使用。 第二种方法`ManipulateAnyStream`是通过使用<xref:System.IO.FileStream> <xref:System.IO.Stream>替换参数来满足规则。

[!code-csharp[FxCop.Design.ConsiderPassingBaseTypes#1](../code-quality/codesnippet/CSharp/ca1011-consider-passing-base-types-as-parameters_1.cs)]
[!code-cpp[FxCop.Design.ConsiderPassingBaseTypes#1](../code-quality/codesnippet/CPP/ca1011-consider-passing-base-types-as-parameters_1.cpp)]
[!code-vb[FxCop.Design.ConsiderPassingBaseTypes#1](../code-quality/codesnippet/VisualBasic/ca1011-consider-passing-base-types-as-parameters_1.vb)]

## <a name="related-rules"></a>相关规则

[CA1059成员不应公开某些具体类型](../code-quality/ca1059-members-should-not-expose-certain-concrete-types.md)