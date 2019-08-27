---
title: 安装 SQL Server 示例数据库 |Microsoft Docs
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: 38840167-c3f8-4cb3-8d15-8af04a0a20a1
caps.latest.revision: 14
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 056e5d1fad258d063e30cfd97e85529ff3a0c9bd
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68160194"
---
# <a name="install-sql-server-sample-databases"></a>安装 SQL Server 示例数据库
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

示例数据库可用于试验 SQL 和 LINQ 查询、 数据绑定、 实体框架建模和等等。  每个数据库产品都有它自己的示例数据库。 Northwind 和 AdventureWorks 是两个常用的 SQL Server 示例数据库。  
  
 **AdventureWorks**是当前提供给 SQL Server 产品的示例数据库。 你可以为.mdf 文件从下载它[Codeplex 上的 AdventureWorks 页](http://msftdbprodsamples.codeplex.com/)。 有可用的数据库的常规和轻型 (LT) 版本此处。 大多数情况下，l T 版本是首选，因为它是不太复杂。  
  
 **Northwind**是一个相对简单的 SQL Server 数据库，已使用多年。 可以为.bak 文件从下载它[CodePlex 上的 Northwind 数据库页](https://northwinddatabase.codeplex.com/)。 若要避免出现权限问题，请将文件解压缩到不是在您的用户文件夹下的新文件夹。  
  
#### <a name="to-restore-a-database-from-a-bak-file-in-visual-studio"></a>若要从 Visual Studio 中的.bak 文件中还原数据库  
  
1. 当备份 Microsoft SQL Server 数据库时，结果将是.bak 文件。 若要使数据库文件另存为再次文件可用，.bak，它必须是*还原*。 在主菜单中，选择**视图** > **SQL Server 对象资源管理器**。 如果看不到它，您可能需要安装它。 转到**Control Panel** > **程序和功能**，查找 Microsoft Visual Studio 2015，然后单击**更改**按钮。 已安装的组件的列表出现时在安装程序窗口中，选择**SQL Server 对象资源管理器**复选框，然后继续进行安装。  
  
2. SQL Server 对象资源管理器中，右键单击任何 SQL Server 数据库引擎 (例如，localdb)，然后选择**新查询**。  
  
     ![SQL Server 对象资源管理器的新查询](../data-tools/media/raddata-sql-server-object-explorer-new-query.png "raddata SQL Server 对象资源管理器的新查询")  
  
3. 首先，您需要.bak 文件中的数据库和日志文件的逻辑的名称。 若要获取它，输入到 SQL 查询编辑器中的此查询，并选择绿色**运行**窗口顶部的按钮。 如有必要，使其指向.bak 文件修改的文件路径。  
  
    ```  
    RESTORE FILELISTONLY  
    FROM DISK = 'C:\nw\northwind.bak'  
    GO  
    ```  
  
     记下显示在结果窗口中的逻辑名称。  对于 Northwind 数据库中，两个逻辑名称是 Northwind 和 Northwind_log。  
  
4. 现在运行此查询来创建数据库。 替换为你自己的源和目标路径、 逻辑数据库名称和 northwind 为相应的物理文件名称。 保留的.mdf 和.ldf 文件扩展名。  
  
    ```  
    RESTORE DATABASE Northwind  
    FROM DISK = 'c:\nw\northwind.bak'  
    WITH MOVE 'Northwind' TO 'c:\nw\northwind.mdf',  
    MOVE 'Northwind_log' TO 'c:\nw\northwind.ldf'  
    ```  
  
5. 在 SQL Server 对象资源管理器中，右键单击**数据库**节点，并且应可以看到 Northwind 数据库节点。 如果不是，然后右键单击数据库并选择**添加新的数据库**。 输入名称和刚创建的.mdf 文件的位置。  
  
6. 数据库现在已准备好用作 Visual Studio 中的数据源。  
  
#### <a name="to-restore-a-database-from-a-bak-file-in-sql-server-management-studio"></a>若要从 SQL Server Management Studio 中的.bak 文件中还原数据库  
  
1. 从下载站点下载 SQL Server Management Studio。  
  
2. 在 SSMS**对象资源管理器**窗口中，右键单击**数据库**节点中，选择**Restore Database**，并提供.bak 文件的位置。  
  
     ![SSMS 还原数据库](../data-tools/media/raddata-ssms-restore-database.png "raddata SSMS 还原数据库")
