---
title: 如何：使用 O-R 设计器配置继承 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: e594af12-e777-434a-bc08-7dd2dac84cdc
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 7f8c08546fdf96c755b3adb80021ab7269509739
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72654708"
---
# <a name="how-to-configure-inheritance-by-using-the-or-designer"></a>如何：通过 O/R 设计器配置继承
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vs_ordesigner_long](../includes/vs-ordesigner-long-md.md)]（[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]）支持通常在关系系统中实现的单表继承概念。 在单表继承中，一个数据库表同时包含父信息和子信息的字段。 使用关系数据时，一个鉴别器列包含的值确定任意记录属于哪个类。

 例如，考虑一个包含公司所有员工的 Persons 表。 一些人是员工，一些人是经理。 Persons 表包含一个名为 `EmployeeType` 的列，其中值 1 表示经理，值 2 表示员工。这个列就是鉴别器列。 在此应用场景中，可以创建一个员工子类，并仅使用 `EmployeeType` 值为 2 的记录来填充该类。 还可以从每个类中移除不适用的列。

 创建一个使用继承（并对应于关系数据）的对象模型可能有些不易理解。 下面的过程概括说明使用 O/R 设计器配置继承所需的步骤。 如果不对照现有的表和列实际操作，则可能很难理解和掌握一般性的操作步骤，因此我们提供了一个使用数据的演练。 有关使用 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] 配置继承的详细分步说明，请参阅[演练：使用单表继承创建 LINQ to SQL 类（O/R 设计器）](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md)。

### <a name="to-create-inherited-data-classes"></a>创建继承的数据类

1. 通过向现有 Visual Basic 或C#项目中添加**LINQ to SQL 类**项来打开 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]。

2. 将要用作基类的表拖到 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]上。

3. 将该表的第二个副本拖到 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]上并重命名该副本。 这是派生类，即子类。

4. 在“工具箱”的“对象关系设计器”选项卡中单击“继承”，然后单击子类（重命名的表）并将其连接到基类。

    > [!NOTE]
    > 单击“工具箱”中的“继承”项，释放鼠标按钮，单击在步骤 3 中创建的该类的第二个副本，然后单击在步骤 2 中创建的第一个类。 继承连线中的箭头将指向第一个类。

5. 在每个类中，删除任何不希望显示和没有用于关联的对象属性。 如果您尝试删除用于关联的对象属性，您将收到错误：[无法删除属性 \<property 名称 >，因为它参与了关联 \<association 名称 >](../data-tools/the-property-property-name-cannot-be-deleted-because-it-is-participating-in-the-association-association-name.md)。

    > [!NOTE]
    > 由于派生类继承其基类中定义的属性，在每个类中不能定义相同的列。 （列作为属性实现。）您可以通过在基类的属性上设置继承修饰符来启用在派生类中创建列。 有关详细信息，请参阅[不在生成中：重写属性和方法](https://msdn.microsoft.com/2167e8f5-1225-4b13-9ebd-02591ba90213)。

6. 在 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]中选择继承连线。

7. 在 "**属性**" 窗口中，将 "鉴别器"**属性**设置为用于区分类中的记录的列名称。

8. 将“派生类鉴别器值”属性设置为数据库中将记录指定为继承类型的值。 （这是存储在鉴别器列中的值，用于指定继承的类。）

9. 将“基类鉴别器值”属性设置为将记录指定为基类型的值。 （这是存储在鉴别器列中的值，用于指定基类。）

10. （可选）还可以设置“继承默认值”属性，以便在继承层次结构中指定类型，当加载与任何定义的继承代码都不匹配的行时将使用该类型。 换句话说，如果记录在其鉴别器列中的值与 "**派生类鉴别器值**" 或 "**基类鉴别**器值" 属性中的值不匹配，则该记录将加载到指定为**继承默认值**。

## <a name="see-also"></a>请参阅
 [LINQ to SQL Visual studio 中的工具](../data-tools/linq-to-sql-tools-in-visual-studio2.md)[演练：创建 LINQ to SQL 类（O-R 设计器）](https://msdn.microsoft.com/library/35aad4a4-2e8a-46e2-ae09-5fbfd333c233) [PAVE Visual Studio 2012 中的数据应用程序开发的新增功能](https://msdn.microsoft.com/3d50d68f-5f44-4915-842f-6d42fce793f1)[访问 visual studio 中的数据](../data-tools/accessing-data-in-visual-studio.md) [LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655) [演练：使用单表继承（O/R 设计器）创建 LINQ to SQL 类](../data-tools/walkthrough-creating-linq-to-sql-classes-by-using-single-table-inheritance-o-r-designer.md)[不在生成中：继承 Visual Basic](https://msdn.microsoft.com/e5e6e240-ed31-4657-820c-079b7c79313c) [继承](https://msdn.microsoft.com/library/81d64ee4-50f9-4d6c-a8dc-257c348d2eea)
