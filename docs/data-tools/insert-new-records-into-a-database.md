---
title: 将新记录插入数据库
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- TableAdapters, inserting new records into
- data [Visual Studio], saving
- databases, inserting new records into
- records, inserting
- saving data
ms.assetid: ea118fff-69b1-4675-b79a-e33374377f04
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: b703d3ccc6ffbd5e2449a1768071b930f606f37f
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85281989"
---
# <a name="insert-new-records-into-a-database"></a>将新记录插入数据库

若要将新记录插入到数据库中，可以使用 `TableAdapter.Update` 方法或 TableAdapter 的 DBDirect 方法之一（具体 `TableAdapter.Insert` 方法为方法）。 有关详细信息，请参阅[TableAdapter](../data-tools/create-and-configure-tableadapters.md)。

如果你的应用程序不使用 Tableadapter，则可以使用命令对象（例如 <xref:System.Data.SqlClient.SqlCommand> ）在数据库中插入新记录。

如果你的应用程序使用数据集存储数据，请使用 `TableAdapter.Update` 方法。 `Update`方法将所有更改（更新、插入和删除）发送到数据库。

如果你的应用程序使用对象存储数据，或如果你想要更好地控制在数据库中创建新记录，请使用 `TableAdapter.Insert` 方法。

如果 TableAdapter 没有 `Insert` 方法，这意味着 tableadapter 配置为使用存储过程，或者其 `GenerateDBDirectMethods` 属性设置为 `false` 。 尝试在数据集设计器中将 TableAdapter 的 `GenerateDBDirectMethods` 属性设置为 `true` ，然后保存该数据集。 **Dataset Designer** 这将重新生成 TableAdapter。 如果 TableAdapter 仍没有 `Insert` 方法，则表可能没有提供足够的架构信息来区分各个行（例如，表上可能没有设置主键）。

## <a name="insert-new-records-by-using-tableadapters"></a>使用 Tableadapter 插入新记录

Tableadapter 提供了不同的方法将新记录插入数据库中，具体取决于应用程序的要求。

如果你的应用程序使用数据集存储数据，则只需在数据集中的所需添加新记录， <xref:System.Data.DataTable> 然后调用 `TableAdapter.Update` 方法。 `TableAdapter.Update`方法将中的任何更改发送 <xref:System.Data.DataTable> 到数据库（包括已修改和已删除的记录）。

### <a name="to-insert-new-records-into-a-database-by-using-the-tableadapterupdate-method"></a>使用 TableAdapter 方法将新记录插入到数据库中

1. <xref:System.Data.DataTable>通过创建新的 <xref:System.Data.DataRow> 并将其添加到集合中，将新记录添加到所需的 <xref:System.Data.DataTable.Rows%2A> 。

2. 将新行添加到后 <xref:System.Data.DataTable> ，调用 `TableAdapter.Update` 方法。 可以通过传入整个 <xref:System.Data.DataSet> 、 <xref:System.Data.DataTable> 、、数组 <xref:System.Data.DataRow> 或单个来控制要更新的数据量 <xref:System.Data.DataRow> 。

   下面的代码演示如何向添加新记录 <xref:System.Data.DataTable> ，然后调用 `TableAdapter.Update` 方法将新行保存到数据库。 （此示例使用 `Region` Northwind 数据库中的表。）

   [!code-vb[VbRaddataSaving#14](../data-tools/codesnippet/VisualBasic/insert-new-records-into-a-database_1.vb)]
   [!code-csharp[VbRaddataSaving#14](../data-tools/codesnippet/CSharp/insert-new-records-into-a-database_1.cs)]

### <a name="to-insert-new-records-into-a-database-by-using-the-tableadapterinsert-method"></a>使用 TableAdapter 方法将新记录插入到数据库中

如果你的应用程序使用对象存储数据，则可以使用 `TableAdapter.Insert` 方法直接在数据库中创建新行。 `Insert`方法接受每个列的各个值作为参数。 调用方法会使用传入的参数值向数据库中插入一条新记录。

- 调用 TableAdapter 的 `Insert` 方法，并传入每个列的值作为参数。

下面的过程演示如何使用 `TableAdapter.Insert` 方法插入行。 此示例将数据插入 `Region` Northwind 数据库的表中。

> [!NOTE]
> 如果没有可用的实例，请实例化要使用的 TableAdapter。

[!code-vb[VbRaddataSaving#15](../data-tools/codesnippet/VisualBasic/insert-new-records-into-a-database_2.vb)]
[!code-csharp[VbRaddataSaving#15](../data-tools/codesnippet/CSharp/insert-new-records-into-a-database_2.cs)]

## <a name="insert-new-records-by-using-command-objects"></a>使用命令对象插入新记录

您可以使用命令对象直接将新记录插入到数据库中。

### <a name="to-insert-new-records-into-a-database-by-using-command-objects"></a>使用命令对象将新记录插入到数据库中

- 创建新的命令对象，并设置其 `Connection` 、 `CommandType` 和 `CommandText` 属性。

下面的示例演示如何使用 command 对象将记录插入到数据库中。 它将数据插入 `Region` Northwind 数据库的表中。

[!code-vb[VbRaddataSaving#16](../data-tools/codesnippet/VisualBasic/insert-new-records-into-a-database_3.vb)]
[!code-csharp[VbRaddataSaving#16](../data-tools/codesnippet/CSharp/insert-new-records-into-a-database_3.cs)]

## <a name="net-security"></a>.NET 安全性

您必须具有对您尝试连接到的数据库的访问权限，以及在所需的表中执行插入的权限。

## <a name="see-also"></a>另请参阅

- [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)
