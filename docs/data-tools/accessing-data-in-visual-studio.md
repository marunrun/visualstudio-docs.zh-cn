---
title: 数据访问和工具
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- "80025080"
helpviewer_keywords:
- data [Visual Studio]
- data access [Visual Studio]
- data [C#]
- ADO.NET, data access
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 5403803a4da0821978a8c6bbfc31e45c31104640
ms.sourcegitcommit: 5483e399f14fb01f528b3b194474778fd6f59fa6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66715274"
---
# <a name="access-data-in-visual-studio"></a>在 Visual Studio 中访问数据

在 Visual Studio 中，可以创建连接到几乎任何数据库产品或服务，任何格式，任何位置中的数据的应用程序 — 在本地计算机上，在本地网络，或在公共、 专用或混合云。

JavaScript、 Python、 PHP、 Ruby 中的应用程序或C++，就像任何其他内容，方法是获取库编写的代码连接到的数据。 对于.NET 应用程序，Visual Studio 提供可用于浏览数据源、 创建对象模型来存储和处理数据在内存中，并将数据绑定到用户界面的工具。 Microsoft Azure 提供了用于.NET、 Java、 Node.js、 PHP、 Python、 Ruby 和移动应用和 Visual Studio 中的工具连接到 Azure 存储 Sdk。

以下列表显示了从 Visual Studio 只需几个可以使用许多数据库和存储系统。 [Microsoft Azure](https://azure.microsoft.com/)产品是数据服务，包括所有预配和管理的基础数据存储区。 **Azure 开发**中的工作负荷[Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)使您能够直接从 Visual Studio 的 Azure 数据存储。

![Azure 开发工作负载](media/azure-development-workload.png)

可以在本地计算机上，在本地网络，或在 Microsoft Azure 虚拟机上托管的其他 SQL 和 NoSQL 数据库产品此处列出的大多数。 如果托管在 Microsoft Azure 虚拟机中的数据库，您负责管理数据库本身。

**Microsoft Azure**

- SQL 数据库
- Azure Cosmos DB
- 存储 （blob、 表、 队列、 文件）
- SQL 数据仓库
- SQL Server Stretch Database
- StorSimple
- 更多内容...

**SQL**

- SQL Server 2005-2016 （包括 Express 和 LocalDB）
- Firebird
- MariaDB
- MySQL
- Oracle
- postgresql
- SQLite
- 更多内容...

**NoSQL**

- Apache Cassandra
- CouchDB
- MongoDB
- NDatabase
- OrientDB |
- RavenDB
- VelocityDB
- 更多内容...

::: moniker range="vs-2017"

许多数据库供应商和第三方通过 NuGet 包支持 Visual Studio 集成。 在 nuget.org 上或通过 NuGet 包管理器在 Visual Studio 中，可以浏览产品/服务 (**工具** > **NuGet 包管理器** > **管理 NuGet解决方案包**)。 其他数据库产品与 Visual Studio 集成扩展。 您可以浏览这些产品/服务[Visual Studio Marketplace](https://marketplace.visualstudio.com/)或导航到**工具** > **扩展和更新**，然后选择**联机**对话框的左窗格中。 有关详细信息，请参阅[Visual Studio 的兼容的数据库系统](../data-tools/installing-database-systems-tools-and-samples.md)。

::: moniker-end

::: moniker range=">=vs-2019"

许多数据库供应商和第三方通过 NuGet 包支持 Visual Studio 集成。 在 nuget.org 上或通过 NuGet 包管理器在 Visual Studio 中，可以浏览产品/服务 (**工具** > **NuGet 包管理器** > **管理 NuGet解决方案包**)。 其他数据库产品与 Visual Studio 集成扩展。 您可以浏览这些产品/服务[Visual Studio Marketplace](https://marketplace.visualstudio.com/)或导航到**扩展** > **管理扩展**，然后选择**联机**对话框的左窗格中。 有关详细信息，请参阅[Visual Studio 的兼容的数据库系统](../data-tools/installing-database-systems-tools-and-samples.md)。

::: moniker-end

> [!NOTE]
> 对 SQL Server 2005 的延长的支持已于 2016 年 4 月 12 日结束。 就数据工具在 Visual Studio 2015 及更高版本将继续使用 SQL Server 2005 不能保证。 有关详细信息，请参阅[SQL Server 2005 的最终支持公告](https://www.microsoft.com/sql-server/sql-server-2005)。

## <a name="net-languages"></a>.NET 语言

所有.NET 数据访问，包括在.NET Core 中都基于 ADO.NET 中，为访问任何类型的数据源、 关系和非关系定义一个接口的一组类。 Visual Studio 具有几个工具和设计人员可使用 ADO.NET 来帮助您连接到数据库，操作数据，并向用户呈现数据。 在本部分中的文档介绍如何使用这些工具。 您还可以直接对 ADO.NET 命令对象进行编程。 直接调用 ADO.NET Api 的详细信息，请参阅[ADO.NET](/dotnet/framework/data/adonet/index)。

与 ASP.NET 相关的数据访问文档，请参阅[使用数据](https://www.asp.net/web-forms/overview/presenting-and-managing-data)ASP.NET 站点上。 使用 ASP.NET MVC 中使用实体框架的教程，请参阅[开始使用 Entity Framework 6 Code First 通过 MVC 5](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application)。

C# 或 Visual Basic 中的通用 Windows 平台 (UWP) 应用可以使用 Microsoft Azure SDK for.NET 访问 Azure 存储和其他 Azure 服务。 Windows.Web.HttpClient 类，与任何 RESTful 服务的通信。 有关详细信息，请参阅[如何连接到 HTTP 服务器使用 Windows.Web.Http](https://msdn.microsoft.com/library/windows/apps/dn469430.aspx)。

对于本地计算机上的数据存储，建议的方法是使用 SQLite，作为应用程序在同一进程中运行。 如果需要一个对象关系映射 (ORM) 层，可以使用实体框架。 有关详细信息，请参阅[数据访问](/windows/uwp/data-access/index)Windows 开发人员中心中。

如果要连接到 Azure 服务，请务必下载最新[Azure SDK 工具](https://azure.microsoft.com/downloads/)。

### <a name="data-providers"></a>数据提供程序

若要用于在 ADO.NET 中的数据库，它必须能够自定义*ADO.NET 数据提供程序*或其他必须公开一个 ODBC 或 OLE DB 接口。 Microsoft 提供了[ADO.NET 数据提供程序的列表](https://docs.microsoft.com/dotnet/framework/data/adonet/ado-net-overview)SQL Server 产品以及 ODBC 和 OLE DB 访问接口。

### <a name="data-modeling"></a>数据建模

在.NET 中，您有用于建模和操作在内存中的数据后已从数据源中检索的三个选择：

[实体框架](../data-tools/entity-data-model-tools-in-visual-studio.md)首选的 Microsoft ORM 技术。 您可以使用它到针对关系数据进行编程作为一流的.NET 对象。 对于新应用程序，它应为默认的第一个选项，需要一个模型时。 它需要从基础 ADO.NET 提供程序的自定义支持。

[LINQ to SQL](../data-tools/linq-to-sql-tools-in-visual-studio2.md)的早期生成的对象关系映射器。 它非常适合不太复杂的方案，但不再处于积极开发阶段。

[数据集](../data-tools/dataset-tools-in-visual-studio.md)最旧的三种建模技术。 它主要用于快速开发"forms over data"应用程序将不处理大量数据或执行复杂的查询或转换在其中。 数据集对象包括逻辑上远远超出了.NET 对象类似于 SQL 数据库对象的 DataTable 和 DataRow 对象。 对于相对简单的应用程序基于 SQL 的数据源，数据集可能仍是一个不错的选择。

没有任何要求使用任何这些技术。 在某些情况下，尤其是在性能很重要，只需可用 DataReader 对象来从数据库读取并将所需的值复制到一个集合对象，如列表\<T >。

## <a name="native-c"></a>本机 C++

C++连接到 SQL Server 的应用程序应使用[Microsoft® ODBC Driver 13.1 for SQL Server](https://www.microsoft.com/download/details.aspx?id=53339)在大多数情况下。 如果链接服务器，则 OLE DB 是必要和为此，您使用[SQL Server Native Client](/sql/relational-databases/native-client/sql-server-native-client)。 可以使用访问其他数据库[ODBC](https://docs.microsoft.com/sql/odbc/microsoft-open-database-connectivity-odbc?view=sql-server-2017)或 OLE DB 驱动程序直接。 ODBC 是当前的标准数据库接口，但大多数数据库系统提供无法通过 ODBC 接口访问的自定义功能。 OLE DB 是一项传统 COM 数据访问技术，是仍受支持但不是建议用于新的应用程序。 有关详细信息，请参阅[视觉对象中的数据访问C++ ](/cpp/data/data-access-in-cpp)。

C++使用 REST 服务的程序可以使用[ C++ REST SDK](https://github.com/Microsoft/cpprestsdk)。

C++使用 Microsoft Azure 存储空间的程序可以使用[Microsoft Azure 存储客户端](https://www.nuget.org/packages/Microsoft.Azure.Storage.CPP)。

数据建模&mdash;Visual Studio 不提供的 ORM 层; 为C++。 [ODB](https://www.codesynthesis.com/products/odb/)是为受欢迎的开源 ORM C++。

若要详细了解连接到数据库，从C++应用程序，请参阅[用于 Visual Studio 数据工具C++ ](../data-tools/visual-studio-data-tools-for-cpp.md)。 详细了解旧版 VisualC++数据访问技术，请参阅[数据访问](/cpp/data/data-access-in-cpp)。

## <a name="javascript"></a>JavaScript

[Visual Studio 中的 JavaScript](/scripting/javascript/javascript-language-reference)是一流的语言，用于构建跨平台应用、 UWP 应用、 云服务、 网站和 web 应用。 可以使用 Bower、 Grunt、 Gulp、 npm 和 Visual Studio 中的从 NuGet 安装你最喜欢的 JavaScript 库和数据库产品。 通过下载 Sdk 从连接到 Azure 存储和服务[Azure 网站](https://azure.microsoft.com/)。 Edge.js 是服务器端 JavaScript (Node.js) 连接到 ADO.NET 数据源的库。

## <a name="python"></a>Python

安装[Visual Studio 中的 Python 支持](../python/overview-of-python-tools-for-visual-studio.md)创建 Python 应用程序。 Azure 文档提供了几个教程，连接到数据，其中包括：

- [Django 和在 Azure 上的 SQL 数据库](/azure/app-service/app-service-web-get-started-python)
- [Django 和 MySQL 在 Azure 上](/azure/app-service-web/web-sites-python-ptvs-django-mysql)
- 适用于[blob](/azure/storage/blobs/storage-quickstart-blobs-python)，[文件](/azure/storage/files/storage-python-how-to-use-file-storage)，[队列](/azure/storage/queues/storage-python-how-to-use-queue-storage)，以及[表 (Cosmo DB)](/azure/cosmos-db/table-storage-how-to-use-python)。

## <a name="related-topics"></a>相关主题

[Microsoft AI 平台](https://azure.microsoft.com/overview/ai-platform/?v=17.42w)&mdash;介绍了 Microsoft 智能云，包括 Cortana Analytics 套件和物联网的支持。

[Microsoft Azure 存储空间](/azure/storage/)&mdash;介绍 Azure 存储，以及如何使用 Azure blob、 表、 队列和文件创建应用程序。

[Azure SQL 数据库](/azure/sql-database/)&mdash;介绍如何连接到 Azure SQL 数据库，关系数据库即服务。

[SQL Server Data Tools](/sql/ssdt/download-sql-server-data-tools-ssdt)&mdash;描述简化设计，探索、 测试和部署的数据连接的应用程序和数据库的工具。

[ADO.NET](/dotnet/framework/data/adonet/index)&mdash;介绍 ADO.NET 体系结构以及如何使用 ADO.NET 类来管理应用程序数据和与数据源和 XML 进行交互。

[ADO.NET 实体框架](https://docs.microsoft.com/ef/ef6/)&mdash;介绍如何创建数据应用程序，使开发人员针对概念模型而不是直接针对关系数据库进行编程。

[WCF 数据服务 4.5](/dotnet/framework/data/wcf/index)&mdash;介绍如何使用[!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)]部署 web 或 intranet 上的数据服务，实现[开放数据协议 (OData)](https://www.odata.org/)。

[Office 解决方案中的数据](../vsto/data-in-office-solutions.md)&mdash;包含指向这些主题介绍了数据在 Office 解决方案中的工作方式。 这包括有关面向架构编程、 数据缓存和服务器端数据访问的信息。

[LINQ （语言集成查询）](/dotnet/csharp/linq/)&mdash;介绍内置 C# 和 Visual Basic 中，以及常见模型用于查询关系数据库、 XML 文档、 数据集和内存中集合的查询功能。

[Visual Studio 中的 XML 工具](../xml-tools/xml-tools-in-visual-studio.md)&mdash;讨论使用 XML 数据，调试 XSLT.NET XML 功能，以及 XML 查询的体系结构。

[XML 文档和数据](/dotnet/standard/data/xml/index)&mdash;提供简要介绍了如何全面、 集成的一组类，使用 XML 文档和.NET 中的数据。
