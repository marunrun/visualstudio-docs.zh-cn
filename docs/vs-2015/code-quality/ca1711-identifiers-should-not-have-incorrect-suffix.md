---
title: CA1711：标识符不应包含错误的后缀 |Microsoft Docs
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
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 1e753083e9b4bda1e33553021ccb0027a2af2533
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544009"
---
# <a name="ca1711-identifiers-should-not-have-incorrect-suffix"></a>CA1711:标识符应采用正确的后缀
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|值|
|-|-|
|TypeName|IdentifiersShouldNotHaveIncorrectSuffix|
|CheckId|CA1711|
|Category|Microsoft。命名|
|是否重大更改|重大|

## <a name="cause"></a>原因
 标识符的后缀不正确。

## <a name="rule-description"></a>规则描述
 按照约定，只有扩展某些基类型或实现某些接口的类型的名称，或从这些类型派生的类型的名称应以特定的保留后缀结尾。 其他类型名称不应使用这些保留的后缀。

 下表列出了保留的后缀以及与它们关联的基类型和接口。

|Suffix|基类型/接口|
|------------|--------------------------|
|Attribute|<xref:System.Attribute?displayProperty=fullName>|
|集合|<xref:System.Collections.ICollection?displayProperty=fullName><br /><br /> <xref:System.Collections.IEnumerable?displayProperty=fullName><br /><br /> <xref:System.Collections.Queue?displayProperty=fullName><br /><br /> <xref:System.Collections.Stack?displayProperty=fullName><br /><br /> <xref:System.Collections.Generic.ICollection%601?displayProperty=fullName><br /><br /> <xref:System.Data.DataSet?displayProperty=fullName><br /><br /> <xref:System.Data.DataTable?displayProperty=fullName>|
|字典|<xref:System.Collections.IDictionary?displayProperty=fullName><br /><br /> <xref:System.Collections.Generic.IDictionary%602?displayProperty=fullName>|
|EventArgs|<xref:System.EventArgs?displayProperty=fullName>|
|EventHandler|事件处理程序委托|
|异常|<xref:System.Exception?displayProperty=fullName>|
|权限|<xref:System.Security.IPermission?displayProperty=fullName>|
|队列|<xref:System.Collections.Queue?displayProperty=fullName>|
|堆栈|<xref:System.Collections.Stack?displayProperty=fullName>|
|Stream|<xref:System.IO.Stream?displayProperty=fullName>|

 此外，**不**应使用以下后缀：

- 委托

- 枚举

- Impl-改为使用 "Core"

- Ex 或类似的后缀，以将其与同一类型的早期版本区分开来

  命名约定为面向公共语言运行时的库提供了通用的外观。 这减少了新软件库所需的学习曲线，并使客户可以放心地了解库是由具有开发托管代码的专业技能的人员开发的。

## <a name="how-to-fix-violations"></a>如何解决冲突
 从类型名称中删除后缀。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 除非后缀在应用程序域中具有明确的含义，否则不要禁止显示来自此规则的警告。

## <a name="related-rules"></a>相关规则
 [CA1710:标识符应具有正确的后缀](../code-quality/ca1710-identifiers-should-have-correct-suffix.md)

## <a name="see-also"></a>另请参阅
 [特性](https://msdn.microsoft.com/library/ee0038ef-b247-4747-a650-3c5c5cd58d8b)[笔尖：事件和委托](https://msdn.microsoft.com/d98fd58b-fa4f-4598-8378-addf4355a115)
