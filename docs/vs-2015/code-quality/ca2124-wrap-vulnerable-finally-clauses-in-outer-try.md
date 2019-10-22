---
title: CA2124：在外尝试中包装易受攻击的 finally 子句 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA2124
- WrapVulnerableFinallyClausesInOuterTry
helpviewer_keywords:
- CA2124
- WrapVulnerableFinallyClausesInOuterTry
ms.assetid: 82efd224-9e60-4b88-a0f5-dfabcc49a254
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 7a2a296f5dd3680209c14849b5bd863c01e6351d
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72660238"
---
# <a name="ca2124-wrap-vulnerable-finally-clauses-in-outer-try"></a>CA2124：在外部 try 块中包装易受攻击的 finally 子句
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|WrapVulnerableFinallyClausesInOuterTry|
|CheckId|CA2124|
|类别|Microsoft.Security|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 在 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 版本1.0 和1.1 中，公共或受保护的方法包含 `try` / `catch` / `finally` 块。 @No__t_0 块似乎会重置安全状态，并且未包含在 `finally` 块中。

## <a name="rule-description"></a>规则说明
 此规则将在代码中查找 `finally` 块的 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 1.1 1.0 目标 / `try`，这些块可能易受到调用堆栈中存在的恶意异常筛选器的影响。 如果在 try 块中发生了诸如模拟等敏感操作，并且引发了异常，则筛选器可在 `finally` 块之前执行。 对于模拟示例，这意味着筛选器将以模拟用户的身份执行。 筛选器当前仅在 Visual Basic 中实施。

> [!WARNING]
> 在 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 版本2.0 及更高版本中，如果重置在包含异常块的方法中直接发生，则运行时将自动保护 `try` / `catch` /  `finally` 块。

## <a name="how-to-fix-violations"></a>如何解决冲突
 将解包的 `try` / `finally` 放置在外部 try 块中。 请参阅后面的第二个示例。 这会强制在筛选器代码之前执行 `finally`。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。

## <a name="pseudo-code-example"></a>伪代码示例

### <a name="description"></a>描述
 下面伪代码说明此规则检测到的模式。

### <a name="code"></a>代码

```
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

## <a name="example"></a>示例
 下面的伪代码演示了可用于保护代码并满足此规则的模式。

```
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
