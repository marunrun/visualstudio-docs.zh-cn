---
title: 将数据从对象保存到数据库
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Visual Studio], saving
- data access [Visual Studio], objects
- saving data
ms.assetid: efd6135a-40cf-4b0d-8f8b-41a5aaea7057
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: b15776b67ded2fc813f1b8bcf82d8aa91f212346
ms.sourcegitcommit: 5483e399f14fb01f528b3b194474778fd6f59fa6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66715027"
---
# <a name="save-data-from-an-object-to-a-database"></a>将数据从对象保存到数据库

可以在将值从您的对象传递到 TableAdapter 的 DBDirect 方法之一将数据保存到数据库的对象中 (例如， `TableAdapter.Insert`)。 有关详细信息，请参阅[TableAdapter](../data-tools/create-and-configure-tableadapters.md)。

若要保存数据的对象的集合，请循环遍历对象 （例如下, 一步的循环） 的集合，并使用 TableAdapter 的之一将每个对象的值发送到数据库`DBDirect`方法。

默认情况下，`DBDirect`方法创建可以直接对数据库运行 TableAdapter 上。 这些方法可以直接调用，并且不需要<xref:System.Data.DataSet>或<xref:System.Data.DataTable>对象来协调更改即可将更新发送到数据库。

> [!NOTE]
> 在配置 TableAdapter 时，主查询必须提供足够的信息供`DBDirect`方法来创建。 例如，如果 TableAdapter 查询的数据配置不具有定义的主键列的表中，它不会生成`DBDirect`方法。

|TableAdapter DBDirect 方法|描述|
| - |-----------------|
|`TableAdapter.Insert`|将新记录添加到数据库并使您能够在各列的值作为方法参数中传递。|
|`TableAdapter.Update`|更新现有数据库中的记录。 `Update`方法采用原始的和新列作为方法参数的值。 用于查找的原始记录的原始值和新值用于更新该记录。<br /><br /> `TableAdapter.Update`方法还用于协调回数据库的数据集的更改，通过采用<xref:System.Data.DataSet>， <xref:System.Data.DataTable>， <xref:System.Data.DataRow>，或数组<xref:System.Data.DataRow>的方法参数。|
|`TableAdapter.Delete`|删除现有的基于原始列值作为方法参数传入数据库中的记录。|

## <a name="to-save-new-records-from-an-object-to-a-database"></a>若要将新记录从对象保存到数据库

- 将值传递给创建的记录`TableAdapter.Insert`方法。

     下面的示例创建新的客户记录中`Customers`表中的值传递`currentCustomer`对象传递给`TableAdapter.Insert`方法。

     [!code-csharp[VbRaddataSaving#23](../data-tools/codesnippet/CSharp/save-data-from-an-object-to-a-database_1.cs)]
     [!code-vb[VbRaddataSaving#23](../data-tools/codesnippet/VisualBasic/save-data-from-an-object-to-a-database_1.vb)]

## <a name="to-update-existing-records-from-an-object-to-a-database"></a>若要更新现有记录从对象到数据库

- 通过调用修改记录`TableAdapter.Update`方法，传入新值更新记录，并传入要找到的记录的原始值。

    > [!NOTE]
    > 您的对象需要维护的原始值，以便将它们传递给`Update`方法。 此示例使用属性与`orig`前缀来存储原始值。

     下面的示例更新中的现有记录`Customers`表中的新的和原始值传递`Customer`对象传递给`TableAdapter.Update`方法。

     [!code-csharp[VbRaddataSaving#24](../data-tools/codesnippet/CSharp/save-data-from-an-object-to-a-database_2.cs)]
     [!code-vb[VbRaddataSaving#24](../data-tools/codesnippet/VisualBasic/save-data-from-an-object-to-a-database_2.vb)]

## <a name="to-delete-existing-records-from-a-database"></a>若要从数据库中删除现有记录

- 通过调用删除记录`TableAdapter.Delete`方法并传入要找到的记录的原始值。

    > [!NOTE]
    > 您的对象需要维护的原始值，以便将它们传递给`Delete`方法。 此示例使用属性与`orig`前缀来存储原始值。

     以下示例将删除来自`Customers`表中的原始值表示通过`Customer`对象传递给`TableAdapter.Delete`方法。

     [!code-csharp[VbRaddataSaving#25](../data-tools/codesnippet/CSharp/save-data-from-an-object-to-a-database_3.cs)]
     [!code-vb[VbRaddataSaving#25](../data-tools/codesnippet/VisualBasic/save-data-from-an-object-to-a-database_3.vb)]

## <a name="net-security"></a>.NET 安全性

您必须有权执行所选`INSERT`， `UPDATE`，或`DELETE`上数据库中的表。

## <a name="see-also"></a>请参阅

- [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)