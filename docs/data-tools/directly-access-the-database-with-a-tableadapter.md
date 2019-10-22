---
title: 使用 TableAdapter 直接访问数据库
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
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
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: e8d5d8e3091b464084df065bb7b889db9fc2194f
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72648514"
---
# <a name="directly-access-the-database-with-a-tableadapter"></a>使用 TableAdapter 直接访问数据库

除了 `InsertCommand`、`UpdateCommand` 和 `DeleteCommand` 外，还会创建 Tableadapter，它具有可直接针对数据库运行的方法。 您可以调用这些方法（`TableAdapter.Insert`、`TableAdapter.Update` 和 `TableAdapter.Delete`）直接操作数据库中的数据。

如果不想创建这些直接方法，请在 "**属性**" 窗口中将 TableAdapter 的 `GenerateDbDirectMethods` 属性设置为 "`false`"。 如果除 TableAdapter 的主查询外，还会将任何查询添加到 TableAdapter，它们是不生成这些 `DbDirect` 方法的独立查询。

## <a name="send-commands-directly-to-a-database"></a>将命令直接发送到数据库

调用 TableAdapter `DbDirect` 执行正在尝试完成的任务的方法。

### <a name="to-insert-new-records-directly-into-a-database"></a>直接在数据库中插入新记录

- 调用 TableAdapter 的 `Insert` 方法，并传入每个列的值作为参数。 下面的过程使用 Northwind 数据库中的 `Region` 表作为示例。

    > [!NOTE]
    > 如果没有可用的实例，请实例化要使用的 TableAdapter。

     [!code-vb[VbRaddataSaving#15](../data-tools/codesnippet/VisualBasic/directly-access-the-database-with-a-tableadapter_1.vb)]
     [!code-csharp[VbRaddataSaving#15](../data-tools/codesnippet/CSharp/directly-access-the-database-with-a-tableadapter_1.cs)]

### <a name="to-update-records-directly-in-a-database"></a>直接在数据库中更新记录

- 调用 TableAdapter 的 `Update` 方法，并传入每个列的新值和原始值作为参数。

    > [!NOTE]
    > 如果没有可用的实例，请实例化要使用的 TableAdapter。

     [!code-vb[VbRaddataSaving#18](../data-tools/codesnippet/VisualBasic/directly-access-the-database-with-a-tableadapter_2.vb)]
     [!code-csharp[VbRaddataSaving#18](../data-tools/codesnippet/CSharp/directly-access-the-database-with-a-tableadapter_2.cs)]

### <a name="to-delete-records-directly-from-a-database"></a>直接从数据库中删除记录

- 调用 TableAdapter 的 `Delete` 方法，并传入每个列的值作为 `Delete` 方法的参数。 下面的过程使用 Northwind 数据库中的 `Region` 表作为示例。

    > [!NOTE]
    > 如果没有可用的实例，请实例化要使用的 TableAdapter。

     [!code-vb[VbRaddataSaving#21](../data-tools/codesnippet/VisualBasic/directly-access-the-database-with-a-tableadapter_3.vb)]
     [!code-csharp[VbRaddataSaving#21](../data-tools/codesnippet/CSharp/directly-access-the-database-with-a-tableadapter_3.cs)]

## <a name="see-also"></a>请参阅

- [使用 Tableadapter 填充数据集](../data-tools/fill-datasets-by-using-tableadapters.md)