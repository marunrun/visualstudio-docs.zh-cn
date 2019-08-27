---
title: 适用于.NET 的 visual Studio data tools |Microsoft Docs
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: c3175080-1dfb-4ab8-a460-92dadbb844b4
caps.latest.revision: 22
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: b42617892e377dcf750e9f5cafc914759b7d0c13
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68146546"
---
# <a name="visual-studio-data-tools-for-net"></a>适用于 NET 的 Visual Studio Data Tools
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 和.NET Framework 一起提供广泛的 API 和工具连接到数据库、 在内存中，数据建模和用户界面中显示数据的支持。  提供数据访问功能的.NET Framework 类被称为[ADO.NET](https://msdn.microsoft.com/library/e80y5yhx\(v=vs.110\).aspx)。 ADO.NET 中的，以及工具在 Visual Studio 中，数据最初被设计主要用于支持关系数据库和 XML。 如今，许多 NoSQL 数据库供应商或第三方提供 ADO.NET 提供程序。  
  
 Visual Studio 2015 更新 2年包括的最新的更新[SQL Server Data Tools](https://msdn.microsoft.com/library/hh272686\(v=vs.103\).aspx)，它实现了对在 Azure 中的最新功能的支持[SQL 数据库](https://azure.microsoft.com/services/sql-database/)和[SQL Server 2016](https://www.microsoft.com/sql-server/sql-server-2016). [.NET Core](https://www.dotnetfoundation.org/projects?searchquery=dotnet+core&type=project)支持 ADO.NET 中，数据集和相关的类型除外。 如果你要以.NET Core 为目标，并且需要对象关系映射 (ORM) 层，使用[实体框架核心](https://msdn.microsoft.com/data/ef.aspx)。  
  
 下图显示了基本的体系结构的简化的视图：  
  
 ![ADO.NET 体系结构](../data-tools/media/raddata-ado-net-architecture-diagram.png "raddata ADO.NET 体系结构关系图")  
  
 这是典型的工作流：  
  
1. 在本地计算机上安装开发或测试数据库。 请参阅[安装数据库系统、 工具和示例](../data-tools/installing-database-systems-tools-and-samples.md)。 如果使用 Azure 数据服务，此步骤不是必需的。  
  
2. 在 Visual Studio 中测试与数据库 （或服务或本地文件） 的连接。 请参阅[添加新连接](../data-tools/add-new-connections.md)。  
  
3. （可选）使用工具来生成和配置新的模型。 基于实体框架的模型是新的应用程序的默认建议。 模型中，使用，无论哪一个是与应用程序进行交互的数据源。 该模型在逻辑上位于数据库或服务与应用程序之间。  请参阅[添加新数据源](../data-tools/add-new-data-sources.md)。  
  
4. 从数据源拖动**数据源**窗口拖到 Windows 窗体、 ASP.NET 或 Windows Presentation Foundation 设计图面上以生成将在你指定的方式向用户显示的数据的数据绑定代码。 请参阅[将控件绑定到 Visual Studio 中的数据](../data-tools/bind-controls-to-data-in-visual-studio.md)。  
  
5. 添加自定义代码的内容，如业务规则、 搜索和数据验证，或若要充分利用基础数据库公开的自定义功能。  
  
   可以跳过步骤 3 和.NET 应用程序发出命令直接向数据库中，而不是使用模型进行编程。 在这种情况下，您将找到相关文档：[ADO.NET](https://msdn.microsoft.com/library/e80y5yhx\(v=vs.110\).aspx)。 请注意，您仍可以使用的数据源配置向导和设计器来填充您自己的内存，然后将 UI 控件数据绑定到这些对象中的对象时生成数据绑定代码。  
  
## <a name="in-this-section"></a>本节内容  
  
- [使用 ADO.NET 创建简单的数据应用程序](../data-tools/create-a-simple-data-application-by-using-adonet.md)  
  
- [添加新连接](../data-tools/add-new-connections.md)  
  
- [添加新数据源](../data-tools/add-new-data-sources.md)  
  
- [Visual Studio 中的实体数据模型工具](../data-tools/entity-data-model-tools-in-visual-studio.md)  
  
- [Visual Studio 中的数据集工具](../data-tools/dataset-tools-in-visual-studio.md)  
  
- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)  
  
- [在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)  
  
- [数据访问错误疑难解答的其他资源](../data-tools/additional-resources-for-troubleshooting-data-access-errors.md)  
  
- [Visual Studio 中的 Windows Communication Foundation 服务和 WCF 数据服务](../data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio.md)  
  
- [在 Visual Studio 中创建和管理数据库和数据层应用程序](../data-tools/creating-and-managing-databases-and-data-tier-applications-in-visual-studio.md)  
  
- [数据访问错误疑难解答的其他资源](../data-tools/additional-resources-for-troubleshooting-data-access-errors.md)  
  
## <a name="see-also"></a>请参阅  
 [在 Visual Studio 中访问数据](../data-tools/accessing-data-in-visual-studio.md)
