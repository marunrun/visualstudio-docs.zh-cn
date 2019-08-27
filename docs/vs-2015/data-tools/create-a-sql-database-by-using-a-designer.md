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
author: gewarren
ms.author: gewarren
manager: jillfra
robots: noindex,nofollow
ms.openlocfilehash: f816095992379748b6d1888b5df54dc5433a8306
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63436972"
---
# <a name="create-a-sql-database-by-using-a-designer"></a>使用设计器创建 SQL 数据库
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以浏览基本任务，例如添加表和定义列，通过使用 Visual Studio 创建和更新 SQL Server Express LocalDB 中的本地数据库文件。 在完成本演练后，以本地数据库为起点进行其他演练，你会发现更高级的功能。  
  
 此外可以通过使用 SQL Server Management Studio （单独下载） 或 TRANSACT-SQL 语句中的创建数据库**SQL Server 对象资源管理器**Visual Studio 工具窗口中的。  
  
 在本演练中，你将探索以下任务：  
  
- [创建一个项目及本地数据库文件](../data-tools/create-a-sql-database-by-using-a-designer.md#BKMK_CreateNewSQLDB)  
  
- [创建表、 列、 主键和外键](../data-tools/create-a-sql-database-by-using-a-designer.md#BKMK_CreateNewTbls)  
  
- [用数据填充表](../data-tools/create-a-sql-database-by-using-a-designer.md#BKMK_Populating)  
  
## <a name="prerequisites"></a>系统必备  
 若要完成本演练，请确保已安装的 SQL Server Data Tools。 上**视图**菜单中，你应看到**SQL Server 对象资源管理器**。 如果没有，请转到**添加或删除程序**，单击**Visual Studio 2015**，选择**更改**，并选中的框旁边**SQL Server Data Tools**.  
  
## <a name="BKMK_CreateNewSQLDB"></a> 创建一个项目及本地数据库文件  
  
#### <a name="to-create-a-project-and-a-database-file"></a>创建项目和数据库文件  
  
1. 创建名为一个 Windows 窗体项目`SampleDatabaseWalkthrough`。  
  
2. 在菜单栏上，选择**项目** > **添加新项**。  
  
3. 在项模板列表中，向下滚动并选择**基于服务的数据库**。  
  
    ![项模板对话框](../data-tools/media/raddata-vsitemtemplates.png "raddata VSItemTemplates")  
  
4. 命名数据库**SampleDatabase**，然后选择**添加**按钮。  
  
5. 如果**数据源**窗口未打开，通过选择 Shift + Alt + D 键，或在菜单栏，选择打开该**视图** > **其他 Windows**  > **数据源**。  
  
6. 在中**数据源**窗口中，选择**添加新数据源**链接。  
  
7. 在中**数据源配置向导**，选择**下一步**按钮四次以接受默认设置，然后选择**完成**按钮。  
  
   通过打开数据库的属性窗口，可查看其连接字串符和主 .mdf 文件的位置。 您会看到数据库文件是在项目文件夹中。  
  
- 在 Visual Studio 中，选择**视图** > **SQL Server 对象资源管理器**如果该窗口尚未打开。 打开属性窗口，展开**数据连接**节点，打开 SampleDatabase.mdf，快捷菜单，然后选中**属性**。  
  
- 或者，可以选择**视图** > **服务器资源管理器**，如果该窗口尚未打开。 打开属性窗口，展开**数据连接**节点。 Sampledatabase.mdf，打开快捷菜单，然后选择**属性**。  
  
## <a name="BKMK_CreateNewTbls"></a> 创建表、 列、 主键和外键  
 在本节中，你将创建几个表，每个表中有一个主键和几行示例数据。 在下一个演练中，你将了解该信息如何显示在应用程序中。 你还将创建外键以指定一个表中的记录如何对应于另一个表中的记录。  
  
#### <a name="to-create-the-customers-table"></a>创建 Customers 表  
  
1. 在中**服务器资源管理器**或**SQL Server 对象资源管理器**，展开**数据连接**节点，然后展开**SampleDatabase.mdf**节点。  
  
2. 打开快捷菜单**表**，然后选择**添加新表**。  
  
     “表设计器”打开并显示一个网格，其中有一个默认行，表示所创建表中的一列。 通过向网格中添加行，即可在表中添加列。  
  
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
  
    ```  
    CREATE TABLE [dbo].[Customers]  
    ```  
  
     将显示如下所示的内容：  
  
     ![表设计器](../data-tools/media/raddata-table-designer.png "raddata 表设计器")  
  
7. 在的左上角**表设计器**，选择**更新**按钮。  
  
8. 在中**预览数据库更新**对话框中，选择**更新数据库**按钮。  
  
     你所做的更改将保存到本地数据库文件中。  
  
#### <a name="to-create-the-orders-table"></a>创建 Orders 表  
  
1. 添加另一个表，然后在下表中为每个条目添加行：  
  
    |列名称|数据类型|允许空|  
    |-----------------|---------------|-----------------|  
    |`OrderID`|`int`|False（清除）|  
    |`CustomerID`|`nchar(5)`|False（清除）|  
    |`OrderDate`|`datetime`|True（已选定）|  
    |`OrderQuantity`|`int`|True（已选定）|  
  
2. 设置**OrderID**作为 primary key，然后删除默认行。  
  
3. 通过更新脚本窗格的第一行来命名 Orders 表，与以下示例相匹配：  
  
    ```  
    CREATE TABLE [dbo].[Orders]  
    ```  
  
4. 在的左上角**表设计器**，选择**更新**按钮。  
  
5. 在中**预览数据库更新**对话框中，选择**更新数据库**按钮。  
  
     你所做的更改将保存到本地数据库文件中。  
  
#### <a name="to-create-a-foreign-key"></a>创建外键  
  
1. 在网格右侧的上下文窗格中，打开快捷菜单**外键**，然后选择**添加新外键**，如下图所示。  
  
     ![在表设计器中添加外键](../data-tools/media/foreignkey.png "ForeignKey")  
  
2. 在出现的文本框中，替换**ToTable**与`Customers`。  
  
3. 在 T-SQL 的窗格中，更新与以下示例相匹配的最后一行：  
  
    ```  
    CONSTRAINT [FK_Orders_Customers] FOREIGN KEY ([CustomerID]) REFERENCES [Customers]([CustomerID])  
    ```  
  
4. 在的左上角**表设计器**，选择**更新**按钮。  
  
5. 在中**预览数据库更新**对话框中，选择**更新数据库**按钮。  
  
     你所做的更改将保存到本地数据库文件中。  
  
## <a name="BKMK_Populating"></a> 用数据填充表  
  
#### <a name="to-populate-the-tables-with-data"></a>将数据填入表中  
  
1. 在中**服务器资源管理器**或**SQL Server 对象资源管理器**，展开示例数据库的节点。  
  
2. 打开快捷菜单**表**节点中，选择**刷新**，然后展开**表**节点。  
  
3. 打开客户表的快捷菜单，然后选择**显示表数据**。  
  
4. 为至少三个客户添加所需数据。  
  
     你可以指定任意五个字符作为客户 ID，但至少选择一个能记住的以便稍后在此过程中使用。  
  
5. 打开订单表的快捷菜单，然后选择**显示表数据**。  
  
6. 为至少三个订单添加数据。  
  
    > [!IMPORTANT]
    > 请确保所有订单 ID 和订单数量是整数，并且每个客户 ID 与 Customers 表中的 CustomerID 列中指定的值相匹配。  
  
7. 在菜单栏上，选择**文件** > **全部保存**。  
  
8. 在菜单栏上，选择**文件** > **关闭解决方案**。  
  
    > [!NOTE]
    > 最好备份刚创建的数据库文件，你可以复制并粘贴到其他位置，或以不同名称另存一份。  
  
## <a name="next-steps"></a>后续步骤  
 现在，已用一些示例数据的本地数据库文件，可以完成任何演示数据库任务的演练。
