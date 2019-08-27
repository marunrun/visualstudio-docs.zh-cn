---
title: 如何：使用 O-R 设计器配置继承
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: e594af12-e777-434a-bc08-7dd2dac84cdc
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 8927e6140792c12f42f1822afd0e715881384f1c
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63402808"
---
# <a name="how-to-configure-inheritance-by-using-the-or-designer"></a>如何：使用 O/R 设计器配置继承
**对象关系设计器**(**O/R 设计器**) 支持通常在关系系统中实现的单表继承概念。 在单表继承中，一个数据库表同时包含父信息和子信息的字段。 使用关系数据时，一个鉴别器列包含的值确定任意记录属于哪个类。

例如，考虑`Persons`表，该表包含所有员工的公司。 一些人是员工，一些人是经理。 `Persons`表包含一个名为列`EmployeeType`的员工的经理和值为 2 的值为 1; 这是鉴别器列。 在此应用场景中，可以创建一个员工子类，并仅使用 `EmployeeType` 值为 2 的记录来填充该类。 还可以从每个类中移除不适用的列。

创建一个使用继承（并对应于关系数据）的对象模型可能有些不易理解。 下面的过程概括说明使用 O/R 设计器配置继承所需的步骤。 按照一般步骤而不引用现有的表和列可能会非常困难，因此提供一个使用数据的演练。 有关配置继承的使用的详细分步指导**O/R 设计器**，请参阅[演练：创建 LINQ to SQL 类通过使用单表继承 （O/R 设计器）](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md)。

## <a name="to-create-inherited-data-classes"></a>创建继承的数据类

1. 打开**O/R 设计器**通过添加**LINQ to SQL 类**到现有 Visual Basic 或 C# 项目的项。

2. 将你想要用作基类拖到的表**O/R 设计器**。

3. 将表拖放到第二个副本拖**O/R 设计器**并将其重命名。 这是派生类，即子类。

4. 在“工具箱”的“对象关系设计器”选项卡中单击“继承”，然后单击子类（重命名的表）并将其连接到基类。

    > [!NOTE]
    > 单击“工具箱”中的“继承”项，释放鼠标按钮，单击在步骤 3 中创建的该类的第二个副本，然后单击在步骤 2 中创建的第一个类。 继承连线上的箭头指向第一个类。

5. 在每个类中，删除任何不希望显示和没有用于关联的对象属性。 如果尝试删除用于关联的对象属性，收到的错误：[该属性\<属性名称 > 不能删除，因为它参与了关联\<关联名称 >](../data-tools/the-property-property-name-cannot-be-deleted-because-it-is-participating-in-the-association-association-name.md)。

    > [!NOTE]
    > 由于派生类继承其基类中定义的属性，在每个类中不能定义相同的列。 （列实现为属性。）通过设置基类属性中的继承修饰符，可以在派生类中创建列。 有关详细信息，请参阅[继承的基础知识 (Visual Basic)](/dotnet/visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics)。

6. 选择中的继承连线**O/R 设计器**。

7. 在中**属性**窗口中，将**鉴别器属性**为区分您的类中记录的列名称。

8. 将“派生类鉴别器值”属性设置为数据库中将记录指定为继承类型的值。 （这是存储在鉴别器列中，用于指定继承的类的值）。

9. 将“基类鉴别器值”属性设置为将记录指定为基类型的值。 （这是存储在鉴别器列中，用于指定基的类的值）。

10. （可选）还可以设置“继承默认值”属性，以便在继承层次结构中指定类型，当加载与任何定义的继承代码都不匹配的行时将使用该类型。 换而言之，如果一条记录在其鉴别器列中的值不匹配的值中任意一种**派生类鉴别器值**或**基类鉴别器值**属性，则请记录将加载到指定为类型**继承默认值**。

## <a name="see-also"></a>请参阅

- [Visual Studio 中的 LINQ to SQL 工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)
- [演练：创建 LINQ to SQL 类（O-R 设计器）](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)
- [在 Visual Studio 中访问数据](../data-tools/accessing-data-in-visual-studio.md)
- [LINQ to SQL](/dotnet/framework/data/adonet/sql/linq/index)
- [演练：使用单表继承创建 LINQ to SQL 类（O/R 设计器）](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md)
- [继承的基础知识 (Visual Basic)](/dotnet/visual-basic/programming-guide/language-features/objects-and-classes/inheritance-basics)
- [继承](/dotnet/csharp/programming-guide/classes-and-structs/inheritance)