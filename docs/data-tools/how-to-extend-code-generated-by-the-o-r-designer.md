---
title: 如何：扩展 O-R 设计器生成的代码
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: d6d1122e-2f55-4607-8d8b-48c3c22600fb
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: e82166ab336023812c63045c031b81d94dea67e0
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62566991"
---
# <a name="how-to-extend-code-generated-by-the-or-designer"></a>如何：扩展 O/R 设计器生成的代码
生成的代码**O/R 设计器**向实体类和设计器图面上的其他对象进行更改时重新生成。 当设计器重新生成代码时，你添加到生成的代码中的任何代码一般都会被重新声称的代码覆盖。 **O/R 设计器**提供了生成分部类文件可以在其中添加功能不会被覆盖的代码。 将你自己的代码添加到生成的代码的一个示例**O/R 设计器**添加数据验证到 LINQ to SQL （实体） 类。 有关详细信息，请参阅[如何：在实体类中添加验证](../data-tools/how-to-add-validation-to-entity-classes.md)。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="add-code-to-an-entity-class"></a>将代码添加到实体类

### <a name="to-create-a-partial-class-and-add-code-to-an-entity-class"></a>创建分部类并向实体类中添加代码

1. 打开或创建一个新的 LINQ to SQL 类文件 (**.dbml**文件) 中**O/R 设计器**。 (双击 **.dbml**中的文件**解决方案资源管理器**或**数据库资源管理器**。)

2. 在 O/R 设计器中，右键单击要为其添加验证的类，然后单击“查看代码”。

     将打开代码编辑器，其中显示所选实体类的分部类。

3. 在该实体类的分部类声明中添加您的代码。

## <a name="add-code-to-a-datacontext"></a>将代码添加到 DataContext

### <a name="to-create-a-partial-class-and-add-code-to-a-datacontext"></a>创建分部类并向 DataContext 中添加代码

1. 打开或创建一个新的 LINQ to SQL 类文件 (**.dbml**文件) 中**O/R 设计器**。 (双击 **.dbml**中的文件**解决方案资源管理器**或**数据库资源管理器**。)

2. 在中**O/R 设计器**，右键单击设计器上的空白区域，然后单击**查看代码**。

     将打开代码编辑器，其中显示 DataContext 的分部类。

3. 在 DataContext 的分部类声明中添加您的代码。

## <a name="see-also"></a>请参阅

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [演练：创建 LINQ to SQL 类（O-R 设计器）](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)