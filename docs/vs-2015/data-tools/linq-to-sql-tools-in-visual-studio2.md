---
title: LINQ to SQL 工具 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: 45e477c0-5c6b-41f9-b2d0-2808fb4f6537
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 470cfabd54fa5f2b92001a635477c60d45fac538
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72651518"
---
# <a name="linq-to-sql-tools-in-visual-studio"></a>Visual Studio 中的 LINQ to SQL 工具
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

LINQ to SQL 是 Microsoft 发布的第一个对象关系映射技术。 它适用于基本方案，并在 Visual Studio 中继续受支持，但它已不再处于活动状态。 在维护已在使用它的旧应用程序或使用 SQL Server 且不需要多表映射的简单应用程序中使用 LINQ to SQL。 通常，当需要对象关系映射器层时，新应用程序应使用实体框架。

 在 Visual Studio 中，通过使用创建表示 SQL 表 LINQ to SQL 类 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] 。

 在 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] 其设计图面上有两个不同的区域：左侧的实体窗格和右侧的方法窗格。 实体窗格是主设计图面，其中显示实体类、关联和继承层次结构。 方法窗格是显示映射到存储过程和函数的 <xref:System.Data.Linq.DataContext> 方法的设计图面。

 [!INCLUDE[vs_ordesigner_long](../includes/vs-ordesigner-long-md.md)] ([!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]) 提供了一个可视化设计图面，用于创建基于数据库中对象的[LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)实体类和关联 (关系) 。 换句话说，[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]用于在应用程序中创建映射到数据库中的对象的对象模型。 它还生成一个强类型 <xref:System.Data.Linq.DataContext>，用于在实体类与数据库之间发送和接收数据。 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]还提供了相关功能，用于将存储过程和函数映射到 <xref:System.Data.Linq.DataContext> 方法以便返回数据和填充实体类。 最后，[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]提供了对实体类之间的继承关系进行设计的能力。

## <a name="opening-the-or-designer"></a>打开 O/R 设计器
 若要将 LINQ to SQL 实体模型添加到项目中，请选择 " **项目 &#124;" 添加新项** "，然后从项目项列表中选择"  **LINQ to SQL 类** "：

 ![LINQ to SQL 类](../data-tools/media/raddata-linq-to-sql-classes.png "raddata LINQ to SQL 类")

 Visual Studio 将创建一个 .dbml 文件并将其添加到你的解决方案中。 这是 XML 映射文件及其相关的代码文件。

 ![解决方案资源管理器中的 LINQ to SQL 类](../data-tools/media/raddata-linq-to-sql-classes-in-solution-explorer.png "解决方案资源管理器中的 raddata LINQ to SQL 类")

 选择 .dbml 文件时，Visual Studio 会显示 O/R 设计器图面，使你能够以视觉方式创建模型。 下图显示了从服务器资源管理器中拖出 Northwind Customers 和 Orders 表后的设计器。 请注意表之间的关系。

 ![LINQ to SQL 设计器](../data-tools/media/raddata-linq-to-sql-designer.png "raddata LINQ to SQL 设计器")

> [!IMPORTANT]
> [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]是一个简单的对象关系映射器，因为它仅支持 1:1 映射关系。 换句话说，实体类与数据库表或视图之间只能具有 1:1 映射关系。 不支持复杂映射（例如，将实体类映射到联接表）;使用实体框架进行复杂的映射。 此外，该设计器还是一个单向代码生成器。 这表示代码文件中只反映对设计器图面所做的更改。 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]中不会反映对代码文件的手动更改。 在保存设计器并重新生成代码时，将覆盖在代码文件中手动进行的所有更改。 有关如何添加用户代码和扩展生成的类的信息 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] ，请参阅 [如何：扩展 O/R 设计器生成的代码](../data-tools/how-to-extend-code-generated-by-the-o-r-designer.md)。

## <a name="creating-and-configuring-the-datacontext"></a>创建和配置 DataContext
 将 **LINQ to SQL 类** 项添加到项目并打开后 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] ，空设计图面表示一个可供配置的空 <xref:System.Data.Linq.DataContext> 。 <xref:System.Data.Linq.DataContext>是使用拖放到设计图面上的第一项提供的连接信息进行配置的。 因此，<xref:System.Data.Linq.DataContext> 是使用放置到设计图面上的第一项中的连接信息进行配置的。 有关类的详细信息 <xref:System.Data.Linq.DataContext> ，请参阅 [DataContext 方法 (O/R Designer) ](../data-tools/datacontext-methods-o-r-designer.md)。

## <a name="creating-entity-classes-that-map-to-database-tables-and-views"></a>创建映射到数据库表和视图的实体类
 通过将数据库表和视图从**服务器资源管理器** / **数据库资源管理器**拖到上，可以创建映射到表和视图的实体类 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] 。 正如上一节中所述，<xref:System.Data.Linq.DataContext> 是使用拖动到设计图面上的第一项所提供的连接信息进行配置的。 如果将一个使用不同连接的后续项添加到 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]中，您可以更改 <xref:System.Data.Linq.DataContext> 的连接。 有关详细信息，请参阅 [如何：创建映射到表和视图的 LINQ to SQL 类 (O/R 设计器) ](../data-tools/how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)。

## <a name="creating-datacontext-methods-that-call-stored-procedures-and-functions"></a>创建调用存储过程和函数的 DataContext 方法
 您可以 <xref:System.Data.Linq.DataContext> 通过将**服务器资源管理器** / **数据库资源管理器**中的拖动到，来创建调用 (映射到) 存储过程和函数的方法 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] 。 存储过程和函数作为 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] 的方法添加到 <xref:System.Data.Linq.DataContext>中。

> [!NOTE]
> 将**服务器资源管理器**数据库资源管理器中的存储过程和函数拖到上时 / **Database Explorer** [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] ，生成的方法的返回类型 <xref:System.Data.Linq.DataContext> 会有所不同，具体取决于放置项的位置。 有关详细信息，请参阅 [DataContext 方法 (O/R Designer) ](../data-tools/datacontext-methods-o-r-designer.md)。

## <a name="configuring-a-datacontext-to-use-stored-procedures-to-save-data-between-entity-classes-and-a-database"></a>配置 DataContext 以使用存储过程来保存实体类和数据库之间的数据
 如上文所述，您可以创建调用存储过程和函数的 <xref:System.Data.Linq.DataContext> 方法。 此外，您还可以分配执行插入、更新和删除操作的默认 [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] 运行时行为可以使用的存储过程。 有关详细信息，请参阅 [如何：分配存储过程以执行 (O/R 设计器) 的更新、插入和删除 ](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md)操作。

## <a name="inheritance-and-the-or-designer"></a>继承和 O/R 设计器
 像其他对象一样，[!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] 类可以使用继承，并可从其他类派生。 在数据库中，可通过多种方式创建继承关系。 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]支持通常在关系系统中实现的单表继承概念。 有关详细信息，请参阅 [如何：使用 O/R 设计器配置继承](../data-tools/how-to-configure-inheritance-by-using-the-o-r-designer.md)。

## <a name="linq-to-sql-queries"></a>LINQ to SQL 查询
 由创建的实体类 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] 旨在与 [LINQ (语言集成查询) ](https://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d)一起使用。 有关详细信息，请参阅 [如何：查询信息](https://msdn.microsoft.com/library/e538d288-2070-40ca-9da6-4fbc68cd6ad0)。

## <a name="separating-the-generated-datacontext-and-entity-class-code-into-different-namespaces"></a>将生成的 DataContext 和实体类代码分离到不同的命名空间
 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]提供上的**上下文命名空间**和**实体命名空间**属性 <xref:System.Data.Linq.DataContext> 。 这些属性决定 <xref:System.Data.Linq.DataContext> 和实体类代码生成到哪个命名空间。 默认情况下，这些属性为空并且 <xref:System.Data.Linq.DataContext> 和实体类生成到应用程序的命名空间。 若要在除应用程序的命名空间以外的命名空间中生成代码，请在“上下文命名空间”和/或“实体命名空间”属性中输入一个值********。

## <a name="in-this-section"></a>本节内容
 [DataContext 方法 (O/R 设计器) ](../data-tools/datacontext-methods-o-r-designer.md) 说明什么 <xref:System.Data.Linq.DataContext> 是方法以及如何创建它们。

 [O/R 设计器 (的数据类继承) ](../data-tools/data-class-inheritance-o-r-designer.md) 描述单表继承的概念以及如何在中实现它 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] 。

 [如何：创建映射到表和视图的 LINQ to SQL 类 (O/R 设计器) ](../data-tools/how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md) 描述如何创建映射到数据库中的表和视图的实体类。

 [如何：在 LINQ to SQL 类 (O/R 设计器之间 (关系) 创建关联) ](../data-tools/how-to-create-an-association-relationship-between-linq-to-sql-classes-o-r-designer.md) 描述如何创建实体类之间的关系 [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] 。

 [如何：创建映射到存储过程和函数的 DataContext 方法 (O/R 设计器) ](../data-tools/how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-o-r-designer.md) 介绍如何创建 <xref:System.Data.Linq.DataContext> 在调用存储过程或函数时运行这些存储过程或函数的方法。

 [如何：分配存储过程以执行 (O/R 设计器的更新、插入和删除) ](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md) 描述如何将配置 <xref:System.Data.Linq.DataContext> 为使用存储过程将数据从实体类保存回数据库。

 [如何： (O/R 设计器更改 DataContext 方法的返回类型) ](../data-tools/how-to-change-the-return-type-of-a-datacontext-method-o-r-designer.md) 描述如何将方法的返回类型设置 <xref:System.Data.Linq.DataContext> 为实体类的类型或由 O/R 设计器创建的自动生成类型。

 [如何：向实体类添加验证](../data-tools/how-to-add-validation-to-entity-classes.md) 介绍如何生成分部方法，以便在属性更改和实体类更新过程中添加代码。

 [如何：打开和关闭复数形式 (O/R 设计器) ](../data-tools/how-to-turn-pluralization-on-and-off-o-r-designer.md) 介绍如何打开和关闭添加到中的类的自动重命名 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] 。

 [如何：使用 O/R 设计器配置继承](../data-tools/how-to-configure-inheritance-by-using-the-o-r-designer.md) 描述如何通过使用单表继承配置实体类 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] 。

 [如何：扩展 O/R 设计器生成的代码](../data-tools/how-to-extend-code-generated-by-the-o-r-designer.md) 描述如何以及在何处添加在 O/R 设计器上的对象更改重新生成代码时不会被覆盖的代码。

 [演练：使用单表继承 (O/R 设计器创建 LINQ to SQL 类) ](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md) 提供有关通过使用单表继承配置实体类的分步说明 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] 。

 [演练：自定义实体类的插入、更新和删除行为](../data-tools/walkthrough-customizing-the-insert-update-and-delete-behavior-of-entity-classes.md) 提供 <xref:System.Data.Linq.DataContext> 在将数据从实体类保存回数据库时将配置为使用存储过程的分步说明。

## <a name="reference-content"></a>参考内容
 <xref:System.Linq>

 <xref:System.Data.Linq>

## <a name="see-also"></a>另请参阅
 [Visual studio data tools for .net](../data-tools/visual-studio-data-tools-for-dotnet.md) [常见问题](https://msdn.microsoft.com/library/252ed666-0679-4eea-b71b-2f14117ef443) [LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655) [在 Visual studio 中访问数据](../data-tools/accessing-data-in-visual-studio.md)
