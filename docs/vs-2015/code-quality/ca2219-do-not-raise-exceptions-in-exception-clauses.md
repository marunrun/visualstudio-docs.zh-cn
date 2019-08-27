---
title: CA2219:不会引发异常子句中的异常 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- DoNotRaiseExceptionsInExceptionClauses
- CA2219
helpviewer_keywords:
- DoNotRaiseExceptionsInExceptionClauses
- CA2219
ms.assetid: 7b9b0bee-4e8e-49a4-8c40-52142b49061f
caps.latest.revision: 7
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 506b9d243ef83242b7e17c295dfc13ef9039d1f6
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68201624"
---
# <a name="ca2219-do-not-raise-exceptions-in-exception-clauses"></a>CA2219:在异常子句中不引发异常
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|DoNotRaiseExceptionsInExceptionClauses|
|CheckId|CA2219|
|类别|Microsoft.Usage|
|是否重大更改|非换行中断|

## <a name="cause"></a>原因
 从引发异常`finally`，筛选器或 fault 子句。

## <a name="rule-description"></a>规则说明
 当在异常子句中引发异常时，则会大大增加调试难度。

 在引发异常时`finally`或 fault 子句，新异常会隐藏活动异常，如果存在。 这使得原来的错误难以检测和调试。

 当筛选器子句中引发异常时，运行时以无提示方式捕获异常，并会导致筛选器来计算结果为 false。 没有办法指示计算为 false，并且从筛选器引发的异常的筛选器之间的差异。 这使得难以检测和调试的筛选器逻辑中的错误。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要解决此冲突的此规则，则不要显式引发异常`finally`，筛选器或 fault 子句。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不要禁止显示此规则的警告。 没有在其下在异常子句中引发的异常提供了一项权益对执行代码的方案。

## <a name="related-rules"></a>相关的规则
 [CA1065:不会引发意外的位置中的异常](../code-quality/ca1065-do-not-raise-exceptions-in-unexpected-locations.md)

## <a name="see-also"></a>请参阅
 [设计警告](../code-quality/design-warnings.md)
