---
title: 将新记录插入数据库
ms.date: 11/04/2016
ms.topic: conceptual
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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 64fc4735fd95c611dd1c2d905be6fa5b45c84664
ms.sourcegitcommit: 5483e399f14fb01f528b3b194474778fd6f59fa6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66715017"
---
# <a name="insert-new-records-into-a-database"></a>将新记录插入数据库

若要向数据库中插入新记录，可以使用`TableAdapter.Update`方法，或 TableAdapter 的 DBDirect 方法之一 (具体而言`TableAdapter.Insert`方法)。 有关详细信息，请参阅[TableAdapter](../data-tools/create-and-configure-tableadapters.md)。

如果你的应用程序不使用 Tableadapter，可以使用命令对象 (例如， <xref:System.Data.SqlClient.SqlCommand>) 若要将新记录插入数据库中。

如果你的应用程序使用数据集来存储数据，使用`TableAdapter.Update`方法。 `Update`方法向数据库发送所有更改 （更新、 插入和删除）。

如果你的应用程序使用对象来存储数据，或如果想要更好地控制在数据库中，创建新记录使用`TableAdapter.Insert`方法。

如果没有在 TableAdapter`Insert`方法，它表示任一 TableAdapter 配置为使用存储的过程或其`GenerateDBDirectMethods`属性设置为`false`。 尝试设置的 TableAdapter`GenerateDBDirectMethods`属性设置为`true`内**数据集设计器**，然后将保存数据集。 这将再生成 TableAdapter。 如果仍不具有 TableAdapter`Insert`方法，表可能不提供足够的架构信息来区分各行 （例如，有可能在表上的没有主密钥集）。

## <a name="insert-new-records-by-using-tableadapters"></a>使用 Tableadapter 插入新记录

Tableadapter 提供不同的方式将新记录插入数据库，具体取决于你的应用程序的要求。

如果你的应用程序使用数据集来存储数据，只可以向所需添加新记录<xref:System.Data.DataTable>数据集，，然后调用`TableAdapter.Update`方法。 `TableAdapter.Update`方法发送的任何更改<xref:System.Data.DataTable>到数据库 （包括已修改和删除记录）。

### <a name="to-insert-new-records-into-a-database-by-using-the-tableadapterupdate-method"></a>若要使用 TableAdapter.Update 方法将新记录插入数据库

1. 将新记录添加到所需<xref:System.Data.DataTable>通过创建一个新<xref:System.Data.DataRow>并将其添加到<xref:System.Data.DataTable.Rows%2A>集合。

2. 新行添加到后<xref:System.Data.DataTable>，调用`TableAdapter.Update`方法。 您可以控制要更新通过传入一个完整的数据量<xref:System.Data.DataSet>、 一个<xref:System.Data.DataTable>，数组<xref:System.Data.DataRow>s 或将单个<xref:System.Data.DataRow>。

   下面的代码演示如何添加到新的记录<xref:System.Data.DataTable>，然后调用`TableAdapter.Update`方法以将新行保存到数据库。 (此示例使用`Region`Northwind 数据库中的表。)

   [!code-vb[VbRaddataSaving#14](../data-tools/codesnippet/VisualBasic/insert-new-records-into-a-database_1.vb)]
   [!code-csharp[VbRaddataSaving#14](../data-tools/codesnippet/CSharp/insert-new-records-into-a-database_1.cs)]

### <a name="to-insert-new-records-into-a-database-by-using-the-tableadapterinsert-method"></a>若要使用 TableAdapter.Insert 方法将新记录插入数据库

如果你的应用程序使用对象来存储数据，则可以使用`TableAdapter.Insert`方法直接在数据库中创建新行。 `Insert`方法接受单个值的每个列作为参数。 调用该方法将一条新记录插入数据库中传递的参数值。

- 调用 TableAdapter 的`Insert`方法，在值中的每个列将作为参数传递。

以下过程演示如何使用`TableAdapter.Insert`方法来插入行。 此示例将数据插入`Region`Northwind 数据库中的表。

> [!NOTE]
> 如果没有可用的实例，实例化想要使用的 TableAdapter。

[!code-vb[VbRaddataSaving#15](../data-tools/codesnippet/VisualBasic/insert-new-records-into-a-database_2.vb)]
[!code-csharp[VbRaddataSaving#15](../data-tools/codesnippet/CSharp/insert-new-records-into-a-database_2.cs)]

## <a name="insert-new-records-by-using-command-objects"></a>使用命令对象将插入新记录

您可以插入新记录直接使用命令对象的数据库。

### <a name="to-insert-new-records-into-a-database-by-using-command-objects"></a>若要使用命令对象将新记录插入数据库

- 创建新的命令对象，并设置其`Connection`， `CommandType`，和`CommandText`属性。

下面的示例演示使用命令对象的数据库到插入记录。 它将数据插入`Region`Northwind 数据库中的表。

[!code-vb[VbRaddataSaving#16](../data-tools/codesnippet/VisualBasic/insert-new-records-into-a-database_3.vb)]
[!code-csharp[VbRaddataSaving#16](../data-tools/codesnippet/CSharp/insert-new-records-into-a-database_3.cs)]

## <a name="net-security"></a>.NET 安全性

必须有权访问尝试连接到数据库以及执行插入到所需的表的权限。

## <a name="see-also"></a>请参阅

- [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)