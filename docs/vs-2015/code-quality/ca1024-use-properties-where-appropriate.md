---
title: CA1024:在适用处使用属性 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 43487aa97afcd41a5375bacc26efba705cbaa76c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68144812"
---
# <a name="ca1024-use-properties-where-appropriate"></a>CA1024:在适用处使用属性
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|UsePropertiesWhereAppropriate|
|CheckId|CA1024|
|类别|Microsoft.Design|
|是否重大更改|重大|

## <a name="cause"></a>原因
 公共或受保护方法具有名称开头的`Get`、 不带参数，并返回一个值，不是数组。

## <a name="rule-description"></a>规则说明
 在大多数情况下，属性表示数据和方法执行的操作。 像字段，使其更易使用访问属性。 一种方法非常适于成为属性，如果存在下列条件之一：

- 不采用任何参数，并返回一个对象的状态信息。

- 接受单个参数要设置对象状态的某些部分。

  属性行为方式就像它们是字段;如果该方法不能它不应更改到的属性。 方法要优于在以下情况下的属性：

- 该方法执行耗时的操作。 此方法是速度明显慢于所需设置或获取字段的值的时间。

- 该方法执行的转换。 访问字段不返回存储的数据的已转换的版本。

- Get 方法具有明显的副作用。 检索字段的值不会产生任何负面影响。

- 执行的顺序非常重要。 设置字段的值不依赖于其他操作的匹配项。

- 连续两次调用该方法创建不同的结果。

- 该方法是静态的但返回调用方可以更改的对象。 检索字段的值不允许调用方更改按字段存储的数据。

- 该方法返回一个数组。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此规则的冲突，请将方法更改为一个属性。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果方法满足至少一个以前列出的条件，禁止显示此规则的警告。

## <a name="controlling-property-expansion-in-the-debugger"></a>控制在调试器中的属性扩展
 编程人员应避免使用属性的一个原因是因为他们不希望调试器自动展开。 例如，该属性可能会涉及分配大型对象或调用 P/Invoke，但它实际上可能不具有任何明显的副作用。

 您可以防止调试器自动扩展通过应用属性<xref:System.Diagnostics.DebuggerBrowsableAttribute?displayProperty=fullName>。 下面的示例显示了此特性应用到一个实例属性。

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
 下面的示例包含多个方法，应将转换为属性，并且多个，应该不是因为它们不类似于字段。

 [!code-csharp[FxCop.Design.MethodsProperties#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Design.MethodsProperties/cs/FxCop.Design.MethodsProperties.cs#1)]
