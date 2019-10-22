---
title: CA1024：在适当的情况下使用属性 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- UsePropertiesWhereAppropriate
- CA1024
helpviewer_keywords:
- CA1024
- UsePropertiesWhereAppropriate
ms.assetid: 3a04f765-af7c-4872-87ad-9cc29e8e657f
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: b190e007cfdb016e54148cf0295c68baf68c5033
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72661961"
---
# <a name="ca1024-use-properties-where-appropriate"></a>CA1024：在适用处使用属性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|UsePropertiesWhereAppropriate|
|CheckId|CA1024|
|类别|Microsoft. Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 公共或受保护方法的名称以 `Get` 开头，不使用任何参数，并且返回的值不是数组。

## <a name="rule-description"></a>规则说明
 在大多数情况下，属性表示数据并执行操作。 像字段一样访问属性，这样可以更方便地使用它们。 如果存在以下情况之一，则方法非常适合成为属性：

- 不采用任何参数，并返回对象的状态信息。

- 接受单个参数以设置对象状态的某些部分。

  属性的行为应与字段相同;如果该方法不能，则不应将其更改为属性。 方法比以下情况下的属性更好：

- 方法执行耗时的操作。 方法的 perceivably 慢于设置或获取字段值所需的时间。

- 方法执行转换。 访问字段不会返回它所存储的数据的转换版本。

- Get 方法具有可观察到的副作用。 检索字段的值不会产生任何副作用。

- 执行顺序很重要。 设置字段的值不依赖于出现其他操作。

- 连续调用方法两次会产生不同的结果。

- 方法是静态的，但会返回可由调用方更改的对象。 检索字段的值不允许调用方更改字段存储的数据。

- 方法返回一个数组。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请将方法更改为属性。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果方法至少满足前面列出的一个条件，则禁止显示此规则发出的警告。

## <a name="controlling-property-expansion-in-the-debugger"></a>控制调试器中的属性扩展
 程序员避免使用属性的原因之一是，它们不希望调试器自动展开它。 例如，属性可能涉及到分配一个大型对象或调用 P/Invoke，但它实际上可能不会有任何明显的副作用。

 可以通过应用 <xref:System.Diagnostics.DebuggerBrowsableAttribute?displayProperty=fullName> 阻止调试器自动扩展属性。 下面的示例演示如何将此特性应用于实例属性。

```vb
Imports System
Imports System.Diagnostics

Namespace Microsoft.Samples

    Public Class TestClass

        ' [...]

        <DebuggerBrowsable(DebuggerBrowsableState.Never)> _
        Public ReadOnly Property LargeObject() As LargeObject
            Get
                ' Allocate large object
                ' [...]
            End Get
        End Property

    End Class

End Namespace
```

```csharp

      using System;
using System.Diagnostics;

namespace Microsoft.Samples
{
    publicclass TestClass
    {
        // [...]

        [DebuggerBrowsable(DebuggerBrowsableState.Never)]
        public LargeObject LargeObject
        {
            get
            {
                // Allocate large object
                // [...]

        }
    }
}
```

## <a name="example"></a>示例
 下面的示例包含多个应转换为属性的方法，而不应转换为多个方法，因为它们的行为类似于字段。

 [!code-csharp[FxCop.Design.MethodsProperties#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.MethodsProperties/cs/FxCop.Design.MethodsProperties.cs#1)]
