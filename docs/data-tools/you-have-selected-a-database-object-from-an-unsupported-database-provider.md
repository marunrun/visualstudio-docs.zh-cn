---
title: 您从不支持的数据库提供程序选择了数据库对象
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: c0f1298e-31aa-471e-ae19-1bafffd2ae40
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: b1dd14c428b90b87e665aa41681b5a9e68eb00e5
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72648012"
---
# <a name="you-have-selected-a-database-object-from-an-unsupported-database-provider"></a>您从不支持的数据库提供程序选择了数据库对象

**O/R 设计器**仅支持 SQL Server 的 .NET Framework 数据提供程序（<xref:System.Data.SqlClient>）。 虽然可以单击“确定”并继续使用来自不支持的数据库提供程序的对象，但在运行时可能遇到意外行为。

> [!NOTE]
> 仅支持使用用于 SQL Server 的 .NET Framework 数据提供程序的数据连接。

## <a name="options"></a>选项

- 单击“确定”，继续设计映射到使用不受支持数据库提供程序的连接的实体类。 使用不支持的数据库提供程序时，可能遇到意外行为。

- 单击 "**取消**" 以停止此操作。 创建或使用用于 SQL Server 的 .NET Framework 提供程序的其他数据连接。

## <a name="see-also"></a>请参阅

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)