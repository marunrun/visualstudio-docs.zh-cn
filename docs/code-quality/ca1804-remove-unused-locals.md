---
title: CA1804:移除未使用的局部变量
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1804
- RemoveUnusedLocals
helpviewer_keywords:
- RemoveUnusedLocals
- CA1804
ms.assetid: cc332e67-6543-4813-bd8a-6f6fc75bf22a
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 0a83d0afffc50c7697fad98c4dc49e31770d63d4
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71233755"
---
# <a name="ca1804-remove-unused-locals"></a>CA1804:移除未使用的局部变量

|||
|-|-|
|TypeName|RemoveUnusedLocals|
|CheckId|CA1804|
|类别|Microsoft.Performance|
|重大更改|不间断|

## <a name="cause"></a>原因
一个方法声明一个局部变量，但不使用除这种变量之外的变量，因为它可能作为赋值语句的接收方。 对于此规则进行的分析，必须使用调试信息生成经过测试的程序集，并且关联的程序数据库（.pdb）文件必须可用。

## <a name="rule-description"></a>规则说明
未使用的局部变量和不必要的赋值会增加程序集的大小并降低性能。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，请删除或使用局部变量。

> [!NOTE]
> 启用C#该选项后，编译器会删除`optimize`未使用的局部变量。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
如果编译器发出了编译器，则禁止显示此规则发出的警告。 如果性能和代码维护不是主要考虑因素，则可以安全地禁止显示此规则发出的警告或禁用规则。

## <a name="example"></a>示例
下面的示例显示了几个未使用的局部变量。

[!code-vb[FxCop.Performance.UnusedLocals#1](../code-quality/codesnippet/VisualBasic/ca1804-remove-unused-locals_1.vb)]
[!code-csharp[FxCop.Performance.UnusedLocals#1](../code-quality/codesnippet/CSharp/ca1804-remove-unused-locals_1.cs)]

## <a name="related-rules"></a>相关规则
[CA1809避免过多的局部变量](../code-quality/ca1809-avoid-excessive-locals.md)

[CA1811避免使用未调用的私有代码](../code-quality/ca1811-avoid-uncalled-private-code.md)

[CA1812避免未实例化的内部类](../code-quality/ca1812-avoid-uninstantiated-internal-classes.md)

[CA1801查看未使用的参数](../code-quality/ca1801-review-unused-parameters.md)