---
title: CA1065:不要在意外的位置引发异常
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1065
- DoNotRaiseExceptionsInUnexpectedLocations
helpviewer_keywords:
- DoNotRaiseExceptionsInUnexpectedLocations
- CA1065
ms.assetid: 4e1bade4-4ca2-4219-abc3-c7b2d741e157
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 257100be0eb2766ef413854795c934b230e29370
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71235249"
---
# <a name="ca1065-do-not-raise-exceptions-in-unexpected-locations"></a>CA1065:不要在意外的位置引发异常

|||
|-|-|
|TypeName|DoNotRaiseExceptionsInUnexpectedLocations|
|CheckId|CA1065|
|类别|Microsoft.Design|
|重大更改|不间断|

## <a name="cause"></a>原因

不应引发异常的方法引发了异常。

## <a name="rule-description"></a>规则说明

不应引发异常的方法可以按如下方式分类：

- 属性获取方法

- 事件访问器方法

- Equals 方法

- GetHashCode 方法

- ToString 方法

- 静态构造函数

- 终结器

- Dispose 方法

- 相等运算符

- 隐式强制转换运算符

以下各节将讨论这些方法类型。

### <a name="property-get-methods"></a>属性获取方法

属性基本上是智能字段。 因此，它们的行为应尽可能像字段一样。 字段不会引发异常，也不应为属性。 如果有一个引发异常的属性，请考虑将其设为方法。

可以从属性 get 方法引发以下异常：

- <xref:System.InvalidOperationException?displayProperty=fullName>和所有派生（包括<xref:System.ObjectDisposedException?displayProperty=fullName>）

- <xref:System.NotSupportedException?displayProperty=fullName>和所有派生

- <xref:System.ArgumentException?displayProperty=fullName>（仅从索引 get 获取）

- <xref:System.Collections.Generic.KeyNotFoundException>（仅从索引 get 获取）

### <a name="event-accessor-methods"></a>事件访问器方法

事件访问器应是不会引发异常的简单操作。 尝试添加或移除事件处理程序时，事件不应引发异常。

事件访问器可能会引发以下异常：

- <xref:System.InvalidOperationException?displayProperty=fullName>和所有派生（包括<xref:System.ObjectDisposedException?displayProperty=fullName>）

- <xref:System.NotSupportedException?displayProperty=fullName>和所有派生

- <xref:System.ArgumentException>和派生

### <a name="equals-methods"></a>Equals 方法

以下**Equals**方法不应引发异常：

- <xref:System.Object.Equals%2A?displayProperty=fullName>

- <xref:System.IEquatable%601.Equals%2A>

**Equals**方法应返回`true`或`false`而不是引发异常。 例如，如果将 Equals 传递两个不匹配的类型，则`false`应只返回， <xref:System.ArgumentException>而不是引发。

### <a name="gethashcode-methods"></a>GetHashCode 方法

以下**GetHashCode**方法通常不应引发异常：

- <xref:System.Object.GetHashCode%2A>

- <xref:System.Collections.IEqualityComparer.GetHashCode%2A>

**GetHashCode**应始终返回值。 否则，可能会丢失哈希表中的项。

采用参数的**GetHashCode**的版本可能会引发<xref:System.ArgumentException>。 但是， **GetHashCode**不应引发异常。

### <a name="tostring-methods"></a>ToString 方法

调试器使用<xref:System.Object.ToString%2A?displayProperty=fullName>来帮助以字符串格式显示有关对象的信息。 因此， **ToString**不应更改对象的状态，并且不应引发异常。

### <a name="static-constructors"></a>静态构造函数

从静态构造函数引发异常将导致该类型在当前应用程序域中不可用。 从静态构造函数引发异常时应具有合理的原因（例如，安全问题）。

### <a name="finalizers"></a>终结器

从终结器引发异常将导致 CLR 快速失败，从而泪水进程。 因此，应始终避免在终结器中引发异常。

### <a name="dispose-methods"></a>Dispose 方法

<xref:System.IDisposable.Dispose%2A?displayProperty=fullName>方法不应引发异常。 Dispose 通常作为`finally`子句中清理逻辑的一部分来调用。 因此，从 Dispose 显式引发异常将强制用户在`finally`子句内添加异常处理。

**Dispose （false）** 代码路径应永远不会引发异常，因为释放几乎始终是从终结器调用的。

### <a name="equality-operators--"></a>相等运算符（= =，！ =）

与 Equals 方法一样，相等运算符应返回`true`或`false`，而不应引发异常。

### <a name="implicit-cast-operators"></a>隐式强制转换运算符

由于用户通常不知道已经调用了隐式转换运算符，因此隐式强制转换运算符引发了异常。 因此，不应从隐式强制转换运算符引发异常。

## <a name="how-to-fix-violations"></a>如何解决冲突

对于属性 getter，请更改逻辑，使其不再需要引发异常，或将属性更改为方法。

对于前面列出的所有其他方法类型，请更改逻辑，使其不再必须引发异常。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

如果冲突是由异常声明引起的，而不是引发的异常，则可以安全地禁止显示此规则发出的警告。

## <a name="related-rules"></a>相关规则

- [CA2219在异常子句中不引发异常](../code-quality/ca2219-do-not-raise-exceptions-in-exception-clauses.md)

## <a name="see-also"></a>请参阅

- [设计警告](../code-quality/design-warnings.md)