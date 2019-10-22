---
title: CA2202：不要多次释放对象 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2202
- Do not dispose objects multiple times
- DoNotDisposeObjectsMultipleTimes
helpviewer_keywords:
- CA2202
ms.assetid: fa85349a-cf1e-42c8-a86b-eacae1f8bd96
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: e0be715d8aea84fac53ea2a796e71850b961730c
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72667406"
---
# <a name="ca2202-do-not-dispose-objects-multiple-times"></a>CA2202：不要多次释放对象
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DoNotDisposeObjectsMultipleTimes|
|CheckId|CA2202|
|类别|Microsoft. 使用情况|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 方法实现包含可导致多次调用 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> 或 Dispose 等效项的代码路径，例如对同一对象的某些类型的 Close （）方法。

## <a name="rule-description"></a>规则说明
 正确实现 <xref:System.IDisposable.Dispose%2A> 方法可多次调用而不引发异常。 但是，这并不能保证是否会生成 <xref:System.ObjectDisposedException?displayProperty=fullName> 不应在一个对象上多次调用 <xref:System.IDisposable.Dispose%2A>。

## <a name="related-rules"></a>相关规则
 [CA2000：超出范围前释放对象](../code-quality/ca2000-dispose-objects-before-losing-scope.md)

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请更改实现，以便与代码路径无关，只为对象调用一次 <xref:System.IDisposable.Dispose%2A>。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。 即使知道对象 <xref:System.IDisposable.Dispose%2A> 可以安全地多次调用，实现也可能会在将来发生更改。

## <a name="example"></a>示例
 嵌套的 `using` 语句（在 Visual Basic 中 `Using`）可能导致违反 CA2202 警告。 如果嵌套的内部 `using` 语句的 IDisposable 资源包含外部 `using` 语句的资源，则嵌套资源的 `Dispose` 方法会释放包含的资源。 出现这种情况时，外部 `using` 语句的 `Dispose` 方法尝试再次释放其资源。

 在下面的示例中，在外部 using 语句中创建的 <xref:System.IO.Stream> 对象在包含 `stream` 对象的 <xref:System.IO.StreamWriter> 对象的 Dispose 方法中释放。 在外部 `using` 语句结束时，`stream` 对象将第二次释放。 第二个版本违反了 CA2202。

```
using (Stream stream = new FileStream("file.txt", FileMode.OpenOrCreate))
{
    using (StreamWriter writer = new StreamWriter(stream))
    {
        // Use the writer object...
    }
}
```

## <a name="example"></a>示例
 若要解决此问题，请使用 `try` / `finally` 块，而不是外部 `using` 语句。 在 `finally` 块中，确保 `stream` 资源为 not null。

```
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
    if(stream != null)
        stream.Dispose();
}
```

## <a name="see-also"></a>请参阅
 <xref:System.IDisposable?displayProperty=fullName> [Dispose 模式](https://msdn.microsoft.com/library/31a6c13b-d6a2-492b-9a9f-e5238c983bcb)
