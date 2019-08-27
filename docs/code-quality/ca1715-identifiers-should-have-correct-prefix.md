---
title: CA1715:标识符应具有正确的前缀
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
- CA1715
- IdentifiersShouldHaveCorrectPrefix
helpviewer_keywords:
- IdentifiersShouldHaveCorrectPrefix
- CA1715
ms.assetid: cf45f8df-6855-4cb6-a4e2-7cfed714cf2f
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 2a793f0a359cadc58c262861ee0495f92188d0b7
ms.sourcegitcommit: 209ed0fcbb8daa1685e8d6b9a97f3857a4ce1152
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2019
ms.locfileid: "69547179"
---
# <a name="ca1715-identifiers-should-have-correct-prefix"></a>CA1715:标识符应具有正确的前缀

|||
|-|-|
|TypeName|IdentifiersShouldHaveCorrectPrefix|
|CheckId|CA1715|
|类别|Microsoft.Naming|
|是否重大更改|正在进行-在接口上引发。<br /><br /> 非换行-对泛型类型参数引发时。|

## <a name="cause"></a>原因

接口的名称不以大写的 "I" 开头。

或

类型或方法的[泛型类型参数](/dotnet/csharp/programming-guide/generics/generic-type-parameters)的名称不以大写 "t" 开头。

默认情况下, 此规则仅查看外部可见的接口、类型和方法, 但这是[可配置](#configurability)的。

## <a name="rule-description"></a>规则说明

按照约定, 某些编程元素的名称以特定的前缀开头。

接口名称应以大写的 "I" 开头, 后跟另一个大写字母。 此规则报告接口名称 (如 "MyInterface" 和 "IsolatedInterface") 的冲突。

泛型类型参数名称应以大写 "t" 开头, 可选择后跟另一个大写字母。 此规则报告泛型类型参数名称 (如 "V" 和 "Type") 的冲突。

命名约定为面向公共语言运行时的库提供了通用的外观。 这减少了新软件库所需的学习曲线, 并使客户可以放心地了解库是由具有开发托管代码的专业技能的人员开发的。

## <a name="configurability"></a>配置

如果从[FxCop 分析器](install-fxcop-analyzers.md)(而不是传统分析) 运行此规则, 则可以配置此规则分析的代码部分。 有关详细信息, 请参阅[配置 FxCop 分析器](configure-fxcop-analyzers.md)。

### <a name="single-character-type-parameters"></a>单字符类型参数

你可以配置是否从该规则中排除单字符类型参数。 例如, 若要指定此规则*不应*分析单字符类型参数, 请将以下键-值对之一添加到项目中的 editorconfig 文件:

```ini
# Package version 2.9.0 and later
dotnet_code_quality.CA1715.exclude_single_letter_type_parameters = true

# Package version 2.6.3 and earlier
dotnet_code_quality.CA2007.allow_single_letter_type_parameters = true
```

> [!NOTE]
> 对于名`T`为的类型参数, 不会触发此规则, `Collection<T>`例如。

### <a name="api-surface"></a>API 图面

你可以根据其可访问性, 将基本代码的哪些部分配置为在上运行此规则。 例如, 若要指定规则只应针对非公共 API 图面运行, 请在项目中的 editorconfig 文件中添加以下键/值对:

```ini
dotnet_code_quality.ca1715.api_surface = private, internal
```

您可以为此规则、所有规则或此类别中的所有规则 (命名) 配置此选项。

## <a name="how-to-fix-violations"></a>如何解决冲突

重命名标识符, 使其具有正确的前缀。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

不禁止显示此规则发出的警告。

## <a name="interface-naming-example"></a>接口命名示例

以下代码段显示了一个错误命名接口:

[!code-cpp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix#1](../code-quality/codesnippet/CPP/ca1715-identifiers-should-have-correct-prefix_1.cpp)]
[!code-vb[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix#1](../code-quality/codesnippet/VisualBasic/ca1715-identifiers-should-have-correct-prefix_1.vb)]
[!code-csharp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix#1](../code-quality/codesnippet/CSharp/ca1715-identifiers-should-have-correct-prefix_1.cs)]

下面的代码片段通过使用 "I" 作为接口的前缀来修复以前的冲突:

[!code-csharp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix2#1](../code-quality/codesnippet/CSharp/ca1715-identifiers-should-have-correct-prefix_2.cs)]
[!code-cpp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix2#1](../code-quality/codesnippet/CPP/ca1715-identifiers-should-have-correct-prefix_2.cpp)]
[!code-vb[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix2#1](../code-quality/codesnippet/VisualBasic/ca1715-identifiers-should-have-correct-prefix_2.vb)]

## <a name="type-parameter-naming-example"></a>类型参数命名示例

以下代码段显示了错误命名的泛型类型参数:

[!code-cpp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix3#1](../code-quality/codesnippet/CPP/ca1715-identifiers-should-have-correct-prefix_3.cpp)]
[!code-vb[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix3#1](../code-quality/codesnippet/VisualBasic/ca1715-identifiers-should-have-correct-prefix_3.vb)]
[!code-csharp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix3#1](../code-quality/codesnippet/CSharp/ca1715-identifiers-should-have-correct-prefix_3.cs)]

下面的代码片段通过使用 "t" 作为泛型类型参数的前缀来修复以前的冲突:

[!code-cpp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix4#1](../code-quality/codesnippet/CPP/ca1715-identifiers-should-have-correct-prefix_4.cpp)]
[!code-csharp[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix4#1](../code-quality/codesnippet/CSharp/ca1715-identifiers-should-have-correct-prefix_4.cs)]
[!code-vb[FxCop.Naming.IdentifiersShouldHaveCorrectPrefix4#1](../code-quality/codesnippet/VisualBasic/ca1715-identifiers-should-have-correct-prefix_4.vb)]

## <a name="related-rules"></a>相关规则

- [CA1722标识符不应具有正确的前缀](../code-quality/ca1722-identifiers-should-not-have-incorrect-prefix.md)