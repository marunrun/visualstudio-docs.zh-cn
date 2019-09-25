---
title: CA1307:指定 StringComparison
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1307
- SpecifyStringComparison
helpviewer_keywords:
- CA1307
- SpecifyStringComparison
ms.assetid: 9b0d5e71-1683-4a0d-bc4a-68b2fbd8af71
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e352eea1b7fcf82cb948315affeae6e30690a4aa
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71234975"
---
# <a name="ca1307-specify-stringcomparison"></a>CA1307:指定 StringComparison

|||
|-|-|
|TypeName|SpecifyStringComparison|
|CheckId|CA1307|
|类别|Microsoft.Globalization|
|重大更改|不间断|

## <a name="cause"></a>原因
字符串比较操作使用未设置<xref:System.StringComparison>参数的方法重载。

## <a name="rule-description"></a>规则说明
许多字符串操作（ <xref:System.String.Compare%2A>和<xref:System.String.Equals%2A>方法）都提供接受<xref:System.StringComparison>枚举值作为参数的重载。

只要存在采用<xref:System.StringComparison>参数的重载，就应该使用它而不是不采用此参数的重载。 通过显式设置此参数，你的代码通常会更清晰且更易于维护。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突，请将字符串比较方法更改为接受<xref:System.StringComparison>枚举作为参数的重载。 例如：将更改`String.Compare(str1, str2)`为`String.Compare(str1, str2, StringComparison.Ordinal)`。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
如果库或应用程序适用于受限制的本地受众，则可以安全地禁止显示此规则发出的警告，而不会对其进行本地化。

## <a name="see-also"></a>请参阅

- [全球化警告](../code-quality/globalization-warnings.md)
- [CA1309使用序号 StringComparison](../code-quality/ca1309-use-ordinal-stringcomparison.md)