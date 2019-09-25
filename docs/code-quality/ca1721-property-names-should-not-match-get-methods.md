---
title: CA1721:属性名不应与 get 方法冲突
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
- CA1721
- PropertyNamesShouldNotMatchGetMethods
helpviewer_keywords:
- CA1721
- PropertyNamesShouldNotMatchGetMethods
ms.assetid: 45a0e853-1f06-4688-af1b-cc634409e295
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 805ceb7abf7096df29894a23be6c8e7b1f6bd5b2
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71233910"
---
# <a name="ca1721-property-names-should-not-match-get-methods"></a>CA1721:属性名不应与 get 方法冲突

|||
|-|-|
|TypeName|PropertyNamesShouldNotMatchGetMethods|
|CheckId|CA1721|
|类别|Microsoft.Naming|
|重大更改|重大|

## <a name="cause"></a>原因

成员的名称以 "Get" 开头，否则与属性的名称匹配。 例如，包含名为 "GetColor" 的方法和名为 "Color" 的属性的类型将导致规则冲突。

默认情况下，此规则仅查看外部可见的成员和属性，但这是[可配置](#configurability)的。

## <a name="rule-description"></a>规则说明

“Get”方法和属性的名称应能够明确区分其功能上的差异。

命名约定为面向公共语言运行时的库提供了通用的外观。 这种一致性缩短了学习新软件库所需的时间，并使客户对库开发的用户信心提高了库开发人员开发托管代码的专业技能。

## <a name="how-to-fix-violations"></a>如何解决冲突

更改名称，使其与前缀为 "Get" 的方法的名称不匹配。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

不禁止显示此规则发出的警告。

> [!NOTE]
> 如果 "Get" 方法是通过实现既也接口引起的，则可能排除此警告。

## <a name="configurability"></a>配置

如果从[FxCop 分析器](install-fxcop-analyzers.md)（而不是传统分析）运行此规则，则可以根据其可访问性，将基本代码的哪些部分配置为在上运行此规则。 例如，若要指定规则只应针对非公共 API 图面运行，请在项目中的 editorconfig 文件中添加以下键/值对：

```ini
dotnet_code_quality.ca1721.api_surface = private, internal
```

您可以为此规则、所有规则或此类别中的所有规则（命名）配置此选项。 有关详细信息，请参阅[配置 FxCop 分析器](configure-fxcop-analyzers.md)。

## <a name="example"></a>示例

下面的示例包含违反此规则的方法和属性。

[!code-csharp[FxCop.Naming.GetMethod#1](../code-quality/codesnippet/CSharp/ca1721-property-names-should-not-match-get-methods_1.cs)]
[!code-vb[FxCop.Naming.GetMethod#1](../code-quality/codesnippet/VisualBasic/ca1721-property-names-should-not-match-get-methods_1.vb)]

## <a name="related-rules"></a>相关规则

- [CA1024使用适当的属性](../code-quality/ca1024-use-properties-where-appropriate.md)