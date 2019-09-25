---
title: CA1823:避免未使用的私有字段
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- AvoidUnusedPrivateFields
- CA1823
helpviewer_keywords:
- AvoidUnusedPrivateFields
- CA1823
ms.assetid: 614f94f6-0dc7-430f-8124-cb889a4a720f
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5f0aa23ff93e193ee06509c1cb635404ec827793
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71233365"
---
# <a name="ca1823-avoid-unused-private-fields"></a>CA1823:避免未使用的私有字段

|||
|-|-|
|TypeName|AvoidUnusedPrivateFields|
|CheckId|CA1823|
|类别|Microsoft.Performance|
|重大更改|不间断|

## <a name="cause"></a>原因
当代码中的私有字段存在，但未被任何代码路径使用时，将报告此规则。

## <a name="rule-description"></a>规则说明
检测到程序集内有似乎未访问过的私有字段。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突，请删除字段或添加使用该字段的代码。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
可以安全地禁止显示此规则发出的警告。

## <a name="related-rules"></a>相关规则
[CA1812避免未实例化的内部类](../code-quality/ca1812-avoid-uninstantiated-internal-classes.md)

[CA1801查看未使用的参数](../code-quality/ca1801-review-unused-parameters.md)

[CA1804删除未使用的局部变量](../code-quality/ca1804-remove-unused-locals.md)

[CA1811避免使用未调用的私有代码](../code-quality/ca1811-avoid-uncalled-private-code.md)