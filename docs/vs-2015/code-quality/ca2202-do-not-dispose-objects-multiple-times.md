---
title: CA2202:不要释放对象多次 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 3dfe606e3083c937db3ba3d1e6cd49d34bace853
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65697973"
---
# <a name="ca2202-do-not-dispose-objects-multiple-times"></a>CA2202:不要多次释放对象
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DoNotDisposeObjectsMultipleTimes|
|CheckId|CA2202|
|类别|Microsoft.Usage|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 方法实现包含可能会导致对多个调用的代码路径<xref:System.IDisposable.Dispose%2A?displayProperty=fullName>或与 Dispose 等效的例如某些类型，对同一对象上的 close （） 方法。

## <a name="rule-description"></a>规则说明
 正确实现<xref:System.IDisposable.Dispose%2A>方法可以多次调用而不引发异常。 但是，不保证和以避免产生<xref:System.ObjectDisposedException?displayProperty=fullName>不应调用<xref:System.IDisposable.Dispose%2A>不止一次对某个对象。

## <a name="related-rules"></a>相关的规则
 [CA2000： 超出范围前释放对象](../code-quality/ca2000-dispose-objects-before-losing-scope.md)

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复此规则的冲突，请更改的代码路径中，因此，而不考虑实现<xref:System.IDisposable.Dispose%2A>仅调用一次的对象。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。 即使<xref:System.IDisposable.Dispose%2A>为已知对象可安全地调用多次，该实现可能在以后更改。

## <a name="example"></a>示例
 嵌套`using`语句 (`Using`在 Visual Basic 中) 可能会导致违反 CA2202 警告的情况。 如果嵌套内部的 IDisposable 资源`using`语句包含的外部资源`using`语句，`Dispose`嵌套资源的方法释放所包含的资源。 发生这种情况时，`Dispose`方法的外部`using`语句尝试第二次释放其资源。

 在以下示例中，<xref:System.IO.Stream>中为外部创建的对象使用语句内部使用的 Dispose 方法中的语句的末尾释放<xref:System.IO.StreamWriter>对象，其中包含`stream`对象。 末尾的外部`using`语句，`stream`第二次在释放对象。 第二个版本都是 ca2202 冲突。

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
 若要解决此问题，请使用`try` / `finally`块而不是外部`using`语句。 在中`finally`块中，请确保`stream`资源不为 null。

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
 <xref:System.IDisposable?displayProperty=fullName> [释放模式](https://msdn.microsoft.com/library/31a6c13b-d6a2-492b-9a9f-e5238c983bcb)
