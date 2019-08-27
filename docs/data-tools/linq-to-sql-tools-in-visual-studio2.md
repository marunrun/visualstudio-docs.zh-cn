---
title: O/R 设计器概述
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 45e477c0-5c6b-41f9-b2d0-2808fb4f6537
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 4105a93d4ad459c8bc1cb3a7a20b37c69f311c12
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62566382"
---
# <a name="linq-to-sql-tools-in-visual-studio"></a>Visual Studio 中的 LINQ to SQL 工具

LINQ to SQL 是由 Microsoft 发布的第一个对象关系映射技术。 它适用于基本方案，并继续支持在 Visual Studio 中，但它不再处于积极开发阶段。 使用 LINQ to SQL 时维护的旧版应用程序已在使用它，或在简单的应用程序使用 SQL Server，不需要多表映射。 一般情况下，新的应用程序应使用实体框架时是必需的对象关系映射器层。

在 Visual Studio 中创建 LINQ to SQL 类表示使用的 SQL 表**对象关系设计器**(**O/R 设计器**)。

**O/R 设计器**有其设计图面上两个不同的区域： 左侧的实体窗格和右侧的方法窗格。 实体窗格是主设计图面，其中显示实体类、关联和继承层次结构。 方法窗格是显示映射到存储过程和函数的 <xref:System.Data.Linq.DataContext> 方法的设计图面。

**O/R 设计器**提供用于创建可视化设计图面[LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)实体类并基于数据库中的对象的关联 （关系）。 换而言之， **O/R 设计器**映射到数据库中的对象的应用程序中创建的对象模型。 它还会生成强类型<xref:System.Data.Linq.DataContext>的发送和接收数据的实体类和数据库之间。 **O/R 设计器**还提供了功能来映射存储的过程和函数到<xref:System.Data.Linq.DataContext>方法以便返回数据和填充实体类。 最后， **O/R 设计器**提供了设计实体类之间的继承关系的功能。

## <a name="open-the-or-designer"></a>打开 O/R 设计器

若要添加 LINQ to SQL 实体模型到你的项目，选择**项目** > **添加新项**，然后选择**LINQ to SQL 类**从项目项的列表：

![LINQ to SQL 类](../data-tools/media/raddata-linq-to-sql-classes.png)

Visual Studio 将创建 *.dbml*文件，并将其添加到你的解决方案。 这是 XML 映射文件和其相关的代码文件。

![LINQ to SQL 类在解决方案资源管理器](../data-tools/media/raddata-linq-to-sql-classes-in-solution-explorer.png)

当选择 *.dbml*文件，Visual Studio 将显示**O/R 设计器**图面，让你直观地创建模型。 下图显示的设计器后 Northwind`Customers`并`Orders`已从拖动表**服务器资源管理器**。 请注意在表之间的关系。

![LINQ to SQL 设计器](../data-tools/media/raddata-linq-to-sql-designer.png)

> [!IMPORTANT]
> **O/R 设计器**是一个简单的对象关系映射器，因为它仅支持 1:1 映射关系。 换句话说，实体类与数据库表或视图之间只能具有 1:1 映射关系。 不支持复杂映射，如将实体类映射到联接表;使用实体框架为复杂的映射。 此外，该设计器还是一个单向代码生成器。 这表示代码文件中只反映对设计器图面所做的更改。 对代码文件的手动更改不会反映在**O/R 设计器**。 在保存设计器并重新生成代码时，将覆盖在代码文件中手动进行的所有更改。 了解如何添加用户代码和扩展由生成的类**O/R 设计器**，请参阅[如何：扩展 O/R 设计器生成的代码](../data-tools/how-to-extend-code-generated-by-the-o-r-designer.md)。

## <a name="create-and-configure-the-datacontext"></a>创建和配置 DataContext

添加后**LINQ to SQL 类**项到项目并打开**O/R 设计器**，空设计图面表示一个空<xref:System.Data.Linq.DataContext>可对其进行配置。 <xref:System.Data.Linq.DataContext> 是使用拖动到设计图面上的第一项所提供的连接信息进行配置的。 因此，<xref:System.Data.Linq.DataContext> 是使用放置到设计图面上的第一项中的连接信息进行配置的。 有关详细信息<xref:System.Data.Linq.DataContext>类，请参阅[DataContext 方法 （O/R 设计器）](../data-tools/datacontext-methods-o-r-designer.md)。

## <a name="create-entity-classes-that-map-to-database-tables-and-views"></a>创建实体类映射到数据库表和视图

可以创建实体类映射到表和视图，通过将数据库表和视图从**服务器资源管理器**或**数据库资源管理器**拖到**O/R 设计器**。 正如上一节中所述，<xref:System.Data.Linq.DataContext> 是使用拖动到设计图面上的第一项所提供的连接信息进行配置的。 如果使用不同的连接的后续项添加到**O/R 设计器**，可以更改用于连接<xref:System.Data.Linq.DataContext>。 有关详细信息，请参阅[如何：创建映射到表和视图的 LINQ to SQL 类（O/R 设计器）](../data-tools/how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)。

## <a name="create-datacontext-methods-that-call-stored-procedures-and-functions"></a>创建调用存储的过程和函数的 DataContext 方法

您可以创建<xref:System.Data.Linq.DataContext>调用的方法 （映射到中） 存储过程和函数，通过将其从拖动**服务器资源管理器**或**数据库资源管理器**拖到**O/R 设计器**. 存储的过程和函数添加到**O/R 设计器**的方法作为<xref:System.Data.Linq.DataContext>。

> [!NOTE]
> 当您将存储的过程和函数从**服务器资源管理器**或**数据库资源管理器**拖到**O/R 设计器**，生成的返回类型<xref:System.Data.Linq.DataContext>方法不同，具体取决于您在何处放置项。 有关详细信息，请参阅[DataContext 方法 （O/R 设计器）](../data-tools/datacontext-methods-o-r-designer.md)。

## <a name="configure-a-datacontext-to-use-stored-procedures-to-save-data-between-entity-classes-and-a-database"></a>配置 DataContext 以使用存储的过程来保存实体类和数据库之间的数据

如上文所述，您可以创建调用存储过程和函数的 <xref:System.Data.Linq.DataContext> 方法。 此外，还可以分配用于 LINQ to SQL 运行时行为，后者将执行插入、 更新和删除的默认的存储的过程。 有关详细信息，请参阅[如何：分配存储过程以便执行更新、插入和删除操作（O/R 设计器）](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md)。

## <a name="inheritance-and-the-or-designer"></a>继承和 O/R 设计器

类似于其他对象，LINQ to SQL 类可以使用继承，并从其他类派生。 在数据库中，可通过多种方式创建继承关系。 **O/R 设计器**支持通常在关系系统中实现的单表继承概念。 有关详细信息，请参阅[如何：使用 O/R 设计器配置继承](../data-tools/how-to-configure-inheritance-by-using-the-o-r-designer.md)。

## <a name="linq-to-sql-queries"></a>LINQ to SQL 查询

创建的实体类**O/R 设计器**设计用于[语言集成查询 (LINQ)](/dotnet/csharp/linq/)。 有关详细信息，请参阅[如何：有关信息的查询](/dotnet/framework/data/adonet/sql/linq/how-to-query-for-information)。

## <a name="separate-the-generated-datacontext-and-entity-class-code-into-different-namespaces"></a>将生成的 DataContext 和实体类代码分离到不同的命名空间

**O/R 设计器**提供**上下文 Namespace**并**实体 Namespace**上的属性<xref:System.Data.Linq.DataContext>。 这些属性决定 <xref:System.Data.Linq.DataContext> 和实体类代码生成到哪个命名空间。 默认情况下，这些属性为空并且 <xref:System.Data.Linq.DataContext> 和实体类生成到应用程序的命名空间。 若要在除应用程序的命名空间以外的命名空间中生成代码，请在“上下文命名空间”和/或“实体命名空间”属性中输入一个值。

## <a name="reference-content"></a>参考内容

- <xref:System.Linq>
- <xref:System.Data.Linq>

## <a name="see-also"></a>请参阅

- [LINQ to SQL (.NET Framework)](/dotnet/framework/data/adonet/sql/linq/index)
- [常见问题 (.NET Framework)](/dotnet/framework/data/adonet/sql/linq/frequently-asked-questions)