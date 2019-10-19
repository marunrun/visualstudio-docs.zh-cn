---
title: CA2100：检查 SQL 查询是否存在安全漏洞 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-code-analysis
ms.topic: reference
f1_keywords:
- Review SQL queries for security vulnerabilities
- ReviewSqlQueriesForSecurityVulnerabilities
- CA2100
helpviewer_keywords:
- CA2100
- ReviewSqlQueriesForSecurityVulnerabilities
ms.assetid: 79670604-c02a-448d-9c0e-7ea0120bc5fe
caps.latest.revision: 26
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: e7258ec98937e7ea84773e788234e5a34772e9d4
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72652199"
---
# <a name="ca2100-review-sql-queries-for-security-vulnerabilities"></a>CA2100：检查 SQL 查询中是否有安全漏洞
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|TypeName|ReviewSqlQueriesForSecurityVulnerabilities|
|CheckId|CA2100|
|类别|Microsoft.Security|
|是否重大更改|不间断|

## <a name="cause"></a>原因
 方法通过使用从字符串参数生成的字符串为方法设置 <xref:System.Data.IDbCommand.CommandText%2A?displayProperty=fullName> 属性。

## <a name="rule-description"></a>规则说明
 此规则假定字符串参数中包含用户输入。 基于用户输入生成的 SQL 命令字符串易于受到 SQL 注入式攻击。 在 SQL 注入式攻击中，恶意用户提供的输入会改变查询的设计，试图破坏或获取对基础数据库的未经授权的访问。 典型方法包括单引号或撇号的注入，这是 SQL 文本字符串分隔符;双短划线，表示 SQL 注释;和一个分号，指示下面的新命令。 如果 "用户输入" 必须是查询的一部分，请使用下列项之一（按有效性顺序列出）来降低遭受攻击的风险。

- 使用存储过程。

- 使用参数化命令字符串。

- 在生成命令字符串之前，验证类型和内容的用户输入。

  以下 [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 类型实现 <xref:System.Data.IDbCommand.CommandText%2A> 属性或提供使用字符串参数设置属性的构造函数。

- <xref:System.Data.Odbc.OdbcCommand?displayProperty=fullName> 和 <xref:System.Data.Odbc.OdbcDataAdapter?displayProperty=fullName>

- <xref:System.Data.OleDb.OleDbCommand?displayProperty=fullName> 和 <xref:System.Data.OleDb.OleDbDataAdapter?displayProperty=fullName>

- <xref:System.Data.OracleClient.OracleCommand?displayProperty=fullName> 和 <xref:System.Data.OracleClient.OracleDataAdapter?displayProperty=fullName>

- [System.data.sqlserverce. SqlCeCommand](<!-- TODO: review code entity reference <xref:assetId:///System.Data.SqlServerCe.SqlCeCommand?qualifyHint=False&amp;autoUpgrade=True>  -->）和 [System.data.sqlserverce. SqlCeDataAdapter] （<!-- TODO: review code entity reference <xref:assetId:///System.Data.SqlServerCe.SqlCeDataAdapter?qualifyHint=False&amp;autoUpgrade=True>  -->)

- <xref:System.Data.SqlClient.SqlCommand?displayProperty=fullName> 和 <xref:System.Data.SqlClient.SqlDataAdapter?displayProperty=fullName>

  请注意，当显式或隐式使用类型的 ToString 方法来构造查询字符串时，将违反此规则。 下面是一个示例。

```
int x = 10;
string query = "SELECT TOP " + x.ToString() + " FROM Table";
```

 违反规则是因为恶意用户可能会重写 ToString （）方法。

 隐式使用 ToString 时也会违反此规则。

```
int x = 10;
string query = String.Format("SELECT TOP {0} FROM Table", x);
```

## <a name="how-to-fix-violations"></a>如何解决冲突
 若要修复与此规则的冲突，请使用参数化查询。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告
 如果命令文本不包含任何用户输入，则可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例
 下面的示例演示了一个方法（`UnsafeQuery`），该方法违反了规则，以及一个方法（`SaferQuery`），该方法通过使用参数化命令字符串满足规则。

 [!code-cpp[FxCop.Security.ReviewSqlQueries#1](../snippets/cpp/VS_Snippets_CodeAnalysis/FxCop.Security.ReviewSqlQueries/cpp/FxCop.Security.ReviewSqlQueries.cpp#1)]
 [!code-csharp[FxCop.Security.ReviewSqlQueries#1](../snippets/csharp/VS_Snippets_CodeAnalysis/FxCop.Security.ReviewSqlQueries/cs/FxCop.Security.ReviewSqlQueries.cs#1)]
 [!code-vb[FxCop.Security.ReviewSqlQueries#1](../snippets/visualbasic/VS_Snippets_CodeAnalysis/FxCop.Security.ReviewSqlQueries/vb/FxCop.Security.ReviewSqlQueries.vb#1)]

## <a name="see-also"></a>请参阅
 [安全性概述](https://msdn.microsoft.com/library/33e09965-61d5-48cc-9e8c-3b047cc4f194)
