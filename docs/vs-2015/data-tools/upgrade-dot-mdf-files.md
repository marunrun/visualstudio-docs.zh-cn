---
title: 升级.mdf 文件 |Microsoft Docs
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
- SQL Server LocalDB
- LocalDB
- SQLEXPRESS
- upgrading SQLExpress to SQLExpress
- upgrading to LocalDB
ms.assetid: 14ca6f76-f80e-4926-8020-3fee2d802b75
caps.latest.revision: 36
author: gewarren
ms.author: gewarren
manager: jillfra
robots: noindex,nofollow
ms.openlocfilehash: 169bf374b5c7ee34f75743e363d56c3737000cbc
ms.sourcegitcommit: 75807551ea14c5a37aa07dd93a170b02fc67bc8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67823447"
---
# <a name="upgrade-mdf-files"></a>升级 .mdf 文件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题介绍在安装较新版本的 Visual Studio 后再升级你的数据库文件 (.mdf) 的选项。 它包括以下任务的说明：  
  
- 升级数据库文件使用较新版本的 SQL Server Express LocalDB  
  
- 升级以使用较新版本的 SQL Server Express 数据库文件  
  
- 使用 Visual Studio 中的数据库文件，但保留了与 SQL Server Express 或 LocalDB 的较旧版本的兼容性  
  
- 使 SQL Server Express 的默认数据库引擎  
  
  可以使用 Visual Studio，打开包含已通过使用的较旧版本的 SQL Server Express 或 LocalDB 数据库文件 (.mdf) 的项目。 但是，若要继续开发你的项目在 Visual Studio 中，您必须具有该版本的 SQL Server Express 或 LocalDB 安装在 Visual Studio 中，作为在同一台计算机上或您必须升级数据库文件。 如果升级数据库文件，您将无法访问通过使用较旧版本的 SQL Server Express 或 LocalDB。  
  
  您可能还会提示您升级如果文件的版本与不兼容的 SQL Server Express 或当前已安装的 LocalDB 实例通过早期版本的 SQL Server Express 或 LocalDB 创建一个数据库文件。 若要解决此问题，Visual Studio 将提示你升级该文件。  
  
> [!IMPORTANT]
> 我们建议在升级之前备份数据库文件。  
  
> [!WARNING]
> 如果升级到 LocalDB 2016 (V13) 的 32 位 LocalDB 2014 (V12) 中创建的.mdf 文件时，你将不能以 32 位版本的 LocalDB 中再次打开该文件。  在 Update 2，LocalDB V13 是仅限 64 位。  
  
 将数据库升级之前，请考虑以下条件：  
  
- 如果你想要在较旧版本和较新版本的 Visual Studio 中项目的工作的情况下不进行升级。  
  
- 如果将在使用 SQL Server Express 而不是 LocalDB 的环境中使用你的应用程序，升级。  
  
- 不升级如果应用程序使用远程连接，因为 LocalDB 不接受这些条款。  
  
- 如果你的应用程序依赖于 Internet 信息服务 (IIS) 上，升级。  
  
- 如果你想要在沙盒环境中测试数据库应用程序，但不想要管理数据库，请考虑升级。  
  
### <a name="to-upgrade-a-database-file"></a>若要升级数据库文件  
  
1. 在中**服务器资源管理器**，选择**连接到数据库**按钮。  
  
2. 在中**添加连接**对话框框中，指定以下信息：  
  
   - **数据源**：`Microsoft SQL Server (SqlClient)`  
  
   - **服务器名称**：  
  
       - 若要使用的默认版本： `(localdb)\MSSQLLocalDB`。  这将指定 ProjectV12 或 ProjectV13，具体取决于安装哪个版本的 Visual Studio 并创建第一个的 LocalDB 实例时。 **MSSQLLocalDB**中的节点**SQL Server 对象资源管理器**显示它指向哪个版本。  
  
       - 若要使用的特定版本：`(localdb)\ProjectsV12`或`(localdb)\ProjectsV13`，其中 V12 是 LocalDB 2014，V13 是 LocalDB 2016。  
  
   - **将数据库文件附加**:主.mdf 文件的物理路径。  
  
   - **逻辑名称**:你想要使用该文件的名称。  
  
3. 选择“确定”  按钮。  
  
4. 系统提示时选择**是**按钮以升级该文件。  
  
   数据库已升级、 附加到 LocalDB 数据库引擎，且不再使用旧版本的 LocalDB 兼容。  
  
   您还可以修改要通过打开连接的快捷菜单，然后选择使用 LocalDB 的 SQL Server Express 连接**修改连接**。 在中**修改连接**对话框框中，将服务器名称更改为`(LocalDB)\MSSQLLocalDB`。 在中**高级属性**对话框框中，请确保**用户实例**设置为**False**。  
  
### <a name="to-upgrade-to-a-newer-version-of-sql-server-express"></a>若要升级到较新版本的 SQL Server Express  
  
1. 在连接到数据库的快捷菜单，选择**修改连接**。  
  
2. 在中**修改连接**对话框中，选择**高级**按钮。  
  
3. 在中**高级属性**对话框中，选择**确定**按钮而无需更改服务器名称。  
  
   升级数据库文件以匹配当前版本的 SQL Server Express。  
  
### <a name="to-work-with-the-database-in-visual-studio-but-retain-compatibility-with-sql-server-express"></a>若要使用 Visual Studio 中的数据库，但保留了与 SQL Server Express 的兼容性  
  
- 在 Visual Studio 中，而无需对其进行升级打开的项目。  
  
  - 若要运行项目，请选择 F5 键。  

  - 若要编辑数据库，请打开中的.mdf 文件**解决方案资源管理器**，并展开中的节点**服务器资源管理器**以使用你的数据库。  
  
### <a name="to-make-sql-server-express-the-default-database-engine"></a>若要使 SQL Server Express 的默认数据库引擎  
  
1. 在菜单栏上，选择**工具** > **选项**。  
  
2. 在中**选项**对话框框中，展开**Data Tools**选项，并选择**数据连接**节点。  
  
3. 在中**SQL Server 实例名称**文字框中，指定的 SQL Server Express 或你想要使用的 LocalDB 实例的名称。 如果不命名的实例，指定`.\SQLEXPRESS or (localdb)\MSSQLLocalDB`。  
  
4. 选择“确定”  按钮。  
  
   SQL Server Express 将为您的应用程序的默认数据库引擎。  
