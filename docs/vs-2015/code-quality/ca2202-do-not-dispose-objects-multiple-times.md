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
ms.openlocfilehash: 31bf7fe33aa59c3a713d2da81ddbd11ed6899723
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546284"
---
# <a name="ca2202-do-not-dispose-objects-multiple-times"></a>CA2202:不要多次释放对象
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|DoNotDisposeObjectsMultipleTimes|
|CheckId|CA2202|
|Category|Microsoft. 使用情况|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 方法实现包含的代码路径可能导致对 <xref:System.IDisposable.Dispose%2A?displayProperty=fullName> 同一对象的多个调用或 Dispose 等效项（如某些类型上的 Close （）方法）。

## <a name="rule-description"></a>规则描述
 正确实现的 <xref:System.IDisposable.Dispose%2A> 方法可以多次调用而不引发异常。 但是，这是不能保证的，为了避免生成， <xref:System.ObjectDisposedException?displayProperty=fullName> 不应对 <xref:System.IDisposable.Dispose%2A> 对象多次调用。

## <a name="related-rules"></a>相关规则
 [CA2000:丢失范围之前释放对象](../code-quality/ca2000-dispose-objects-before-losing-scope.md)

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请更改实现，以便与代码路径无关， <xref:System.IDisposable.Dispose%2A> 只为对象调用一次。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。 即使 <xref:System.IDisposable.Dispose%2A> 已知对象可以安全地多次调用，实现也可能会在将来发生变化。

## <a name="example"></a>示例
 嵌套 `using` 的语句（ `Using` 在 Visual Basic 中）可能导致违反 CA2202 警告。 如果嵌套内部语句的 IDisposable 资源 `using` 包含外部语句的资源 `using` ， `Dispose` 则嵌套资源的方法会释放包含的资源。 出现这种情况时， `Dispose` 外部语句的方法将 `using` 尝试再次释放其资源。

 在下面的示例中，在 <xref:System.IO.Stream> 外部 using 语句中创建的对象将在 <xref:System.IO.StreamWriter> 包含该对象的对象的 Dispose 方法中的内部 using 语句的末尾释放 `stream` 。 在外部语句结束时 `using` ，将 `stream` 再次释放该对象。 第二个版本违反了 CA2202。

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
 若要解决此问题，请使用 `try` / `finally` 块而不是外部 `using` 语句。 在 `finally` 块中，确保 `stream` 资源不为 null。

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

## <a name="see-also"></a>另请参阅
 <xref:System.IDisposable?displayProperty=fullName> [释放模式](https://msdn.microsoft.com/library/31a6c13b-d6a2-492b-9a9f-e5238c983bcb)
