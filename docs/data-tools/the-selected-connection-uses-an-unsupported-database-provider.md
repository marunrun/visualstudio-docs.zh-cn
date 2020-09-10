---
title: 不支持的数据库提供程序
description: 所选连接使用不支持的数据库提供程序
ms.date: 11/04/2016
ms.topic: error-reference
ms.assetid: 4d25dfa1-8fa4-4529-9b90-973bc2ec2993
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 9ff4120796a40da00e258026d8db84ba6e9dbb21
ms.sourcegitcommit: 2a201c93ed526b0f7e5848657500f1111b08ac2a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/10/2020
ms.locfileid: "89743263"
---
# <a name="the-selected-connection-uses-an-unsupported-database-provider"></a>所选连接使用不支持的数据库提供程序

当你将不使用 .NET Framework 数据提供程序的项从 **服务器资源管理器** 或 **数据库资源管理器** 中的 SQL Server 拖到 [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)时，将显示此消息。

**O/R 设计器**仅支持使用 SQL Server 的 .NET Framework 提供程序的数据连接。 只有指向 Microsoft SQL Server 或 Microsoft SQL Server 数据库文件的连接才有效。

若要更正此错误，只需将使用 .NET Framework 数据提供程序 SQL Server 的数据连接中的项添加到 **O/R 设计器**中。

## <a name="see-also"></a>请参阅

- <xref:System.Data.SqlClient>
- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
