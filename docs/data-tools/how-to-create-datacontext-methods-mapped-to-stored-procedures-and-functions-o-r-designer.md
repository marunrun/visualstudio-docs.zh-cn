---
title: 将 DataContext 方法映射到 sprocs 和函数
description: 了解如何使用对象关系设计器 (O/R 设计器) 来创建映射到存储过程 (sprocs) 和函数的 DataContext 方法。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: e7ca32f1-50b3-48af-ad92-ceafd749296a
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 4cb02a7fc7fdcbb4ff3c9c3750e722ff0fe031a5
ms.sourcegitcommit: ed26b6e313b766c4d92764c303954e2385c6693e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2020
ms.locfileid: "94434943"
---
# <a name="how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-or-designer"></a>如何：创建映射到存储流程和函数的 DataContext 方法（O/R 设计器）

可以将存储过程和函数作为方法添加到 **O/R 设计器** 中 <xref:System.Data.Linq.DataContext> 。 调用该方法并传入所需参数将对数据库运行存储过程或函数，并返回 <xref:System.Data.Linq.DataContext> 方法的返回类型的数据。 有关方法的详细信息 <xref:System.Data.Linq.DataContext> ，请参阅 [DataContext 方法 (O/R Designer) ](../data-tools/datacontext-methods-o-r-designer.md)。

> [!NOTE]
> 在将 [!INCLUDE[vbtecdlinq](../data-tools/includes/vbtecdlinq_md.md)] 更改从实体类保存到数据库时，还可以使用存储过程重写执行插入、更新和删除操作的默认运行时行为。 有关详细信息，请参阅[如何：分配存储过程以便执行更新、插入和删除操作（O/R 设计器）](../data-tools/how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-o-r-designer.md)。

## <a name="create-datacontext-methods"></a>创建 DataContext 方法

可以通过将 <xref:System.Data.Linq.DataContext> 存储过程或函数从 <strong>服务器资源管理器或 * * 数据库资源管理器</strong> 拖到 **O/R 设计器** 上来创建方法。

> [!NOTE]
> 生成的方法的返回类型 <xref:System.Data.Linq.DataContext> 因您在 **O/R 设计器** 上放置存储过程或函数的位置而异。 如果直接将项放置在现有实体类上，则将创建具有该实体类返回类型的 <xref:System.Data.Linq.DataContext> 方法。 如果将项放到 **O/R 设计器** 的空白区域，则将创建 <xref:System.Data.Linq.DataContext> 返回自动生成类型的方法。 在将 <xref:System.Data.Linq.DataContext> 方法添加到方法窗格后可以更改该方法的返回类型。 若要检查或更改 <xref:System.Data.Linq.DataContext> 方法的返回类型，请选中该方法并在“属性”窗口中检查“返回类型”属性。 有关详细信息，请参阅 [如何：更改 DataContext 方法的返回类型 (O/R 设计器) ](../data-tools/how-to-change-the-return-type-of-a-datacontext-method-o-r-designer.md)。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-create-datacontext-methods-that-return-automatically-generated-types"></a>创建返回自动生成类型的 DataContext 方法

1. 在 **服务器资源管理器** 或 **数据库资源管理器** 中，展开您正在使用的数据库的 " **存储过程** " 节点。

2. 找到所需的存储过程并将其拖到 **O/R 设计器** 的空白区域。

     具有自动生成返回类型的 <xref:System.Data.Linq.DataContext> 方法即被创建，并出现在“方法”窗格中。

### <a name="to-create-datacontext-methods-that-have-the-return-type-of-an-entity-class"></a>创建具有实体类的返回类型的 DataContext 方法

1. 在 **服务器资源管理器** 或 **数据库资源管理器** 中，展开您正在使用的数据库的 " **存储过程** " 节点。

2. 找到所需的存储过程并将其拖到 **O/R 设计器** 中的现有实体类。

     具有所选实体类的返回类型的 <xref:System.Data.Linq.DataContext> 方法即被创建，并出现在“方法”窗格中。

> [!NOTE]
> 有关更改返回类型的现有<xref:System.Data.Linq.DataContext>方法，请参阅[如何：更改 DataContext 方法的返回类型（O/R 设计器）](../data-tools/how-to-change-the-return-type-of-a-datacontext-method-o-r-designer.md)。

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [DataContext 方法 (O/R 设计器) ](../data-tools/datacontext-methods-o-r-designer.md)
- [演练：创建 LINQ to SQL 类](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)
- [Visual Basic 中的 LINQ 简介](/dotnet/visual-basic/programming-guide/language-features/linq/introduction-to-linq)
- [C# 中的 LINQ](/dotnet/csharp/linq/linq-in-csharp)
