---
title: 访问数据
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
f1_keywords:
- "80025080"
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- data [Visual Studio]
- data access [Visual Studio]
- data [C#]
- ADO.NET, data access
ms.assetid: 9812a6d5-23d2-4427-8b98-70a2abfec3bc
caps.latest.revision: 103
author: jillre
ms.author: jillfra
manager: jillfra
robots: noindex,nofollow
ms.openlocfilehash: 158bc4c2fc7734957c7d3e946390ab1339a322ba
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299438"
---
# <a name="accessing-data-in-visual-studio"></a>在 Visual Studio 中访问数据
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 Visual Studio 中，你可以创建应用程序，这些应用程序在任何格式、任何位置、本地计算机上、在本地计算机上或在公共、私有或混合云中连接到数据。

 对于 JavaScript、Python、PHP、Ruby 或C++中的应用程序，你可以通过获取库和编写代码来连接到你执行任何其他操作的数据。 对于 .NET 应用程序，Visual Studio 提供的工具可用于浏览数据源、创建对象模型以便在内存中存储和处理数据，以及将数据绑定到用户界面。     Microsoft Azure 提供适用于 .NET、Java、node.js、PHP、Python、Ruby 和移动应用的 Sdk 以及 Visual Studio 中用于连接到 Azure 存储的工具。

 以下列表仅显示了可从 Visual Studio 中使用的多个数据库和存储系统中的几个。 [Microsoft Azure](https://azure.microsoft.com/)产品是数据服务，其中包括基础数据存储的所有预配和管理。  [Azure Tools For Visual studio](https://www.visualstudio.com/features/azure-tools-vs.aspx)是一个可选组件，使你能够直接从 Visual Studio 使用 azure 数据存储。 此处列出的大多数其他 SQL 和 NoSQL 数据库产品都可以托管在本地计算机、本地网络或虚拟机上的 Microsoft Azure 中。 在此方案中，你负责管理数据库本身。

 **Microsoft Azure**

||||
|-|-|-|
|SQL 数据库|DocumentDB|存储（blob、表、队列、文件）|
|SQL 数据仓库|SQL Server Stretch Database|StorSimple|

 更多内容...

 **SQL**

||||
|-|-|-|
|SQL Server 2005 –2016，包括 Express 和 LocalDB|Firebird|MariaDB|
|MySQL|Oracle|PostgreSQL|
|SQLite|||

 更多内容...

 **NoSQL**

||||
|-|-|-|
|Apache Cassandra|CouchDB|MongoDB|
|NDatabase|OrientDB|RavenDB|
|VelocityDB|||

 更多内容...

 许多数据库供应商和第三方支持通过 NuGet 包与 Visual Studio 集成。 可以通过 Visual Studio 中的 NuGet 包管理器或 Visual Studio 中的 NuGet 包管理器来浏览 nuget.org （**Tools** > **Nuget 包管理器** > **管理解决方案的 nuget 包**）。 其他数据库产品与 Visual Studio 集成以作为扩展。   通过导航到 "**工具**" > "**扩展和更新**"，然后在对话框的左窗格中选择 "**联机**"，可以在 Visual Studio 库中浏览这些产品/服务。  有关详细信息，请参阅[安装数据库系统、工具和示例](../data-tools/installing-database-systems-tools-and-samples.md)。

> [!NOTE]
> 2005年4月 12 2016 日结束对 SQL Server 的扩展支持。   不保证 Visual Studio 2015 和更高版本中的数据工具在此日期后继续与 SQL Server 2005 一起工作。 有关详细信息，请参阅[SQL Server 2005 的支持终止公告](https://www.microsoft.com/sql-server/sql-server-2005)。

### <a name="net-languages"></a>.NET 语言
 所有 .NET 数据访问（包括在 .NET Core 中）都基于 ADO.NET，这是一组类，用于定义用于访问任何类型数据源（关系数据源和非关系数据源）的接口。 Visual Studio 有多个工具和设计器，可与 ADO.NET 配合使用，帮助你连接到数据库、操作数据，以及向用户提供数据。 本部分中的文档介绍了如何使用这些工具。 你还可以对 ADO.NET 命令对象直接编程。 有关直接调用 ADO.NET Api 的详细信息，请参阅 MSDN Library 中的[ADO.NET](https://msdn.microsoft.com/library/e80y5yhx\(v=vs.110\).aspx) 。

 有关专门与 ASP.NET 相关的数据访问文档，请参阅使用 ASP.NET 站点上的[数据](https://docs.microsoft.com/aspnet/web-forms/overview/presenting-and-managing-data/)。 有关将实体框架与 ASP.NET MVC 配合使用的教程，请参阅使用[mvc 5 Code First 实体框架6入门](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application)。

 或 Visual Basic 中C#的通用 WINDOWS 平台（UWP）应用可以使用用于 .NET 的 Microsoft Azure SDK 访问 azure 存储和其他 azure 服务。 HttpClient 类启用与任何 RESTful 服务的通信。 有关详细信息，请参阅[如何使用 Windows 连接到 http 服务器](https://msdn.microsoft.com/library/windows/apps/dn469430.aspx)。

 对于本地计算机上的数据存储，推荐的方法是使用 SQLite，此方法在应用程序的进程中运行。 如果需要对象关系映射（ORM）层，则可以使用实体框架。 有关详细信息，请参阅 Windows 开发人员中心中的[数据访问](https://msdn.microsoft.com/windows/uwp/data-access/index)。

 如果要连接到 Azure 服务，请确保下载最新的[AZURE SDK 工具](https://azure.microsoft.com/downloads/)。

#### <a name="data-providers"></a>数据提供程序
 对于在 ADO.NET 中使用的数据库，该数据库必须具有自定义*ADO.NET 数据访问*接口，否则必须公开 ODBC 或 OLE DB 接口。 Microsoft 提供 SQL Server 产品以及 ODBC 和 OLE DB 提供程序的[ADO.NET 数据提供程序列表](https://msdn.microsoft.com/data/dd363565)。

#### <a name="data-modeling"></a>数据建模
 在 .NET 中，你有三种方法可以在从数据源中检索数据后在内存中对数据进行建模和操作：

 实体框架首选的 Microsoft ORM 技术。 您可以使用它来针对关系数据编程，作为第一类 .NET 对象。 对于新应用程序，它应该是需要模型时的默认首选项。 它需要基础 ADO.NET 提供程序的自定义支持。

 LINQ to SQL 早期代对象关系映射器。 它适用于不太复杂的方案，但不再处于活动状态。

 数据集最早的三个建模技术。 它主要设计用于快速开发 "窗体超过数据" 应用程序，在这些应用程序中，您不会处理大量数据或执行复杂的查询或转换。 DataSet 对象包含在逻辑上类似于 SQL 数据库对象的 DataTable 和 DataRow 对象比 .NET 对象多很多。 对于基于 SQL 数据源的相对简单的应用程序，数据集可能仍是一个不错的选择。

 不需要使用其中的任何一种技术。 在某些情况下，尤其是在性能至关重要的情况下，你只需使用 DataReader 对象从数据库中读取数据，并将所需的值复制到集合对象（如 List\<T > 中）。

### <a name="native-c"></a>本机 C++
 C++连接到 SQL Server 的应用程序应使用[SQL Server Native Client](https://msdn.microsoft.com/sqlserver/aa937733.aspx)。 您可以直接使用[ODBC](https://msdn.microsoft.com/library/ms710252\(v=vs.85\).aspx)或 OLE DB 驱动程序来访问其他数据库。 ODBC 是当前的标准数据库接口，但大多数数据库系统都提供无法通过 ODBC 接口访问的自定义功能。  OLE DB 是一种旧的 COM 数据访问技术，仍受支持，但不建议用于新应用程序。  有关详细信息，请参阅[数据访问](https://msdn.microsoft.com/library/a9455752-39c4-4457-b14e-197772d3df0b)。

 C++使用 rest 服务的程序可以使用[ C++ rest SDK](https://github.com/Microsoft/cpprestsdk)。

 C++与 Microsoft Azure 存储一起使用的程序可以使用[Microsoft Azure 存储客户端](https://www.nuget.org/packages/wastorage)。

#### <a name="data-modeling"></a>数据建模
 Visual Studio 不提供的C++ORM 层。  [ODB](https://www.codesynthesis.com/products/odb/)是适用于的C++常用开源 ORM。

 有关旧的视觉C++数据访问技术的详细信息，请参阅[数据访问](https://msdn.microsoft.com/library/a9455752-39c4-4457-b14e-197772d3df0b)

### <a name="javascript"></a>JavaScript
 [Visual Studio 中的 JavaScript](https://msdn.microsoft.com/library/hh334522.aspx)是一种用于构建跨平台应用、UWP 应用、云服务、网站和 web 应用的一流语言。 你可以从 Visual Studio 中使用 Bower、Grunt、Gulp、npm 和 NuGet 来安装你最喜欢的 JavaScript 库和数据库产品。 通过从[azure 网站](https://azure.microsoft.com/)下载 sdk 来连接到 azure 存储和服务。  Edge 是将服务器端 JavaScript （node.js）连接到 ADO.NET 数据源的库。

### <a name="python"></a>Python
 随你最喜欢的 Python 框架一起安装[针对 Visual Studio 的 Python 工具](http://microsoft.github.io/PTVS/)，以创建 CPython 或 IronPython （.net）应用程序。  针对 Visual Studio 的 Python 工具网站包含多个有关连接到数据的教程，包括 azure[上的 Django 和 SQL 数据库](https://github.com/Microsoft/PTVS/wiki/Django-and-SQL-Database-on-Azure)、azure 上的[Django 和 MySQL](https://github.com/Microsoft/PTVS/wiki/Django-and-MySQL-on-Azure)以及[Azure 上的瓶和 MongoDB](https://github.com/Microsoft/PTVS/wiki/Bottle-and-MongoDB-on-Azure)。

## <a name="in-this-section"></a>本节内容
 [安装数据库系统、工具和示例](../data-tools/installing-database-systems-tools-and-samples.md)讨论如何获取数据库产品以及支持它们的 Visual Studio 扩展插件或驱动程序，以及在哪里可以找到用于试验和学习目的的示例数据库。

 [适用于 .net 的 Visual Studio 数据工具](https://msdn.microsoft.com/6b145922-2f00-47db-befc-bf351b4809a1)介绍如何使用 Visual Studio 工具窗口连接到数据源、创建数据集或实体框架模型，以及如何将数据绑定到用户界面控件。

## <a name="related-topics"></a>相关主题
 [数据、设备和分析](https://msdn.microsoft.com/data-and-devices)提供 Microsoft 智能云的简介，包括 Cortana Analytics Suite 和对物联网的支持。

 [Microsoft Azure 存储](/azure/storage/)介绍 Azure 存储，以及如何使用 Azure blob、表、队列和文件创建应用程序。

 [AZURE SQL 数据库](https://azure.microsoft.com/documentation/services/sql-database/)介绍如何连接到 Azure SQL 数据库（一种关系数据库即服务）。

 [SQL Server Data Tools](https://msdn.microsoft.com/library/hh272686\(v=vs.103\).aspx)介绍简化数据连接的应用程序和数据库的设计、探索、测试和部署的工具。

 [ADO.NET](https://msdn.microsoft.com/library/5b96ed06-9759-4966-a797-a1d5f6ee50ca)介绍 ADO.NET 的体系结构，以及如何使用 ADO.NET 类来管理应用程序数据以及与数据源和 XML 进行交互。

 [ADO.NET 实体框架](https://msdn.microsoft.com/data/ef)介绍如何创建允许开发人员针对概念模型而不是直接针对关系数据库进行编程的数据应用程序。

 [WCF 数据服务 4.5](https://msdn.microsoft.com/library/73d2bec3-7c92-4110-b905-11bb0462357a)介绍如何使用 [!INCLUDE[ssAstoria](../includes/ssastoria-md.md)] 在实现[Open Data Protocol （OData）](https://go.microsoft.com/fwlink/?LinkID=182204)的 web 或 intranet 上部署数据服务。

 [Office 解决方案中的数据](https://msdn.microsoft.com/library/8478c095-864b-4ed3-8a70-1fc19b411c6a)包含指向一些主题的链接，这些主题说明了如何在 Office 解决方案中使用数据。 这包括有关面向架构的编程、数据缓存和服务器端数据访问的信息。

 [LINQ （语言集成查询）](https://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d)描述内置于C#和 Visual Basic 的查询功能，以及用于查询关系数据库、XML 文档、数据集和内存中集合的通用模型。

 [Visual Studio 中的 XML 工具](../xml-tools/xml-tools-in-visual-studio.md)讨论如何使用 XML 数据、调试 XSLT、.NET Framework XML 功能以及 XML 查询的体系结构。

 [XML 文档和数据](https://msdn.microsoft.com/library/e695047f-3c0f-4045-8708-5baea91cc380)概述了一组全面的集成类，这些类可用于在 .NET Framework 中处理 XML 文档和数据。
