---
title: CA2202:不要多次释放对象
ms.date: 07/16/2019
ms.topic: reference
f1_keywords:
- CA2202
- Do not dispose objects multiple times
- DoNotDisposeObjectsMultipleTimes
helpviewer_keywords:
- CA2202
ms.assetid: fa85349a-cf1e-42c8-a86b-eacae1f8bd96
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7c7fa7756383426f990e18225995a768de9fefbd
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71231740"
---
# <a name="ca2202-do-not-dispose-objects-multiple-times"></a>CA2202:不要多次释放对象

|||
|-|-|
|TypeName|DoNotDisposeObjectsMultipleTimes|
|CheckId|CA2202|
|类别|Microsoft.Usage|
|重大更改|不间断|

## <a name="cause"></a>原因

方法实现包含的代码路径可能导致对<xref:System.IDisposable.Dispose%2A?displayProperty=fullName>同一对象的多个调用或 Dispose 等效项 (如某些类型上的 Close () 方法)。

## <a name="rule-description"></a>规则说明

正确实现<xref:System.IDisposable.Dispose%2A>的方法可以多次调用而不引发异常。 但是, 这是不能保证的<xref:System.ObjectDisposedException?displayProperty=fullName> , 为了避免生成, 不应对对象多次调用。 <xref:System.IDisposable.Dispose%2A>

## <a name="related-rules"></a>相关规则

- [CA2000在失去范围之前释放对象](../code-quality/ca2000-dispose-objects-before-losing-scope.md)

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突, 请更改实现, 以便与代码路径无关, <xref:System.IDisposable.Dispose%2A>只为对象调用一次。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

不禁止显示此规则发出的警告。 <xref:System.IDisposable.Dispose%2A>即使已知对象可以安全地多次调用, 实现也可能会在将来发生变化。

## <a name="example"></a>示例

嵌套`using`的语句`Using` (在 Visual Basic 中) 可能导致违反 CA2202 警告。 如果嵌套内部`using`语句的 IDisposable 资源包含外部`using`语句的资源, `Dispose`则嵌套资源的方法会释放包含的资源。 出现这种情况时, `Dispose`外部`using`语句的方法将尝试再次释放其资源。

在下面的示例中, <xref:System.IO.Stream>在外部 using 语句中创建的对象将在包含该`stream`对象的<xref:System.IO.StreamWriter>对象的 Dispose 方法中的内部 using 语句的末尾释放。 在外部`using`语句结束时, 将再次释放`stream`该对象。 第二个版本违反了 CA2202。

```csharp
using (Stream stream = new FileStream("file.txt", FileMode.OpenOrCreate))
{
    using (StreamWriter writer = new StreamWriter(stream))
    {
        // Use the writer object...
    }
}
```

## <a name="example"></a>示例

若要解决此问题, 请`try`使用/ `finally`块而不是`using`外部语句。 在块中, 确保`stream`资源不为 null。 `finally`

```csharp
Stream stream = null;
try
{
    stream = new FileStream("file.txt", FileMode.OpenOrCreate);
    using (StreamWriter writer = new StreamWriter(stream))
    {
        stream = null;
        // Use the writer object...
    }
}
finally
{
    stream?.Dispose();
}
```

> [!TIP]
> 上述语法是[null 条件运算符。](/dotnet/csharp/language-reference/operators/member-access-operators#null-conditional-operators--and-) `?.`

## <a name="see-also"></a>请参阅

- <xref:System.IDisposable?displayProperty=fullName>
- [释放模式](/dotnet/standard/design-guidelines/dispose-pattern)