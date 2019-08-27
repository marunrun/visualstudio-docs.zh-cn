---
title: CA2124:Try 包装易受攻击的 finally 子句在外部 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: de2bd0bfbf60ef717e00daaa668475cb43a9d35c
ms.sourcegitcommit: 748d9cd7328a30f8c80ce42198a94a4b5e869f26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67890942"
---
# <a name="ca2124-wrap-vulnerable-finally-clauses-in-outer-try"></a>CA2124:在外部 try 块中包装易受攻击的 finally 子句
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|WrapVulnerableFinallyClausesInOuterTry|
|CheckId|CA2124|
|类别|Microsoft.Security|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 在版本 1.0 和 1.1 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]，包含公共或受保护方法`try` / `catch` / `finally`块。 `finally`块似乎要重置安全状态，并且不括在`finally`块。

## <a name="rule-description"></a>规则说明
 此规则查找`try` / `finally`面向的 1.0 和 1.1 版的代码中的块，[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]可能容易受到恶意的异常筛选器存在于调用堆栈中。 如果模拟等敏感操作发生在 try 块中，且会引发异常，该筛选器可以执行之前`finally`块。 对于模拟的示例中，这意味着该筛选器将执行作为被模拟用户。 筛选器是目前仅在 Visual Basic 中实施。

> [!WARNING]
> 在版本 2.0 及更高版本的[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]，运行时自动保护`try` / `catch` /  `finally`重置该方法内直接发生的情况下阻止从恶意的异常筛选器，包含异常块。

## <a name="how-to-fix-violations"></a>如何解决冲突
 放置未包装`try` / `finally`在外部 try 块中。 请参阅后面的第二个示例。 这会强制`finally`之前筛选器代码执行。

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
 下面的伪代码演示的模式可用于保护你的代码和满足此规则。

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
