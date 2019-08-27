---
title: CA1710:标识符应具有正确的后缀 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 16b4c2fb13a8de1824233b491d752b796aea907d
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65676553"
---
# <a name="ca1710-identifiers-should-have-correct-suffix"></a>CA1710:标识符应具有正确的后缀
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|IdentifiersShouldHaveCorrectSuffix|
|CheckId|CA1710|
|类别|Microsoft.Naming|
|是否重大更改|重大|

## <a name="cause"></a>原因
 标识符不具有正确的后缀。

## <a name="rule-description"></a>规则说明
 按照约定，类型扩展某些基类型或实现特定接口或从这些类型派生的类型的名称具有与基类型或接口关联的后缀。

 命名约定提供了通用的外观对于库面向公共语言运行时。 这会减少所需的新软件库，并会增加客户信心库由必须在托管代码中开发的专业知识的人学习曲线。

 下表列出了基本类型和接口具有关联的后缀。

|基类型/接口|Suffix|
|--------------------------|------------|
|<xref:System.Attribute?displayProperty=fullName>|特性|
|<xref:System.EventArgs?displayProperty=fullName>|EventArgs|
|<xref:System.Exception?displayProperty=fullName>|例外|
|<xref:System.Collections.ICollection?displayProperty=fullName>|集合|
|<xref:System.Collections.IDictionary?displayProperty=fullName>|词典|
|<xref:System.Collections.IEnumerable?displayProperty=fullName>|集合|
|<xref:System.Collections.Queue?displayProperty=fullName>|集合或队列|
|<xref:System.Collections.Stack?displayProperty=fullName>|集合或堆栈|
|<xref:System.Collections.Generic.ICollection%601?displayProperty=fullName>|集合|
|<xref:System.Collections.Generic.IDictionary%602?displayProperty=fullName>|词典|
|<xref:System.Data.DataSet?displayProperty=fullName>|数据集|
|<xref:System.Data.DataTable?displayProperty=fullName>|集合或 DataTable|
|<xref:System.IO.Stream?displayProperty=fullName>|流|
|<xref:System.Security.IPermission?displayProperty=fullName>|权限|
|<xref:System.Security.Policy.IMembershipCondition?displayProperty=fullName>|条件|
|一个事件处理程序委托。|EventHandler|

 类型实现<xref:System.Collections.ICollection>和是通用的类型的数据结构，如字典、 堆栈或队列，允许提供有意义信息的预期用法的类型的名称。

 类型实现<xref:System.Collections.ICollection>和是特定项的集合具有 Collection 一词结尾的名称。 例如，集合<xref:System.Collections.Queue>对象将具有名称 QueueCollection。 Collection 后缀表示后，可以使用枚举集合的成员`foreach`(`For Each`中[!INCLUDE[vbprvb](../includes/vbprvb-md.md)]) 语句。

 类型实现<xref:System.Collections.IDictionary>名称以字典一词结尾，即使该类型还实现<xref:System.Collections.IEnumerable>或<xref:System.Collections.ICollection>。 Collection 和字典后缀命名约定使用户能够区分以下两个枚举模式。

 具有后缀 Collection 的类型遵循此枚举模式。

```
foreach(SomeType x in SomeCollection) { }
```

 使用字典后缀的类型遵循此枚举模式。

```
foreach(SomeType x in SomeDictionary.Values) { }
```

 一个<xref:System.Data.DataSet>对象的集合组成<xref:System.Data.DataTable>包含的集合的对象<xref:System.Data.DataColumn?displayProperty=fullName>和<xref:System.Data.DataRow?displayProperty=fullName>对象，等等。 这些集合实现<xref:System.Collections.ICollection>通过基<xref:System.Data.InternalDataCollectionBase?displayProperty=fullName>类。

## <a name="how-to-fix-violations"></a>如何解决冲突
 重命名该类型，以便使用正确的字词作为后缀。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 它是安全地禁止显示一个警告，如果类型是一种通用的数据结构可能会扩展，或将包含一组任意的各种项，请使用后缀 Collection。 在这种情况下，提供了有关实现、 性能或数据结构的其他特征有意义的信息的名称 binarytree (例如，)。 在某些情况下，该类型的特定类型 (例如，StringCollection) 集合，不要禁止显示此规则的警告因为后缀指示后，可以使用枚举类型`foreach`语句。

 对于其他后缀，不要禁止显示此规则的警告。 该后缀，可为表露类型名称的预期的用法。

## <a name="related-rules"></a>相关的规则
 [CA1711:标识符应采用正确的后缀](../code-quality/ca1711-identifiers-should-not-have-incorrect-suffix.md)

## <a name="see-also"></a>请参阅
 [特性](https://msdn.microsoft.com/library/ee0038ef-b247-4747-a650-3c5c5cd58d8b) [NIB:事件和委托](https://msdn.microsoft.com/d98fd58b-fa4f-4598-8378-addf4355a115)
