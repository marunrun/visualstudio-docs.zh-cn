---
title: 创建数据库文件和使用表设计器
description: 本教程将介绍如何在 Visual Studio 中使用表设计器添加到数据库表和外键。 它还演示如何将数据通过图形界面添加。
ms.date: 11/03/2017
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
ms.openlocfilehash: 6f227a7948f5a842120341432c03747119988ddf
ms.sourcegitcommit: aeb1a1135dd789551e15aa5124099a5fe3f0f32b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2019
ms.locfileid: "66501078"
---
# <a name="create-a-database-and-add-tables-in-visual-studio"></a>创建数据库并在 Visual Studio 中添加表

可以使用 Visual Studio 创建和更新 SQL Server Express LocalDB 中的本地数据库文件。 此外可以通过执行 TRANSACT-SQL 语句中的创建数据库**SQL Server 对象资源管理器**Visual Studio 工具窗口中的。 在本主题中，我们将创建 *.mdf*文件，并使用表设计器中添加表和键。

## <a name="prerequisites"></a>系统必备

若要完成本演练，您必须具有可选**数据存储和处理**在 Visual Studio 中安装的工作负荷。 若要安装它，打开**Visual Studio 安装程序**，然后选择**修改**或**详细** > **修改**旁边的版本你想要修改的 visual Studio。

::: moniker range=">=vs-2019"

上**工作负荷**选项卡上，在**其他工具集**，选择**数据存储和处理**，然后单击**修改**若要添加到工作负荷Visual Studio。

::: moniker-end

::: moniker range="=vs-2017"

上**工作负荷**选项卡上，在**Web 和云**，选择**数据存储和处理**，然后单击**修改**若要添加到工作负荷Visual Studio。

::: moniker-end

## <a name="create-a-project-and-a-local-database-file"></a>创建一个项目及本地数据库文件

1. 创建一个新**Windows 窗体应用程序**项目，并命名**SampleDatabaseWalkthrough**。

2. 在菜单栏上，选择**项目** > **添加新项**。

3. 在项模板列表中，向下滚动并选择**基于服务的数据库**。

     ![“项模板”对话框](../data-tools/media/raddata-vsitemtemplates.png)

4. 命名数据库**SampleDatabase**，然后单击**添加**。

### <a name="add-a-data-source"></a>添加数据源

1. 如果**数据源**窗口未打开，通过按打开**Shift**+**Alt**+**D**或选择**视图** > **其他 Windows** > **数据源**菜单栏上。

1. 在中**数据源**窗口中，选择**添加新数据源**链接。

   “数据源配置”向导随即打开  。

1. 上**选择数据源类型**页上，选择**数据库**，然后选择**下一步**。

1. 上**选择数据库模型**页上，选择**下一步**接受默认值 （数据集）。

1. 上**选择数据连接**页上，选择**SampleDatabase.mdf**在下拉列表中，文件，然后选择**下一步**。

1. 上**将连接字符串保存到应用程序配置文件**页上，选择**下一步**。

1. 一个**选择数据库对象**页上，你会看到一条消息，指出数据库不包含任何对象。 选择“完成”  。

### <a name="view-properties-of-the-data-connection"></a>查看的数据连接属性

您可以查看的连接字符串*SampleDatabase.mdf*通过打开属性窗口中的数据连接文件：

- 选择**视图** > **SQL Server 对象资源管理器**以打开**SQL Server 对象资源管理器**窗口。 展开 **(localdb) \MSSQLLocalDB** > **数据库**，然后右键单击*SampleDatabase.mdf* ，然后选择**属性**.

- 或者，可以选择**视图** > **服务器资源管理器**，如果该窗口尚未打开。 打开属性窗口，展开**数据连接**节点，打开快捷菜单*SampleDatabase.mdf*，然后选择**属性**。

## <a name="create-tables-and-keys-by-using-table-designer"></a>使用表设计器创建表和键

在本部分中，将创建两个表，每个表和若干行的示例数据中的主键。 你将创建外键以指定一个表中的记录如何与其他表中的记录相对应。

### <a name="create-the-customers-table"></a>创建客户表

1. 在中**服务器资源管理器**，展开**数据连接**节点，然后展开**SampleDatabase.mdf**节点。

2. 打开快捷菜单**表**，然后选择**添加新表**。

     “表设计器”打开并显示一个网格，其中有一个默认行，表示所创建表中的一列  。 通过向网格中添加行，即可在表中添加列。

3. 在网格中，为下列各个条目添加行：

    |列名称|数据类型|允许空|
    |-----------------|---------------|-----------------|
    |`CustomerID`|`nchar(5)`|False（清除）|
    |`CompanyName`|`nvarchar(50)`|False（清除）|
    |`ContactName`|`nvarchar (50)`|True（已选定）|
    |`Phone`|`nvarchar (24)`|True（已选定）|

4. 打开快捷菜单`CustomerID`行，并选择**设置主键**。

5. 打开默认行的快捷菜单，然后选择**删除**。

6. 通过更新脚本窗格的第一行来命名 Customers 表，与以下示例相匹配：

    ```sql
    CREATE TABLE [dbo].[Customers]
    ```

    将显示如下所示的内容：

    ![表设计器](../data-tools/media/raddata-table-designer.png)

7. 在的左上角**表设计器**，选择**更新**。

8. 在中**预览数据库更新**对话框中，选择**更新数据库**。

    你所做的更改将保存到本地数据库文件中。

### <a name="create-the-orders-table"></a>创建订单表

1. 添加另一个表，然后在下表中为每个条目添加行：

    |列名称|数据类型|允许空|
    |-----------------|---------------|-----------------|
    |`OrderID`|`int`|False（清除）|
    |`CustomerID`|`nchar(5)`|False（清除）|
    |`OrderDate`|`datetime`|True（已选定）|
    |`OrderQuantity`|`int`|True（已选定）|

2. 设置**OrderID**作为 primary key，然后删除默认行。

3. 通过更新脚本窗格的第一行来命名 Orders 表，与以下示例相匹配：

    ```sql
    CREATE TABLE [dbo].[Orders]
    ```

4. 在的左上角**表设计器**，选择**更新**按钮。

5. 在中**预览数据库更新**对话框中，选择**更新数据库**按钮。

    你所做的更改将保存到本地数据库文件中。

### <a name="create-a-foreign-key"></a>创建外键

1. 在网格右侧的上下文窗格中，打开快捷菜单**外键**，然后选择**添加新外键**，如下图所示。

     ![在表设计器中添加外键](../data-tools/media/foreignkey.png)

2. 在显示的文本框中，将“ToTable”替换为“Customers”   。

3. 在 T-SQL 的窗格中，更新与以下示例相匹配的最后一行：

    ```sql
    CONSTRAINT [FK_Orders_Customers] FOREIGN KEY ([CustomerID]) REFERENCES [Customers]([CustomerID])
    ```

4. 在的左上角**表设计器**，选择**更新**按钮。

5. 在中**预览数据库更新**对话框中，选择**更新数据库**按钮。

    你所做的更改将保存到本地数据库文件中。

## <a name="populate-the-tables-with-data"></a>用数据填充表

1. 在中**服务器资源管理器**或**SQL Server 对象资源管理器**，展开示例数据库的节点。

2. 打开快捷菜单**表**节点中，选择**刷新**，然后展开**表**节点。

3. 打开客户表的快捷菜单，然后选择**显示表数据**。

4. 添加任何所需的某些客户的数据。

    你可以指定任意五个字符作为客户 ID，但至少选择一个能记住的以便稍后在此过程中使用。

5. 打开订单表的快捷菜单，然后选择**显示表数据**。

6. 添加一些订单数据。

    > [!IMPORTANT]
    > 请确保所有订单 ID 和订单数量是整数，并且每个客户 ID 与 Customers 表中的“CustomerID”列中指定的值匹配  。

7. 在菜单栏上，选择**文件** > **全部保存**。

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中访问数据](accessing-data-in-visual-studio.md)
