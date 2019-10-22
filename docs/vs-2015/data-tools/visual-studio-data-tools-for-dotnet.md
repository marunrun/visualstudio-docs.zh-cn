---
title: 适用于 .NET 的 Visual Studio 数据工具 |Microsoft Docs
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: c3175080-1dfb-4ab8-a460-92dadbb844b4
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 9d591595c65f00e0198ded9492ae0b8399e363e5
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72670102"
---
# <a name="visual-studio-data-tools-for-net"></a>适用于 NET 的 Visual Studio Data Tools
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 和 .NET Framework 一起提供广泛的 API 和工具支持，用于连接到数据库、对内存中的数据进行建模，以及在用户界面中显示数据。  提供数据访问功能的 .NET Framework 类称为[ADO.NET](https://msdn.microsoft.com/library/e80y5yhx\(v=vs.110\).aspx)。 ADO.NET 以及 Visual Studio 中的数据工具最初设计为支持关系数据库和 XML。 如今，许多 NoSQL 数据库供应商或第三方提供 ADO.NET 提供商。

 Visual Studio 2015 Update 2 包括[SQL Server Data Tools](https://msdn.microsoft.com/library/hh272686\(v=vs.103\).aspx)的最新更新，该更新支持 Azure [SQL 数据库](https://azure.microsoft.com/services/sql-database/)和[SQL Server 2016](https://www.microsoft.com/sql-server/sql-server-2016)中的最新功能。 除数据集和相关类型之外， [.Net Core](https://www.dotnetfoundation.org/projects?searchquery=dotnet+core&type=project)还支持 ADO.NET。 如果面向的是 .NET Core 并且需要对象关系映射（ORM）层，请使用[Entity Framework Core](https://msdn.microsoft.com/data/ef.aspx)。

 下图显示了基本体系结构的简化视图：

 ![ADO.NET 体系结构](../data-tools/media/raddata-ado-net-architecture-diagram.png "raddata ADO.NET 体系结构示意图")

 典型的工作流如下所示：

1. 在本地计算机上安装开发或测试数据库。 请参阅[安装数据库系统、工具和示例](../data-tools/installing-database-systems-tools-and-samples.md)。 如果你使用的是 Azure 数据服务，则不需要执行此步骤。

2. 在 Visual Studio 中测试与数据库（或服务或本地文件）的连接。 请参阅[添加新连接](../data-tools/add-new-connections.md)。

3. 可有可无使用工具生成和配置新的模型。 基于实体框架的模型是新应用程序的默认建议。 使用的模型是应用程序与之交互的数据源。 模型在逻辑上位于数据库或服务与应用程序之间。  请参阅[添加新数据源](../data-tools/add-new-data-sources.md)。

4. 将数据源从 "**数据源**" 窗口拖动到 Windows 窗体、ASP.NET 或 Windows Presentation Foundation 设计图面上，以生成将按你指定的方式向用户显示数据的数据绑定代码。 请参阅[在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)。

5. 为业务规则、搜索和数据验证等项目添加自定义代码，或利用基础数据库公开的自定义功能。

   您可以跳过步骤3，并对 .NET 应用程序进行编程以直接向数据库发出命令，而不使用模型。 在这种情况下，您将找到相关文档：[ADO.NET](https://msdn.microsoft.com/library/e80y5yhx\(v=vs.110\).aspx)。 请注意，在内存中填充自己的对象，然后将数据绑定 UI 控件数据绑定到这些对象时，仍可以使用 "数据源配置向导" 和 "设计器" 生成数据绑定代码。

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
