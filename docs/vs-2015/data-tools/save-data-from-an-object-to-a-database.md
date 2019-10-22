---
title: 将对象中的数据保存到数据库 |Microsoft Docs
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
- data [Visual Studio], saving
- data access [Visual Studio], objects
- saving data
ms.assetid: efd6135a-40cf-4b0d-8f8b-41a5aaea7057
caps.latest.revision: 12
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 6c1470c831177e74e7670d696b44fc2b0119a9a9
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72607458"
---
# <a name="save-data-from-an-object-to-a-database"></a>将数据从对象保存到数据库
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以通过将对象中的值传递给 TableAdapter 的 DBDirect 方法之一（例如 `TableAdapter.Insert`），将对象中的数据保存到数据库。

 若要保存对象集合中的数据，请遍历对象的集合（例如，next 循环），并使用 TableAdapter 的 DBDirect 方法之一将每个对象的值发送到数据库。

 默认情况下，DBDirect 方法是在可以直接对数据库运行的 TableAdapter 上创建的。 可以直接调用这些方法，而不需要 <xref:System.Data.DataSet> 或 <xref:System.Data.DataTable> 对象来协调更改以便将更新发送到数据库。

> [!NOTE]
> 配置 TableAdapter 时，主查询必须提供足够的信息，以便创建 DBDirect 方法。 例如，如果将 TableAdapter 配置为查询未定义主键列的表中的数据，则不会生成 DBDirect 方法。

|TableAdapter DBDirect 方法|描述|
|----------------------------------|-----------------|
|`TableAdapter.Insert`|将新记录添加到数据库，并使您能够作为方法参数传入单独的列值。|
|`TableAdapter.Update`|更新数据库中的现有记录。 @No__t_0 方法将原始列值和新列值作为方法参数使用。 原始值用于查找原始记录，新值用于更新该记录。<br /><br /> @No__t_0 方法还用于通过将 <xref:System.Data.DataSet>、<xref:System.Data.DataTable>、<xref:System.Data.DataRow> 或 <xref:System.Data.DataRow>s 的数组作为方法参数来协调数据集中的更改。|
|`TableAdapter.Delete`|基于作为方法参数传入的原始列值删除数据库中的现有记录。|

### <a name="to-save-new-records-from-an-object-to-a-database"></a>将新记录从对象保存到数据库

- 通过将值传递给 `TableAdapter.Insert` 方法来创建记录。

     下面的示例通过将 `currentCustomer` 对象中的值传递给 `TableAdapter.Insert` 方法，在 `Customers` 表中创建新的客户记录。

     [!code-csharp[VbRaddataSaving#23](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form3.cs#23)]
     [!code-vb[VbRaddataSaving#23](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form3.vb#23)]

### <a name="to-update-existing-records-from-an-object-to-a-database"></a>将对象中的现有记录更新到数据库

- 通过调用 `TableAdapter.Update` 方法修改记录，并传入新值以更新记录，并传入原始值以定位记录。

    > [!NOTE]
    > 对象需要维护原始值才能将其传递到 `Update` 方法。 此示例使用具有 `orig` 前缀的属性存储原始值。

     下面的示例通过将 `Customer` 对象中的新值和原始值传递到 `TableAdapter.Update` 方法来更新 `Customers` 表中的现有记录。

     [!code-csharp[VbRaddataSaving#24](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form3.cs#24)]
     [!code-vb[VbRaddataSaving#24](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form3.vb#24)]

### <a name="to-delete-existing-records-from-a-database"></a>删除数据库中的现有记录

- 通过调用 `TableAdapter.Delete` 方法，并传入原始值以定位记录，删除记录。

    > [!NOTE]
    > 对象需要维护原始值才能将其传递到 `Delete` 方法。 此示例使用具有 `orig` 前缀的属性存储原始值。

     下面的示例通过将 `Customer` 对象中的原始值传递到 `TableAdapter.Delete` 方法，从 `Customers` 表中删除一条记录。

     [!code-csharp[VbRaddataSaving#25](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form3.cs#25)]
     [!code-vb[VbRaddataSaving#25](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form3.vb#25)]

## <a name="net-framework-security"></a>.NET Framework 安全性
 您必须有权在数据库中的表上执行所选的 INSERT、UPDATE 或 DELETE。

## <a name="see-also"></a>请参阅
 [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)
