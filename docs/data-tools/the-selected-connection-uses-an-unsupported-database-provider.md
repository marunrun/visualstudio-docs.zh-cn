---
title: 所选连接使用不支持的数据库提供程序
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 4d25dfa1-8fa4-4529-9b90-973bc2ec2993
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: ce72f9d4f93db5d4f96bfe54e6cb0d29f4e0727b
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72639971"
---
# <a name="the-selected-connection-uses-an-unsupported-database-provider"></a>所选连接使用不支持的数据库提供程序

当你将不使用 .NET Framework 数据提供程序的项从**服务器资源管理器**或**数据库资源管理器**中的 SQL Server 拖到[Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)时，将显示此消息。

**O/R 设计器**仅支持使用 SQL Server 的 .NET Framework 提供程序的数据连接。 只有指向 Microsoft SQL Server 或 Microsoft SQL Server 数据库文件的连接才有效。

若要更正此错误，只需将使用 .NET Framework 数据提供程序 SQL Server 的数据连接中的项添加到**O/R 设计器**中。

## <a name="see-also"></a>请参阅

- <xref:System.Data.SqlClient>
- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
