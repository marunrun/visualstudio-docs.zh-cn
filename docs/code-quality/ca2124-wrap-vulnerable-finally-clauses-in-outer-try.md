---
title: CA2124:在外部 try 块中包装易受攻击的 finally 子句
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA2124
- WrapVulnerableFinallyClausesInOuterTry
helpviewer_keywords:
- CA2124
- WrapVulnerableFinallyClausesInOuterTry
ms.assetid: 82efd224-9e60-4b88-a0f5-dfabcc49a254
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0008767f7d37e2c088dad58a328b025f81090ad8
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71232455"
---
# <a name="ca2124-wrap-vulnerable-finally-clauses-in-outer-try"></a>CA2124:在外部 try 块中包装易受攻击的 finally 子句

|||
|-|-|
|TypeName|WrapVulnerableFinallyClausesInOuterTry|
|CheckId|CA2124|
|类别|Microsoft.Security|
|重大更改|不间断|

## <a name="cause"></a>原因
在 .NET Framework 版本1.0 和1.1 中，公共或受保护的`try`方法包含/ `catch` / `finally`块。 该`finally`块显示为重置安全状态，并且未包含`finally`在块中。

## <a name="rule-description"></a>规则说明
此规则将`try`在代码中查找/ `finally`目标为版本1.0 和 1.1 .NET Framework 的代码块，这些代码可能易受到调用堆栈中存在的恶意异常筛选器的影响。 如果在 try 块中发生了诸如模拟等敏感操作，并且引发了异常，则筛选器可以在`finally`块之前执行。 对于模拟示例，这意味着筛选器将以模拟用户的身份执行。 筛选器当前仅在 Visual Basic 中实施。

> [!NOTE]
> 在 .NET Framework 版本2.0 及更高版本中，如果重置操作`try`直接发生在方法中，则运行时将自动保护/  / `catch` `finally`块免受恶意异常筛选器的攻击包含异常块。

## <a name="how-to-fix-violations"></a>如何解决冲突
将解包`try` /置于外部try 块中`finally` 。 请参阅后面的第二个示例。 这会强制`finally`在筛选器代码之前执行。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。

## <a name="pseudo-code-example"></a>伪代码示例

### <a name="description"></a>描述

下面伪代码说明此规则检测到的模式。

```csharp
try {
   // Do some work.
   Impersonator imp = new Impersonator("John Doe");
   imp.AddToCreditCardBalance(100);
}
finally {
   // Reset security state.
   imp.Revert();
}
```

下面的伪代码演示了可用于保护代码并满足此规则的模式。

```csharp
try {
     try {
        // Do some work.
     }
     finally {
        // Reset security state.
     }
}
catch()
{
    throw;
}
```