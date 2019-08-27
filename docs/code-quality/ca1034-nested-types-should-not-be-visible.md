---
title: CA1034:嵌套类型不应是可见的
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- NestedTypesShouldNotBeVisible
- CA1034
helpviewer_keywords:
- NestedTypesShouldNotBeVisible
- CA1034
ms.assetid: e9789a2c-2540-42a1-8705-ae7104011194
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: a086ad80bd13fb18f866769db34d72cae3e67496
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68922863"
---
# <a name="ca1034-nested-types-should-not-be-visible"></a>CA1034:嵌套类型不应是可见的

|||
|-|-|
|TypeName|NestedTypesShouldNotBeVisible|
|CheckId|CA1034|
|类别|Microsoft.Design|
|是否重大更改|重大|

## <a name="cause"></a>原因

外部可见类型包含外部可见的类型声明。 嵌套的枚举和受保护的类型不受此规则的保护。

## <a name="rule-description"></a>规则说明
嵌套类型是在另一个类型的范围内声明的类型。 嵌套类型适用于封装包含类型的私有实现详细信息。 如果用于此用途，则嵌套类型不应是外部可见的。

不要使用外部可见的嵌套类型进行逻辑分组或避免名称冲突;请改用命名空间。

嵌套类型包括成员可访问性的概念, 而某些程序员并不清楚清楚。

在高级自定义方案中, 可以在子类和嵌套类型中使用受保护的类型。

## <a name="how-to-fix-violations"></a>如何解决冲突
如果不想让嵌套类型在外部可见, 请更改类型的可访问性。 否则, 请从其父级中删除嵌套类型。 如果嵌套的目的是对嵌套类型进行分类, 请改用命名空间来创建层次结构。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。

## <a name="example"></a>示例
下面的示例演示违反规则的类型。

[!code-cpp[FxCop.Design.NestedTypes#1](../code-quality/codesnippet/CPP/ca1034-nested-types-should-not-be-visible_1.cpp)]
[!code-csharp[FxCop.Design.NestedTypes#1](../code-quality/codesnippet/CSharp/ca1034-nested-types-should-not-be-visible_1.cs)]
[!code-vb[FxCop.Design.NestedTypes#1](../code-quality/codesnippet/VisualBasic/ca1034-nested-types-should-not-be-visible_1.vb)]