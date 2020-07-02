---
title: CA1710：标识符应具有正确的后缀 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1710
- IdentifiersShouldHaveCorrectSuffix
helpviewer_keywords:
- IdentifiersShouldHaveCorrectSuffix
- CA1710
ms.assetid: 2b8e6dce-b4e8-4a66-ba9a-6b79be5bfe8c
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 0ee7ce7c4e9edad9d941b4a70b2a199a37130e43
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543983"
---
# <a name="ca1710-identifiers-should-have-correct-suffix"></a>CA1710:标识符应具有正确的后缀
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|项|值|
|-|-|
|TypeName|IdentifiersShouldHaveCorrectSuffix|
|CheckId|CA1710|
|类别|Microsoft。命名|
|是否重大更改|重大|

## <a name="cause"></a>原因
 标识符的后缀不正确。

## <a name="rule-description"></a>规则描述
 按照约定，扩展某些基类型或实现某些接口的类型的名称或从这些类型派生的类型具有与基类型或接口关联的后缀。

 命名约定为面向公共语言运行时的库提供了通用的外观。 这减少了新软件库所需的学习曲线，并使客户可以放心地了解库是由具有开发托管代码的专业技能的人员开发的。

 下表列出了具有关联后缀的基类型和接口。

|基类型/接口|Suffix|
|--------------------------|------------|
|<xref:System.Attribute?displayProperty=fullName>|特性|
|<xref:System.EventArgs?displayProperty=fullName>|EventArgs|
|<xref:System.Exception?displayProperty=fullName>|例外|
|<xref:System.Collections.ICollection?displayProperty=fullName>|集合|
|<xref:System.Collections.IDictionary?displayProperty=fullName>|字典|
|<xref:System.Collections.IEnumerable?displayProperty=fullName>|集合|
|<xref:System.Collections.Queue?displayProperty=fullName>|集合或队列|
|<xref:System.Collections.Stack?displayProperty=fullName>|集合或堆栈|
|<xref:System.Collections.Generic.ICollection%601?displayProperty=fullName>|集合|
|<xref:System.Collections.Generic.IDictionary%602?displayProperty=fullName>|字典|
|<xref:System.Data.DataSet?displayProperty=fullName>|数据集|
|<xref:System.Data.DataTable?displayProperty=fullName>|集合或 DataTable|
|<xref:System.IO.Stream?displayProperty=fullName>|Stream|
|<xref:System.Security.IPermission?displayProperty=fullName>|权限|
|<xref:System.Security.Policy.IMembershipCondition?displayProperty=fullName>|条件|
|事件处理程序委托。|EventHandler|

 实现 <xref:System.Collections.ICollection> 并且是一种通用类型的数据结构（如字典、堆栈或队列）的类型是允许的名称，这些名称提供有关类型的预期用法的有用信息。

 实现和的类型 <xref:System.Collections.ICollection> 是特定项的集合，其名称以单词 "collection" 结尾。 例如，对象的集合的 <xref:System.Collections.Queue> 名称为 "QueueCollection"。 "Collection" 后缀表示可以使用 `foreach` （ `For Each` in）语句枚举集合的成员 [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] 。

 实现的类型的 <xref:System.Collections.IDictionary> 名称以单词 "Dictionary" 结尾，即使该类型还实现了 <xref:System.Collections.IEnumerable> 或 <xref:System.Collections.ICollection> 。 "集合" 和 "字典" 后缀命名约定使用户能够区分以下两个枚举模式。

 具有 "Collection" 后缀的类型遵循此枚举模式。

```
foreach(SomeType x in SomeCollection) { }
```

 带有 "Dictionary" 后缀的类型遵循此枚举模式。

```
foreach(SomeType x in SomeDictionary.Values) { }
```

 <xref:System.Data.DataSet>对象包含对象的集合 <xref:System.Data.DataTable> ，这些对象由和对象的集合组成 <xref:System.Data.DataColumn?displayProperty=fullName> <xref:System.Data.DataRow?displayProperty=fullName> 。 这些集合 <xref:System.Collections.ICollection> 通过基类实现 <xref:System.Data.InternalDataCollectionBase?displayProperty=fullName> 。

## <a name="how-to-fix-violations"></a>如何解决冲突
 重命名该类型，使其具有正确的字词后缀。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果类型是可能被扩展的通用数据结构，或者将保留任意一组不同的项，则可以安全地禁止显示警告以使用 "集合" 后缀。 在这种情况下，提供有关实现、性能或数据结构的其他特征的有用信息的名称可能有意义（例如，BinaryTree）。 在类型表示特定类型的集合的情况下（例如，StringCollection），请勿禁止显示此规则的警告，因为后缀指示可以使用语句来枚举该类型 `foreach` 。

 对于其他后缀，不要禁止显示此规则发出的警告。 后缀允许从类型名称中清晰地使用预期用法。

## <a name="related-rules"></a>相关规则
 [CA1711:标识符应采用正确的后缀](../code-quality/ca1711-identifiers-should-not-have-incorrect-suffix.md)

## <a name="see-also"></a>另请参阅
 [特性](https://msdn.microsoft.com/library/ee0038ef-b247-4747-a650-3c5c5cd58d8b)[笔尖：事件和委托](https://msdn.microsoft.com/d98fd58b-fa4f-4598-8378-addf4355a115)
