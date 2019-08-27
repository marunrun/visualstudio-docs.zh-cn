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
author: gewarren
ms.author: gewarren
manager: jillfra
robots: noindex,nofollow
ms.openlocfilehash: 7f13a97adbec1da1bd0f279e14cf510532b9c62f
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65688626"
---
# <a name="accessing-data-in-visual-studio"></a>在 Visual Studio 中访问数据
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

在 Visual Studio 中，可以创建连接到几乎任何数据库产品或服务，任何格式，任何位置中的数据的应用程序 — 在本地计算机上，在本地网络，或在公共、 专用或混合云。

 JavaScript、 Python、 PHP、 Ruby 中的应用程序或C++，就像任何其他内容，方法是获取库编写的代码连接到的数据。 对于.NET 应用程序，Visual Studio 提供可用于浏览数据源、 创建对象模型来存储和处理数据在内存中，并将数据绑定到用户界面的工具。     Microsoft Azure 提供了用于.NET、 Java、 Node.js、 PHP、 Python、 Ruby 和移动应用和 Visual Studio 中的工具连接到 Azure 存储 Sdk。

 以下列表显示了从 Visual Studio 只需几个可以使用许多数据库和存储系统。 [Microsoft Azure](https://azure.microsoft.com/)产品是数据服务，包括所有预配和管理的基础数据存储区。  [Azure Tools for Visual Studio](https://www.visualstudio.com/features/azure-tools-vs.aspx)是一个可选组件，使您能够直接从 Visual Studio 的 Azure 数据存储。 可以在本地计算机上，在本地网络，或在 Microsoft Azure 虚拟机上托管的其他 SQL 和 NoSQL 数据库产品此处列出的大多数。 在此方案中，您负责管理数据库本身。

 **Microsoft Azure**

||||
|-|-|-|
|SQL 数据库|DocumentDB|存储 （blob、 表、 队列、 文件）|
|SQL 数据仓库|SQL Server Stretch Database|StorSimple|

 更多内容...

 **SQL**

||||
|-|-|-|
|SQL Server 2005 – 2016，其中包括 Express 和 LocalDB|Firebird|MariaDB|
|MySQL|Oracle|postgresql|
|SQLite|||

 更多内容...

 **NoSQL**

||||
|-|-|-|
|Apache Cassandra|CouchDB|MongoDB|
|NDatabase|OrientDB|RavenDB|
|VelocityDB|||

 更多内容...

 许多数据库供应商和第三方通过 NuGet 包支持 Visual Studio 集成。 在 nuget.org 上或通过 NuGet 包管理器在 Visual Studio 中，可以浏览产品/服务 (**工具** > **NuGet 包管理器** > **管理 NuGet解决方案包**)。 其他数据库产品与 Visual Studio 集成扩展。   您可以通过导航到浏览 Visual Studio 库中的这些产品/服务**工具** > **扩展和更新**，然后选择**联机**左侧在对话框的窗格。  有关详细信息，请参阅[安装数据库系统、 工具和示例](../data-tools/installing-database-systems-tools-and-samples.md)。

> [!NOTE]
> 对 SQL Server 2005 的延长的支持已于 2016 年 4 月 12 日结束。   就数据工具在 Visual Studio 2015 及更高版本将继续使用 SQL Server 2005 在此日期之后不能保证。 有关详细信息，请参阅[SQL Server 2005 的最终支持公告](https://www.microsoft.com/sql-server/sql-server-2005)。

### <a name="net-languages"></a>.NET 语言
 所有.NET 数据访问，包括在.NET Core 中，都基于 ADO.NET 中，定义用于访问任何类型的关系和非关系数据源的接口的一组类。 Visual Studio 具有几个工具和设计人员可使用 ADO.NET 来帮助您连接到数据库，操作数据，并向用户呈现数据。 在本部分中的文档介绍如何使用这些工具。 您还可以直接对 ADO.NET 命令对象进行编程。 直接调用 ADO.NET Api 的详细信息，请参阅[ADO.NET](https://msdn.microsoft.com/library/e80y5yhx\(v=vs.110\).aspx) MSDN 库中。

 专门与 ASP.NET 相关的数据访问文档，请参阅[使用数据](http://www.asp.net/web-forms/overview/presenting-and-managing-data)ASP.NET 站点上。 使用 ASP.NET MVC 中使用实体框架的教程，请参阅[开始使用 Entity Framework 6 Code First 通过 MVC 5](http://www.asp.net/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application)。

 C# 或 Visual Basic 中的通用 Windows 平台 (UWP) 应用可以使用 Microsoft Azure SDK for.NET 访问 Azure 存储和其他 Azure 服务。 Windows.Web.HttpClient 类，与任何 RESTful 服务的通信。 有关详细信息，请参阅[如何连接到 HTTP 服务器使用 Windows.Web.Http](https://msdn.microsoft.com/library/windows/apps/dn469430.aspx)。

 对于本地计算机上的数据存储，建议的方法是使用 SQLite，作为应用程序在同一进程中运行。 如果需要一个对象关系映射 (ORM) 层，可以使用实体框架。 有关详细信息，请参阅[数据访问](https://msdn.microsoft.com/windows/uwp/data-access/index)Windows 开发人员中心中。

 如果要连接到 Azure 服务，请务必下载最新[Azure SDK 工具](https://azure.microsoft.com/downloads/)。

#### <a name="data-providers"></a>数据提供程序
 若要用于在 ADO.NET 中的数据库，它必须能够自定义*ADO.NET 数据提供程序*或其他必须公开一个 ODBC 或 OLE DB 接口。 Microsoft 提供了[ADO.NET 数据提供程序的列表](https://msdn.microsoft.com/data/dd363565)SQL Server 产品以及 ODBC 和 OLE DB 访问接口。

#### <a name="data-modeling"></a>数据建模
 在.NET 中，您有用于建模和操作在内存中的数据后已从数据源中检索的三个选择：

 实体框架的首选 Microsoft ORM 技术。 您可以使用它到针对关系数据进行编程作为一流的.NET 对象。 对于新应用程序，它应为默认的第一个选项，需要一个模型时。 它需要从基础 ADO.NET 提供程序的自定义支持。

 LINQ to SQL 的早期生成的对象关系映射器。 它非常适合不太复杂的方案，但不再处于积极开发阶段。

 数据集最旧的三种建模技术。 它主要用于快速开发"forms over data"应用程序将不处理大量数据或执行复杂的查询或转换在其中。 数据集对象包括逻辑上远远超出了.NET 对象类似于 SQL 数据库对象的 DataTable 和 DataRow 对象。 对于相对简单的应用程序基于 SQL 的数据源，数据集可能仍是一个不错的选择。

 没有任何要求使用任何这些技术。 在某些情况下，尤其是在性能很重要，只需可用 DataReader 对象来从数据库读取并将所需的值复制到一个集合对象，如列表\<T >。

### <a name="native-c"></a>本机 C++
 C++连接到 SQL Server 的应用程序应使用[SQL Server Native Client](https://msdn.microsoft.com/sqlserver/aa937733.aspx)。 可以使用访问其他数据库[ODBC](https://msdn.microsoft.com/library/ms710252\(v=vs.85\).aspx)或 OLE DB 驱动程序直接。 ODBC 是当前的标准数据库接口，但大多数数据库系统提供无法通过 ODBC 接口访问的自定义功能。  OLE DB 是一项传统 COM 数据访问技术，是仍受支持但不是建议用于新的应用程序。  有关详细信息，请参阅[数据访问](https://msdn.microsoft.com/library/a9455752-39c4-4457-b14e-197772d3df0b)。

 C++使用 REST 服务的程序可以使用[ C++ REST SDK](https://github.com/Microsoft/cpprestsdk)。

 C++使用 Microsoft Azure 存储空间的程序可以使用[Microsoft Azure 存储客户端](http://www.nuget.org/packages/wastorage)。

#### <a name="data-modeling"></a>数据建模
 Visual Studio 不提供的 ORM 层为C++。  [ODB](http://www.codesynthesis.com/products/odb/)是为受欢迎的开源 ORM C++。

 详细了解旧版 VisualC++数据访问技术，请参阅[数据访问](https://msdn.microsoft.com/library/a9455752-39c4-4457-b14e-197772d3df0b)

### <a name="javascript"></a>JavaScript
 [Visual Studio 中的 JavaScript](https://msdn.microsoft.com/library/hh334522.aspx)是一流的语言，用于构建跨平台应用、 UWP 应用、 云服务、 网站和 web 应用。 可以使用 Bower、 Grunt、 Gulp、 npm 和 Visual Studio 中的从 NuGet 安装你最喜欢的 JavaScript 库和数据库产品。 通过下载 Sdk 从连接到 Azure 存储和服务[Azure 网站](https://azure.microsoft.com/)。  Edge.js 是服务器端 JavaScript (Node.js) 连接到 ADO.NET 数据源的库。

### <a name="python"></a>Python
 安装[Python Tools for Visual Studio](http://microsoft.github.io/PTVS/)以及你最喜欢的 Python 框架来创建 CPython 或 IronPython (.NET) 的应用程序。  Python Tools for Visual Studio 网站提供了几个教程，连接到数据，包括[Django 和在 Azure 上的 SQL 数据库](https://github.com/Microsoft/PTVS/wiki/Django-and-SQL-Database-on-Azure)， [Django 和在 Azure 上的 MySQL](https://github.com/Microsoft/PTVS/wiki/Django-and-MySQL-on-Azure)和[Bottle 和 MongoDB 上Azure](https://github.com/Microsoft/PTVS/wiki/Bottle-and-MongoDB-on-Azure)。

## <a name="in-this-section"></a>本节内容
 [安装数据库系统、 工具和示例](../data-tools/installing-database-systems-tools-and-samples.md)讨论了如何获取数据库产品的 Visual Studio 扩展插件或驱动程序支持它们，以及在哪里可以找到的实验和学习目的的示例数据库。

 [适用于.NET 的 visual Studio data tools](https://msdn.microsoft.com/6b145922-2f00-47db-befc-bf351b4809a1)介绍如何使用 Visual Studio 工具窗口连接到数据源，创建数据集或实体框架模型，并将数据绑定到用户界面控件。

## <a name="related-topics"></a>相关主题
 [数据、 设备和分析](https://msdn.microsoft.com/data-and-devices)介绍了 Microsoft 智能云，包括 Cortana Analytics 套件和物联网的支持。

 [Microsoft Azure 存储空间](/azure/storage/)介绍 Azure 存储，以及如何使用 Azure blob、 表、 队列和文件创建应用程序。

 [Azure SQL 数据库](https://azure.microsoft.com/documentation/services/sql-database/)介绍如何连接到 Azure SQL 数据库，关系数据库即服务。

 [SQL Server Data Tools](https://msdn.microsoft.com/library/hh272686\(v=vs.103\).aspx)描述简化设计，探索、 测试和部署的数据连接的应用程序和数据库的工具。

 [ADO.NET](https://msdn.microsoft.com/library/5b96ed06-9759-4966-a797-a1d5f6ee50ca)介绍 ADO.NET 体系结构以及如何使用 ADO.NET 类来管理应用程序数据和与数据源和 XML 进行交互。

 [ADO.NET 实体框架](https://msdn.microsoft.com/data/ef)介绍如何创建数据应用程序，使开发人员针对概念模型而不是直接针对关系数据库进行编程。

 [WCF 数据服务 4.5](https://msdn.microsoft.com/library/73d2bec3-7c92-4110-b905-11bb0462357a)介绍了如何使用[!INCLUDE[ssAstoria](../includes/ssastoria-md.md)]部署 web 或 intranet 上的数据服务，实现[开放数据协议 (OData)](http://go.microsoft.com/fwlink/?LinkID=182204)。

 [Office 解决方案中的数据](https://msdn.microsoft.com/library/8478c095-864b-4ed3-8a70-1fc19b411c6a)包含指向这些主题介绍了数据在 Office 解决方案中的工作方式。 这包括有关面向架构编程、 数据缓存和服务器端数据访问的信息。

 [LINQ （语言集成查询）](https://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d)介绍了内置的查询功能C#和 Visual Basic 和通用模型用于查询关系数据库、 XML 文档、 数据集和内存中集合。

 [Visual Studio 中的 XML 工具](../xml-tools/xml-tools-in-visual-studio.md)讨论使用 XML 数据，调试 XSLT，.NET Framework XML 功能，以及 XML 查询的体系结构。

 [XML 文档和数据](https://msdn.microsoft.com/library/e695047f-3c0f-4045-8708-5baea91cc380)提供简要介绍了如何全面、 集成的一组类，使用 XML 文档和.NET Framework 中的数据。
