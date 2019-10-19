---
title: DataContext 方法（O-R 设计器）
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: c149f4e5-3b61-4c33-892e-3e26d47f3eeb
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 0e81f2337931f565e0068a852bf9b8284350690c
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72648545"
---
# <a name="datacontext-methods-or-designer"></a>DataContext 方法（O/R 设计器）

<xref:System.Data.Linq.DataContext> 方法（在[Visual Studio 中 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)的上下文中）是在数据库中运行存储过程和函数的 <xref:System.Data.Linq.DataContext> 类的方法。

<xref:System.Data.Linq.DataContext> 类是一个 [!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] 类，它充当 SQL Server 数据库与映射到该数据库的 [!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] 实体类之间的管道。 <xref:System.Data.Linq.DataContext> 类包含用于连接数据库以及操作数据库数据的连接字符串信息和方法。 默认情况下，<xref:System.Data.Linq.DataContext> 类包含多个可以调用的方法，例如用于将已更新数据从 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 类发送到数据库的 [!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] 方法。 还可以创建其他映射到存储过程和函数的 <xref:System.Data.Linq.DataContext> 方法。 换句话说，调用这些自定义方法将在 <xref:System.Data.Linq.DataContext> 方法映射到的数据库中运行存储过程或函数。 和可以添加方法对任何类进行扩展一样，您也可以将新方法添加到 <xref:System.Data.Linq.DataContext> 类。 但是，在对**O/R 设计器**上下文中 <xref:System.Data.Linq.DataContext> 方法的讨论中，这是映射到所讨论的存储过程和函数的 <xref:System.Data.Linq.DataContext> 方法。

## <a name="methods-pane"></a>方法窗格

映射到存储过程和函数的 <xref:System.Data.Linq.DataContext> 方法将显示在**O/R 设计器**的 "**方法**" 窗格中。 “方法”窗格位于“实体”窗格（主设计图面）的旁边。 "**方法**" 窗格列出了通过使用**O/R 设计器**创建的所有 <xref:System.Data.Linq.DataContext> 方法。 默认情况下，**方法**窗格为空;将存储过程或函数从**服务器资源管理器**或**数据库资源管理器**拖到**O/R 设计器**上，以创建 <xref:System.Data.Linq.DataContext> 方法并填充**方法**窗格。 有关详细信息，请参阅[如何：创建映射到存储过程和函数的 DataContext 方法（O/R 设计器）](../data-tools/how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-o-r-designer.md)。

> [!NOTE]
> 打开并关闭方法窗格，方法是右键单击**O/R 设计器**，然后单击 **"隐藏方法窗格**" 或 "**显示方法窗格**"，或使用键盘快捷方式**CTRL** +**1**。

## <a name="two-types-of-datacontext-methods"></a>DataContext 方法的两种类型

DataContext 方法指的是那些映射到数据库中的存储过程和函数的方法。 可以在**O/R 设计器**的**方法**窗格中创建和添加 DataContext 方法。 有两种不同类型的 <xref:System.Data.Linq.DataContext> 方法；一种会返回一个或多个结果集，而另一种则不会：

- 返回一个或多个结果集的 <xref:System.Data.Linq.DataContext> 方法：

   如果应用程序只需运行数据库中的存储过程和函数并返回结果，可创建这种 <xref:System.Data.Linq.DataContext> 方法。 有关详细信息，请参阅[如何：创建映射到存储过程和函数的 DataContext 方法（O/R 设计器）](../data-tools/how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-o-r-designer.md)、ISingleResult \<T > 和 <xref:System.Data.Linq.IMultipleResults>。

- 不返回结果集的 <xref:System.Data.Linq.DataContext> 方法，例如：对特定实体类执行插入、更新和删除操作。

   如果应用程序需要运行存储过程而不是使用默认 <xref:System.Data.Linq.DataContext> 行为来保存实体类和数据库之间修改的数据，可创建这种 [!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] 方法。 有关详细信息，请参阅[如何：分配存储过程以执行更新、插入和删除（O/R 设计器）](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md)。

## <a name="return-types-of-datacontext-methods"></a>DataContext 方法的返回类型

在将存储过程和函数从**服务器资源管理器**或**数据库资源管理器**拖到**O/R 设计器**上时，生成的 <xref:System.Data.Linq.DataContext> 方法的返回类型会有所不同，具体取决于放置项的位置。 直接将项放在现有实体类上将创建一个 <xref:System.Data.Linq.DataContext> 方法，该方法具有实体类的返回类型;将项拖放到**O/R 设计器**的空白区域（在任一窗格中）将创建返回自动生成类型的 <xref:System.Data.Linq.DataContext> 方法。 自动生成的类型具有与存储过程或函数名称和属性（映射到存储过程或函数所返回的字段）匹配的名称。

> [!NOTE]
> 在将 <xref:System.Data.Linq.DataContext> 方法添加到方法窗格后可以更改该方法的返回类型。 若要检查或更改 <xref:System.Data.Linq.DataContext> 方法的返回类型，请选中该方法并在“属性”窗口中检查“返回类型”属性。 有关详细信息，请参阅[如何：更改 DataContext 方法的返回类型（O/R 设计器）](../data-tools/how-to-change-the-return-type-of-a-datacontext-method-o-r-designer.md)。

从数据库拖动到 O/R 设计器图面上的对象将根据数据库中对象的名称自动命名。 如果多次拖动相同的对象，则会将数字添加到新名称的末尾，以区分名称。 如果数据库对象名称包含空格或 Visual Basic 或 C# 中不支持的字符，将使用下划线替代空格或无效字符。

## <a name="see-also"></a>请参阅

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)
- [存储过程](/dotnet/framework/data/adonet/sql/linq/stored-procedures)
- [如何：创建映射到存储过程和函数的 DataContext 方法（O/R 设计器）](../data-tools/how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-o-r-designer.md)
- [如何：分配存储过程以便执行更新、插入和删除操作（O/R 设计器）](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md)
- [演练：自定义实体类的插入、更新和删除行为](../data-tools/walkthrough-customizing-the-insert-update-and-delete-behavior-of-entity-classes.md)
- [演练：创建 LINQ to SQL 类（O-R 设计器）](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)