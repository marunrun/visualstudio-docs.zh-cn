---
title: LINQ to SQL 工具 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: 45e477c0-5c6b-41f9-b2d0-2808fb4f6537
caps.latest.revision: 15
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 24b874ab71cba23a3fe6cf4a6fb36293d6753935
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65697762"
---
# <a name="linq-to-sql-tools-in-visual-studio"></a>LINQ to SQL 工具在 Visual Studio 中
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

LINQ to SQL 是由 Microsoft 发布的第一个对象关系映射技术。 它适用于基本方案，并继续支持在 Visual Studio 中，但它不再处于积极开发阶段。 使用 LINQ to SQL 时维护的旧版应用程序已在使用它，或在简单的应用程序使用 SQL Server，不需要多表映射。 一般情况下，新的应用程序应使用实体框架时是必需的对象关系映射器层。

 在 Visual Studio 中创建 LINQ to SQL 类表示使用的 SQL 表[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]。

 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]有其设计图面上两个不同的区域： 左侧的实体窗格和右侧的方法窗格。 实体窗格是主设计图面，其中显示实体类、关联和继承层次结构。 方法窗格是显示映射到存储过程和函数的 <xref:System.Data.Linq.DataContext> 方法的设计图面。

 [!INCLUDE[vs_ordesigner_long](../includes/vs-ordesigner-long-md.md)] ([!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]) 提供用于创建可视化设计图面[LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655)实体类并基于数据库中的对象的关联 （关系）。 换句话说，[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]用于在应用程序中创建映射到数据库中的对象的对象模型。 它还生成一个强类型 <xref:System.Data.Linq.DataContext>，用于在实体类与数据库之间发送和接收数据。 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]还提供了相关功能，用于将存储过程和函数映射到 <xref:System.Data.Linq.DataContext> 方法以便返回数据和填充实体类。 最后，[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]提供了对实体类之间的继承关系进行设计的能力。

## <a name="opening-the-or-designer"></a>打开 O/R 设计器
 若要添加 LINQ to SQL 实体模型到你的项目，选择**项目&#124;添加新项**，然后选择**LINQ to SQL 类**从项目项的列表：

 ![LINQ to SQL 类](../data-tools/media/raddata-linq-to-sql-classes.png "raddata LINQ to SQL 类")

 Visual Studio 创建一个.dbml 文件，并将其添加到你的解决方案。 这是 XML 映射文件和其相关的代码文件。

 ![在解决方案资源管理器中的 LINQ to SQL 类](../data-tools/media/raddata-linq-to-sql-classes-in-solution-explorer.png "raddata LINQ to SQL 类在解决方案资源管理器")

 当选中此.dbml 文件时，Visual Studio 将显示该对话框可直观地创建模型 O/R 设计器图面。 下图显示的设计器后从服务器资源管理器中拖动到 Northwind Customers 和 Orders 表。 请注意在表之间的关系。

 ![LINQ to SQL 设计器](../data-tools/media/raddata-linq-to-sql-designer.png "raddata LINQ to SQL 设计器")

> [!IMPORTANT]
> [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]是一个简单的对象关系映射器，因为它仅支持 1:1 映射关系。 换句话说，实体类与数据库表或视图之间只能具有 1:1 映射关系。 不支持复杂映射，如将实体类映射到联接表;使用实体框架为复杂的映射。 此外，该设计器还是一个单向代码生成器。 这表示代码文件中只反映对设计器图面所做的更改。 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]中不会反映对代码文件的手动更改。 在保存设计器并重新生成代码时，将覆盖在代码文件中手动进行的所有更改。 了解如何添加用户代码和扩展由生成的类[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]，请参阅[如何：扩展 O/R 设计器生成的代码](../data-tools/how-to-extend-code-generated-by-the-o-r-designer.md)。

## <a name="creating-and-configuring-the-datacontext"></a>创建和配置 DataContext
 添加后**LINQ to SQL 类**项到项目并打开[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]，空设计图面表示一个空<xref:System.Data.Linq.DataContext>可对其进行配置。 <xref:System.Data.Linq.DataContext>配置通过拖动到设计图面上的第一项提供的连接信息... 因此，<xref:System.Data.Linq.DataContext> 是使用放置到设计图面上的第一项中的连接信息进行配置的。 有关详细信息<xref:System.Data.Linq.DataContext>类，请参阅[DataContext 方法 （O/R 设计器）](../data-tools/datacontext-methods-o-r-designer.md)。

## <a name="creating-entity-classes-that-map-to-database-tables-and-views"></a>创建映射到数据库表和视图的实体类
 可以创建实体类映射到表和视图，通过将数据库表和视图从**服务器资源管理器**/**数据库资源管理器**拖到[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]。 正如上一节中所述，<xref:System.Data.Linq.DataContext> 是使用拖动到设计图面上的第一项所提供的连接信息进行配置的。 如果将一个使用不同连接的后续项添加到 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]中，您可以更改 <xref:System.Data.Linq.DataContext> 的连接。 有关详细信息，请参阅[如何：创建映射到表和视图的 LINQ to SQL 类（O/R 设计器）](../data-tools/how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)。

## <a name="creating-datacontext-methods-that-call-stored-procedures-and-functions"></a>创建调用存储过程和函数的 DataContext 方法
 您可以创建<xref:System.Data.Linq.DataContext>调用的方法 （映射到中） 存储过程和函数，通过将其从拖动**服务器资源管理器**/**数据库资源管理器**到[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]. 存储过程和函数作为 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] 的方法添加到 <xref:System.Data.Linq.DataContext>中。

> [!NOTE]
> 当您将存储的过程和函数从**服务器资源管理器**/**数据库资源管理器**拖动到[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]，生成的返回类型<xref:System.Data.Linq.DataContext>方法不同具体取决于项的放置位置。 有关详细信息，请参阅[DataContext 方法 （O/R 设计器）](../data-tools/datacontext-methods-o-r-designer.md)。

## <a name="configuring-a-datacontext-to-use-stored-procedures-to-save-data-between-entity-classes-and-a-database"></a>配置 DataContext 以使用存储过程来保存实体类和数据库之间的数据
 如上文所述，您可以创建调用存储过程和函数的 <xref:System.Data.Linq.DataContext> 方法。 此外，您还可以分配执行插入、更新和删除操作的默认 [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] 运行时行为可以使用的存储过程。 有关详细信息，请参阅[如何：分配存储过程以便执行更新、插入和删除操作（O/R 设计器）](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md)。

## <a name="inheritance-and-the-or-designer"></a>继承和 O/R 设计器
 像其他对象一样，[!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] 类可以使用继承，并可从其他类派生。 在数据库中，可通过多种方式创建继承关系。 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]支持通常在关系系统中实现的单表继承概念。 有关详细信息，请参阅[如何：使用 O/R 设计器配置继承](../data-tools/how-to-configure-inheritance-by-using-the-o-r-designer.md)。

## <a name="linq-to-sql-queries"></a>LINQ to SQL 查询
 创建的实体类[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]设计用于[LINQ （语言集成查询）](https://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d)。 有关详细信息，请参阅[如何：有关信息的查询](https://msdn.microsoft.com/library/e538d288-2070-40ca-9da6-4fbc68cd6ad0)。

## <a name="separating-the-generated-datacontext-and-entity-class-code-into-different-namespaces"></a>将生成的 DataContext 和实体类代码分离到不同的命名空间
 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]提供了**上下文 Namespace**并**实体 Namespace**上的属性<xref:System.Data.Linq.DataContext>。 这些属性决定 <xref:System.Data.Linq.DataContext> 和实体类代码生成到哪个命名空间。 默认情况下，这些属性为空并且 <xref:System.Data.Linq.DataContext> 和实体类生成到应用程序的命名空间。 若要在除应用程序的命名空间以外的命名空间中生成代码，请在“上下文命名空间”和/或“实体命名空间”属性中输入一个值。

## <a name="in-this-section"></a>本节内容
 [DataContext 方法 （O/R 设计器）](../data-tools/datacontext-methods-o-r-designer.md)解释了内容<xref:System.Data.Linq.DataContext>方法以及如何创建它们。

 [数据类继承 （O/R 设计器）](../data-tools/data-class-inheritance-o-r-designer.md)介绍的概念，单表继承以及如何在中实现[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]。

 [如何：创建 LINQ to SQL 类映射到表和视图 （O/R 设计器）](../data-tools/how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)介绍如何创建映射到数据库中表和视图的实体类。

 [如何：创建 LINQ to SQL 类 （O/R 设计器） 之间的关联 （关系）](../data-tools/how-to-create-an-association-relationship-between-linq-to-sql-classes-o-r-designer.md)介绍如何创建之间的关系[!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)]实体类。

 [如何：创建映射到存储的过程和函数 （O/R 设计器） 的 DataContext 方法](../data-tools/how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-o-r-designer.md)介绍如何创建<xref:System.Data.Linq.DataContext>运行存储的过程或函数调用时，它们的方法。

 [如何：分配存储的过程以便执行更新、 插入和删除操作 （O/R 设计器）](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md)介绍了如何配置<xref:System.Data.Linq.DataContext>时要使用存储的过程将数据保存从实体类返回到数据库。

 [如何：更改 DataContext 方法 （O/R 设计器） 的返回类型](../data-tools/how-to-change-the-return-type-of-a-datacontext-method-o-r-designer.md)介绍了如何设置的返回类型<xref:System.Data.Linq.DataContext>方法为实体类的类型或由 O/R 设计器创建的自动生成类型。

 [如何：向实体类添加验证](../data-tools/how-to-add-validation-to-entity-classes.md)介绍了如何生成分部方法，使属性更改和实体类更新过程添加代码。

 [如何：将复数化打开和关闭 （O/R 设计器）](../data-tools/how-to-turn-pluralization-on-and-off-o-r-designer.md)介绍如何打开和关闭添加到类的自动重命名[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]。

 [如何：通过使用 O/R 设计器配置继承](../data-tools/how-to-configure-inheritance-by-using-the-o-r-designer.md)介绍了如何配置使用单表继承中的使用的实体类[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]。

 [如何：扩展 O/R 设计器生成的代码](../data-tools/how-to-extend-code-generated-by-the-o-r-designer.md)介绍了如何以及在何处添加对 O/R 设计器上的对象的更改重新生成代码时不会被覆盖的代码。

 [演练：创建 LINQ to SQL 类通过使用单表继承 （O/R 设计器）](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md)分步说明，介绍如何配置使用单表继承中的使用的实体类[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]。

 [演练：自定义插入、 更新和删除实体类的行为](../data-tools/walkthrough-customizing-the-insert-update-and-delete-behavior-of-entity-classes.md)提供了配置的分步说明<xref:System.Data.Linq.DataContext>时要使用存储的过程将数据保存从实体类返回到数据库。

## <a name="reference-content"></a>参考内容
 <xref:System.Linq>

 <xref:System.Data.Linq>

## <a name="see-also"></a>请参阅
 [适用于.NET 的 visual Studio data tools](../data-tools/visual-studio-data-tools-for-dotnet.md) [Frequently Asked Questions](https://msdn.microsoft.com/library/252ed666-0679-4eea-b71b-2f14117ef443) [LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655) [访问 Visual Studio 中的数据](../data-tools/accessing-data-in-visual-studio.md)
