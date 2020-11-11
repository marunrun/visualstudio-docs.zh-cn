---
title: LINQ to SQL O/R 设计器概述
description: 简要了解 Visual Studio 中的 LINQ to SQL 工具。 了解对象关系设计器（O/R 设计器）。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: overview
ms.assetid: 45e477c0-5c6b-41f9-b2d0-2808fb4f6537
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: af394318d18244fc6e20e517d0ff985ca5e5ad1f
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2020
ms.locfileid: "94436232"
---
# <a name="linq-to-sql-tools-in-visual-studio"></a>Visual Studio 中的 LINQ to SQL 工具

LINQ to SQL 是 Microsoft 发布的首个对象关系映射技术。 它在基本方案中运行良好，且继续在 Visual Studio 中受到支持，但不再处于积极开发状态。 在维护已在使用的 LINQ to SQL 旧版应用程序时，或者在使用 SQL Server 且不需要多表映射的简单应用程序中，请使用 LINQ to SQL。 通常，当需要对象关系映射器层时，新的应用程序应使用实体框架。

## <a name="install-the-linq-to-sql-tools"></a>安装 LINQ to SQL 工具

在 Visual Studio 中，可通过使用对象关系设计器（O/R 设计器）创建表示 SQL 表的 LINQ to SQL 类 。 O/R 设计器是用于编辑 .dbml 文件的 UI。 使用设计器图面编辑 .dbml 文件需要 LINQ to SQL 工具，默认情况下，这些工具未作为 Visual Studio 的任何工作负载的一部分进行安装。

要安装 LINQ to SQL 工具，请启动 Visual Studio 安装程序，依次选择“修改”和“单个组件”选项卡，然后在“代码工具”类别下选择“LINQ to SQL 工具”   。

## <a name="what-is-the-or-designer"></a>什么是 O/R 设计器

O/R 设计器的设计图面上有两个不同的区域：左侧的实体窗格和右侧的方法窗格。 实体窗格是主设计图面，其中显示实体类、关联和继承层次结构。 方法窗格是显示映射到存储过程和函数的 <xref:System.Data.Linq.DataContext> 方法的设计图面。

O/R 设计器提供了一个可视化设计图面，用于创建基于数据库中对象的 [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index) 实体类和关联（关系）。 换句话说，O/R 设计器会在应用程序中创建映射到数据库中对象的对象模型。 它还生成一个强类型 <xref:System.Data.Linq.DataContext>，在实体类与数据库之间发送和接收数据。 O/R 设计器还提供了相关功能，用于将存储过程和函数映射到 <xref:System.Data.Linq.DataContext> 方法，以便返回数据和填充实体类。 最后，O/R 设计器提供了对实体类之间的继承关系进行设计的能力。

## <a name="open-the-or-designer"></a>打开 O/R 设计器

要将 LINQ to SQL 实体模型添加到项目中，请选择“项目” > “添加新项”，然后选择项目项列表中的“LINQ to SQL 类”  ：

![LINQ to SQL 类](../data-tools/media/raddata-linq-to-sql-classes.png)

Visual Studio 会创建 .dbml 文件，并将其添加到解决方案。 这是 XML 映射文件及其相关代码文件。

![解决方案资源管理器中的 LINQ to SQL 类](../data-tools/media/raddata-linq-to-sql-classes-in-solution-explorer.png)

选择 .dbml 文件时，Visual Studio 会显示 O/R 设计器图面，该图面可用于直观地创建模型。 下图显示从服务器资源管理器中拖动 Northwind `Customers` 和 `Orders` 表之后的设计器。 注意表之间的关系。

![LINQ to SQL 设计器](../data-tools/media/raddata-linq-to-sql-designer.png)

> [!IMPORTANT]
> O/R 设计器是一个简单的对象关系映射器，因为它仅支持 1:1 映射关系。 换句话说，实体类与数据库表或视图之间只能具有 1:1 映射关系。 不支持复杂映射（例如，将实体类映射到联接表）；对于复杂映射，可使用实体框架。 此外，该设计器还是一个单向代码生成器。 这表示代码文件中只反映对设计器图面所做的更改。 O/R 设计器中不会反映对代码文件的手动更改。 在保存设计器并重新生成代码时，将覆盖在代码文件中手动进行的所有更改。 了解如何添加用户代码和扩展由生成的类 **O/R 设计器** ，请参阅 [如何：扩展 O/R 设计器生成的代码](../data-tools/how-to-extend-code-generated-by-the-o-r-designer.md)。

## <a name="create-and-configure-the-datacontext"></a>创建并配置 DataContext

向项目添加“LINQ to SQL 类”项并打开 O/R 设计器后，空设计图面中会显示一个可供配置的空 <xref:System.Data.Linq.DataContext> 。 <xref:System.Data.Linq.DataContext> 是使用拖动到设计图面上的第一项所提供的连接信息进行配置的。 因此，<xref:System.Data.Linq.DataContext> 是使用放置到设计图面上的第一项中的连接信息进行配置的。 有关 <xref:System.Data.Linq.DataContext> 类的详细信息，请参阅 [DataContext 方法（O/R 设计器）](../data-tools/datacontext-methods-o-r-designer.md)。

## <a name="create-entity-classes-that-map-to-database-tables-and-views"></a>创建映射到数据库表和视图的实体类

通过将数据库表和视图从“服务器资源管理器”或“数据库资源管理器”拖动到 O/R 设计器上，可以创建映射到表和视图的实体类  。 正如上一节中所述，<xref:System.Data.Linq.DataContext> 是使用拖动到设计图面上的第一项所提供的连接信息进行配置的。 如果将一个使用不同连接的后续项添加到 O/R 设计器中，则可以更改 <xref:System.Data.Linq.DataContext> 的连接。 有关详细信息，请参阅[如何：创建映射到表和视图的 LINQ to SQL 类（O/R 设计器）](../data-tools/how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)。

## <a name="create-datacontext-methods-that-call-stored-procedures-and-functions"></a>创建调用存储过程和函数的 DataContext 方法

可以通过将存储过程和函数从“服务器资源管理器”或“数据库资源管理器”拖动到 O/R 设计器上来创建调用（映射到）这些存储过程和函数的 <xref:System.Data.Linq.DataContext> 方法  。 存储过程和函数作为 <xref:System.Data.Linq.DataContext> 的方法添加到 O/R 设计器中。

> [!NOTE]
> 将存储过程和函数从“服务器资源管理器”或“数据库资源管理器”拖动到 O/R 设计器上时，生成的 <xref:System.Data.Linq.DataContext> 方法的返回类型取决于项的放置位置  。 有关详细信息，请参阅 [DataContext 方法（O/R 设计器）](../data-tools/datacontext-methods-o-r-designer.md)。

## <a name="configure-a-datacontext-to-use-stored-procedures-to-save-data-between-entity-classes-and-a-database"></a>配置 DataContext 以使用存储过程来保存实体类和数据库之间的数据

如上文所述，您可以创建调用存储过程和函数的 <xref:System.Data.Linq.DataContext> 方法。 此外，还可以分配执行插入、更新和删除操作的默认 LINQ to SQL 运行时行为可以使用的存储过程。 有关详细信息，请参阅[如何：分配存储过程以便执行更新、插入和删除操作（O/R 设计器）](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md)。

## <a name="inheritance-and-the-or-designer"></a>继承和 O/R 设计器

像其他对象一样，LINQ to SQL 类可以使用继承，并可从其他类派生。 在数据库中，可通过多种方式创建继承关系。 O/R 设计器支持通常在关系系统中实现的单表继承概念。 有关详细信息，请参阅[如何：使用 O/R 设计器配置继承](../data-tools/how-to-configure-inheritance-by-using-the-o-r-designer.md)。

## <a name="linq-to-sql-queries"></a>LINQ to SQL 查询

O/R 设计器创建的实体类设计为与[语言集成查询 (LINQ)](/dotnet/csharp/linq/) 一起使用。 有关详细信息，请参阅[如何：查询信息](/dotnet/framework/data/adonet/sql/linq/how-to-query-for-information)。

## <a name="separate-the-generated-datacontext-and-entity-class-code-into-different-namespaces"></a>将生成的 DataContext 与实体类代码分离到不同的命名空间

O/R 设计器为 <xref:System.Data.Linq.DataContext> 提供了“上下文命名空间”和“实体命名空间”属性  。 这些属性决定 <xref:System.Data.Linq.DataContext> 和实体类代码生成到哪个命名空间。 默认情况下，这些属性为空并且 <xref:System.Data.Linq.DataContext> 和实体类生成到应用程序的命名空间。 若要在除应用程序的命名空间以外的命名空间中生成代码，请在“上下文命名空间”和/或“实体命名空间”属性中输入一个值。

## <a name="reference-content"></a>参考内容

- <xref:System.Linq>
- <xref:System.Data.Linq>

## <a name="see-also"></a>另请参阅

- [LINQ to SQL (.NET Framework)](/dotnet/framework/data/adonet/sql/linq/index)
- [常见问题解答 (.NET Framework)](/dotnet/framework/data/adonet/sql/linq/frequently-asked-questions)
