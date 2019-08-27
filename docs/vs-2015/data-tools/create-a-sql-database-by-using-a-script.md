---
title: 通过使用脚本创建 SQL 数据库 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
ms.assetid: 36f913c0-f5a7-4831-83a0-baba721ac95c
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 7c0dc7b406f7e04aaa9848e2f5dcb96f17430f6d
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63436955"
---
# <a name="create-a-sql-database-by-using-a-script"></a>通过使用脚本创建 SQL 数据库
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在本演练中，您使用 Visual Studio 创建的小型数据库中包含的示例代码[使用 ADO.NET 创建简单的数据应用](../data-tools/create-a-simple-data-application-by-using-adonet.md)。  
  
 **在本主题中**  
  
- [创建包含数据库架构的脚本](../data-tools/create-a-sql-database-by-using-a-script.md#CreateScript)  
  
- [创建一个数据库项目并导入架构](../data-tools/create-a-sql-database-by-using-a-script.md#CreateProject)  
  
- [将数据库部署](../data-tools/create-a-sql-database-by-using-a-script.md#DeployDatabase)  
  
## <a name="prerequisites"></a>系统必备  
 若要完成本演练，必须具有 SQL Server Express LocalDB 或安装另一个 SQL 数据库。  
  
## <a name="CreateScript"></a> 创建包含数据库架构的脚本  
  
#### <a name="to-create-a-script-from-which-you-can-import-a-schema"></a>若要创建可从中导入架构的脚本  
  
1. 在中[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]，在菜单栏上，选择**文件** > **新建** > **文件**。  
  
     **新的文件**对话框随即出现。  
  
2. 在中**类别**列表中，选择**常规**。  
  
3. 在中**模板**列表中，选择**Sql 文件**，然后选择**打开**按钮。  
  
     打开 TRANSACT-SQL 编辑器。  
  
4. 复制以下 TRANSACT-SQL 代码，并将其粘贴到 TRANSACT-SQL 编辑器。  
  
    ```  
    PRINT N'Creating Sales...';  
    GO  
    CREATE SCHEMA [Sales]  
        AUTHORIZATION [dbo];  
    GO  
    PRINT N'Creating Sales.Customer...';  
    GO  
    CREATE TABLE [Sales].[Customer] (  
        [CustomerID]   INT           IDENTITY (1, 1) NOT NULL,  
        [CustomerName] NVARCHAR (40) NOT NULL,  
        [YTDOrders]    INT           NOT NULL,  
        [YTDSales]     INT           NOT NULL  
    );  
    GO  
    PRINT N'Creating Sales.Orders...';  
    GO  
    CREATE TABLE [Sales].[Orders] (  
        [CustomerID] INT      NOT NULL,  
        [OrderID]    INT      IDENTITY (1, 1) NOT NULL,  
        [OrderDate]  DATETIME NOT NULL,  
        [FilledDate] DATETIME NULL,  
        [Status]     CHAR (1) NOT NULL,  
        [Amount]     INT      NOT NULL  
    );  
    GO  
    PRINT N'Creating Sales.Def_Customer_YTDOrders...';  
    GO  
    ALTER TABLE [Sales].[Customer]  
        ADD CONSTRAINT [Def_Customer_YTDOrders] DEFAULT 0 FOR [YTDOrders];  
    GO  
    PRINT N'Creating Sales.Def_Customer_YTDSales...';  
    GO  
    ALTER TABLE [Sales].[Customer]  
        ADD CONSTRAINT [Def_Customer_YTDSales] DEFAULT 0 FOR [YTDSales];  
    GO  
    PRINT N'Creating Sales.Def_Orders_OrderDate...';  
    GO  
    ALTER TABLE [Sales].[Orders]  
        ADD CONSTRAINT [Def_Orders_OrderDate] DEFAULT GetDate() FOR [OrderDate];  
    GO  
    PRINT N'Creating Sales.Def_Orders_Status...';  
    GO  
    ALTER TABLE [Sales].[Orders]  
        ADD CONSTRAINT [Def_Orders_Status] DEFAULT 'O' FOR [Status];  
    GO  
    PRINT N'Creating Sales.PK_Customer_CustID...';  
    GO  
    ALTER TABLE [Sales].[Customer]  
        ADD CONSTRAINT [PK_Customer_CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) WITH (ALLOW_PAGE_LOCKS = ON, ALLOW_ROW_LOCKS = ON, PAD_INDEX = OFF, IGNORE_DUP_KEY = OFF, STATISTICS_NORECOMPUTE = OFF);  
    GO  
    PRINT N'Creating Sales.PK_Orders_OrderID...';  
    GO  
    ALTER TABLE [Sales].[Orders]  
        ADD CONSTRAINT [PK_Orders_OrderID] PRIMARY KEY CLUSTERED ([OrderID] ASC) WITH (ALLOW_PAGE_LOCKS = ON, ALLOW_ROW_LOCKS = ON, PAD_INDEX = OFF, IGNORE_DUP_KEY = OFF, STATISTICS_NORECOMPUTE = OFF);  
    GO  
    PRINT N'Creating Sales.FK_Orders_Customer_CustID...';  
    GO  
    ALTER TABLE [Sales].[Orders]  
        ADD CONSTRAINT [FK_Orders_Customer_CustID] FOREIGN KEY ([CustomerID]) REFERENCES [Sales].[Customer] ([CustomerID]) ON DELETE NO ACTION ON UPDATE NO ACTION;  
    GO  
    PRINT N'Creating Sales.CK_Orders_FilledDate...';  
    GO  
    ALTER TABLE [Sales].[Orders]  
        ADD CONSTRAINT [CK_Orders_FilledDate] CHECK ((FilledDate >= OrderDate) AND (FilledDate < '01/01/2020'));  
    GO  
    PRINT N'Creating Sales.CK_Orders_OrderDate...';  
    GO  
    ALTER TABLE [Sales].[Orders]  
        ADD CONSTRAINT [CK_Orders_OrderDate] CHECK ((OrderDate > '01/01/2005') and (OrderDate < '01/01/2020'));  
    GO  
    PRINT N'Creating Sales.uspCancelOrder...';  
    GO  
    CREATE PROCEDURE [Sales].[uspCancelOrder]  
    @OrderID INT  
    AS  
    BEGIN  
    DECLARE @Delta INT, @CustomerID INT  
    BEGIN TRANSACTION  
        SELECT @Delta = [Amount], @CustomerID = [CustomerID]  
         FROM [Sales].[Orders] WHERE [OrderID] = @OrderID;  
  
    UPDATE [Sales].[Orders]  
       SET [Status] = 'X'  
    WHERE [OrderID] = @OrderID;  
  
    UPDATE [Sales].[Customer]  
       SET  
       YTDOrders = YTDOrders - @Delta  
        WHERE [CustomerID] = @CustomerID  
    COMMIT TRANSACTION  
    END  
    GO  
    PRINT N'Creating Sales.uspFillOrder...';  
    GO  
    CREATE PROCEDURE [Sales].[uspFillOrder]  
    @OrderID INT, @FilledDate DATETIME  
    AS  
    BEGIN  
    DECLARE @Delta INT, @CustomerID INT  
    BEGIN TRANSACTION  
        SELECT @Delta = [Amount], @CustomerID = [CustomerID]  
         FROM [Sales].[Orders] WHERE [OrderID] = @OrderID;  
  
    UPDATE [Sales].[Orders]  
       SET [Status] = 'F',  
           [FilledDate] = @FilledDate  
    WHERE [OrderID] = @OrderID;  
  
    UPDATE [Sales].[Customer]  
       SET  
       YTDSales = YTDSales + @Delta  
        WHERE [CustomerID] = @CustomerID  
    COMMIT TRANSACTION  
    END  
    GO  
    PRINT N'Creating Sales.uspNewCustomer...';  
    GO  
    CREATE PROCEDURE [Sales].[uspNewCustomer]  
    @CustomerName NVARCHAR (40),  
    @CustomerID INT OUTPUT  
    AS  
    BEGIN  
    INSERT INTO [Sales].[Customer] (CustomerName) VALUES (@CustomerName);  
    SET @CustomerID = SCOPE_IDENTITY();  
    RETURN @@ERROR  
    END  
    GO  
    PRINT N'Creating Sales.uspPlaceNewOrder...';  
    GO  
    CREATE PROCEDURE [Sales].[uspPlaceNewOrder]  
    @CustomerID INT, @Amount INT, @OrderDate DATETIME, @Status CHAR (1)='O'  
    AS  
    BEGIN  
    DECLARE @RC INT  
    BEGIN TRANSACTION  
    INSERT INTO [Sales].[Orders] (CustomerID, OrderDate, FilledDate, Status, Amount)   
         VALUES (@CustomerID, @OrderDate, NULL, @Status, @Amount)  
    SELECT @RC = SCOPE_IDENTITY();  
    UPDATE [Sales].[Customer]  
       SET  
       YTDOrders = YTDOrders + @Amount  
        WHERE [CustomerID] = @CustomerID  
    COMMIT TRANSACTION  
    RETURN @RC  
    END  
    GO  
    CREATE PROCEDURE [Sales].[uspShowOrderDetails]  
    @CustomerID INT=0  
    AS  
    BEGIN  
    SELECT [C].[CustomerName], CONVERT(date, [O].[OrderDate]), CONVERT(date, [O].[FilledDate]), [O].[Status], [O].[Amount]  
      FROM [Sales].[Customer] AS C  
      INNER JOIN [Sales].[Orders] AS O  
         ON [O].[CustomerID] = [C].[CustomerID]  
      WHERE [C].[CustomerID] = @CustomerID  
    END  
    GO  
    ```  
  
5. 在菜单栏上，选择**文件** > **保存 sqlquery_1.sql 另存为**。  
  
     **将文件另存为**对话框随即出现。  
  
6. 在中**文件名**框中，输入`SampleImportScript.sql`，记下其位置也将在其中保存该文件，并选择**保存**按钮。  
  
7. 在菜单栏上，选择**文件** > **关闭解决方案**。  
  
     接下来，创建一个数据库项目，并从已创建的脚本然后导入架构。  
  
## <a name="CreateProject"></a> 创建一个数据库项目并导入架构  
  
#### <a name="to-create-a-database-project"></a>创建数据库项目  
  
1. 在菜单栏上，依次选择“文件” > “新建” > “项目”。  
  
     此时将出现“新建项目”对话框。  
  
2. 下**已安装**，展开**模板**节点，展开**其他语言**节点中，选择**SQL Server**类别，然后选择**SQL Server 数据库项目**模板。  
  
    > [!NOTE]
    > **其他语言**节点不会出现在 Visual Studio 的所有安装。  
  
3. 在中**名称**框中，输入`Small Database`。  
  
4. 选择**创建解决方案目录**如果尚未选中的复选框。  
  
5. 清除**添加到源代码管理**复选框，如果它还不是已清除，并选择**确定**按钮。  
  
     将创建数据库项目，并将出现在**解决方案资源管理器**。  
  
     接下来，从脚本导入数据库架构。  
  
#### <a name="to-import-a-database-schema-from-a-script"></a>若要从脚本导入数据库架构  
  
1. 在菜单栏上，选择**项目** > **导入** > **脚本**。  
  
2. 上**欢迎**页上，查看文本，并选择**下一步**按钮。  
  
3. 选择**单个文件**选项按钮，并选择**浏览**按钮。  
  
     **导入 SQL 脚本**对话框随即出现。  
  
4. 打开保存 SampleImportScript.sql 文件的文件夹，选择该文件，并选择**打开**按钮。  
  
5. 选择**完成**按钮以关闭**导入 SQL 脚本**对话框。  
  
     导入脚本，并且该脚本定义的对象添加到您的数据库项目。  
  
6. 查看摘要，然后依次**完成**按钮以关闭**导入 SQL 脚本文件**对话框。  
  
7. 在中**解决方案资源管理器**，展开 Sales、 脚本和安全文件夹的项目，并验证它们是否包含.sql 文件。  
  
8. 在中**SQL Server 对象资源管理器**，验证数据库显示在**项目**节点。  
  
     此时，数据库只包含系统对象，如表和存储的过程。 部署数据库后，它将包含用户表和存储的过程的脚本定义。  
  
## <a name="DeployDatabase"></a> 将数据库部署  
 当您按下**F5**密钥，部署 （或发布） 到 LocalDB 数据库的默认数据库。 可以在通过打开项目的属性页将数据库部署到不同位置选择**调试**选项卡，然后再更改连接字符串。
