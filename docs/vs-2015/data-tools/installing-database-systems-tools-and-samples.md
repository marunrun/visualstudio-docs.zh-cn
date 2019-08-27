---
title: 安装数据库系统、 工具和示例 |Microsoft Docs
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
- sample databases
- databases, samples
ms.assetid: 821de34b-eaa9-40af-b9aa-b8305de16899
caps.latest.revision: 31
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 63d9dd0844cb3e7422f8d78a0ee2e3cb4e0b1fab
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68196071"
---
# <a name="installing-database-systems-tools-and-samples"></a>安装数据库系统、工具和示例
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 本身不包括任何数据库系统之外，它在内部使用。 若要开发 Visual Studio 中的数据连接应用程序，您通常在本地开发计算机上安装数据库系统，然后部署应用程序和数据库到生产环境时，他们就可以。 对于数据库系统可从.NET 应用程序，可以在 Visual Studio 数据工具窗口中可见，它必须具有 ADO.NET 数据提供程序。 如果你打算在.NET 应用程序中使用实体数据模型提供程序必须支持实体框架。     通过 NuGet 包管理器或通过 Visual Studio 库提供多个提供程序。  
  
 SQL 开发，请确保已在 Visual Studio 中安装 SQL Server Data Tools。 单击**视图**菜单。 如果看不到 SQL Server 对象资源管理器，转到控制面板，并更改 Visual Studio。 在安装程序中，选择**Microsoft SQL Server Data Tools**。  
  
 如果使用 Azure 存储 Api，Azure 存储仿真程序在本地计算机上安装在开发过程中为了避免产生费用，直到准备好部署到生产环境。 有关详细信息，请参阅[使用 Azure 存储模拟器进行开发和测试](https://azure.microsoft.com/documentation/articles/storage-use-emulator/)。  
  
 以下列表包含一些更受欢迎的数据库系统，可在 Visual Studio 项目中。 表格并不详尽。 提供 ADO.NET 数据提供程序，与 Visual Studio 工具的深度集成的第三方供应商的列表，请参阅[ADO.NET 数据提供程序](https://msdn.microsoft.com/library/dd363565.aspx)。  
  
### <a name="microsoft-sql-server"></a>Microsoft SQL Server  
 SQL Server 是 Microsoft 旗舰数据库产品/服务。 SQL Server 2016 提供突破性的性能、 高级的安全性和丰富的、 集成的报表和分析。 它提供用于不同用途的各种版本中： 从高度可缩放、 高性能业务分析，以在一台计算机上使用。 SQL Server Express 是适用于重新分发和嵌入的 SQL Server 的全功能版本。  LocalDB 是 SQL Server Express，不需要配置并在应用程序的进程中运行的简化的版本。 您可以下载中的一个或两个产品[SQL Server Express 下载页](https://www.microsoft.com/sql-server/sql-server-editions-express)。 许多 SQL 示例在本部分中使用 SQL Server LocalDB。 SQL Server Management Studio (SSMS) 是一个独立的数据库管理应用程序具有比在 Visual Studio SQL Server 对象资源管理器提供更多的功能。 可以从上一链接来获取 SSMS。  
  
### <a name="oracle"></a>Oracle  
 您可以下载从 Oracle 数据库的付费或免费版本[Oracle 技术网络](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/index-092322.html)页。 对于实体框架和 Tableadapter 的设计时支持，您将需要[Developer Tools for Visual Studio](http://www.oracle.com/technetwork/developer-tools/visual-studio/overview/index.html)。 其他官方的 Oracle 产品，包括 Oracle 即时客户端，可通过 NuGet 包管理器。  可以按照中的说明下载 Oracle 示例架构[Oracle 联机文档](http://docs.oracle.com/cd/E11882_01/server.112/e10831/toc.htm)。  
  
### <a name="mysql"></a>MySQL  
 MySQL 是企业和网站中广泛使用的受欢迎的开源数据库系统。 有关 MySQL，MySQL for Visual Studio 和相关的产品的下载在[Windows 上的 MySQL](http://www.mysql.com/why-mysql/windows/)。  第三方提供各种 Visual Studio 扩展和独立的管理应用程序的 MySQL。 您可以浏览产品/服务在 NuGet 包管理器 (**工具** > **NuGet 包管理器** > **为解决方案管理 NuGet 包**).  
  
### <a name="postgresql"></a>postgresql  
 PostgreSQL 是一个免费的开源对象关系数据库系统。 若要在 Windows 上安装它，您可以从下载[PostgreSQL 下载页](http://www.postgresql.org/download/windows/)。  此外可以从源代码构建 PostgreSQL。  PostgreSQL core 系统包括一个 C 语言接口。 许多第三方提供来自.NET 应用程序使用 PostgreSQL 的 NuGet 包。  您可以浏览产品/服务在 NuGet 包管理器 (**工具** > **NuGet 包管理器** > **为解决方案管理 NuGet 包**). 可能是最受欢迎的包提供的[npgsql.org](http://www.npgsql.org)。  
  
### <a name="sqlite"></a>SQLite  
 SQLite 是嵌入的 SQL 数据库引擎应用程序自身的进程中运行。 你可以下载它从[SQLite 下载页](http://www.sqlite.org/download.html)。 SQLite 的许多第三方 NuGet 包，还提供。 您可以浏览产品/服务在 NuGet 包管理器 (**工具** > **NuGet 包管理器** > **为解决方案管理 NuGet 包**).  
  
### <a name="firebird"></a>Firebird  
 Firebird 是一个开放源代码 SQL 数据库系统。 你可以下载它从[Firebird 下载页](http://firebirdsql.org/en/downloads/)。 ADO.NET 数据提供程序是通过 NuGet 包管理器。  
  
## <a name="see-also"></a>请参阅  
 [如何确定 SQL Server 及其组件的版本](http://support.microsoft.com/kb/321185)
