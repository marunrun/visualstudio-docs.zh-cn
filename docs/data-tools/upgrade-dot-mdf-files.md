---
title: 升级 .mdf 文件
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Express
- SQL Server LocalDB
- LocalDB
- SQLEXPRESS
- upgrading SQLExpress to SQLExpress
- upgrading to LocalDB
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 1b2b6029002e62f5b13f5fc40bc24f817364c148
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67821665"
---
# <a name="upgrade-mdf-files"></a>升级 .mdf 文件

本主题介绍了用于升级数据库文件 ( *.mdf*) 安装较新版本的 Visual Studio 之后。 它包括以下任务的说明：

- 升级数据库文件使用较新版本的 SQL Server Express LocalDB

- 升级以使用较新版本的 SQL Server Express 数据库文件

- 使用 Visual Studio 中的数据库文件，但保留了与 SQL Server Express 或 LocalDB 的较旧版本的兼容性

- 使 SQL Server Express 的默认数据库引擎

可以使用 Visual Studio 中打开项目的包含数据库文件 ( *.mdf*)，已通过使用的较旧版本的 SQL Server Express 或 LocalDB。 但是，若要继续开发你的项目在 Visual Studio 中，您必须具有该版本的 SQL Server Express 或 LocalDB 安装在 Visual Studio 中，作为在同一台计算机上或您必须升级数据库文件。 如果升级数据库文件，您将无法访问通过使用较旧版本的 SQL Server Express 或 LocalDB。

您可能还会提示您升级如果文件的版本与不兼容的 SQL Server Express 或当前已安装的 LocalDB 实例通过早期版本的 SQL Server Express 或 LocalDB 创建一个数据库文件。 若要解决此问题，Visual Studio 将提示你升级该文件。

> [!IMPORTANT]
> 我们建议在升级之前备份数据库文件。

> [!WARNING]
> 如果升级 *.mdf* LocalDB 2014 (V12) 32 位到 LocalDB 2016 (V13) 或更高版本中创建的文件，您将不能在 32 位版本的 LocalDB 中再次打开该文件。

将数据库升级之前，请考虑以下条件：

- 如果你想要在较旧版本和较新版本的 Visual Studio 中项目的工作的情况下不进行升级。

- 如果将在使用 SQL Server Express 而不是 LocalDB 的环境中使用你的应用程序，升级。

- 不升级如果应用程序使用远程连接，因为 LocalDB 不接受这些条款。

- 如果你的应用程序依赖于 Internet 信息服务 (IIS) 上，升级。

- 如果你想要在沙盒环境中测试数据库应用程序，但不想要管理数据库，请考虑升级。

### <a name="to-upgrade-a-database-file-to-use-the-localdb-version"></a>若要升级的数据库文件使用的 LocalDB 版本

1. 在中**服务器资源管理器**，选择**连接到数据库**按钮。

2. 在中**添加连接**对话框框中，指定以下信息：

    - **数据源**：`Microsoft SQL Server (SqlClient)`

    - **服务器名称**：

        - 若要使用的默认版本： `(localdb)\MSSQLLocalDB`。  这将指定 ProjectV12 或 ProjectV13，具体取决于安装哪个版本的 Visual Studio 并创建第一个的 LocalDB 实例时。 **MSSQLLocalDB**中的节点**SQL Server 对象资源管理器**显示它指向哪个版本。

        - 若要使用的特定版本：`(localdb)\ProjectsV12`或`(localdb)\ProjectsV13`，其中 V12 是 LocalDB 2014，V13 是 LocalDB 2016。

    - **将数据库文件附加**:主数据库的物理路径 *.mdf*文件。

    - **逻辑名称**:你想要使用该文件的名称。

3. 选择“确定”  按钮。

4. 系统提示时选择**是**按钮以升级该文件。

    数据库已升级、 附加到 LocalDB 数据库引擎，且不再使用旧版本的 LocalDB 兼容。

您还可以修改要通过打开连接的快捷菜单，然后选择使用 LocalDB 的 SQL Server Express 连接**修改连接**。 在中**修改连接**对话框框中，将服务器名称更改为`(LocalDB)\MSSQLLocalDB`。 在中**高级属性**对话框框中，请确保**用户实例**设置为**False**。

### <a name="to-upgrade-a-database-file-to-use-the-sql-server-express-version"></a>若要升级的数据库文件使用的 SQL Server Express 版本

1. 在连接到数据库的快捷菜单，选择**修改连接**。

2. 在中**修改连接**对话框中，选择**高级**按钮。

3. 在中**高级属性**对话框中，选择**确定**按钮而无需更改服务器名称。

    升级数据库文件以匹配当前版本的 SQL Server Express。

### <a name="to-work-with-the-database-in-visual-studio-but-retain-compatibility-with-sql-server-express"></a>若要使用 Visual Studio 中的数据库，但保留了与 SQL Server Express 的兼容性

- 在 Visual Studio 中，而无需对其进行升级打开的项目。

  - 若要运行项目，请选择**F5**密钥。

  - 若要编辑数据库，请打开 *.mdf*中的文件**解决方案资源管理器**，并展开节点中的**服务器资源管理器**以使用你的数据库。

### <a name="to-make-sql-server-express-the-default-database-engine"></a>若要使 SQL Server Express 的默认数据库引擎

1. 在菜单栏上，选择**工具** > **选项**。

2. 在中**选项**对话框框中，展开**Database Tools**选项，并选择**数据连接**。

3. 在中**SQL Server 实例名称**文字框中，指定的 SQL Server Express 或你想要使用的 LocalDB 实例的名称。 如果不命名的实例，指定`.\SQLEXPRESS or (LocalDB)\MSSQLLocalDB`。

4. 选择“确定”  按钮。

    SQL Server Express 将为您的应用程序的默认数据库引擎。

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中访问数据](accessing-data-in-visual-studio.md)
