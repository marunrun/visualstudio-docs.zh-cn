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
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 9b6c91e6074e34a8207325e25f4a48b94dd037ef
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72639445"
---
# <a name="walkthrough-create-a-dataset-with-the-dataset-designer"></a>演练：创建具有数据集设计器的数据集

在本演练中，您将使用**数据集设计器**创建一个数据集。 本文将指导你完成创建新项目的过程，并向其中添加新的**数据集**项。 您将了解如何在不使用向导的情况下创建基于数据库中的表的表。

## <a name="prerequisites"></a>Prerequisites

本演练使用 SQL Server Express LocalDB 和 Northwind 示例数据库。

1. 如果没有 SQL Server Express 的 LocalDB，请从[SQL Server Express 下载 "页](https://www.microsoft.com/sql-server/sql-server-editions-express)或通过**Visual Studio 安装程序**安装它。 在 Visual Studio 安装程序中，SQL Server Express LocalDB 可以作为**数据存储和处理**工作负荷的一部分进行安装，也可以作为单个组件安装。

2. 按照以下步骤安装 Northwind 示例数据库：

    1. 在 Visual Studio 中，打开 " **SQL Server 对象资源管理器**" 窗口。 （SQL Server 对象资源管理器作为 Visual Studio 安装程序中的**数据存储和处理**工作负荷的一部分安装。）展开 " **SQL Server** " 节点。 右键单击 LocalDB 实例，然后选择 "**新建查询**"。

       此时将打开查询编辑器窗口。

    2. 将[Northwind transact-sql 脚本](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true)复制到剪贴板。 此 T-sql 脚本从头开始创建 Northwind 数据库，并用数据填充它。

    3. 将 T-sql 脚本粘贴到查询编辑器中，然后选择 "**执行**" 按钮。

       一小段时间后，查询完成执行并创建 Northwind 数据库。

## <a name="create-a-new-windows-forms-application-project"></a>创建新的 Windows 窗体应用程序项目

1. 在 Visual Studio 的 "**文件**" 菜单上，选择 "**新建** > **项目**"。

2. 在左侧窗格中展开 "**视觉对象C#**  " 或 " **Visual Basic** "，然后选择 " **Windows 桌面**"。

3. 在中间窗格中，选择 " **Windows 窗体应用程序**" 项目类型。

4. 将项目命名为**DatasetDesignerWalkthrough**，然后选择 **"确定"** 。

     Visual Studio 会将项目添加到**解决方案资源管理器**并在设计器中显示一个新窗体。

## <a name="add-a-new-dataset-to-the-application"></a>向应用程序添加新的数据集

1. 在“项目”菜单上，选择“添加新项”。

     “添加新项”对话框随即出现。

2. 在左侧窗格中，选择 "**数据**"，然后在中间窗格中选择 "数据**集**"。

3. 将数据集命名为**NorthwindDataset**，然后选择 "**添加**"。

     Visual Studio 会将名为**NorthwindDataset**的文件添加到项目中，并在**数据集设计器**中打开它。

## <a name="create-a-data-connection-in-server-explorer"></a>在服务器资源管理器中创建数据连接

1. 在“视图”菜单上，单击“服务器资源管理器”。

2. 在**服务器资源管理器**中，单击 "**连接到数据库**" 按钮。

3. 创建与 Northwind 示例数据库的连接。

## <a name="create-the-tables-in-the-dataset"></a>在数据集中创建表

本节说明如何向数据集添加表。

### <a name="to-create-the-customers-table"></a>创建 Customers 表

1. 展开在**服务器资源管理器**中创建的数据连接，然后展开 "**表**" 节点。

2. 将 " **Customers** " 表从**服务器资源管理器**拖动到**数据集设计器**上。

     **客户**数据表和**CustomersTableAdapter**将添加到数据集。

### <a name="to-create-the-orders-table"></a>创建 Orders 表

- 将**Orders**表从**服务器资源管理器**拖动到**数据集设计器**上。

     "**客户**" 和 "**订单**" 表之间的**订单**数据表、 **OrdersTableAdapter**和数据关系将添加到数据集。

### <a name="to-create-the-orderdetails-table"></a>创建 OrderDetails 表

- 将 "**订单详细信息**" 表从**服务器资源管理器**拖动到**数据集设计器**上。

     订单**详细信息**数据表、 **OrderDetailsTableAdapter**和**Orders**表与**OrderDetails**表之间的数据关系将添加到数据集。

## <a name="next-steps"></a>后续步骤

- 保存数据集。

- 在 "**数据源**" 窗口中选择项，然后将其拖到窗体上。 有关详细信息，请参阅[将 Windows 窗体控件绑定到 Visual Studio 中的数据](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)。

- 向 Tableadapter 添加更多查询。

- 将验证逻辑添加到数据集中的数据表 <xref:System.Data.DataTable.ColumnChanging> 或 <xref:System.Data.DataTable.RowChanging> 事件。 有关详细信息，请参阅[验证数据集中的数据](../data-tools/validate-data-in-datasets.md)。

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中创建和配置数据集](../data-tools/create-and-configure-datasets-in-visual-studio.md)
- [在 Visual Studio 中将 Windows 窗体控件绑定到数据](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)
- [验证数据](../data-tools/validate-data-in-datasets.md)