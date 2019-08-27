---
title: CA1720:标识符不应包含类型名称
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
- CA1720
- IdentifiersShouldNotContainTypeNames
helpviewer_keywords:
- IdentifiersShouldNotContainTypeNames
- CA1720
ms.assetid: c95ee48f-f23a-45f0-ac9e-a3c1ecfabdea
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a35bec2395ccec649443df71e87904c71bf635d8
ms.sourcegitcommit: 209ed0fcbb8daa1685e8d6b9a97f3857a4ce1152
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2019
ms.locfileid: "69547109"
---
# <a name="ca1720-identifiers-should-not-contain-type-names"></a>CA1720:标识符不应包含类型名称

|||
|-|-|
|TypeName|IdentifiersShouldNotContainTypeNames|
|CheckId|CA1720|
|类别|Microsoft.Naming|
|是否重大更改|重大|

## <a name="cause"></a>原因

成员中参数的名称包含数据类型名称。

或

成员的名称包含特定于语言的数据类型名称。

默认情况下, 此规则仅查看外部可见成员, 但这是[可配置](#configurability)的。

## <a name="rule-description"></a>规则说明

参数和成员的名称比描述其类型 (需要由开发工具提供) 更好。 对于成员的名称, 如果必须使用数据类型名称, 请使用与语言无关的名称, 而不是特定于语言的名称。 例如, 使用与语言无关C#的`Int32`数据`int`类型名称 (而不是类型名称)。

将按照不区分大小写的方式检查参数或成员的名称中的每个离散标记:

- Bool
- WChar
- Int8
- UInt8
- Short
- UShort
- Int
- UInt
- 整数
- UInteger
- Long
- ULong
- 无符号
- 有符号
- Float
- Float32
- Float64

此外, 还会对照不区分大小写的方法对以下与语言无关的数据类型名称检查参数的名称:

- Object
- Obj
- Boolean
- Char
- String
- SByte
- Byte
- UByte
- Int16
- UInt16
- Int32
- UInt32
- Int64
- UInt64
- IntPtr
- Ptr
- 指针
- UInptr
- UPtr
- UPointer
- Single
- Double
- Decimal
- Guid

## <a name="how-to-fix-violations"></a>如何解决冲突

**如果针对参数触发:**

将参数名称中的数据类型标识符替换为可更好地描述其含义的字词或更通用的字词, 如 "value"。

**如果对成员触发:**

将成员名称中特定于语言的数据类型标识符替换为可更好地描述其含义的术语、与语言无关的等效项或更通用的字词, 如 "value"。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

偶尔使用基于类型的参数和成员名称可能是合适的。 但是, 对于新的开发, 不会出现任何已知方案, 你应禁止显示此规则发出的警告。 对于先前随附的库, 可能必须禁止显示此规则发出的警告。

## <a name="configurability"></a>配置

如果从[FxCop 分析器](install-fxcop-analyzers.md)(而不是传统分析) 运行此规则, 则可以根据其可访问性, 将基本代码的哪些部分配置为在上运行此规则。 例如, 若要指定规则只应针对非公共 API 图面运行, 请在项目中的 editorconfig 文件中添加以下键/值对:

```ini
dotnet_code_quality.ca1720.api_surface = private, internal
```

您可以为此规则、所有规则或此类别中的所有规则 (命名) 配置此选项。 有关详细信息, 请参阅[配置 FxCop 分析器](configure-fxcop-analyzers.md)。

## <a name="related-rules"></a>相关规则

- [CA1709标识符应采用正确的大小写](../code-quality/ca1709-identifiers-should-be-cased-correctly.md)
- [CA1708标识符的差别应超过大小写](../code-quality/ca1708-identifiers-should-differ-by-more-than-case.md)
- [CA1707标识符不应包含下划线](../code-quality/ca1707-identifiers-should-not-contain-underscores.md)
- [CA1719参数名不应与成员名匹配](../code-quality/ca1719-parameter-names-should-not-match-member-names.md)