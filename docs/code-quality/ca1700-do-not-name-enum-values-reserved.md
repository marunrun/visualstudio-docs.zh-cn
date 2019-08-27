---
title: CA1700:未命名枚举值&#39;保留&#39;
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- CA1700
- DoNotNameEnumValuesReserved
helpviewer_keywords:
- DoNotNameEnumValuesReserved
- CA1700
ms.assetid: 7a7e01c3-ae7d-4c82-a646-91b58864a749
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0f4b08c10fa0d9aa4dea2a58d7e219371baf13ac
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62797389"
---
# <a name="ca1700-do-not-name-enum-values-39reserved39"></a>CA1700:未命名枚举值&#39;保留&#39;

|||
|-|-|
|TypeName|DoNotNameEnumValuesReserved|
|CheckId|CA1700|
|类别|Microsoft.Naming|
|是否重大更改|重大|

## <a name="cause"></a>原因

枚举成员的名称包含单词"保留"。

## <a name="rule-description"></a>规则说明

此规则假定当前不使用名称中包含“reserved”的枚举成员，而是将其作为一个占位符，以在将来的版本中重命名或移除它。 重命名或移除成员是一项重大更改。 不应期望用户只是因为其名称包含"保留"，也不能依赖用户读取或遵守文档会忽略该成员。 此外，由于保留的成员显示在对象浏览器和智能的集成的开发环境中，它们可能会导致的混淆的成员实际上正在使用的相关。

而不是使用保留的成员，将添加到未来版本中枚举的一个新成员。 在大多数情况下添加新成员不是一项重大更改，只要添加不会导致要更改的原始成员的值。

在有限数量的情况下成员的添加是一项重大更改，即使原始成员保留其原始值。 首先，新的成员不能返回从现有的代码路径而不会破坏使用的调用方`switch`(`Select`中[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]) 返回值使用一个包含整个成员列表和的引发异常的语句默认情况。 次要问题是，客户端代码可能不处理行为的反射方法更改如<xref:System.Enum.IsDefined%2A?displayProperty=fullName>。 相应地，如果要从现有方法中返回具有新的成员，或者已知的应用程序不兼容时由于较差的反射，唯一的非中断性解决方案是：

1. 添加新的枚举，它包含原始的和新成员。

2. 标记使用的原始枚举<xref:System.ObsoleteAttribute?displayProperty=fullName>属性。

   请按照相同的过程的任何外部可见的类型或公开原始枚举的成员。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复此规则的冲突，请删除或重命名的成员。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

它可以安全地禁止显示此规则的警告，当前使用的成员或对以前发布的库。

## <a name="related-rules"></a>相关的规则

[CA2217:不使用 FlagsAttribute 标记枚举](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)

[CA1712:不要使用类型名称的枚举值的前缀](../code-quality/ca1712-do-not-prefix-enum-values-with-type-name.md)

[CA1028:枚举存储应为 Int32](../code-quality/ca1028-enum-storage-should-be-int32.md)

[CA1008:枚举应具有零值](../code-quality/ca1008-enums-should-have-zero-value.md)

[CA1027:用 FlagsAttribute 标记枚举](../code-quality/ca1027-mark-enums-with-flagsattribute.md)