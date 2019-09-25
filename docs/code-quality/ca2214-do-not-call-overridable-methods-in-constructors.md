---
title: CA2214:不要在构造函数中调用可重写的方法
ms.date: 05/29/2016
ms.topic: reference
f1_keywords:
- DoNotCallOverridableMethodsInConstructors
- CA2214
helpviewer_keywords:
- CA2214
- DoNotCallOverridableMethodsInConstructors
ms.assetid: 335b57ca-a6e8-41b4-a20e-57ee172c97c3
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 8eb881da0a7ed243bda35079f617a314053f2d85
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71231291"
---
# <a name="ca2214-do-not-call-overridable-methods-in-constructors"></a>CA2214:不要在构造函数中调用可重写的方法

|||
|-|-|
|TypeName|DoNotCallOverridableMethodsInConstructors|
|CheckId|CA2214|
|类别|Microsoft.Usage|
|重大更改|不间断|

## <a name="cause"></a>原因

未密封类型的构造函数将调用在其类中定义的虚方法。

## <a name="rule-description"></a>规则说明

调用虚方法时，在运行时之前不会选择执行方法的实际类型。 当构造函数调用虚方法时，调用方法的实例的构造函数可能未执行。

> [!NOTE]
> 此规则的旧分析实现具有不同的诊断消息 " **\[构造函数名称] 包含一个调用链，该调用链会导致调用类定义的虚方法。查看以下调用堆栈中是否有意外**的结果：。 此规则的[FxCop 分析器](install-fxcop-analyzers.md)实现具有 "**请勿在构造函数中调用可重写方法**" 的诊断消息。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，请不要从该类型的构造函数内调用类型的虚拟方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

不禁止显示此规则发出的警告。 应对构造函数进行重新设计，以消除对虚拟方法的调用。

## <a name="example"></a>示例

下面的示例演示违反此规则的效果。 测试应用程序将创建的实例`DerivedType`，这将导致它的基类`BadlyConstructedType`（）构造函数执行。 `BadlyConstructedType`的构造函数错误地调用了`DoSomething`虚方法。 如输出所示， `DerivedType.DoSomething()`在执行`DerivedType`构造函数之前执行。

[!code-csharp[FxCop.Usage.CtorVirtual#1](../code-quality/codesnippet/CSharp/ca2214-do-not-call-overridable-methods-in-constructors_1.cs)]
[!code-vb[FxCop.Usage.CtorVirtual#1](../code-quality/codesnippet/VisualBasic/ca2214-do-not-call-overridable-methods-in-constructors_1.vb)]

该示例产生下面的输出：

```txt
Calling base ctor.
Derived DoSomething is called - initialized ? No
Calling derived ctor.
```