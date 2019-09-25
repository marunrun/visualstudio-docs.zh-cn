---
title: CA2100:检查 SQL 查询是否存在安全漏洞
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- Review SQL queries for security vulnerabilities
- ReviewSqlQueriesForSecurityVulnerabilities
- CA2100
helpviewer_keywords:
- CA2100
- ReviewSqlQueriesForSecurityVulnerabilities
ms.assetid: 79670604-c02a-448d-9c0e-7ea0120bc5fe
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- CPP
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 837abb051467135b6332b53b2c59e5016d3adff6
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2019
ms.locfileid: "71233063"
---
# <a name="ca2100-review-sql-queries-for-security-vulnerabilities"></a>CA2100:检查 SQL 查询是否存在安全漏洞

|||
|-|-|
|TypeName|ReviewSqlQueriesForSecurityVulnerabilities|
|CheckId|CA2100|
|类别|Microsoft.Security|
|重大更改|不间断|

## <a name="cause"></a>原因

方法通过使用从<xref:System.Data.IDbCommand.CommandText%2A?displayProperty=fullName>字符串参数生成的字符串为方法设置属性。

## <a name="rule-description"></a>规则说明

此规则假定字符串参数中包含用户输入。 基于用户输入生成的 SQL 命令字符串易于受到 SQL 注入式攻击。 在 SQL 注入式攻击中，恶意用户提供的输入会改变查询的设计，试图破坏或获取对基础数据库的未经授权的访问。 典型方法包括单引号或撇号的注入，这是 SQL 文本字符串分隔符;双短划线，表示 SQL 注释;和一个分号，指示下面的新命令。 如果 "用户输入" 必须是查询的一部分，请使用下列项之一（按有效性顺序列出）来降低遭受攻击的风险。

- 使用存储过程。

- 使用参数化命令字符串。

- 在生成命令字符串之前，验证类型和内容的用户输入。

下面的 .net 类型实现<xref:System.Data.IDbCommand.CommandText%2A>属性，或提供使用字符串参数设置属性的构造函数。

- <xref:System.Data.Odbc.OdbcCommand?displayProperty=fullName> 和 <xref:System.Data.Odbc.OdbcDataAdapter?displayProperty=fullName>

- <xref:System.Data.OleDb.OleDbCommand?displayProperty=fullName> 和 <xref:System.Data.OleDb.OleDbDataAdapter?displayProperty=fullName>

- <xref:System.Data.OracleClient.OracleCommand?displayProperty=fullName> 和 <xref:System.Data.OracleClient.OracleDataAdapter?displayProperty=fullName>

- <xref:System.Data.SqlClient.SqlCommand?displayProperty=fullName> 和 <xref:System.Data.SqlClient.SqlDataAdapter?displayProperty=fullName>

请注意，当显式或隐式使用类型的 ToString 方法来构造查询字符串时，将违反此规则。 下面是一个示例。

```csharp
int x = 10;
string query = "SELECT TOP " + x.ToString() + " FROM Table";
```

违反规则是因为恶意用户可能会重写 ToString （）方法。

隐式使用 ToString 时也会违反此规则。

```csharp
int x = 10;
string query = String.Format("SELECT TOP {0} FROM Table", x);
```

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复与此规则的冲突，请使用参数化查询。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

如果命令文本不包含任何用户输入，则可以安全地禁止显示此规则发出的警告。

## <a name="example"></a>示例

下面的示例演示了一个方法`UnsafeQuery`，该方法违反了规则和一个方法`SaferQuery`，该方法通过使用参数化命令字符串满足规则。

[!code-vb[FxCop.Security.ReviewSqlQueries#1](../code-quality/codesnippet/VisualBasic/ca2100-review-sql-queries-for-security-vulnerabilities_1.vb)]
[!code-csharp[FxCop.Security.ReviewSqlQueries#1](../code-quality/codesnippet/CSharp/ca2100-review-sql-queries-for-security-vulnerabilities_1.cs)]
[!code-cpp[FxCop.Security.ReviewSqlQueries#1](../code-quality/codesnippet/CPP/ca2100-review-sql-queries-for-security-vulnerabilities_1.cpp)]

## <a name="see-also"></a>请参阅

- [安全性概述](/dotnet/framework/data/adonet/security-overview)