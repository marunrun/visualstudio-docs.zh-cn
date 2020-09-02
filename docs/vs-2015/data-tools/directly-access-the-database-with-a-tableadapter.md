---
title: 使用 TableAdapter 直接访问数据库 |Microsoft Docs
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
- databases [Visual Basic], accessing with a TableAdapter
- DBDirect methods
- datasets [Visual Basic], adding to projects
- data [Visual Studio], saving
- TableAdapter.Delete method
- GenerateDbDirectMethods property
- TableAdapter.Insert method
- TableAdapter.GenerateDBDirectMethods property
- TableAdapter.Update method
- saving data
- TableAdapters
ms.assetid: 012c5924-91f7-4790-b2a6-f51402b7014b
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 58500e59a624dac55824033b8b9667754a9040c5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72657364"
---
# <a name="directly-access-the-database-with-a-tableadapter"></a>使用 TableAdapter 直接访问数据库
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

除了 `InsertCommand` 、和外，还会 `UpdateCommand` `DeleteCommand` 创建可直接针对数据库运行的 tableadapter 的方法。 这些方法 (`TableAdapter.Insert` 、 `TableAdapter.Update` 和 `TableAdapter.Delete`) 可以直接在数据库中处理数据。

 如果不想创建这些直接方法，请 `GenerateDbDirectMethods` `false` 在 " **属性** " 窗口中将 TableAdapter 的属性设置为。 如果除 TableAdapter 的主查询外，还会将任何查询添加到 TableAdapter，它们是不生成这些 DbDirect 方法的独立查询。

## <a name="sendcommandsdirectly-to-a-database"></a>Sendcommandsdirectly 到数据库
 调用用于执行正在尝试完成的任务的 TableAdapter DbDirect 方法。

#### <a name="to-insert-new-records-directly-into-a-database"></a>直接在数据库中插入新记录

- 调用 TableAdapter 的 `Insert` 方法，并传入每个列的值作为参数。 下面的过程使用 `Region` Northwind databaseas 中的表。

    > [!NOTE]
    > 如果没有可用的实例，请实例化要使用的 TableAdapter。

     [!code-csharp[VbRaddataSaving#15](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs#15)]
     [!code-vb[VbRaddataSaving#15](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb#15)]

#### <a name="to-update-records-directly-in-a-database"></a>直接在数据库中更新记录

- 调用 TableAdapter 的 `Update` 方法，并传入每个列的新值和原始值作为参数。

    > [!NOTE]
    > 如果没有可用的实例，请实例化要使用的 TableAdapter。

     [!code-csharp[VbRaddataSaving#18](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs#18)]
     [!code-vb[VbRaddataSaving#18](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb#18)]

#### <a name="to-delete-records-directly-from-a-database"></a>直接从数据库中删除记录

- 调用 TableAdapter 的 `Delete` 方法，并传入每个列的值作为方法的参数 `Delete` 。 下面的过程使用 `Region` Northwind databaseas 中的表。

    > [!NOTE]
    > 如果没有可用的实例，请实例化要使用的 TableAdapter。

     [!code-csharp[VbRaddataSaving#21](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Class1.cs#21)]
     [!code-vb[VbRaddataSaving#21](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Class1.vb#21)]

## <a name="see-also"></a>另请参阅
 [使用 Tableadapter 填充数据集](../data-tools/fill-datasets-by-using-tableadapters.md)
