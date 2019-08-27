---
title: 用 TableAdapter DBDirect 方法保存数据
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- TableAdapters, walkthroughs
- data [Visual Studio], saving
- saving data, walkthroughs
- data [Visual Studio], TableAdapter
ms.assetid: 74a6773b-37e1-4d96-a39c-63ee0abf49b1
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: ed5b0f84ea19e465a9d820d9f25c4fc19546c639
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62567567"
---
# <a name="save-data-with-the-tableadapter-dbdirect-methods"></a>用 TableAdapter DBDirect 方法保存数据

本演练提供了有关使用 TableAdapter 的 DBDirect 方法直接对数据库运行 SQL 语句的详细的说明。 TableAdapter 的 DBDirect 方法可对数据库更新进行精确的控制。 可用于运行特定的 SQL 语句和存储的过程的调用单个`Insert`， `Update`，并`Delete`方法，根据需要由你的应用程序 (而不是重载`Update`执行更新的方法INSERT 和 DELETE 语句都在一个调用中的)。

在本演练中，你将学会如何执行以下任务：

- 创建新的“Windows 窗体应用程序”。

- 创建和配置具有的数据集[数据源配置向导](../data-tools/media/data-source-configuration-wizard.png)。

- 选择从“数据源”窗口拖动某些项时要在窗体上创建的控件。 有关详细信息，请参阅[设置从数据源窗口中拖动时创建的控件](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)。

- 通过将某些项从“数据源”窗口拖到窗体上来创建数据绑定窗体。

- 添加方法来直接访问数据库并执行插入、 更新和删除。

## <a name="prerequisites"></a>系统必备

本演练使用 SQL Server Express LocalDB 和 Northwind 示例数据库。

1. 如果您没有 SQL Server Express LocalDB，安装它从[SQL Server Express 下载页](https://www.microsoft.com/sql-server/sql-server-editions-express)，或通过**Visual Studio 安装程序**。 在中**Visual Studio 安装程序**，可以作为的一部分安装 SQL Server Express LocalDB**数据存储和处理**工作负荷，或作为单个组件。

2. 通过执行以下步骤安装 Northwind 示例数据库：

    1. 在 Visual Studio 中打开**SQL Server 对象资源管理器**窗口。 (SQL Server 对象资源管理器安装的一部分**数据存储和处理**Visual Studio 安装程序中的工作负载。)展开**SQL Server**节点。 LocalDB 实例上右键单击并选择**新查询**。

       查询编辑器窗口随即打开。

    2. 复制[Northwind Transact SQL 脚本](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)到剪贴板。 此 T-SQL 脚本从零开始创建 Northwind 数据库，并使用数据填充它。

    3. 将 T-SQL 脚本粘贴到查询编辑器，然后选择**Execute**按钮。

       后不久，查询完成运行并创建 Northwind 数据库。

## <a name="create-a-windows-forms-application"></a>创建 Windows 窗体应用程序

第一步是创建**Windows 窗体应用程序**。

1. 在 Visual Studio 中，在**文件**菜单中，选择**新建** > **项目**。

2. 展开**Visual C#** 或**Visual Basic**在左侧窗格中，然后选择**Windows 桌面**。

3. 在中间窗格中，选择**Windows 窗体应用**项目类型。

4. 将项目命名**TableAdapterDbDirectMethodsWalkthrough**，然后选择**确定**。

     创建“TableAdapterDbDirectMethodsWalkthrough”项目并将其添加到“解决方案资源管理器”中。

## <a name="create-a-data-source-from-your-database"></a>从您的数据库创建数据源

此步骤根据 Northwind 示例数据库中的 `Region` 表，使用“数据源配置”向导创建数据源。 你必须具有对 Northwind 示例数据库的访问权限，才能创建连接。 有关设置 Northwind 示例数据库的信息，请参阅[如何：安装示例数据库](../data-tools/installing-database-systems-tools-and-samples.md)。

### <a name="to-create-the-data-source"></a>创建数据源

1. 上**数据**菜单中，选择**显示数据源**。

   “数据源”窗口随即打开。

2. 在“数据源”窗口，选择“添加新数据源”以启动“数据源配置”向导。

3. 上**选择数据源类型**屏幕上，选择**数据库**，然后选择**下一步**。

4. 上**选择您的数据连接**屏幕上，执行下列操作之一：

    - 如果下拉列表中包含到 Northwind 示例数据库的数据连接，请选择该连接。

         或

    - 选择“新建连接”以启动“添加/修改连接”对话框。

5. 如果你的数据库需要密码，选择选项以包括敏感数据，然后选择**下一步**。

6. 上**将连接字符串保存到应用程序配置文件**屏幕上，选择**下一步**。

7. 上**选择数据库对象**屏幕上，展开**表**节点。

8. 选择`Region`表，，然后选择**完成**。

     将“NorthwindDataSet”添加到项目后，“数据源”窗口中即会显示 `Region` 表。

## <a name="add-controls-to-the-form-to-display-the-data"></a>将控件添加到窗体以显示数据

通过将某些项从“数据源”窗口拖到窗体上来创建数据绑定控件。

若要创建 Windows 窗体上的数据绑定控件，将主**地区**从节点**数据源**拖到窗体的窗口。

用于导航记录的 <xref:System.Windows.Forms.DataGridView> 控件和工具栏（<xref:System.Windows.Forms.BindingNavigator>）将显示在窗体上。 一个[NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md)， `RegionTableAdapter`， <xref:System.Windows.Forms.BindingSource>，和<xref:System.Windows.Forms.BindingNavigator>组件栏中出现。

### <a name="to-add-buttons-that-will-call-the-individual-tableadapter-dbdirect-methods"></a>添加将调用单个 TableAdapter DbDirect 方法的按钮

1. 将三个 <xref:System.Windows.Forms.Button> 控件从“工具箱”拖到“Form1”上（在“RegionDataGridView”的下面）。

2. 在每个按钮上设置下列“名称”和“文本”属性。

    |名称|Text|
    |----------|----------|
    |`InsertButton`|**插入**|
    |`UpdateButton`|**更新**|
    |`DeleteButton`|**删除**|

### <a name="to-add-code-to-insert-new-records-into-the-database"></a>添加将新记录插入数据库所使用的代码

1. 选择**InsertButton**以创建 click 事件的事件处理程序并在代码编辑器中打开你的窗体。

2. 用下面的代码替换 `InsertButton_Click` 事件处理程序：

     [!code-vb[VbRaddataSaving#1](../data-tools/codesnippet/VisualBasic/save-data-with-the-tableadapter-dbdirect-methods_1.vb)]
     [!code-csharp[VbRaddataSaving#1](../data-tools/codesnippet/CSharp/save-data-with-the-tableadapter-dbdirect-methods_1.cs)]

### <a name="to-add-code-to-update-records-in-the-database"></a>添加更新数据库中的记录所使用的代码

1. 双击“UpdateButton”以创建 Click 事件的事件处理程序，并在代码编辑器中打开窗体。

2. 用下面的代码替换 `UpdateButton_Click` 事件处理程序：

     [!code-vb[VbRaddataSaving#2](../data-tools/codesnippet/VisualBasic/save-data-with-the-tableadapter-dbdirect-methods_2.vb)]
     [!code-csharp[VbRaddataSaving#2](../data-tools/codesnippet/CSharp/save-data-with-the-tableadapter-dbdirect-methods_2.cs)]

### <a name="to-add-code-to-delete-records-from-the-database"></a>添加代码以从数据库中删除记录

1. 选择**DeleteButton**以创建 click 事件的事件处理程序并在代码编辑器中打开你的窗体。

2. 用下面的代码替换 `DeleteButton_Click` 事件处理程序：

     [!code-vb[VbRaddataSaving#3](../data-tools/codesnippet/VisualBasic/save-data-with-the-tableadapter-dbdirect-methods_3.vb)]
     [!code-csharp[VbRaddataSaving#3](../data-tools/codesnippet/CSharp/save-data-with-the-tableadapter-dbdirect-methods_3.cs)]

## <a name="run-the-application"></a>运行此应用程序

- 选择**F5**运行该应用程序。

- 选择**插入**按钮，并验证新的记录显示在网格中。

- 选择**更新**按钮，然后验证是否在网格中更新记录。

- 选择**删除**按钮，并验证记录是否从网格中被删除。

## <a name="next-steps"></a>后续步骤

具体取决于应用程序的要求，有可能想要创建数据绑定窗体后执行的几个步骤。 你可以通过以下操作来增强此演练的效果：

- 将搜索功能添加到该窗体。

- 通过从“数据源”窗口中选择“使用向导配置数据集”，将其他表添加到数据集中。 可以通过将相关节点拖到窗体上来添加显示相关数据的控件。 有关详细信息，请参阅[中的数据集的关系](relationships-in-datasets.md)。

## <a name="see-also"></a>请参阅

- [将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)