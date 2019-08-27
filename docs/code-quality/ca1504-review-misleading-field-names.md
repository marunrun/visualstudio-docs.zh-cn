---
title: CA1504:检查令人误解的字段名
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- ReviewMisleadingFieldNames
- CA1504
helpviewer_keywords:
- CA1504
- ReviewMisleadingFieldNames
ms.assetid: 94136ff1-4aaf-4dc2-9170-48c171ab7499
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: df6ab704c2dfdbf8ebdf8eb42f56d8d64600736f
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68921830"
---
# <a name="ca1504-review-misleading-field-names"></a>CA1504:检查令人误解的字段名

|||
|-|-|
|TypeName|ReviewMisleadingFieldNames|
|CheckId|CA1504|
|类别|Microsoft.Maintainability|
|是否重大更改|不间断|

## <a name="cause"></a>原因
实例字段的名称以 "s_" 开头, 或 ( `static` `Shared`在中[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]为) 字段的名称以 "m_" 开头。

## <a name="rule-description"></a>规则说明
以 "s_" 开头的字段名称与多个用户的静态数据相关联。 同样, 以 "m_" 开头的字段名称与实例 (成员) 数据相关联。 为了更轻松地维护代码, 名称应遵循一般使用的约定。

## <a name="how-to-fix-violations"></a>如何解决冲突
若要修复与此规则的冲突, 请使用相应的前缀重命名该字段。 或者, 通过添加或删除`static`修饰符, 使字段与当前后缀一致。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
不禁止显示此规则发出的警告。