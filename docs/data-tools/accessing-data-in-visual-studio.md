---
title: 在 Visual Studio 中处理数据
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- data [Visual Studio]
- data access [Visual Studio]
- data [C#]
- ADO.NET, data access
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 7c7aa1544f998a88424c0087fadceab63757d23b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "77272086"
---
# <a name="work-with-data-in-visual-studio"></a>在 Visual Studio 中处理数据

在 Visual Studio 中，你可以创建应用程序，这些应用程序在任何格式、任何位置、本地计算机上、在本地计算机上或在公共、私有或混合云中连接到数据。

对于 JavaScript、Python、PHP、Ruby 或 c + + 中的应用程序，你可以通过获取库和编写代码来连接到你执行任何其他操作等数据。 对于 .NET 应用程序，Visual Studio 提供的工具可用于浏览数据源、创建对象模型以便在内存中存储和处理数据，以及将数据绑定到用户界面。 Microsoft Azure 提供适用于 .NET、Java、Node.js、PHP、Python、Ruby 和移动应用的 Sdk 以及 Visual Studio 中用于连接到 Azure 存储的工具。

::: moniker range="vs-2017"
以下列表仅显示了可从 Visual Studio 中使用的多个数据库和存储系统中的几个。 [Microsoft Azure](https://azure.microsoft.com/)产品是数据服务，其中包括基础数据存储的所有预配和管理。 利用[Visual studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)中的**azure 开发**工作负载，你可以直接从 Visual studio 使用 azure 数据存储。
::: moniker-end
::: moniker range=">=vs-2019"
以下列表仅显示了可从 Visual Studio 中使用的多个数据库和存储系统中的几个。 [Microsoft Azure](https://azure.microsoft.com/)产品是数据服务，其中包括基础数据存储的所有预配和管理。 利用[Visual studio 2019](https://visualstudio.microsoft.com/downloads)中的**azure 开发**工作负载，你可以直接从 Visual studio 使用 azure 数据存储。
::: moniker-end

![Azure 开发工作负载](media/azure-development-workload.png)

此处列出的大多数其他 SQL 和 NoSQL 数据库产品都可以托管在本地计算机、本地网络或虚拟机上的 Microsoft Azure 中。 如果在 Microsoft Azure 虚拟机中托管数据库，则需要负责管理数据库本身。

**Microsoft Azure**

- SQL 数据库
- Azure Cosmos DB
- 存储 (blob、表、队列、文件) 
- SQL 数据仓库
- SQL Server Stretch Database
- StorSimple
- 等等。

**SQL**

- SQL Server 2005-2016 (包括 Express 和 LocalDB) 
- Firebird
- MariaDB
- MySQL
- Oracle
- PostgreSQL
- SQLite
- 等等。

**NoSQL**

- Apache Cassandra
- CouchDB
- MongoDB
- NDatabase
- OrientDB |
- RavenDB
- VelocityDB
- 等等。

::: moniker range="vs-2017"

许多数据库供应商和第三方支持通过 NuGet 包与 Visual Studio 集成。 你可以在 nuget.org 上浏览产品或通过 Visual Studio 中的 nuget 包管理器 (**工具**"  >  **nuget 包管理器**"  >  **管理解决方案) 的 nuget 包**。 其他数据库产品与 Visual Studio 集成以作为扩展。 可以在[Visual Studio Marketplace](https://marketplace.visualstudio.com/)中浏览这些产品/服务，或者导航到 "**工具**"  >  "**扩展和更新**"，然后在对话框的左窗格中选择 "**联机**"。 有关详细信息，请参阅 [Visual Studio 的兼容数据库系统](../data-tools/installing-database-systems-tools-and-samples.md)。

::: moniker-end

::: moniker range=">=vs-2019"

许多数据库供应商和第三方支持通过 NuGet 包与 Visual Studio 集成。 你可以在 nuget.org 上浏览产品或通过 Visual Studio 中的 nuget 包管理器 (**工具**"  >  **nuget 包管理器**"  >  **管理解决方案) 的 nuget 包**。 其他数据库产品与 Visual Studio 集成以作为扩展。 你可以在[Visual Studio Marketplace](https://marketplace.visualstudio.com/)中浏览这些产品，或者导航到 "**扩展**" "  >  **管理扩展**"，然后在对话框的左窗格中选择 "**联机**"。 有关详细信息，请参阅 [Visual Studio 的兼容数据库系统](../data-tools/installing-database-systems-tools-and-samples.md)。

::: moniker-end

> [!NOTE]
> 对 SQL Server 2005 的延长支持已于 2016 年 4 月 12 日结束。 不保证 Visual Studio 2015 和更高版本中的数据工具将继续与 SQL Server 2005 一起使用。 有关详细信息，请参阅 [SQL Server 2005 的支持终止公告](https://www.microsoft.com/sql-server/sql-server-2005)。

## <a name="net-languages"></a>.NET 语言

所有 .NET 数据访问（包括在 .NET Core 中）都基于 ADO.NET，这是一组类，用于定义用于访问任何类型数据源（关系数据源和非关系数据源）的接口。 Visual Studio 有多个工具和设计器，可与 ADO.NET 配合使用，帮助你连接到数据库、操作数据，以及向用户提供数据。 本部分中的文档介绍了如何使用这些工具。 你还可以对 ADO.NET 命令对象直接编程。 有关直接调用 ADO.NET Api 的详细信息，请参阅 [ADO.NET](/dotnet/framework/data/adonet/index)。

有关与 ASP.NET 相关的数据访问文档，请参阅使用 ASP.NET 站点上的 [数据](https://www.asp.net/web-forms/overview/presenting-and-managing-data) 。 有关将实体框架与 ASP.NET MVC 配合使用的教程，请参阅使用 [mvc 5 Code First 实体框架6入门](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application)。

通用 Windows 平台 (UWP) c # 中的应用或 Visual Basic 可以使用用于 .NET 的 Microsoft Azure SDK 访问 Azure 存储和其他 Azure 服务。 HttpClient 类启用与任何 RESTful 服务的通信。 有关详细信息，请参阅 [如何使用 Windows 连接到 http 服务器](https://msdn.microsoft.com/library/windows/apps/dn469430.aspx)。

对于本地计算机上的数据存储，推荐的方法是使用 SQLite，此方法在应用程序的进程中运行。 如果需要 (ORM) 层的对象关系映射，则可以使用实体框架。 有关详细信息，请参阅 Windows 开发人员中心中的 [数据访问](/windows/uwp/data-access/index) 。

如果要连接到 Azure 服务，请确保下载最新的 [AZURE SDK 工具](https://azure.microsoft.com/downloads/)。

### <a name="data-providers"></a>数据提供程序

对于在 ADO.NET 中使用的数据库，该数据库必须具有自定义 *ADO.NET 数据访问* 接口，否则必须公开 ODBC 或 OLE DB 接口。 Microsoft 提供 SQL Server 产品以及 ODBC 和 OLE DB 提供程序的 [ADO.NET 数据提供程序列表](/dotnet/framework/data/adonet/ado-net-overview) 。

### <a name="data-modeling"></a>数据建模

在 .NET 中，你有三种方法可以在从数据源中检索数据后在内存中对数据进行建模和操作：

[实体框架](../data-tools/entity-data-model-tools-in-visual-studio.md) 首选的 Microsoft ORM 技术。 您可以使用它来针对关系数据编程，作为第一类 .NET 对象。 对于新应用程序，它应该是需要模型时的默认首选项。 它需要基础 ADO.NET 提供程序的自定义支持。

[LINQ to SQL](../data-tools/linq-to-sql-tools-in-visual-studio2.md) 早期代对象关系映射器。 它适用于不太复杂的方案，但不再处于活动状态。

[数据集](../data-tools/dataset-tools-in-visual-studio.md) 最早的三个建模技术。 它主要设计用于快速开发 "窗体超过数据" 应用程序，在这些应用程序中，您不会处理大量数据或执行复杂的查询或转换。 DataSet 对象包含在逻辑上类似于 SQL 数据库对象的 DataTable 和 DataRow 对象比 .NET 对象多很多。 对于基于 SQL 数据源的相对简单的应用程序，数据集可能仍是一个不错的选择。

不需要使用其中的任何一种技术。 在某些情况下，尤其是在性能至关重要的情况下，只需使用 DataReader 对象从数据库中读取数据，并将需要的值复制到集合对象（如 List） \<T> 。

## <a name="native-c"></a>本机 C++

在大多数情况下，连接到 SQL Server 的 c + + 应用程序应使用 [Microsoft® ODBC 驱动程序13.1 进行 SQL Server](https://www.microsoft.com/download/details.aspx?id=53339) 。 如果服务器已链接，则 OLE DB 是必需的，并且你使用 [SQL Server Native Client](/sql/relational-databases/native-client/sql-server-native-client)。 您可以直接使用 [ODBC](/sql/odbc/microsoft-open-database-connectivity-odbc?view=sql-server-2017) 或 OLE DB 驱动程序来访问其他数据库。 ODBC 是当前的标准数据库接口，但大多数数据库系统都提供无法通过 ODBC 接口访问的自定义功能。 OLE DB 是一种旧的 COM 数据访问技术，仍受支持，但不建议用于新应用程序。 有关详细信息，请参阅 [Visual C++ 中的数据访问](/cpp/data/data-access-in-cpp)。

使用 REST 服务的 c + + 程序可使用 [c + + REST SDK](https://github.com/Microsoft/cpprestsdk)。

使用 Microsoft Azure 存储的 c + + 程序可以使用 [Microsoft Azure 存储客户端](https://www.nuget.org/packages/Microsoft.Azure.Storage.CPP)。

数据建模 &mdash; Visual Studio 不提供 c + + 的 ORM 层。 [ODB](https://www.codesynthesis.com/products/odb/) 是适用于 c + + 的常用开源 ORM。

若要详细了解如何从 c + + 应用程序连接到数据库，请参阅 [Visual Studio data tools For c + +](../data-tools/visual-studio-data-tools-for-cpp.md)。 有关旧 Visual C++ 数据访问技术的详细信息，请参阅 [数据访问](/cpp/data/data-access-in-cpp)。

## <a name="javascript"></a>Javascript

[Visual Studio 中的 JavaScript](/scripting/javascript/javascript-language-reference) 是一种用于构建跨平台应用、UWP 应用、云服务、网站和 web 应用的一流语言。 你可以从 Visual Studio 中使用 Bower、Grunt、Gulp、npm 和 NuGet 来安装你最喜欢的 JavaScript 库和数据库产品。 通过从 [azure 网站](https://azure.microsoft.com/)下载 sdk 来连接到 azure 存储和服务。 Edge.js 是将服务器端 JavaScript ( # A1) 连接到 ADO.NET 数据源的库。

## <a name="python"></a>Python

[在 Visual Studio 中安装 python 支持](../python/overview-of-python-tools-for-visual-studio.md)以创建 python 应用程序。 Azure 文档包含几个有关连接到数据的教程，其中包括：

- [Azure 上的 Django 和 SQL 数据库](/azure/app-service/app-service-web-get-started-python)
- [Azure 上的 Django 和 MySQL](/azure/app-service-web/web-sites-python-ptvs-django-mysql)
- [ (COSMO DB) ](/azure/cosmos-db/table-storage-how-to-use-python)使用[blob](/azure/storage/blobs/storage-quickstart-blobs-python)、[文件](/azure/storage/files/storage-python-how-to-use-file-storage)、[队列](/azure/storage/queues/storage-python-how-to-use-queue-storage)和表。

## <a name="related-topics"></a>相关主题

[MICROSOFT AI 平台](https://azure.microsoft.com/overview/ai-platform/?v=17.42w) &mdash;提供 Microsoft 智能云的简介，包括 Cortana Analytics Suite 和对物联网的支持。

[Microsoft Azure 存储](/azure/storage/) &mdash;介绍 Azure 存储，以及如何使用 Azure blob、表、队列和文件创建应用程序。

[AZURE SQL 数据库](/azure/sql-database/) &mdash;介绍如何连接到 Azure SQL 数据库（一种关系数据库即服务）。

[SQL Server Data Tools](/sql/ssdt/download-sql-server-data-tools-ssdt) &mdash;介绍简化数据连接的应用程序和数据库的设计、探索、测试和部署的工具。

[ADO.NET](/dotnet/framework/data/adonet/index) &mdash;介绍 ADO.NET 的体系结构，以及如何使用 ADO.NET 类来管理应用程序数据以及与数据源和 XML 进行交互。

[ADO.NET 实体框架](/ef/ef6/) &mdash;介绍如何创建允许开发人员针对概念模型而不是直接针对关系数据库进行编程的数据应用程序。

[WCF 数据服务 4.5](/dotnet/framework/data/wcf/index) &mdash;描述如何使用 [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)] 在实现[Open Data Protocol (OData) ](https://www.odata.org/)的 web 或 intranet 上部署数据服务。

[Office 解决方案](../vsto/data-in-office-solutions.md) &mdash; 中的数据包含指向一些主题的链接，这些主题说明了如何在 Office 解决方案中使用数据。 这包括有关面向架构的编程、数据缓存和服务器端数据访问的信息。

[LINQ (语言集成查询) ](/dotnet/csharp/linq/) &mdash;介绍 c # 和 Visual Basic 中内置的查询功能，以及用于查询关系数据库、XML 文档、数据集和内存中集合的通用模型。

[Visual Studio](../xml-tools/xml-tools-in-visual-studio.md) &mdash; 中的 XML 工具讨论如何使用 XML 数据、调试 XSLT、.NET XML 功能和 XML 查询的体系结构。

[XML 文档和数据](/dotnet/standard/data/xml/index) &mdash;概述了一组全面的集成类，这些类可用于 .NET 中的 XML 文档和数据。
