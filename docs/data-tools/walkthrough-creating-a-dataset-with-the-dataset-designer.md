---
title: 演练：使用数据集设计器创建数据集
ms.date: 09/11/2017
ms.topic: conceptual
helpviewer_keywords:
- datasets [Visual Basic], walkthroughs
- XML schemas, creating datasets
- data [Visual Studio], Dataset Designer
- Dataset Designer, walkthroughs
- datasets [Visual Basic], creating
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: f91c24885cc6817889671dd7a1a6e7e1686ce93f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62564995"
---
# <a name="walkthrough-create-a-dataset-with-the-dataset-designer"></a>演练：使用数据集设计器创建数据集

在本演练中创建数据集使用**数据集设计器**。 本文将指导您完成创建新的项目并添加新的过程**数据集**到它的项。 您将了解如何创建不使用向导根据数据库中的表的表。

## <a name="prerequisites"></a>系统必备

本演练使用 SQL Server Express LocalDB 和 Northwind 示例数据库。

1. 如果您没有 SQL Server Express LocalDB，安装它从[SQL Server Express 下载页](https://www.microsoft.com/sql-server/sql-server-editions-express)，或通过**Visual Studio 安装程序**。 在 Visual Studio 安装程序中，SQL Server Express LocalDB 可以安装的一部分**数据存储和处理**工作负荷，或作为单个组件。

2. 通过执行以下步骤安装 Northwind 示例数据库：

    1. 在 Visual Studio 中打开**SQL Server 对象资源管理器**窗口。 (SQL Server 对象资源管理器安装的一部分**数据存储和处理**Visual Studio 安装程序中的工作负载。)展开**SQL Server**节点。 LocalDB 实例上右键单击并选择**新查询**。

       查询编辑器窗口随即打开。

    2. 复制[Northwind Transact SQL 脚本](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)到剪贴板。 此 T-SQL 脚本从零开始创建 Northwind 数据库，并使用数据填充它。

    3. 将 T-SQL 脚本粘贴到查询编辑器，然后选择**Execute**按钮。

       后不久，查询完成执行，并创建 Northwind 数据库。

## <a name="create-a-new-windows-forms-application-project"></a>创建新的 Windows 窗体应用程序项目

1. 在 Visual Studio 中，在**文件**菜单中，选择**新建** > **项目**。

2. 展开**Visual C#** 或**Visual Basic**在左侧窗格中，然后选择**Windows 桌面**。

3. 在中间窗格中，选择**Windows 窗体应用**项目类型。

4. 将项目命名**DatasetDesignerWalkthrough**，然后选择**确定**。

     Visual Studio 将添加到项目**解决方案资源管理器**和设计器中显示新窗体。

## <a name="add-a-new-dataset-to-the-application"></a>将新的数据集添加到应用程序

1. 在“项目”菜单上，选择“添加新项”。

     “添加新项”对话框随即出现。

2. 在左侧窗格中，选择**数据**，然后选择**数据集**在中间窗格中。

3. 命名数据集**NorthwindDataset**，然后选择**添加**。

     Visual Studio 将添加名为的文件**NorthwindDataset.xsd**到该项目并将其在中打开**数据集设计器**。

## <a name="create-a-data-connection-in-server-explorer"></a>在服务器资源管理器中创建数据连接

1. 在“视图”菜单上，单击“服务器资源管理器”。

2. 在中**服务器资源管理器**，单击**连接到数据库**按钮。

3. 创建到 Northwind 示例数据库的连接。

## <a name="create-the-tables-in-the-dataset"></a>在数据集中创建表

本部分介绍如何将表添加到数据集。

### <a name="to-create-the-customers-table"></a>创建 Customers 表

1. 展开中创建的数据连接**服务器资源管理器**，然后展开**表**节点。

2. 拖动**客户**表从**服务器资源管理器**拖到**数据集设计器**。

     一个**客户**数据表并**CustomersTableAdapter**添加到数据集。

### <a name="to-create-the-orders-table"></a>创建 Orders 表

- 拖动**订单**表从**服务器资源管理器**拖到**数据集设计器**。

     **订单**数据表**OrdersTableAdapter**，和数据之间的关系**客户**并**订单**表将添加到数据集。

### <a name="to-create-the-orderdetails-table"></a>若要创建 OrderDetails 表

- 拖动**订单详细信息**表从**服务器资源管理器**拖到**数据集设计器**。

     **订单详细信息**数据表**OrderDetailsTableAdapter**，和之间的数据关系**订单**并**OrderDetails**表将添加到数据集。

## <a name="next-steps"></a>后续步骤

- 保存的数据集。

- 选择中的项**数据源**窗口并将其拖到窗体上。 有关详细信息，请参阅[绑定 Windows 窗体控件添加到 Visual Studio 中的数据](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)。

- 向 Tableadapter 添加更多的查询。

- 添加验证逻辑<xref:System.Data.DataTable.ColumnChanging>或<xref:System.Data.DataTable.RowChanging>数据表中数据集的事件。 有关详细信息，请参阅[验证数据集中](../data-tools/validate-data-in-datasets.md)。

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中创建和配置数据集](../data-tools/create-and-configure-datasets-in-visual-studio.md)
- [在 Visual Studio 中将 Windows 窗体控件绑定到数据](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)
- [验证数据](../data-tools/validate-data-in-datasets.md)