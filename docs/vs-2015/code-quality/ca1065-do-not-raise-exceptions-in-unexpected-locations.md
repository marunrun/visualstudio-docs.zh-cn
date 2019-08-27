---
title: CA1065:不会引发意外的位置中的异常 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1065
- DoNotRaiseExceptionsInUnexpectedLocations
helpviewer_keywords:
- DoNotRaiseExceptionsInUnexpectedLocations
- CA1065
ms.assetid: 4e1bade4-4ca2-4219-abc3-c7b2d741e157
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 6c5a393c32d7f7182fc3226689e24d20a4cae1ac
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68200406"
---
# <a name="ca1065-do-not-raise-exceptions-in-unexpected-locations"></a>CA1065:不要在意外的位置引发异常
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DoNotRaiseExceptionsInUnexpectedLocations|
|CheckId|CA1065|
|类别|Microsoft.Design|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 不应引发异常的方法引发了异常。

## <a name="rule-description"></a>规则说明
 不应引发异常的方法可以进行分类，如下所示：

- 属性 Get 方法

- 事件访问器方法

- Equals 方法

- GetHashCode 方法

- ToString 方法

- 静态构造函数

- 终结器

- Dispose 方法

- 相等运算符

- 隐式强制转换运算符

  以下各节讨论这些方法类型。

### <a name="property-get-methods"></a>属性 Get 方法
 属性是基本上就是智能字段。 因此，它们应该表现得像尽可能多地一个字段。 字段不会引发异常，也不应该属性。 如果您有一个属性，它将引发异常，请考虑使它成为方法。

 允许属性 get 方法从引发以下异常：

- <xref:System.InvalidOperationException?displayProperty=fullName> 所有派生类 (包括<xref:System.ObjectDisposedException?displayProperty=fullName>)

- <xref:System.NotSupportedException?displayProperty=fullName> 所有派生类

- <xref:System.ArgumentException?displayProperty=fullName> （仅限通过索引，以获得）

- <xref:System.Collections.Generic.KeyNotFoundException> （仅限通过索引，以获得）

### <a name="event-accessor-methods"></a>事件访问器方法
 事件访问器应该是简单的操作，不会引发异常。 当您尝试添加或删除事件处理程序时，事件不应引发异常。

 允许从事件访问器中引发以下异常：

- <xref:System.InvalidOperationException?displayProperty=fullName> 所有派生类 (包括<xref:System.ObjectDisposedException?displayProperty=fullName>)

- <xref:System.NotSupportedException?displayProperty=fullName> 所有派生类

- <xref:System.ArgumentException> 派生类

### <a name="equals-methods"></a>Equals 方法
 以下**等于**方法不应引发异常：

- <xref:System.Object.Equals%2A?displayProperty=fullName>

- [M:IEquatable.Equals](http://go.microsoft.com/fwlink/?LinkId=113472)

  **等于**方法应返回`true`或`false`而不是引发异常。 例如，如果等于传递两个不匹配的类型则只应返回`false`而不是引发<xref:System.ArgumentException>。

### <a name="gethashcode-methods"></a>GetHashCode 方法
 以下**GetHashCode**方法不应通常引发异常：

- <xref:System.Object.GetHashCode%2A>

- [M:IEqualityComparer.GetHashCode(T)](http://go.microsoft.com/fwlink/?LinkId=113477)

  **GetHashCode**应始终返回一个值。 否则，可能会丢失哈希表中的项。

  版本**GetHashCode**采用自变量可能会引发<xref:System.ArgumentException>。 但是， **Object.GetHashCode**应永远不会引发异常。

### <a name="tostring-methods"></a>ToString 方法
 调试器使用<xref:System.Object.ToString%2A?displayProperty=fullName>可帮助将以字符串格式显示有关对象的信息。 因此， **ToString**不应更改对象的状态和不应引发异常。

### <a name="static-constructors"></a>静态构造函数
 从静态构造函数引发的异常会导致为当前应用程序域中不可用的类型。 引发静态构造函数中的异常，应具有非常合理的理由 （例如安全问题）。

### <a name="finalizers"></a>终结器
 来自终结器引发异常会导致 CLR 快速，失败的终止进程。 因此，在终结器引发的异常应始终避免。

### <a name="dispose-methods"></a>Dispose 方法
 一个<xref:System.IDisposable.Dispose%2A?displayProperty=fullName>方法不应引发异常。 作为一部分的清理逻辑中通常称为 dispose`finally`子句。 因此，从 Dispose 中显式引发异常会强制用户在添加异常处理内部`finally`子句。

 **Dispose （false)** 代码路径应永远不会引发异常，因为这几乎总是从终结器调用。

### <a name="equality-operators--"></a>相等运算符 (= =、 ！ =)
 Equals 方法，如相等运算符应返回任一`true`或`false`和不应引发异常。

### <a name="implicit-cast-operators"></a>隐式强制转换运算符
 因为用户通常是不知道已调用隐式强制转换运算符，隐式强制转换运算符所引发的异常是完全意外。 因此，应从隐式强制转换运算符不引发任何异常。

## <a name="how-to-fix-violations"></a>如何解决冲突
 对于属性 getter，或者更改逻辑，以使其不再具有要引发异常，或者将属性更改为一种方法。

 对于所有其他方法类型前面列出，更改逻辑，以便它不再引发异常。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 它可以安全地禁止显示此规则的警告，如果冲突引起异常声明而不是引发的异常。

## <a name="related-rules"></a>相关的规则
 [CA2219:不会引发异常子句中的异常](../code-quality/ca2219-do-not-raise-exceptions-in-exception-clauses.md)

## <a name="see-also"></a>请参阅
 [设计警告](../code-quality/design-warnings.md)
