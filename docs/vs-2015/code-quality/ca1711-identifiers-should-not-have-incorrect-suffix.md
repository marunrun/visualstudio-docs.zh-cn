---
title: CA1711:标识符应采用正确的后缀 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- CA1711
- IdentifiersShouldNotHaveIncorrectSuffix
helpviewer_keywords:
- CA1711
- IdentifiersShouldNotHaveIncorrectSuffix
ms.assetid: a63359ab-386d-44ae-b381-ee3a983aca29
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: c0ed08a50ce7e4c665839f6dccb4913e13d0d774
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65676477"
---
# <a name="ca1711-identifiers-should-not-have-incorrect-suffix"></a>CA1711:标识符应采用正确的后缀
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|IdentifiersShouldNotHaveIncorrectSuffix|
|CheckId|CA1711|
|类别|Microsoft.Naming|
|是否重大更改|重大|

## <a name="cause"></a>原因
 标识符具有正确的后缀。

## <a name="rule-description"></a>规则说明
 按照约定，只有扩展某些基类型或实现特定接口或从这些类型派生的类型的类型的名称应与特定的保留后缀结尾。 其他类型名称不应使用这些保留的后缀。

 下表列出了保留的后缀的基类型和接口与它们相关联。

|Suffix|基类型/接口|
|------------|--------------------------|
|特性|<xref:System.Attribute?displayProperty=fullName>|
|集合|<xref:System.Collections.ICollection?displayProperty=fullName><br /><br /> <xref:System.Collections.IEnumerable?displayProperty=fullName><br /><br /> <xref:System.Collections.Queue?displayProperty=fullName><br /><br /> <xref:System.Collections.Stack?displayProperty=fullName><br /><br /> <xref:System.Collections.Generic.ICollection%601?displayProperty=fullName><br /><br /> <xref:System.Data.DataSet?displayProperty=fullName><br /><br /> <xref:System.Data.DataTable?displayProperty=fullName>|
|词典|<xref:System.Collections.IDictionary?displayProperty=fullName><br /><br /> <xref:System.Collections.Generic.IDictionary%602?displayProperty=fullName>|
|EventArgs|<xref:System.EventArgs?displayProperty=fullName>|
|EventHandler|事件处理程序委托|
|例外|<xref:System.Exception?displayProperty=fullName>|
|权限|<xref:System.Security.IPermission?displayProperty=fullName>|
|Queue|<xref:System.Collections.Queue?displayProperty=fullName>|
|堆栈|<xref:System.Collections.Stack?displayProperty=fullName>|
|流|<xref:System.IO.Stream?displayProperty=fullName>|

 此外，以下后缀应**不**使用：

- 委托

- Enum

- 此实现-请改用 Core

- Ex 或类似的后缀，以使其不同于早期版本的相同的类型

  命名约定提供了通用的外观对于库面向公共语言运行时。 这会减少所需的新软件库，并会增加客户信心库由必须在托管代码中开发的专业知识的人学习曲线。

## <a name="how-to-fix-violations"></a>如何解决冲突
 删除类型名称的后缀。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 除非后缀在应用程序域中具有明确的含义，否则不要禁止显示来自此规则的警告。

## <a name="related-rules"></a>相关的规则
 [CA1710:标识符应具有正确的后缀](../code-quality/ca1710-identifiers-should-have-correct-suffix.md)

## <a name="see-also"></a>请参阅
 [特性](https://msdn.microsoft.com/library/ee0038ef-b247-4747-a650-3c5c5cd58d8b) [NIB:事件和委托](https://msdn.microsoft.com/d98fd58b-fa4f-4598-8378-addf4355a115)
