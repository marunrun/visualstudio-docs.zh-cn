---
title: 使用设计器创建 SQL 数据库 |Microsoft Docs
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
- SQL Server Express
- local data
- LocalDB
- SQLEXPRESS
- data [Visual Studio], Local data
- SQL Express
- data [Visual Studio], walkthroughs
- databases, creating
- database files, creating
ms.assetid: 99c2b06f-47aa-414e-8057-a3453712fd23
caps.latest.revision: 54
author: jillre
ms.author: jillfra
manager: jillfra
robots: noindex,nofollow
ms.openlocfilehash: 33b97050f04fd23a9fa3b6c3c641faa5dfe4802f
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72651063"
---
# <a name="create-a-sql-database-by-using-a-designer"></a>使用设计器创建 SQL 数据库
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以通过使用 Visual Studio 创建和更新 SQL Server Express LocalDB 中的本地数据库文件来浏览基本任务，例如添加表和定义列。 在完成本演练后，以本地数据库为起点进行其他演练，你会发现更高级的功能。

 你还可以通过在 Visual Studio 的 " **SQL Server 对象资源管理器**工具" 窗口中使用 SQL Server Management Studio （单独下载）或 transact-sql 语句来创建数据库。

 在本演练中，你将探索以下任务：

- [创建项目和本地数据库文件](../data-tools/create-a-sql-database-by-using-a-designer.md#BKMK_CreateNewSQLDB)

- [创建表、列、主键和外键](../data-tools/create-a-sql-database-by-using-a-designer.md#BKMK_CreateNewTbls)

- [用数据填充表](../data-tools/create-a-sql-database-by-using-a-designer.md#BKMK_Populating)

## <a name="prerequisites"></a>Prerequisites
 若要完成本演练，请确保已安装 SQL Server Data Tools。 在 "**视图**" 菜单上，应会看到**SQL Server 对象资源管理器**。 如果不存在，请转到 "**添加或删除程序**"，单击 " **Visual Studio 2015**"，选择 "**更改**"，然后选择 " **SQL Server Data Tools**" 旁边的框。

## <a name="BKMK_CreateNewSQLDB"></a>创建项目和本地数据库文件

#### <a name="to-create-a-project-and-a-database-file"></a>创建项目和数据库文件

1. 创建一个名为 `SampleDatabaseWalkthrough` Windows 窗体项目。

2. 在菜单栏上，选择 "**项目** > "**添加新项**"。

3. 在项模板列表中，向下滚动并选择 "**基于服务的数据库**"。

    !["项模板" 对话框](../data-tools/media/raddata-vsitemtemplates.png "raddata VSItemTemplates")

4. 将数据库命名为**sampledatabase.mdf**，然后选择 "**添加**" 按钮。

5. 如果 "**数据源**" 窗口未打开，请选择 Shift + Alt + D 键，或在菜单栏上选择 "**视图**"  > **其他 Windows**  > **数据源**，将其打开。

6. 在 "**数据源**" 窗口中，选择 "**添加新数据源**" 链接。

7. 在 "**数据源配置向导**" 中，选择 "**下一步**" 按钮四次以接受默认设置，然后选择 "**完成**" 按钮。

   通过打开数据库的属性窗口，可查看其连接字串符和主 .mdf 文件的位置。 你会看到该数据库文件位于项目文件夹中。

- 在 Visual Studio 中，如果该窗口尚未打开，请选择 "**查看** > "**SQL Server 对象资源管理器**。 展开 "**数据连接**" 节点，打开 "sampledatabase.mdf" 的快捷菜单，然后选择 "**属性**"，打开 "属性" 窗口。

- 或者，如果该窗口尚未打开，还可以选择 "**查看** > "**服务器资源管理器**。 展开 "**数据连接**" 节点，打开 "属性" 窗口。 打开 Sampledatabase.mdf 的快捷菜单，然后选择 "**属性**"。

## <a name="BKMK_CreateNewTbls"></a>创建表、列、主键和外键
 在本节中，你将创建几个表，每个表中有一个主键和几行示例数据。 在下一个演练中，你将了解该信息如何显示在应用程序中。 你还将创建外键以指定一个表中的记录如何对应于另一个表中的记录。

#### <a name="to-create-the-customers-table"></a>创建 Customers 表

1. 在**服务器资源管理器**或**SQL Server 对象资源管理器**中，展开 "**数据连接**" 节点，然后展开 " **sampledatabase.mdf** " 节点。

2. 打开**表**的快捷菜单，然后选择 "**添加新表**"。

     “表设计器”打开并显示一个网格，其中有一个默认行，表示所创建表中的一列。 通过向网格中添加行，即可在表中添加列。

3. 在网格中，为下列各个条目添加行：

    |列名称|数据类型|允许空|
    |-----------------|---------------|-----------------|
    |`CustomerID`|`nchar(5)`|False（清除）|
    |`CompanyName`|`nvarchar(50)`|False（清除）|
    |`ContactName`|`nvarchar (50)`|True（已选定）|
    |`Phone`|`nvarchar (24)`|True（已选定）|

4. 打开 "`CustomerID`" 行的快捷菜单，然后选择 "**设置主键**"。

5. 打开默认行的快捷菜单，然后选择 "**删除**"。

6. 通过更新脚本窗格的第一行来命名 Customers 表，与以下示例相匹配：

    ```
    CREATE TABLE [dbo].[Customers]
    ```

     将显示如下所示的内容：

     ![表设计器](../data-tools/media/raddata-table-designer.png "raddata 表设计器")

7. 在**表设计器**的左上角，选择 "**更新**" 按钮。

8. 在 "**预览数据库更新**" 对话框中，选择 "**更新数据库**" 按钮。

     你所做的更改将保存到本地数据库文件中。

#### <a name="to-create-the-orders-table"></a>创建 Orders 表

1. 添加另一个表，然后在下表中为每个条目添加行：

    |列名称|数据类型|允许空|
    |-----------------|---------------|-----------------|
    |`OrderID`|`int`|False（清除）|
    |`CustomerID`|`nchar(5)`|False（清除）|
    |`OrderDate`|`datetime`|True（已选定）|
    |`OrderQuantity`|`int`|True（已选定）|

2. 将 "**订单 id** " 设置为主键，然后删除默认行。

3. 通过更新脚本窗格的第一行来命名 Orders 表，与以下示例相匹配：

    ```
    CREATE TABLE [dbo].[Orders]
    ```

4. 在**表设计器**的左上角，选择 "**更新**" 按钮。

5. 在 "**预览数据库更新**" 对话框中，选择 "**更新数据库**" 按钮。

     你所做的更改将保存到本地数据库文件中。

#### <a name="to-create-a-foreign-key"></a>创建外键

1. 在网格右侧的上下文窗格中，打开 "**外键**" 的快捷菜单，然后选择 "**添加新外键**"，如下图所示。

     ![在表设计器中添加外键](../data-tools/media/foreignkey.png "ForeignKey")

2. 在出现的文本框中，将**ToTable**替换为 `Customers`。

3. 在 T-sql 窗格中，更新最后一行以与以下示例匹配：

    ```
    CONSTRAINT [FK_Orders_Customers] FOREIGN KEY ([CustomerID]) REFERENCES [Customers]([CustomerID])
    ```

4. 在**表设计器**的左上角，选择 "**更新**" 按钮。

5. 在 "**预览数据库更新**" 对话框中，选择 "**更新数据库**" 按钮。

     你所做的更改将保存到本地数据库文件中。

## <a name="BKMK_Populating"></a>用数据填充表

#### <a name="to-populate-the-tables-with-data"></a>将数据填入表中

1. 在**服务器资源管理器**或**SQL Server 对象资源管理器**中，展开示例数据库的节点。

2. 打开 "**表**" 节点的快捷菜单，选择 "**刷新**"，然后展开 "**表**" 节点。

3. 打开 "Customers" 表的快捷菜单，然后选择 "**显示表数据**"。

4. 为至少三个客户添加所需数据。

     你可以指定任意五个字符作为客户 ID，但至少选择一个能记住的以便稍后在此过程中使用。

5. 打开 Orders 表的快捷菜单，然后选择 "**显示表数据**"。

6. 为至少三个订单添加数据。

    > [!IMPORTANT]
    > 请确保所有订单 ID 和订单数量是整数，并且每个客户 ID 与 Customers 表中的 CustomerID 列中指定的值相匹配。

7. 在菜单栏上，选择 "**文件**"  >  "**全部保存**"。

8. 在菜单栏上，选择 "**文件** > **关闭解决方案**"。

    > [!NOTE]
    > 最好备份刚创建的数据库文件，你可以复制并粘贴到其他位置，或以不同名称另存一份。

## <a name="next-steps"></a>后续步骤
 现在您有了包含一些示例数据的本地数据库文件，您可以完成演示数据库任务的任何演练。
