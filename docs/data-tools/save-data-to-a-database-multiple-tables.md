---
title: 将数据保存到数据库（多个表）
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- updating datasets, walkthroughs
- data [Visual Studio], saving
- saving data, walkthroughs
- data [Visual Studio], updating
ms.assetid: 7ebe03da-ce8c-4cbc-bac0-a2fde4ae4d07
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: bcb551cdcd5b2505c6ac536a440fcc3e70464bfb
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72648197"
---
# <a name="save-data-to-a-database-multiple-tables"></a>将数据保存到数据库（多个表）

应用程序开发中最常用方案之一是在 Windows 应用程序窗体上显示数据、编辑数据并将更新后的数据发回数据库。 本演练创建可显示两个相关表的数据的窗体，并显示如何编辑记录和将更改保存回数据库。 此示例使用源自 Northwind 示例数据库的 `Customers` 和 `Orders` 表。

通过调用 TableAdapter 的 `Update` 方法，可以将应用程序中的数据保存回数据库。 将表从 "**数据源**" 窗口拖到窗体上时，将自动添加保存数据所需的代码。 添加到窗体中的任何其他表都要求手动添加此代码。 本演练显示了如何添加从多个表保存更新的代码。

本演练涉及以下任务：

- 使用 "[数据源配置向导](../data-tools/media/data-source-configuration-wizard.png)" 在您的应用程序中创建和配置数据源。

- 设置 "[数据源" 窗口](add-new-data-sources.md#data-sources-window)中项的控件。 有关详细信息，请参阅[设置在从 "数据源" 窗口中拖动时要创建的控件](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)。

- 通过将某些项从“数据源”窗口拖动到窗体上来创建数据绑定控件。

- 修改数据集的每个表中的几个记录。

- 修改用于将数据集中的更新后的数据发回数据库的代码。

## <a name="prerequisites"></a>Prerequisites

本演练使用 SQL Server Express LocalDB 和 Northwind 示例数据库。

1. 如果没有 SQL Server Express 的 LocalDB，请从[SQL Server Express 下载 "页](https://www.microsoft.com/sql-server/sql-server-editions-express)或通过**Visual Studio 安装程序**安装它。 在**Visual Studio 安装程序**中，可以将 SQL Server Express LocalDB 作为**数据存储和处理**工作负荷的一部分进行安装，也可以作为单个组件安装。

2. 按照以下步骤安装 Northwind 示例数据库：

    1. 在 Visual Studio 中，打开 " **SQL Server 对象资源管理器**" 窗口。 （SQL Server 对象资源管理器作为 Visual Studio 安装程序中的**数据存储和处理**工作负荷的一部分安装。）展开 " **SQL Server** " 节点。 右键单击 LocalDB 实例，然后选择 "**新建查询**"。

       此时将打开查询编辑器窗口。

    2. 将[Northwind transact-sql 脚本](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)复制到剪贴板。 此 T-sql 脚本从头开始创建 Northwind 数据库，并用数据填充它。

    3. 将 T-sql 脚本粘贴到查询编辑器中，然后选择 "**执行**" 按钮。

       一小段时间后，查询将完成运行，并创建 Northwind 数据库。

## <a name="create-the-windows-forms-application"></a>创建 Windows 窗体应用程序

为C#或 Visual Basic 创建新的**Windows 窗体应用**项目。 将项目命名为 **UpdateMultipleTablesWalkthrough**。

## <a name="create-the-data-source"></a>创建数据源

此步骤使用“数据源配置向导”从 Northwind 数据库创建一个数据源。 你必须具有对 Northwind 示例数据库的访问权限，才能创建连接。 有关设置 Northwind 示例数据库的信息，请参阅[如何：安装示例数据库](../data-tools/installing-database-systems-tools-and-samples.md)。

1. 在 "**数据**" 菜单上，选择 "**显示数据源**"。

   “数据源”窗口随即打开。

2. 在“数据源”窗口，选择“添加新数据源”以启动“数据源配置”向导。

3. 在 "**选择数据源类型**" 屏幕上，选择 "**数据库**"，然后选择 "**下一步**"。

4. 在 "**选择你的数据连接**" 屏幕上，执行以下操作之一：

    - 如果下拉列表中包含到 Northwind 示例数据库的数据连接，请选择该连接。

         或

    - 选择“新建连接”，打开“添加/修改连接”对话框。

5. 如果数据库需要密码，请选择该选项以包括敏感数据，然后选择 "**下一步**"。

6. 在 "将**连接字符串保存到应用程序配置文件**" 中，选择 "**下一步**"。

7. 在 "**选择数据库对象**" 屏幕上，展开 "**表**" 节点。

8. 选择 " **Customers** " 和 " **Orders** " 表，然后选择 "**完成**"。

     “NorthwindDataSet”将添加到项目，这些表将显示在“数据源”窗口中。

## <a name="set-the-controls-to-be-created"></a>设置要创建的控件

对于本演练，`Customers` 表中的数据位于**详细信息**布局中，其中的数据显示在单独的控件中。 @No__t_0 表中的数据位于 <xref:System.Windows.Forms.DataGridView> 控件中显示的**网格**布局中。

### <a name="to-set-the-drop-type-for-the-items-in-the-data-sources-window"></a>设置“数据源”窗口中项的拖放类型

1. 在 "**数据源**" 窗口中，展开 " **Customers** " 节点。

2. 在 " **customers** " 节点上，从控件列表中选择 "**详细信息**"，将 " **Customers** " 表的控件更改为单个控件。 有关详细信息，请参阅[设置在从 "数据源" 窗口中拖动时要创建的控件](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)。

## <a name="create-the-data-bound-form"></a>创建数据绑定窗体

通过将某些项从“数据源”窗口拖到窗体，可创建数据绑定控件。

1. 将主“Customers”节点从“数据源”窗口拖到“Form1”上。

     带有描述性标签的数据绑定控件将显示在窗体上，同时还显示一个工具条 (<xref:System.Windows.Forms.BindingNavigator>)，用于在记录间进行导航。 组件栏中显示[NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md)、`CustomersTableAdapter`、<xref:System.Windows.Forms.BindingSource> 和 <xref:System.Windows.Forms.BindingNavigator>。

2. 将相关的“Orders”节点从“数据源”窗口拖到“Form1”上。

    > [!NOTE]
    > 相关的“Orders”节点位于“Fax”列下，该节点是“Customers”节点的子节点。

     用于导航记录的 <xref:System.Windows.Forms.DataGridView> 控件和工具栏（<xref:System.Windows.Forms.BindingNavigator>）将显示在窗体上。 组件栏中出现 `OrdersTableAdapter` 和 <xref:System.Windows.Forms.BindingSource>。

## <a name="add-code-to-update-the-database"></a>添加更新数据库的代码

通过调用“Customers”和“Orders”TableAdapter 的 `Update` 方法，可更新数据库。 默认情况下，<xref:System.Windows.Forms.BindingNavigator> 的 "**保存**" 按钮的事件处理程序将添加到窗体的代码中，以将更新发送到数据库。 此过程修改代码以按正确的顺序发送更新。这消除了引发引用完整性错误的可能性。 该代码还将通过在 try-catch 块中包装更新调用来实现错误处理。 可以根据应用程序的需要修改代码。

> [!NOTE]
> 为清楚起见，本演练不使用事务。 但是，如果要更新两个或多个相关表，请在事务中包含所有的更新逻辑。 事务是确保在提交任何更改之前数据库的所有相关更改都成功的进程。 有关详细信息，请参阅[事务和并发](/dotnet/framework/data/adonet/transactions-and-concurrency)。

### <a name="to-add-update-logic-to-the-application"></a>将更新逻辑添加到应用程序

1. 选择 <xref:System.Windows.Forms.BindingNavigator> 上的 "**保存**" 按钮。 这将打开 "代码编辑器" 到 `bindingNavigatorSaveItem_Click` 事件处理程序。

2. 替换事件处理程序中的代码以调用相关 TableAdapter 的 `Update` 方法。 下面的代码首先创建三个临时数据表以保存每个 <xref:System.Data.DataRowState> 的更新信息（<xref:System.Data.DataRowState.Deleted>、<xref:System.Data.DataRowState.Added> 和 <xref:System.Data.DataRowState.Modified>）。 更新按正确的顺序运行。 代码应类似于：

     [!code-vb[VbRaddataSaving#10](../data-tools/codesnippet/VisualBasic/save-data-to-a-database-multiple-tables_1.vb)]
     [!code-csharp[VbRaddataSaving#10](../data-tools/codesnippet/CSharp/save-data-to-a-database-multiple-tables_1.cs)]

## <a name="test-the-application"></a>测试应用程序

1. 按 F5。

2. 对每个表中的一条或多条记录的数据执行一些更改。

3. 选择“保存”按钮。

4. 检查数据库中的值以验证更改是否已保存。

## <a name="see-also"></a>请参阅

- [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)