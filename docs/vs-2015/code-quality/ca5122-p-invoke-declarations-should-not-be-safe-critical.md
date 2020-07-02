---
title: CA5122 P-Invoke 声明不应是安全关键的 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
ms.assetid: f2581a6d-2a0e-40c1-b600-f5dc70909200
caps.latest.revision: 6
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: a6a6ee7796ae437b564f6826376219291143e449
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545088"
---
# <a name="ca5122-pinvoke-declarations-should-not-be-safe-critical"></a>CA5122 P/Invoke 声明不应是安全关键的
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|PInvokesShouldNotBeSafeCriticalFxCopRule|
|CheckId|CA5122|
|类别|Microsoft.Security|
|是否重大更改|重大|

## <a name="cause"></a>原因
 A P/Invoke 声明已标记有 <xref:System.Security.SecuritySafeCriticalAttribute>：

```csharp
[assembly: AllowPartiallyTrustedCallers]

// ...
public class C
{
    [SecuritySafeCritical]
    [DllImport("kernel32.dll")]
    public static extern bool Beep(int frequency, int duration); // CA5122 – safe critical p/invoke
   }
```

 在本例中，`C.Beep(...)` 已标记为安全可靠关键的方法。

## <a name="rule-description"></a>规则描述
 当方法执行安全敏感性操作时，将被标记为 SecuritySafeCritical，但透明代码使用它们也是安全的。 安全透明度模型的一个基本规则是透明代码可能从不通过 P/Invoke 直接调用本机代码。 因此，将 P/Invoke 标记为安全关键将使透明代码无法调用它，并且会误导安全分析。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要使 P/Invoke 可用于透明代码，请为之公开安全可靠关键的包装器方法：

```csharp
[assembly: AllowPartiallyTrustedCallers

class C
{
   [SecurityCritical]
   [DllImport(“kernel32.dll”, EntryPoint=”Beep”)]
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
