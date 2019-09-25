---
title: CA1802:在合适的位置使用文本
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
- UseLiteralsWhereAppropriate
- CA1802
helpviewer_keywords:
- UseLiteralsWhereAppropriate
- CA1802
ms.assetid: 2515e4cd-9e61-486d-b067-58ba1a743ce4
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 435eb5a9fd7e41a69c873df4c728e42551734a37
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71253363"
---
# <a name="ca1802-use-literals-where-appropriate"></a>CA1802:在合适的位置使用文本

|||
|-|-|
|TypeName|UseLiteralsWhereAppropriate|
|CheckId|CA1802|
|类别|Microsoft.Performance|
|重大更改|不间断|

## <a name="cause"></a>原因

字段声明为， `static`并且`readonly` `ReadOnly`在`Shared` Visual Basic 中声明，并使用编译时可的值初始化。

默认情况下，此规则仅查看外部可见字段，但这是[可配置](#configurability)的。

## <a name="rule-description"></a>规则说明

当调用声明类型`static readonly`的静态构造函数时，将在运行时计算字段的值。 `static readonly`如果字段在声明时被初始化并且静态构造函数不是显式声明的，则编译器将发出一个静态构造函数来初始化字段。

`const`字段的值是在编译时计算的，并存储在元数据中，这会在与`static readonly`字段进行比较时增加运行时性能。

由于分配给目标字段的值是在编译时可的，因此将声明更改为`const`字段，以便在编译时而不是在运行时计算该值。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，请`static`将`readonly`和修饰符替换`const`为修饰符。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

如果性能不是问题，则可以安全地禁止显示此规则发出的警告，或禁用规则。

## <a name="configurability"></a>配置

如果从[FxCop 分析器](install-fxcop-analyzers.md)（而不是传统分析）运行此规则，则可以根据其可访问性，将基本代码的哪些部分配置为在上运行此规则。 例如，若要指定规则只应针对非公共 API 图面运行，请在项目中的 editorconfig 文件中添加以下键/值对：

```ini
dotnet_code_quality.ca1802.api_surface = private, internal
```

您可以为此规则、所有规则或此类别中的所有规则（性能）配置此选项。 有关详细信息，请参阅[配置 FxCop 分析器](configure-fxcop-analyzers.md)。

## <a name="example"></a>示例

下面的示例演示了一个类型`UseReadOnly`，该类型违反了规则和满足规则`UseConstant`的类型。

[!code-vb[FxCop.Performance.UseLiterals#1](../code-quality/codesnippet/VisualBasic/ca1802-use-literals-where-appropriate_1.vb)]
[!code-csharp[FxCop.Performance.UseLiterals#1](../code-quality/codesnippet/CSharp/ca1802-use-literals-where-appropriate_1.cs)]