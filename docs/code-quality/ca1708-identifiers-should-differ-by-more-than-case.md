---
title: CA1708:标识符应以大小写之外的差别进行区分
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
- IdentifiersShouldDifferByMoreThanCase
- CA1708
helpviewer_keywords:
- CA1708
- IdentifiersShouldDifferByMoreThanCase
ms.assetid: dac0f01d-dd21-484d-add1-c8cd2bf6969f
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5098e2feadc6d67c466e31ab19d059ac70c7d833
ms.sourcegitcommit: 209ed0fcbb8daa1685e8d6b9a97f3857a4ce1152
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2019
ms.locfileid: "69547398"
---
# <a name="ca1708-identifiers-should-differ-by-more-than-case"></a>CA1708:标识符应以大小写之外的差别进行区分

|||
|-|-|
|TypeName|IdentifiersShouldDifferByMoreThanCase|
|CheckId|CA1708|
|类别|Microsoft.Naming|
|是否重大更改|重大|

## <a name="cause"></a>原因

当两个类型、成员、参数或完全限定的命名空间的名称转换为小写时, 它们的名称相同。

默认情况下, 此规则仅查看外部可见类型、成员和命名空间, 但这是[可配置](#configurability)的。

## <a name="rule-description"></a>规则说明

不能仅通过大小写区分命名空间、类型、成员和参数的标识符，因为针对公共语言运行时的语言不需要区分大小写。 例如, [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]是一种广泛使用的不区分大小写的语言。

此规则仅对公共可见成员触发。

## <a name="how-to-fix-violations"></a>如何解决冲突

选择一个唯一的名称, 当与其他标识符进行比较时, 该名称不区分大小写。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

不禁止显示此规则发出的警告。 库可能无法用于 .NET 中的所有可用语言。

## <a name="configurability"></a>配置

如果从[FxCop 分析器](install-fxcop-analyzers.md)(而不是传统分析) 运行此规则, 则可以根据其可访问性, 将基本代码的哪些部分配置为在上运行此规则。 例如, 若要指定规则只应针对非公共 API 图面运行, 请在项目中的 editorconfig 文件中添加以下键/值对:

```ini
dotnet_code_quality.ca1708.api_surface = private, internal
```

您可以为此规则、所有规则或此类别中的所有规则 (命名) 配置此选项。 有关详细信息, 请参阅[配置 FxCop 分析器](configure-fxcop-analyzers.md)。

## <a name="example-of-a-violation"></a>冲突示例

下面的示例演示违反此规则的情况。

[!code-csharp[FxCop.Naming.IdentifiersShouldDifferByMoreThanCase#1](../code-quality/codesnippet/CSharp/ca1708-identifiers-should-differ-by-more-than-case_1.cs)]

## <a name="related-rules"></a>相关规则

- [CA1709标识符应采用正确的大小写](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)