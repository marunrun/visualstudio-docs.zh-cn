---
title: 更改 DataContext 方法的返回类型（O-R 设计器）
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: c5b66bff-6dbb-43c0-bffa-317133ca5b9e
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: fac3a26f77151d7e09b620ef084d42a9ab50f1e5
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75586531"
---
# <a name="how-to-change-the-return-type-of-a-datacontext-method-or-designer"></a>如何：更改 DataContext 方法的返回类型（O/R 设计器）
基于存储过程或函数创建的 <xref:System.Data.Linq.DataContext> 方法的返回类型有所不同，这取决于您在**O/R 设计器**中删除存储过程或函数的位置。 如果直接将项放置在现有实体类上，则将创建具有该实体类返回类型的 <xref:System.Data.Linq.DataContext> 方法（如果该存储过程或函数返回的数据架构与实体类的形状相匹配）。 如果将项放到**O/R 设计器**的空白区域，则将创建返回自动生成类型的 <xref:System.Data.Linq.DataContext> 方法。 在将 <xref:System.Data.Linq.DataContext> 方法添加到方法窗格后可以更改该方法的返回类型。 若要检查或更改 <xref:System.Data.Linq.DataContext> 方法的返回类型，请选中该方法并在“属性”窗口中单击“返回类型”属性。

> [!NOTE]
> 不能使用“属性”窗口将返回类型设置为实体类的 <xref:System.Data.Linq.DataContext> 方法恢复为返回自动生成类型。 若要将 <xref:System.Data.Linq.DataContext> 方法恢复为返回自动生成类型，必须将原始数据库对象再次拖动到 O/R 设计器上。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="to-change-the-return-type-of-a-datacontext-method-from-the-auto-generated-type-to-an-entity-class"></a>将 DataContext 方法的返回类型从自动生成类型更改为实体类

1. 在方法窗格中选择该 <xref:System.Data.Linq.DataContext> 方法。

2. 在“属性”窗口中选择“返回类型”，然后从“返回类型”列表中选择一个可用的实体类。 如果所需的实体类不在列表中，请将其添加到**O/R 设计器**中或在其中创建，以将其添加到列表。

3. 保存 .dbml 文件。

## <a name="to-change-the-return-type-of-a-datacontext-method-from-an-entity-class-back-to-the-auto-generated-type"></a>将 DataContext 方法的返回类型从实体类重新更改为自动生成类型

1. 在“方法”窗格中选择 <xref:System.Data.Linq.DataContext> 方法并删除该方法。

2. 将数据库对象从**服务器资源管理器**或**数据库资源管理器**拖到**O/R 设计器**的空白区域。

3. 保存 .dbml 文件。

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)
- [DataContext 方法（O/R 设计器）](../data-tools/datacontext-methods-o-r-designer.md)
- [如何：创建映射到存储过程和函数的 DataContext 方法（O/R 设计器）](../data-tools/how-to-create-datacontext-methods-mapped-to-stored-procedures-and-functions-o-r-designer.md)
