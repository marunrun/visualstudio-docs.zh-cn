---
title: 您选择了不受支持的数据库提供程序的数据库对象 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: c0f1298e-31aa-471e-ae19-1bafffd2ae40
caps.latest.revision: 8
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 05a4407eba52ec3940b70ffab220ef354af90e9d
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72657788"
---
# <a name="you-have-selected-a-database-object-from-an-unsupported-database-provider"></a>您从不支持的数据库提供程序选择了数据库对象
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

@No__t_0 （[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]）仅支持用于 SQL Server （<xref:System.Data.SqlClient>）的 .NET Framework 数据提供程序。 虽然可以单击“确定”并继续使用来自不支持的数据库提供程序的对象，但在运行时可能遇到意外行为。

> [!NOTE]
> 仅支持使用用于 SQL Server 的 .NET Framework 数据提供程序的数据连接。

### <a name="to-correct-this-error"></a>更正此错误

- 单击“确定”，继续设计映射到使用不受支持数据库提供程序的连接的实体类。 使用不支持的数据库提供程序时，可能遇到意外行为。

     或

- 单击“取消”。

     操作停止。 创建或使用采用了用于 SQL Server 的 .NET Framework 提供程序的数据连接。

## <a name="see-also"></a>请参阅
 [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md) [LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655) [.NET Framework 数据提供程序](https://msdn.microsoft.com/library/03a9fc62-2d24-491a-9fe6-d6bdb6dcb131)