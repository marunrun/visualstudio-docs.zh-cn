---
title: CA5122 P-Invoke 声明不应为安全临界
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: f2581a6d-2a0e-40c1-b600-f5dc70909200
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7922681307b576f8da523cdd08fb808fb36b3d8c
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71237001"
---
# <a name="ca5122-pinvoke-declarations-should-not-be-safe-critical"></a>CA5122 P/Invoke 声明不应是安全关键的

|||
|-|-|
|TypeName|PInvokesShouldNotBeSafeCriticalFxCopRule|
|CheckId|CA5122|
|类别|Microsoft.Security|
|重大更改|重大|

## <a name="cause"></a>原因
A P/Invoke 声明已标记有 <xref:System.Security.SecuritySafeCriticalAttribute>：

```csharp
[assembly: AllowPartiallyTrustedCallers]

// ...
public class C
{
    [SecuritySafeCritical]
    [DllImport("kernel32.dll")]
    public static extern bool Beep(int frequency, int duration); // CA5122 - safe critical p/invoke
   }
```

在本例中，`C.Beep(...)` 已标记为安全可靠关键的方法。

## <a name="rule-description"></a>规则说明
当方法执行安全敏感性操作时，将被标记为 SecuritySafeCritical，但透明代码使用它们也是安全的。 安全透明度模型的一个基本规则是透明代码可能从不通过 P/Invoke 直接调用本机代码。 因此，将 P/Invoke 标记为安全关键将使透明代码无法调用它，并且会误导安全分析。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要使 P/Invoke 可用于透明代码，请为之公开安全可靠关键的包装器方法：

```csharp
[assembly: AllowPartiallyTrustedCallers

class C
{
   [SecurityCritical]
   [DllImport("kernel32.dll", EntryPoint="Beep")]
   private static extern bool BeepPinvoke(int frequency, int duration); // Security Critical P/Invoke

   [SecuritySafeCritical]
   public static bool Beep(int frequency, int duration)
   {
      return BeepPInvoke(frequency, duration);
   }
}
```

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。