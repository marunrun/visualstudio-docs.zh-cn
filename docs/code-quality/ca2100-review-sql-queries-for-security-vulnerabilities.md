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
ms.openlocfilehash: b3ba92e154e3091f6ec483ba469c3fe60f50ec61
ms.sourcegitcommit: 5483e399f14fb01f528b3b194474778fd6f59fa6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66744808"
---
# <a name="ca2100-review-sql-queries-for-security-vulnerabilities"></a>CA2100:检查 SQL 查询是否存在安全漏洞

|||
|-|-|
|TypeName|ReviewSqlQueriesForSecurityVulnerabilities|
|CheckId|CA2100|
|类别|Microsoft.Security|
|是否重大更改|非换行|

## <a name="cause"></a>原因

一种方法设置<xref:System.Data.IDbCommand.CommandText%2A?displayProperty=fullName>属性使用的方法生成的字符串参数的字符串。

## <a name="rule-description"></a>规则说明

此规则假定字符串参数中包含用户输入。 基于用户输入生成的 SQL 命令字符串易于受到 SQL 注入式攻击。 在 SQL 注入攻击，恶意用户提供输入，在尝试损坏或未经授权地访问基础数据库中更改查询的设计。 典型的方法包括注入的单个引号或撇号，这是 SQL 文本字符串分隔符;表示 SQL 注释; 的两个短划线并使用分号，这表示，新的命令如下所示。 如果用户输入必须是使用以下命令，其中一个查询的一部分的顺序列出的效率，以降低攻击风险。

- 使用存储的过程。

- 使用参数化的命令字符串。

- 验证类型和内容的用户输入，然后构建命令字符串。

以下.NET 类型实现<xref:System.Data.IDbCommand.CommandText%2A>属性或提供通过使用字符串自变量来设置属性的构造函数。

- <xref:System.Data.Odbc.OdbcCommand?displayProperty=fullName> 和 <xref:System.Data.Odbc.OdbcDataAdapter?displayProperty=fullName>

- <xref:System.Data.OleDb.OleDbCommand?displayProperty=fullName> 和 <xref:System.Data.OleDb.OleDbDataAdapter?displayProperty=fullName>

- <xref:System.Data.OracleClient.OracleCommand?displayProperty=fullName> 和 <xref:System.Data.OracleClient.OracleDataAdapter?displayProperty=fullName>

- <xref:System.Data.SqlClient.SqlCommand?displayProperty=fullName> 和 <xref:System.Data.SqlClient.SqlDataAdapter?displayProperty=fullName>

请注意，此规则冲突时显式或隐式使用 ToString 方法的类型来构造查询字符串。 下面是一个示例。

```csharp
int x = 10;
string query = "SELECT TOP " + x.ToString() + " FROM Table";
```

因为恶意用户可以重写 tostring （） 方法违反该规则。

隐式使用 ToString 时也被违反该规则。

```csharp
int x = 10;
string query = String.Format("SELECT TOP {0} FROM Table", x);
```

## <a name="how-to-fix-violations"></a>如何解决冲突

若要修复此规则的冲突，请使用参数化的查询。

## <a name="when-to-suppress-warnings"></a>何时禁止显示警告

它可以安全地禁止显示此规则的警告，如果命令文本不包含任何用户输入。

## <a name="example"></a>示例

下面的示例演示一种方法， `UnsafeQuery`，这违反了规则和方法， `SaferQuery`，满足该规则使用参数化的命令字符串。

[!code-vb[FxCop.Security.ReviewSqlQueries#1](../code-quality/codesnippet/VisualBasic/ca2100-review-sql-queries-for-security-vulnerabilities_1.vb)]
[!code-csharp[FxCop.Security.ReviewSqlQueries#1](../code-quality/codesnippet/CSharp/ca2100-review-sql-queries-for-security-vulnerabilities_1.cs)]
[!code-cpp[FxCop.Security.ReviewSqlQueries#1](../code-quality/codesnippet/CPP/ca2100-review-sql-queries-for-security-vulnerabilities_1.cpp)]

## <a name="see-also"></a>请参阅

- [安全性概述](/dotnet/framework/data/adonet/security-overview)