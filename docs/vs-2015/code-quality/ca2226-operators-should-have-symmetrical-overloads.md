---
title: CA2226：运算符应有对称重载 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- OperatorsShouldHaveSymmetricalOverloads
- CA2226
helpviewer_keywords:
- OperatorsShouldHaveSymmetricalOverloads
- CA2226
ms.assetid: d202401a-ea14-4559-b15e-0ea4f5b68789
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 9772577c2b1466cf3d1b5267129aa761db983021
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72658910"
---
# <a name="ca2226-operators-should-have-symmetrical-overloads"></a>CA2226：运算符应有对称重载
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|OperatorsShouldHaveSymmetricalOverloads|
|CheckId|CA2226|
|类别|Microsoft. 使用情况|
|是否重大更改|非重大更改|

## <a name="cause"></a>原因
 某个类型实现了相等运算符或不等运算符，却未实现相反运算符。

## <a name="rule-description"></a>规则说明
 在某些情况下，相等性或不等性适用于类型的实例，而相反的运算符未定义。 类型通常通过返回相等运算符的求反值来实现不相等运算符。

 对于C#违反此规则的情况，编译器将发出错误。

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请同时实现相等运算符和不相等运算符，或删除存在的运算符。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 不禁止显示此规则发出的警告。 您的类型的工作方式与 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 一致。

## <a name="related-rules"></a>相关规则
 [CA1046：不要对引用类型重载相等运算符](../code-quality/ca1046-do-not-overload-operator-equals-on-reference-types.md)

 [CA2225：运算符重载具有命名的备用项](../code-quality/ca2225-operator-overloads-have-named-alternates.md)

 [CA2224：重载相等运算符时重写 Equals 方法](../code-quality/ca2224-override-equals-on-overloading-operator-equals.md)

 [CA2218：重写 Equals 时重写 GetHashCode](../code-quality/ca2218-override-gethashcode-on-overriding-equals.md)

 [CA2231：重写 ValueType.Equals 时应重载相等运算符](../code-quality/ca2231-overload-operator-equals-on-overriding-valuetype-equals.md)
