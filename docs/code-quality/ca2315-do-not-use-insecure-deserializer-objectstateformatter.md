---
title: CA2315:不要使用不安全反序列化程序 ObjectStateFormatter
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
- CA2315
- DoNotUseInsecureDeserializerObjectStateFormatter
ms.openlocfilehash: 793fa9df333eed7e485d7d8829849ae30d9c93a2
ms.sourcegitcommit: db30651dc0ce4d0b274479b23a6bd102a5559098
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2019
ms.locfileid: "65135485"
---
# <a name="ca2315-do-not-use-insecure-deserializer-objectstateformatter"></a>CA2315:不要使用不安全反序列化程序 ObjectStateFormatter

|||
|-|-|
|TypeName|DoNotUseInsecureDeserializerObjectStateFormatter|
|CheckId|CA2315|
|类别|Microsoft.Security|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因

一个<xref:System.Web.UI.ObjectStateFormatter?displayProperty=nameWithType>反序列化方法是调用或引用。

## <a name="rule-description"></a>规则说明

[!INCLUDE[insecure-deserializers-description](includes/insecure-deserializers-description-md.md)]

此规则查找<xref:System.Web.UI.ObjectStateFormatter?displayProperty=nameWithType>反序列化方法调用或引用。

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
        ObjectStateFormatter formatter = new ObjectStateFormatter();
        return formatter.Deserialize(new MemoryStream(bytes));
    }
}
```

```vb
Imports System.IO
Imports System.Web.UI

Public Class ExampleClass
    Public Function MyDeserialize(bytes As Byte()) As Object
        Dim formatter As ObjectStateFormatter = New ObjectStateFormatter()
        Return formatter.Deserialize(New MemoryStream(bytes))
    End Function
End Class
```