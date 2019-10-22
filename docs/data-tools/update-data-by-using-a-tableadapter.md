---
title: 使用 TableAdapter 更新数据
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Visual Studio], saving
- data [Visual Studio], TableAdapters
- updating data, TableAdapters
- TableAdapters, updating data
- data [Visual Studio], updating
- saving data
ms.assetid: 5e32e10e-9bac-4969-9bdd-b8f6919d3516
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: b54aeb91ea873b23b1e68731e40542df04fcbd01
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72648114"
---
# <a name="update-data-by-using-a-tableadapter"></a>使用 TableAdapter 更新数据

修改并验证数据集中的数据后，可以通过调用[TableAdapter](../data-tools/create-and-configure-tableadapters.md)的 `Update` 方法，将更新后的数据发回数据库。 @No__t_0 方法根据表中每个数据行的 <xref:System.Data.DataRow.RowState%2A> 更新单个数据表并运行正确的命令（INSERT、UPDATE 或 DELETE）。 当数据集具有相关表时，Visual Studio 将生成用于执行更新的 TableAdapterManager 类。 TableAdapterManager 类确保按在数据库中定义的外键约束按照正确顺序进行更新。 使用数据绑定控件时，数据绑定体系结构会创建名为 tableAdapterManager 的 TableAdapterManager 类的成员变量。

> [!NOTE]
> 尝试使用数据集的内容更新数据源时，可能会出现错误。 若要避免错误，建议将调用适配器 `Update` 方法的代码放入 `try` / `catch` 块内。

根据业务需要，更新数据源的确切过程可能有所不同，但包含以下步骤：

1. 在 `try` / `catch` 块中调用适配器的 `Update` 方法。

2. 如果捕获到异常，请找到导致错误的数据行。

3. 协调数据行中的问题（以编程方式或通过向用户呈现无效行进行修改），然后重试更新（<xref:System.Data.DataRow.HasErrors%2A> <xref:System.Data.DataTable.GetErrors%2A>）。

## <a name="save-data-to-a-database"></a>将数据保存到数据库

调用 TableAdapter 的 `Update` 方法。 传递包含要写入数据库的值的数据表的名称。

### <a name="to-update-a-database-by-using-a-tableadapter"></a>使用 TableAdapter 更新数据库

- 在 `try` / `catch` 块中包含 TableAdapter 的 `Update` 方法。 下面的示例演示如何从 `try` / `catch` 块内更新 `NorthwindDataSet` 中 `Customers` 表的内容。

     [!code-csharp[VbRaddataSaving#9](../data-tools/codesnippet/CSharp/update-data-by-using-a-tableadapter_1.cs)]
     [!code-vb[VbRaddataSaving#9](../data-tools/codesnippet/VisualBasic/update-data-by-using-a-tableadapter_1.vb)]

## <a name="see-also"></a>请参阅

- [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)