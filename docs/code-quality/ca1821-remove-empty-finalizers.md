---
title: CA1821:移除空终结器
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- RemoveEmptyFinalizers
- CA1821
helpviewer_keywords:
- CA1821
ms.assetid: 3f4855a0-e4a0-46e6-923c-4c3b7074048d
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9c8c4d4ca04c7a9a21cd1e80e4dc06e8d5a92c2f
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68921377"
---
# <a name="ca1821-remove-empty-finalizers"></a>CA1821:移除空终结器

|||
|-|-|
|TypeName|RemoveEmptyFinalizers|
|CheckId|CA1821|
|类别|Microsoft.Performance|
|是否重大更改|不间断|

## <a name="cause"></a>原因
类型实现了一个空的终结器, 只调用基类型的终结器或只调用有条件发出的方法。

## <a name="rule-description"></a>规则说明
应尽可能避免终结器，因为跟踪对象生存期会产生额外的性能系统开销。 垃圾回收器将在收集对象之前运行终结器。 这意味着将需要两个集合来收集对象。 空终结器会产生这种额外的开销, 而不会带来任何好处。

## <a name="how-to-fix-violations"></a>如何解决冲突
删除空的终结器。 如果调试需要终结器, 请将整个终结器置于指令`#if DEBUG / #endif`中。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
请勿禁止显示此规则的消息。 取消终止失败会降低性能, 而不会带来任何好处。

## <a name="example"></a>示例
下面的示例演示了应删除的空终结器、应括在指令中`#if DEBUG / #endif`的终结器以及正确`#if DEBUG / #endif`使用指令的终结器。

[!code-csharp[FxCop.Performance.RemoveEmptyFinalizers#1](../code-quality/codesnippet/CSharp/ca1821-remove-empty-finalizers_1.cs)]