---
title: CA1707:标识符不应包含下划线
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IdentifiersShouldNotContainUnderscores
- CA1707
helpviewer_keywords:
- CA1707
- IdentifiersShouldNotContainUnderscores
ms.assetid: 5fb539ef-c304-4323-90c0-b14386da9774
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: adfa0ccd63d0433d367b0e7278693608bb83d685
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71234274"
---
# <a name="ca1707-identifiers-should-not-contain-underscores"></a>CA1707:标识符不应包含下划线

|||
|-|-|
|TypeName|IdentifiersShouldNotContainUnderscores|
|CheckId|CA1707|
|类别|Microsoft.Naming|
|重大更改|正在进行-对程序集引发<br /><br /> 无间断-在类型参数上引发|

## <a name="cause"></a>原因

标识符的名称包含下划线（\_）字符。

## <a name="rule-description"></a>规则说明

按照约定，标识符名称不包含下划线（\_）字符。 规则将检查命名空间、类型、成员和参数。

命名约定为面向公共语言运行时的库提供了通用的外观。 这减少了新软件库所需的学习曲线，并使客户可以放心地了解库是由具有开发托管代码的专业技能的人员开发的。

## <a name="how-to-fix-violations"></a>如何解决冲突

删除名称中的所有下划线字符。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

不禁止显示此规则发出的警告。

## <a name="related-rules"></a>相关规则

- [CA1709标识符应采用正确的大小写](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)
- [CA1708标识符的差别应超过大小写](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)
