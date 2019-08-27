---
title: CA2213:应释放可释放的字段
ms.date: 05/14/2019
ms.topic: reference
f1_keywords:
- DisposableFieldsShouldBeDisposed
- CA2213
helpviewer_keywords:
- CA2213
- DisposableFieldsShouldBeDisposed
ms.assetid: e99442c9-70e2-47f3-b61a-d8ac003bc6e5
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b38157fcc23561b47a919151aa78a71f98b3909b
ms.sourcegitcommit: 283f2dbce044a18e9f6ac6398f6fc78e074ec1ed
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/16/2019
ms.locfileid: "65804998"
---
# <a name="ca2213-disposable-fields-should-be-disposed"></a>CA2213:应释放可释放的字段

|||
|-|-|
|TypeName|DisposableFieldsShouldBeDisposed|
|CheckId|CA2213|
|类别|Microsoft.Usage|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因

实现的类型<xref:System.IDisposable?displayProperty=fullName>声明还实现的类型的字段<xref:System.IDisposable>。 <xref:System.IDisposable.Dispose%2A>字段的方法不由调用<xref:System.IDisposable.Dispose%2A>声明类型的方法。

## <a name="rule-description"></a>规则说明

一种类型负责释放其所有非托管资源。 规则 CA2213 检查以查看是否可释放类型 (即，一个实现<xref:System.IDisposable>)`T`声明字段`F`，它是可释放类型的实例`FT`。 每个字段`F`的已分配给本地创建的对象方法或包含类型的初始值设定项内`T`，规则将尝试查找调用`FT.Dispose`。 该规则会搜索调用的方法`T.Dispose`和一个级别较低 (即，调用的方法调用的方法`T.Dispose`)。

> [!NOTE]
> 以外[特殊情况](#special-cases)，规则 CA2213 激发仅用于分配包含类型的方法和初始值设定项中的本地创建可释放对象的字段。 如果创建或分配外部类型的对象`T`，该规则不会激发。 这将减少干扰的情况下，其中包含类型本身不必拥有负责释放的对象。

### <a name="special-cases"></a>特殊情况

即使它们分配的对象不本地创建，也可以为以下类型的字段激发规则 CA2213:

- <xref:System.IO.Stream?displayProperty=nameWithType>
- <xref:System.IO.TextReader?displayProperty=nameWithType>
- <xref:System.IO.TextWriter?displayProperty=nameWithType>
- <xref:System.Resources.IResourceReader?displayProperty=nameWithType>

将其中一种类型的对象传递给构造函数，然后将其分配给字段指示*释放所有权的转移*为新构造的类型。 也就是说，现负责释放的对象的新构造的类型。 如果不释放此对象，这违反了 CA2213 时发生。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复此规则的冲突，请调用<xref:System.IDisposable.Dispose%2A>所实现的类型的字段上<xref:System.IDisposable>。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

则可以安全地禁止显示此规则的警告，如果：

- 已标记的类型不负责释放资源持有的字段 (即，类型不具有*释放所有权*)
- 对调用<xref:System.IDisposable.Dispose%2A>在更深层次的调用规则检查级别上发生

## <a name="example"></a>示例

以下代码片段显示了一种类型`TypeA`实现<xref:System.IDisposable>。

[!code-csharp[FxCop.Usage.IDisposablePattern#1](../code-quality/codesnippet/CSharp/ca2213-disposable-fields-should-be-disposed_1.cs)]

以下代码片段显示了一种类型`TypeB`，通过声明一个字段违反规则 CA2213`aFieldOfADisposableType`作为可释放类型 (`TypeA`) 而不调用<xref:System.IDisposable.Dispose%2A>字段上。

[!code-csharp[FxCop.Usage.IDisposableFields#1](../code-quality/codesnippet/CSharp/ca2213-disposable-fields-should-be-disposed_2.cs)]

## <a name="see-also"></a>请参阅

- <xref:System.IDisposable?displayProperty=fullName>
- [Dispose 模式](/dotnet/standard/design-guidelines/dispose-pattern)