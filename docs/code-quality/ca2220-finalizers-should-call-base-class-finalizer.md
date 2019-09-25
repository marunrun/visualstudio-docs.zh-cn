---
title: CA2220:终结器应调用基类的终结器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2220
- FinalizersShouldCallBaseClassFinalizer
helpviewer_keywords:
- CA2220
- FinalizersShouldCallBaseClassFinalizer
ms.assetid: 48329f42-170d-45ee-a381-e33f55a240c5
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e5af6b7872f0fa05183334e6acd2bc4922f84990
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71231163"
---
# <a name="ca2220-finalizers-should-call-base-class-finalizer"></a>CA2220:终结器应调用基类的终结器

|||
|-|-|
|TypeName|FinalizersShouldCallBaseClassFinalizer|
|CheckId|CA2220|
|类别|Microsoft.Usage|
|重大更改|不间断|

## <a name="cause"></a>原因

重写<xref:System.Object.Finalize%2A?displayProperty=fullName>的类型不会在其<xref:System.Object.Finalize%2A>基类中调用方法。

## <a name="rule-description"></a>规则说明

终止必须通过继承层次结构传播。 若要确保这一点，类型必须从其<xref:System.Object.Finalize%2A>自身<xref:System.Object.Finalize%2A>的方法中调用其基类方法。 C#编译器自动添加对基类终结器的调用。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，请<xref:System.Object.Finalize%2A> <xref:System.Object.Finalize%2A>从方法中调用基类型的方法。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

不禁止显示此规则发出的警告。 针对公共语言运行时的某些编译器会将对基类型的终结器的调用插入到 Microsoft 中间语言（MSIL）中。 如果报告了此规则发出的警告，则编译器不会插入调用，你必须将其添加到你的代码中。

## <a name="example"></a>示例

下面的 Visual Basic 示例显示了一个`TypeB`正确调用其基类<xref:System.Object.Finalize%2A>中的方法的类型。

[!code-vb[FxCop.Usage.IDisposableBaseCalled#1](../code-quality/codesnippet/VisualBasic/ca2220-finalizers-should-call-base-class-finalizer_1.vb)]

## <a name="see-also"></a>请参阅

- [释放模式](/dotnet/standard/design-guidelines/dispose-pattern)