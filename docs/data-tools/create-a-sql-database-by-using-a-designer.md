---
title: 创建数据库文件并使用表设计器
description: 本教程介绍如何在 Visual Studio 中使用表设计器向数据库添加表和外键。 它还演示如何通过图形界面添加数据。
ms.date: 09/19/2019
ms.topic: conceptual
helpviewer_keywords:
- database tables, creating
- database files, creating
- table designer
ms.assetid: 99c2b06f-47aa-414e-8057-a3453712fd23
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 365037d3eeeec5077d724ca72d43cce5dcbe0ebd
ms.sourcegitcommit: 528178a304e66c0cb7ab98b493fe3c409f87493a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71273359"
---
# <a name="create-a-database-and-add-tables-in-visual-studio"></a>在 Visual Studio 中创建数据库并添加表

可以使用 Visual Studio 来创建和更新 SQL Server Express LocalDB 中的本地数据库文件。 还可以通过在 Visual Studio 的 " **SQL Server 对象资源管理器**工具" 窗口中执行 transact-sql 语句来创建数据库。 在本主题中，我们将创建一个 *.mdf*文件并使用表设计器添加表和键。

## <a name="prerequisites"></a>系统必备

若要完成本演练，你需要安装在 Visual Studio 中的 **.net 桌面开发**和**数据存储和处理**工作负荷。 若要进行安装，请打开**Visual Studio 安装程序**，然后选择要修改的 Visual Studio 版本旁边的 "**修改**（或**更多** > **修改**）"。

## <a name="create-a-project-and-a-local-database-file"></a>创建一个项目及本地数据库文件

1. 创建新的**Windows 窗体应用**项目，并将其命名为**SampleDatabaseWalkthrough**。

2. 在菜单栏上，选择 "**项目** > " "**添加新项**"。

3. 在项模板列表中，向下滚动并选择 "**基于服务的数据库**"。

   ![“项模板”对话框](../data-tools/media/raddata-vsitemtemplates.png)

4. 将数据库命名为**sampledatabase.mdf**，然后单击 "**添加**"。

### <a name="add-a-data-source"></a>添加数据源

1. 如果 "**数据源**" 窗口未打开，请按**Shift**+**Alt**+**D**或选择 "在上**查看** > **其他 Windows** > **数据源**" 来打开它。菜单栏。

1. 在 "**数据源**" 窗口中，选择 "**添加新数据源**"。

   ![在 Visual Studio 中添加新数据源](media/add-new-data-source.png)

   “数据源配置”向导随即打开。

1. 在 "**选择数据源类型**" 页上，选择 "**数据库**"，然后选择 "**下一步**"。

1. 在 "**选择数据库模型**" 页上，选择 "**下一步**" 以接受默认值（数据集）。

1. 在 "**选择你的数据连接**" 页上，选择下拉列表中的 " **sampledatabase.mdf** " 文件，然后选择 "**下一步**"。

1. 在 "将**连接字符串保存到应用程序配置文件**中" 页上，选择 "**下一步**"。

1. 在 "**选择数据库对象**" 页上，您将看到一条消息，指出该数据库不包含任何对象。 选择“完成”。

### <a name="view-properties-of-the-data-connection"></a>查看数据连接的属性

可以通过打开数据连接的属性窗口，查看*sampledatabase.mdf*文件的连接字符串：

- 选择 "**查看** > **SQL Server 对象资源管理器**" 以打开 " **SQL Server 对象资源管理器**" 窗口。 展开 **（localdb） "\MSSQLLocalDB** > **数据库**"，然后右键单击 " *sampledatabase.mdf* "，然后选择 "**属性**"。

- 或者，如果该窗口尚未打开，还可以选择 "**查看** > **服务器资源管理器**"。 展开 "**数据连接**" 节点，右键单击 sampledatabase.mdf，然后选择 "**属性**"，以打开属性窗口 *。*

  > [!TIP]
  > 如果无法展开 "数据连接" 节点，或未列出 Sampledatabase.mdf 连接，请在服务器资源管理器工具栏中选择 "**连接到数据库**" 按钮。 在 "**添加连接**" 对话框中，确保在 "**数据源**" 下选择 " **Microsoft SQL Server 数据库文件**"，然后浏览到并选择 sampledatabase.mdf 文件。 通过选择 **"确定"** 完成添加连接。

## <a name="create-tables-and-keys-by-using-table-designer"></a>使用表设计器创建表和键

在本部分中，将创建两个表、每个表中有一个主键和几行示例数据。 你还将创建外键以指定一个表中的记录如何对应于另一个表中的记录。

### <a name="create-the-customers-table"></a>创建 Customers 表

1. 在**服务器资源管理器**中，展开 "**数据连接**" 节点，然后展开 " **sampledatabase.mdf** " 节点。

   如果无法展开 "数据连接" 节点，或未列出 Sampledatabase.mdf 连接，请在服务器资源管理器工具栏中选择 "**连接到数据库**" 按钮。 在 "**添加连接**" 对话框中，确保在 "**数据源**" 下选择 " **Microsoft SQL Server 数据库文件**"，然后浏览到并选择 sampledatabase.mdf 文件。 通过选择 **"确定"** 完成添加连接。

2. 右键单击 "**表**"，然后选择 "**添加新表**"。

   表设计器将打开并显示一个网格，其中包含一个默认行，表示要创建的表中的单个列。 通过向网格中添加行，即可在表中添加列。

3. 在网格中，为下列各个条目添加行：

   |列名称|数据类型|允许空|
   |-----------------|---------------|-----------------|
   |`CustomerID`|`nchar(5)`|False（清除）|
   |`CompanyName`|`nvarchar(50)`|False（清除）|
   |`ContactName`|`nvarchar (50)`|True（已选定）|
   |`Phone`|`nvarchar (24)`|True（已选定）|

4. 右键单击该行，然后`CustomerID`选择 "**设置主键**"。

5. 右键单击默认行（`Id`），然后选择 "**删除**"。

6. 通过更新脚本窗格的第一行来命名 Customers 表，与以下示例相匹配：

   ```sql
   CREATE TABLE [dbo].[Customers]
   ```

   将显示如下所示的内容：

   ![表设计器](../data-tools/media/table-designer.png)

7. 在**表设计器**的左上角，选择 "**更新**"。

8. 在 "**预览数据库更新**" 对话框中，选择 "**更新数据库**"。

   "Customers" 表在本地数据库文件中创建。

### <a name="create-the-orders-table"></a>创建 Orders 表

1. 添加另一个表，然后在下表中为每个条目添加行：

   |列名称|数据类型|允许空|
   |-----------------|---------------|-----------------|
   |`OrderID`|`int`|False（清除）|
   |`CustomerID`|`nchar(5)`|False（清除）|
   |`OrderDate`|`datetime`|True（已选定）|
   |`OrderQuantity`|`int`|True（已选定）|

2. 将 "**订单 id** " 设置为主键，然后删除默认行。

3. 通过更新脚本窗格的第一行来命名 Orders 表，与以下示例相匹配：

   ```sql
   CREATE TABLE [dbo].[Orders]
   ```

4. 在**表设计器**的左上角，选择 "**更新**"。

5. 在 "**预览数据库更新**" 对话框中，选择 "**更新数据库**"。

   Orders 表是在本地数据库文件中创建的。 如果在服务器资源管理器中展开 "**表**" 节点，则会看到两个表：

   ![表节点服务器资源管理器中展开](media/server-explorer-tables-node.png)

### <a name="create-a-foreign-key"></a>创建外键

1. 在 Orders 表的表设计器网格右侧的上下文窗格中，右键单击 "**外键**"，然后选择 "**添加新外键**"。

   ![在 Visual Studio 中的表设计器中添加外键](../data-tools/media/add-foreign-key.png)

2. 在出现的文本框中，将文本 " **ToTable** " 替换为 "**客户**"。

3. 在 T-sql 窗格中，更新最后一行以与以下示例匹配：

   ```sql
   CONSTRAINT [FK_Orders_Customers] FOREIGN KEY ([CustomerID]) REFERENCES [Customers]([CustomerID])
   ```

4. 在**表设计器**的左上角，选择 "**更新**"。

5. 在 "**预览数据库更新**" 对话框中，选择 "**更新数据库**"。

   创建外键。

## <a name="populate-the-tables-with-data"></a>用数据填充表

1. 在**服务器资源管理器**或**SQL Server 对象资源管理器**中，展开示例数据库的节点。

2. 打开 "**表**" 节点的快捷菜单，选择 "**刷新**"，然后展开 "**表**" 节点。

3. 打开 "Customers" 表的快捷菜单，然后选择 "**显示表数据**"。

4. 为某些客户添加所需的任何数据。

    你可以指定任意五个字符作为客户 ID，但至少选择一个能记住的以便稍后在此过程中使用。

5. 打开 Orders 表的快捷菜单，然后选择 "**显示表数据**"。

6. 为一些订单添加数据。

    > [!IMPORTANT]
    > 请确保所有订单 ID 和订单数量是整数，并且每个客户 ID 与 Customers 表中的“CustomerID”列中指定的值匹配。

7. 在菜单栏上，选择 "**文件** > " "**全部保存**"。

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中访问数据](accessing-data-in-visual-studio.md)
