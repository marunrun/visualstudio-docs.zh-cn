---
title: CA1700:不为保留的枚举&#39;值命名&#39;
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
ms.openlocfilehash: 5171123827481c99bbc35c10b04aaf942a15fabb
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71234393"
---
# <a name="ca1700-do-not-name-enum-values-39reserved39"></a>CA1700:不为保留的枚举&#39;值命名&#39;

|||
|-|-|
|TypeName|DoNotNameEnumValuesReserved|
|CheckId|CA1700|
|类别|Microsoft.Naming|
|重大更改|重大|

## <a name="cause"></a>原因

枚举成员的名称包含单词 "reserved"。

## <a name="rule-description"></a>规则说明

此规则假定当前不使用名称中包含“reserved”的枚举成员，而是将其作为一个占位符，以在将来的版本中重命名或移除它。 重命名或移除成员是一项重大更改。 不应指望用户只是因为其名称包含 "保留" 而忽略成员，也不能依赖于用户阅读或遵守文档。 此外，由于保留成员显示在对象浏览器和智能集成开发环境中，因此它们可能会导致混淆实际使用的成员。

在将来的版本中，将新成员添加到枚举，而不是使用保留成员。 在大多数情况下，添加新成员不是一项重大更改，只要添加不会导致原始成员的值发生变化。

在有限的情况下，添加成员是一项重大更改，即使原始成员保留其原始值也是如此。 主要是，无法从现有代码路径返回新成员，并且不会中断对包含`switch`整个`Select`成员列表[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]的返回值使用（in）语句并引发异常的调用方默认情况。 第二个问题是：客户端代码可能无法处理反射方法（如） <xref:System.Enum.IsDefined%2A?displayProperty=fullName>的行为更改。 相应地，如果新成员必须从现有方法返回，或者由于反射的使用不正确而发生已知的应用程序不兼容性，则唯一的不间断解决方案是：

1. 添加包含原始成员和新成员的新枚举。

2. 用<xref:System.ObsoleteAttribute?displayProperty=fullName>特性标记原始枚举。

   对于公开原始枚举的任何外部可见类型或成员，请遵循相同的过程。

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，请删除或重命名该成员。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

对于当前使用的成员或以前发布的库，可以安全地禁止显示此规则发出的警告。

## <a name="related-rules"></a>相关规则

[CA2217不要用 FlagsAttribute 标记枚举](../code-quality/ca2217-do-not-mark-enums-with-flagsattribute.md)

[CA1712不要将类型名称作为枚举值的前缀](../code-quality/ca1712-do-not-prefix-enum-values-with-type-name.md)

[CA1028枚举存储应为 Int32](../code-quality/ca1028-enum-storage-should-be-int32.md)

[CA1008枚举应具有零值](../code-quality/ca1008-enums-should-have-zero-value.md)

[CA1027用 FlagsAttribute 标记枚举](../code-quality/ca1027-mark-enums-with-flagsattribute.md)