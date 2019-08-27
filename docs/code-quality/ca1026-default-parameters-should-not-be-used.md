---
title: CA1026:不应使用默认形参
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1026
- DefaultParametersShouldNotBeUsed
helpviewer_keywords:
- CA1026
- DefaultParametersShouldNotBeUsed
ms.assetid: 09643415-36ef-4d0f-9411-5721e14e2512
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 888e1b5d551e357eb732dfe3f7661d51cbdf089d
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68923144"
---
# <a name="ca1026-default-parameters-should-not-be-used"></a>CA1026:不应使用默认形参

|||
|-|-|
|TypeName|DefaultParametersShouldNotBeUsed|
|CheckId|CA1026|
|类别|Microsoft.Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
外部可见类型包含使用默认参数的外部可见方法。

## <a name="rule-description"></a>规则说明
在公共语言规范 (CLS) 下允许使用默认参数的方法;但是, CLS 允许编译器忽略分配给这些参数的值。 为忽略默认参数值的编译器编写的代码必须为每个默认参数显式提供参数。 若要跨编程语言维护所需的行为, 则应使用提供默认参数的方法重载替换使用默认参数的方法。

C++当访问托管代码时, 编译器将忽略托管扩展的默认参数值。 Visual Basic 编译器支持具有使用[可选](/dotnet/visual-basic/language-reference/modifiers/optional)关键字的默认参数的方法。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突, 请将使用默认参数的方法替换为提供默认参数的方法重载。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。

## <a name="example"></a>示例
下面的示例演示一个使用默认参数的方法, 以及提供等效功能的重载方法。

[!code-vb[FxCop.Design.DefaultParameters#1](../code-quality/codesnippet/VisualBasic/ca1026-default-parameters-should-not-be-used_1.vb)]

## <a name="related-rules"></a>相关规则
[CA1025用形参数组替换重复的实参](../code-quality/ca1025-replace-repetitive-arguments-with-params-array.md)

## <a name="see-also"></a>请参阅
[语言独立性和与语言无关的组件](/dotnet/standard/language-independence-and-language-independent-components)