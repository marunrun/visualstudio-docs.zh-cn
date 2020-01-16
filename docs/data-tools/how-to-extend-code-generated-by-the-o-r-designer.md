---
title: 如何：扩展由 O-R 设计器生成的代码
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: d6d1122e-2f55-4607-8d8b-48c3c22600fb
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 588eb0f61dbc16fb1625752417ac5257bf48320f
ms.sourcegitcommit: f3f668ecaf11b4c2738ebc91923c6b5e38e74670
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/16/2020
ms.locfileid: "76113684"
---
# <a name="how-to-extend-code-generated-by-the-or-designer"></a>如何：扩展由 O/R 设计器生成的代码
当对实体类和设计器图面上的其他对象进行更改时，将重新生成由**O/R 设计器**生成的代码。 当设计器重新生成代码时，你添加到生成的代码中的任何代码一般都会被重新声称的代码覆盖。 **O/R 设计器**提供生成分部类文件的功能，在这些文件中，您可以添加不覆盖的代码。 将你自己的代码添加到**O/R 设计器**生成的代码的一个示例是将数据验证添加到 LINQ to SQL （实体）类中。 有关详细信息，请参阅[如何：向实体类添加验证](../data-tools/how-to-add-validation-to-entity-classes.md)。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="add-code-to-an-entity-class"></a>向实体类中添加代码

### <a name="to-create-a-partial-class-and-add-code-to-an-entity-class"></a>创建分部类并向实体类中添加代码

1. 在**O/R 设计器**中打开或创建一个新的 LINQ to SQL 类文件（ **.dbml**文件）。 （双击**解决方案资源管理器**或**数据库资源管理器**中的 **.dbml**文件。）

2. 在 O/R 设计器中，右键单击要为其添加验证的类，然后单击“查看代码”。

     将打开代码编辑器，其中显示所选实体类的分部类。

3. 在该实体类的分部类声明中添加您的代码。

## <a name="add-code-to-a-datacontext"></a>向 DataContext 中添加代码

### <a name="to-create-a-partial-class-and-add-code-to-a-datacontext"></a>创建分部类并向 DataContext 中添加代码

1. 在**O/R 设计器**中打开或创建一个新的 LINQ to SQL 类文件（ **.dbml**文件）。 （双击**解决方案资源管理器**或**数据库资源管理器**中的 **.dbml**文件。）

2. 在**O/R 设计器**中，右键单击设计器上的空白区域，然后单击 "**查看代码**"。

     将打开代码编辑器，其中显示 DataContext 的分部类。

3. 在 DataContext 的分部类声明中添加您的代码。

## <a name="see-also"></a>另请参阅

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [演练：创建 LINQ to SQL 类（O-R 设计器）](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)
