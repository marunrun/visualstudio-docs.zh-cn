---
title: 创建参数化 TableAdapter 查询
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Visual Studio], TableAdapters
- TableAdapters, parameterized queries
- data [Visual Studio], searching data
- queries [Visual Studio], creating
- TableAdapters, searching data
- queries [Visual Studio], TableAdapters
ms.assetid: 104d1d19-b5a9-4071-b81e-1b3af08e9c7b
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 0926558c4d6e94032e2af2c75189f287da8d4811
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72642149"
---
# <a name="create-parameterized-tableadapter-queries"></a>创建参数化 TableAdapter 查询

参数化查询将返回满足查询内的 WHERE 子句条件的数据。 例如，通过在返回客户列表的 SQL 语句的末尾添加 `WHERE City = @City`，可以参数化客户列表，使之只显示某个城市的客户。

在**数据集设计器**中创建参数化 TableAdapter 查询。你还可以在 Windows 应用程序中使用 "**数据**" 菜单上的 "**参数化数据源**" 命令来创建它们。 "**参数化数据源**" 命令创建窗体上的控件，您可以在其中输入参数值和运行查询。

> [!NOTE]
> 构造参数化查询时，请使用特定于要编码的数据库的参数表示法。 例如，Access 和 OleDb 数据源使用问号“?”表示参数，所以 WHERE 子句将类似于：`WHERE City = ?`。

## <a name="create-a-parameterized-tableadapter-query"></a>创建参数化 TableAdapter 查询

### <a name="to-create-a-parameterized-query-in-the-dataset-designer"></a>在“数据集设计器”中创建参数化查询

- 将 WHERE 子句和所需参数添加到 SQL 语句中，以创建新的 TableAdapter。 有关详细信息，请参阅[创建和配置 tableadapter](../data-tools/create-and-configure-tableadapters.md)。

     或

- 将 WHERE 子句和所需参数添加到 SQL 语句中，以向现有 TableAdapter 中添加查询。

### <a name="to-create-a-parameterized-query-while-designing-a-data-bound-form"></a>在设计数据绑定窗体时创建参数化查询

1. 在窗体中选择已绑定到数据集的控件。 有关详细信息，请参阅[将 Windows 窗体控件绑定到 Visual Studio 中的数据](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)。

2. 在 "**数据**" 菜单上，选择 "**添加查询**"。

3. 将 WHERE 语句和所需参数添加到 SQL 语句中，以完成“搜索标准生成器”对话框。

### <a name="to-add-a-query-to-an-existing-data-bound-form"></a>将查询添加到现有数据绑定窗体

1. 在“Windows 窗体设计器”中打开窗体。

2. 在 "**数据**" 菜单上，选择 "**添加查询**" 或 "**数据智能标记**"。

    > [!NOTE]
    > 如果“添加查询”在“数据”菜单上不可用，请在窗体上选择一个控件，该窗体将显示你希望参数化功能添加到的数据源。 例如，如果窗体在 <xref:System.Windows.Forms.DataGridView> 控件中显示数据，则选择该控件。 如果窗体在各个控件中显示数据，则选择任意数据绑定控件。

3. 在 "**选择数据源表**" 区域中，选择要向其添加参数化的表。

4. 如果要创建新查询，请在“新建查询名称”框中键入名称。

     或

     在“现有查询名称”框中选择查询。

5. 在 "**查询" 文本框**中，键入采用参数的查询。

6. 选择“确定”。

     用于输入参数的控件和“加载”按钮将添加到 <xref:System.Windows.Forms.ToolStrip> 控件的窗体中。

### <a name="query-for-null-values"></a>查询 null 值

如果要查询没有当前值的记录，可以为 TableAdapter 参数分配 null 值。 例如，请考虑以下查询，该查询在其 `WHERE` 子句中有一个 `ShippedDate` 参数：

```sql
SELECT CustomerID, OrderDate, ShippedDate
FROM Orders
WHERE (ShippedDate = @ShippedDate) OR (ShippedDate IS NULL)
```

如果这是对 TableAdapter 的查询，则可以使用以下代码查询未附带的所有订单：

[!code-csharp[VbRaddataTableAdapters#8](../data-tools/codesnippet/CSharp/create-parameterized-tableadapter-queries_1.cs)]
[!code-vb[VbRaddataTableAdapters#8](../data-tools/codesnippet/VisualBasic/create-parameterized-tableadapter-queries_1.vb)]

使查询能够接受空值：

1. 在**数据集设计器**中，选择需要接受 null 参数值的 TableAdapter 查询。

2. 在 "**属性**" 窗口中，选择 "**参数**"，然后单击省略号（ **...** ）按钮以打开 "**参数集合编辑器**"。

3. 选择允许空值的参数，并将**AllowDbNull**属性设置为 `true`。

## <a name="see-also"></a>请参阅

- [使用 Tableadapter 填充数据集](../data-tools/fill-datasets-by-using-tableadapters.md)