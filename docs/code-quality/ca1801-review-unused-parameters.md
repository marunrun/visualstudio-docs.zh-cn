---
title: CA1801:检查未使用的参数
ms.date: 06/24/2019
ms.topic: reference
f1_keywords:
- AvoidUnusedParameters
- CA1801
- ReviewUnusedParameters
helpviewer_keywords:
- CA1801
- ReviewUnusedParameters
ms.assetid: 5d73545c-e153-4b7c-a7b2-be6bf5aca5be
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a73ce207d8efb0c6309ba52648c7231f89bc7984
ms.sourcegitcommit: 0f44ec8ba0263056ad04d2d0dc904ad4206ce8fc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/06/2019
ms.locfileid: "70766046"
---
# <a name="ca1801-review-unused-parameters"></a>CA1801:检查未使用的参数

|||
|-|-|
|TypeName|ReviewUnusedParameters|
|CheckId|CA1801|
|类别|Microsoft.Usage|
|是否重大更改|否-如果该成员在程序集外部不可见，不管你进行了何种更改。<br /><br /> 否-如果将成员更改为在其主体中使用参数，则为。<br /><br /> 如果删除参数，则该参数在程序集外可见。|

## <a name="cause"></a>原因

方法签名包含方法体中未使用的参数。

此规则不检查以下几种方法：

- 委托引用的方法。

- 用作事件处理程序的方法。

- 用`abstract` （`MustOverride`在 Visual Basic）修饰符中声明的方法。

- 用`virtual` （`Overridable`在 Visual Basic）修饰符中声明的方法。

- 用`override` （`Overrides`在 Visual Basic）修饰符中声明的方法。

- 用`extern` （`Declare`语句 Visual Basic）修饰符声明的方法。

如果使用[FxCop 分析器](install-fxcop-analyzers.md)，则此规则不会标记使用[丢弃](/dotnet/csharp/discards)符号命名的参数， `_` `_1`例如、、和`_2`。 这会减少签名要求所需的参数的警告性噪音，例如，用作委托的方法、具有特殊属性的参数或其值在运行时由框架隐式访问但未在中被引用的参数编写.

## <a name="rule-description"></a>规则说明

查看未在方法体中使用的非虚方法中的参数，以确保不存在任何不正确来访问它们。 未使用的参数会产生维护和性能成本。

有时，违反此规则可能会指向方法中的实现 bug。 例如，参数应已在方法体中使用。 如果参数必须存在，因为向后兼容性，则禁止显示此规则的警告。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，请删除未使用的参数（重大更改），或在方法体中使用参数（非重大更改）。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

可以安全地禁止显示此规则发出的警告：

- 在以前发布的代码中，修复程序会是一项重大更改。

- 对于的自定义扩展<xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert?displayProperty=nameWithType>方法中的参数。`this` <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert>类中的函数是静态的，因此无需访问方法体中的`this`参数。

## <a name="example"></a>示例

下面的示例演示了两种方法。 一个方法违反了规则，另一个方法满足规则。

[!code-csharp[FxCop.Usage.ReviewUnusedParameters#1](../code-quality/codesnippet/CSharp/ca1801-review-unused-parameters_1.cs)]

## <a name="related-rules"></a>相关规则

[CA1811避免使用未调用的私有代码](../code-quality/ca1811-avoid-uncalled-private-code.md)

[CA1812避免未实例化的内部类](../code-quality/ca1812-avoid-uninstantiated-internal-classes.md)

[CA1804删除未使用的局部变量](../code-quality/ca1804-remove-unused-locals.md)
