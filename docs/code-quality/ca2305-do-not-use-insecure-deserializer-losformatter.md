---
title: CA2305：请勿使用不安全的反序列化程序 LosFormatter
ms.date: 05/01/2019
ms.topic: reference
author: dotpaul
ms.author: paulming
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
f1_keywords:
- CA2305
- DoNotUseInsecureDeserializerLosFormatter
ms.openlocfilehash: 145d45d79f1dda27d5c69f0c481277572d3eeaa2
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71237732"
---
# <a name="ca2305-do-not-use-insecure-deserializer-losformatter"></a>CA2305：请勿使用不安全的反序列化程序 LosFormatter

|||
|-|-|
|TypeName|DoNotUseInsecureDeserializerLosFormatter|
|CheckId|CA2305|
|类别|Microsoft.Security|
|重大更改|不间断|

## <a name="cause"></a>原因

调用<xref:System.Web.UI.LosFormatter?displayProperty=nameWithType>或引用了反序列化方法。

## <a name="rule-description"></a>规则说明

[!INCLUDE[insecure-deserializers-description](includes/insecure-deserializers-description-md.md)]

此规则查找<xref:System.Web.UI.LosFormatter?displayProperty=nameWithType>反序列化方法调用或引用。

## <a name="how-to-fix-violations"></a>如何解决冲突

[!INCLUDE[insecure-deserializers-fixes-for-always-insecure-deserializers](includes/insecure-deserializers-fixes-for-always-insecure-deserializers-md.md)]

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

[!INCLUDE[insecure-deserializers-common-safe-to-suppress](includes/insecure-deserializers-common-safe-to-suppress-md.md)]

## <a name="pseudo-code-examples"></a>伪代码示例

### <a name="violation"></a>冲突

```csharp
using System.IO;
using System.Web.UI;

public class ExampleClass
{
    public object MyDeserialize(byte[] bytes)
    {
        LosFormatter formatter = new LosFormatter();
        return formatter.Deserialize(new MemoryStream(bytes));
    }
}
```

```vb
Imports System.IO
Imports System.Web.UI

Public Class ExampleClass
    Public Function MyDeserialize(bytes As Byte()) As Object
        Dim formatter As LosFormatter = New LosFormatter()
        Return formatter.Deserialize(New MemoryStream(bytes))
    End Function
End Class
```