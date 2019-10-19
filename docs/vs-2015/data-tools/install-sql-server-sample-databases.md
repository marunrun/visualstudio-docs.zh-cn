---
title: 安装 SQL Server 示例数据库 |Microsoft Docs
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: 38840167-c3f8-4cb3-8d15-8af04a0a20a1
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3991d3b741162b4b1993e5359ad427c17f00321a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72651527"
---
# <a name="install-sql-server-sample-databases"></a>安装 SQL Server 示例数据库
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

示例数据库对于试验 SQL 和 LINQ 查询、数据绑定、实体框架建模很有用。  每个数据库产品都有其自己的示例数据库。 Northwind 和 AdventureWorks 是两个热门 SQL Server 示例数据库。

 **AdventureWorks**是为 SQL Server 产品提供的当前示例数据库。 你可以从[Codeplex 上的 AdventureWorks 页面](http://msftdbprodsamples.codeplex.com/)将其下载为 .mdf 文件。 此处提供了数据库的常规和轻型（LT）版本。 在大多数情况下，最好是 LT 版本，因为它不太复杂。

 **Northwind**是一个相对简单的 SQL Server 数据库，多年来使用。 可以从[CodePlex 上的 Northwind 数据库页](https://northwinddatabase.codeplex.com/)将其作为 .bak 文件下载。 若要避免权限问题，请将文件解压缩到不在用户文件夹下的新文件夹中。

#### <a name="to-restore-a-database-from-a-bak-file-in-visual-studio"></a>在 Visual Studio 中从 .bak 文件还原数据库

1. 备份 Microsoft SQL Server 数据库时，结果为 .bak 文件。 若要使 .bak 文件作为数据库文件再次使用，则必须*还原*该文件。 在主菜单上，选择 "**查看** > **SQL Server 对象资源管理器**"。 如果看不到该示例，可能需要安装它。 转到 **"控制面板**"  >  "**程序和功能**"，找到 Microsoft Visual Studio 2015 "，然后单击"**更改**"按钮。 当安装的组件列表显示在安装程序窗口中时，选中 " **SQL Server 对象资源管理器**" 复选框，然后继续安装。

2. 在 SQL Server 对象资源管理器中，右键单击任何 SQL Server 的数据库引擎（例如 localdb），然后选择 "**新建查询**"。

     ![SQL Server 对象资源管理器新查询](../data-tools/media/raddata-sql-server-object-explorer-new-query.png "raddata SQL Server 对象资源管理器新查询")

3. 首先，需要数据库的逻辑名称和 .bak 文件中的日志文件。 为此，请在 SQL 查询编辑器中输入此查询，然后选择窗口顶部的绿色 "**运行**" 按钮。 如有必要，请修改文件路径以指向 .bak 文件。

    ```
    RESTORE FILELISTONLY
    FROM DISK = 'C:\nw\northwind.bak'
    GO
    ```

     记下 "结果" 窗口中显示的逻辑名称。  对于 Northwind 数据库，两个逻辑名称为 Northwind 和 Northwind_log。

4. 现在运行此查询以创建数据库。 根据需要替换为 Northwind 的源路径和目标路径、逻辑数据库名称和物理文件名。 保留 .mdf 和 .ldf 文件扩展名。

    ```
    RESTORE DATABASE Northwind
    FROM DISK = 'c:\nw\northwind.bak'
    WITH MOVE 'Northwind' TO 'c:\nw\northwind.mdf',
    MOVE 'Northwind_log' TO 'c:\nw\northwind.ldf'
    ```

5. 在 SQL Server 对象资源管理器中，右键单击 "**数据库**" 节点，你应看到 Northwind 数据库节点。 否则，右键单击 "数据库"，然后选择 "**添加新数据库**"。 输入刚刚创建的 .mdf 文件的名称和位置。

6. 数据库现在可以在 Visual Studio 中用作数据源。

#### <a name="to-restore-a-database-from-a-bak-file-in-sql-server-management-studio"></a>在 SQL Server Management Studio 中从 .bak 文件还原数据库

1. 从下载站点下载 SQL Server Management Studio。

2. 在 SSMS**对象资源管理器**窗口中，右键单击 "**数据库**" 节点，选择 "**还原数据库**"，并提供 .bak 文件的位置。

     ![SSMS 还原数据库](../data-tools/media/raddata-ssms-restore-database.png "raddata SSMS 还原数据库")
