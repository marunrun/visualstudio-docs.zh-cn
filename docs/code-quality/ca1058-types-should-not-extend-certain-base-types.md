---
title: CA1058:类型不应扩展某些基类型
ms.date: 03/11/2019
ms.topic: reference
f1_keywords:
- TypesShouldNotExtendCertainBaseTypes
- CA1058
helpviewer_keywords:
- CA1058
- TypesShouldNotExtendCertainBaseTypes
ms.assetid: 8446ee40-beb1-49fa-8733-4d8e813471c0
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fa1ffbb393700647f12c455c8d1307a77548f2d1
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71235497"
---
# <a name="ca1058-types-should-not-extend-certain-base-types"></a>CA1058:类型不应扩展某些基类型

|||
|-|-|
|TypeName|TypesShouldNotExtendCertainBaseTypes|
|CheckId|CA1058|
|类别|Microsoft.Design|
|重大更改|重大|

## <a name="cause"></a>原因

类型扩展了以下基类型之一：

- <xref:System.ApplicationException?displayProperty=fullName>
- <xref:System.Xml.XmlDocument?displayProperty=fullName>
- <xref:System.Collections.CollectionBase?displayProperty=fullName>
- <xref:System.Collections.DictionaryBase?displayProperty=fullName>
- <xref:System.Collections.Queue?displayProperty=fullName>
- <xref:System.Collections.ReadOnlyCollectionBase?displayProperty=fullName>
- <xref:System.Collections.SortedList?displayProperty=fullName>
- <xref:System.Collections.Stack?displayProperty=fullName>

默认情况下，此规则仅查看外部可见类型，但这是[可配置](#configurability)的。

## <a name="rule-description"></a>规则说明

异常应派生自<xref:System.Exception?displayProperty=fullName> <xref:System>命名空间中的或它的其中一个子类。

<xref:System.Xml.XmlDocument>如果要创建基础对象模型或数据源的 XML 视图，请不要创建的子类。

### <a name="non-generic-collections"></a>非泛型集合

尽可能使用和/或扩展泛型集合。 不要在代码中扩展非泛型集合，除非你之前已将其发布。

**错误用法的示例**

```csharp
public class MyCollection : CollectionBase
{
}

public class MyReadOnlyCollection : ReadOnlyCollectionBase
{
}
```

**正确用法的示例**

```csharp
public class MyCollection : Collection<T>
{
}

public class MyReadOnlyCollection : ReadOnlyCollection<T>
{
}
```

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，请从其他基类型或泛型集合派生该类型。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

不要禁止显示此规则发出的有关<xref:System.ApplicationException>的冲突。 可以安全地禁止显示此规则发出的有关<xref:System.Xml.XmlDocument>冲突的警告。 如果以前发布了代码，则可以安全地禁止显示非泛型集合的警告。

## <a name="configurability"></a>配置

如果从[FxCop 分析器](install-fxcop-analyzers.md)（而不是传统分析）运行此规则，则可以根据其可访问性，将基本代码的哪些部分配置为在上运行此规则。 例如，若要指定规则只应针对非公共 API 图面运行，请在项目中的 editorconfig 文件中添加以下键/值对：

```ini
dotnet_code_quality.ca1058.api_surface = private, internal
```

您可以为此规则、所有规则或此类别中的所有规则（设计）配置此选项。 有关详细信息，请参阅[配置 FxCop 分析器](configure-fxcop-analyzers.md)。