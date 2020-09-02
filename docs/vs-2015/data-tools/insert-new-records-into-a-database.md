---
title: 在数据库中插入新记录 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- TableAdapters, inserting new records into
- data [Visual Studio], saving
- databases, inserting new records into
- records, inserting
- saving data
ms.assetid: ea118fff-69b1-4675-b79a-e33374377f04
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3c686a764f42f50a3e59da3e8b37b219ddb7b11c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72651564"
---
# <a name="insert-new-records-into-a-database"></a>将新记录插入数据库
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

若要将新记录插入到数据库中，可以使用 `TableAdapter.Update` 方法，或者使用 TableAdapter 的 DBDirect 方法之一 (具体 `TableAdapter.Insert` 方法) 。

 如果你的应用程序不使用 Tableadapter，则可以使用命令对象 (例如，  <xref:System.Data.SqlClient.SqlCommand>) 在数据库中插入新记录。

 如果你的应用程序使用数据集存储数据，请使用 `TableAdapter.Update` 方法。 `Update`方法将 (更新、插入和删除) 的所有更改发送到数据库。

 如果你的应用程序使用对象存储数据，或如果你想要更好地控制在数据库中创建新记录，请使用 `TableAdapter.Insert` 方法。

 如果 TableAdapter 没有 `Insert` 方法，这意味着 tableadapter 配置为使用存储过程，或者其 `GenerateDBDirectMethods` 属性设置为 `false` 。 尝试在数据集设计器中将 TableAdapter 的 `GenerateDBDirectMethods` 属性设置为 `true` ，然后保存该数据集。 这将重新生成 TableAdapter。 如果 TableAdapter 仍没有 `Insert` 方法，则表可能没有提供足够的架构信息来区分单个行 (例如，表中可能没有设置) 的主键。

## <a name="insert-new-records-by-using-tableadapters"></a>使用 Tableadapter 插入新记录
 Tableadapter 提供了不同的方法将新记录插入数据库中，具体取决于应用程序的要求。

 如果你的应用程序使用数据集存储数据，则只需在数据集中的所需添加新记录 <xref:System.Data.DataTable> ，然后调用 `TableAdapter.Update` 方法。 `TableAdapter.Update`方法将中的任何更改发送 <xref:System.Data.DataTable> 到数据库 (包括) 修改和删除记录。

#### <a name="to-insert-new-records-into-a-database-by-using-the-tableadapterupdate-method"></a>使用 TableAdapter 方法将新记录插入到数据库中

1. <xref:System.Data.DataTable>通过创建新的 <xref:System.Data.DataRow> 并将其添加到集合中，将新记录添加到所需的 <xref:System.Data.DataTable.Rows%2A> 。 有关详细信息，请参阅 [如何：将行添加到 DataTable](https://msdn.microsoft.com/library/78ebbb43-c402-49cf-81da-0715289487bf)。

2. 将新行添加到后 <xref:System.Data.DataTable> ，调用 `TableAdapter.Update` 方法。 可以通过传入整个 <xref:System.Data.DataSet> 、 <xref:System.Data.DataTable> 、、数组 <xref:System.Data.DataRow> 或单个来控制要更新的数据量 <xref:System.Data.DataRow> 。

    下面的代码演示如何向添加新记录 <xref:System.Data.DataTable> ，然后调用 `TableAdapter.Update` 方法将新行保存到数据库。  (此示例使用 `Region` Northwind 数据库中的表。 ) 

    [!code-csharp[VbRaddataSaving#14](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form5.cs#14)]
    [!code-vb[VbRaddataSaving#14](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form5.vb#14)]

   如果你的应用程序使用对象存储数据，则可以使用 `TableAdapter.Insert` 方法直接在数据库中创建新行。 `Insert`方法接受每个列的各个值作为参数。 调用方法会使用传入的参数值向数据库中插入一条新记录。

   下面的过程使用 `Region` Northwind 数据库中的表作为示例。

#### <a name="to-insert-new-records-into-a-database-by-using-the-tableadapterinsert-method"></a>使用 TableAdapter 方法将新记录插入到数据库中

- 调用 TableAdapter 的 `Insert` 方法，并传入每个列的值作为参数。

    > [!NOTE]
    > 如果没有可用的实例，请实例化要使用的 TableAdapter。

     [!code-csharp[VbRaddataSaving#15](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs#15)]
     [!code-vb[VbRaddataSaving#15](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb#15)]

## <a name="insert-new-records-by-using-command-objects"></a>使用命令对象插入新记录
 下面的示例使用命令对象将新记录直接插入到数据库中。

 下面的过程使用 `Region` Northwind 数据库中的表作为示例。

#### <a name="to-insert-new-records-into-a-database-by-using-command-objects"></a>使用命令对象将新记录插入到数据库中

- 创建新的命令对象，并设置其 `Connection` 、 `CommandType` 和 `CommandText` 属性。

     [!code-csharp[VbRaddataSaving#16](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs#16)]
     [!code-vb[VbRaddataSaving#16](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb#16)]

## <a name="net-framework-security"></a>.NET Framework 安全性
 您必须具有对您尝试连接到的数据库的访问权限，以及在所需的表中执行插入的权限。

## <a name="see-also"></a>另请参阅
 [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)
