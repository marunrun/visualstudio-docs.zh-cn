---
title: CA1719:参数名不应与成员名冲突
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- ParameterNamesShouldNotMatchMemberNames
- CA1719
helpviewer_keywords:
- CA1719
- ParameterNamesShouldNotMatchMemberNames
ms.assetid: c6fea690-1659-4ee7-a1c5-125ad6754525
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9b3e34bec0e199e1eb0b49a88517e9551b9b13cd
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68921631"
---
# <a name="ca1719-parameter-names-should-not-match-member-names"></a>CA1719:参数名不应与成员名冲突

|||
|-|-|
|TypeName|ParameterNamesShouldNotMatchMemberNames|
|CheckId|CA1719|
|类别|Microsoft.Naming|
|是否重大更改|重大|

## <a name="cause"></a>原因
在不区分大小写的情况下, 外部可见成员的名称与它的其中一个参数的名称匹配。

## <a name="rule-description"></a>规则说明
参数名称应传达参数的含义，成员名称应传达成员的含义。 两者相同的设计非常少见。 使参数与其成员同名会导致不直观的效果，会使库难以使用。

## <a name="how-to-fix-violations"></a>如何解决冲突
选择与成员名称不匹配的参数名称。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
对于新开发, 不会发生任何已知方案, 你必须禁止显示此规则发出的警告。 对于装运库, 可能必须禁止显示此规则发出的警告。

## <a name="related-rules"></a>相关规则
[CA1709标识符应采用正确的大小写](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)

[CA1708标识符的差别应超过大小写](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)

[CA1707标识符不应包含下划线](../code-quality/ca1707-identifiers-should-not-contain-underscores.md)