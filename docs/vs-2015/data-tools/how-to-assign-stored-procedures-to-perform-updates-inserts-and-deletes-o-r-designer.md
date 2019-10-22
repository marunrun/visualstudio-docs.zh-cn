---
title: 如何：分配存储过程以执行更新、插入和删除（O-R 设计器） |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: e88224ab-ff61-4a3a-b6b8-6f3694546cac
caps.latest.revision: 5
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 2054a55f0633d5d4add51fee2e933d9f4d829fcf
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72609978"
---
# <a name="how-to-assign-stored-procedures-to-perform-updates-inserts-and-deletes-or-designer"></a>如何：分配存储流程来执行更新、插入和删除操作（O/R 设计器）
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以将存储过程添加到 O/R 设计器并作为典型的 <xref:System.Data.Linq.DataContext> 方法执行。 将更改从实体类保存到数据库时（例如在调用 [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] 方法时），还可以使用存储过程重写执行插入、更新和删除操作的默认 <xref:System.Data.Linq.DataContext.SubmitChanges%2A> 运行时行为。

> [!NOTE]
> 如果存储过程的返回值需要发送回客户端（例如在存储过程中计算出的值），则在存储过程中创建输出参数。 如果无法使用输出参数，则编写分部方法实现，而不是依靠 O/R 设计器生成的重写。 在成功完成 INSERT 或 UPDATE 操作后，需要将映射到数据库生成的值的成员设置为相应的值。 有关详细信息，请参阅[开发人员在重写默认行为中的责任](https://msdn.microsoft.com/library/c6909ddd-e053-46a8-980c-0e12a9797be1)。

> [!NOTE]
> [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] 会自动为标识（自动递增）列、rowguidcol（数据库生成的 GUID）列和时间戳列处理数据库生成的值。 在其他列类型中，数据库生成的值将意外导致 Null 值。 若要返回数据库生成的值，应手动将 <xref:System.Data.Linq.Mapping.ColumnAttribute.IsDbGenerated%2A> 设置为 `true` 并将 <xref:System.Data.Linq.Mapping.ColumnAttribute.AutoSync%2A> 设置为下列值之一：<xref:System.Data.Linq.Mapping.AutoSync>、<xref:System.Data.Linq.Mapping.AutoSync> 或 <xref:System.Data.Linq.Mapping.AutoSync>。

## <a name="configuring-the-update-behavior-of-an-entity-class"></a>配置实体类的更新行为
 默认情况下，在使用对 [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] 实体类中的数据所做的更改来更新数据库（插入、更新和删除）时，更新逻辑是由 [!INCLUDE[vbtecdlinq](../includes/vbtecdlinq-md.md)] 运行时提供的。 运行时创建默认的 Insert、Update 和 Delete 命令，这些命令基于表的架构（列和主键信息）。 当不需要默认行为时，可以通过分配特定的存储过程，以执行操作表中数据所必需的插入、更新和删除来配置更新行为。 在不生成默认行为时（例如，实体类映射到视图时），也可以这样做。 最后，在数据库要求通过存储过程访问表时，您可以重写默认的更新行为。

 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]

#### <a name="to-assign-stored-procedures-to-override-the-default-behavior-of-an-entity-class"></a>指定存储过程以重写实体类的默认行为

1. 在设计器中打开“LINQ to SQL”文件。 （双击**解决方案资源管理器**中的 .dbml 文件。）

2. 在**服务器资源管理器**/**数据库资源管理器**中，展开 "**存储过程**" 并找到要用于实体类的 Insert、Update 和/或 Delete 命令的存储过程。

3. 将该存储过程拖到 O/R 设计器上。

     该存储过程将作为 <xref:System.Data.Linq.DataContext> 方法添加到方法窗格中。 有关详细信息，请参阅[DataContext 方法（O/R 设计器）](../data-tools/datacontext-methods-o-r-designer.md)。

4. 选择要使用存储过程对其执行更新的实体类。

5. 在“属性”窗口中选择要替代的命令（“插入”、“更新”或“删除”）。

6. 单击“使用运行时”旁边的省略号 (...) 以打开“配置行为”对话框。

7. 选择“自定义”。

8. 在“自定义”列表中选择所需的存储过程。

9. 检查“方法自变量”和“类属性”列表以验证“方法自变量”是否映射到相应的“类属性”。 将原始方法参数（Original_*g*）映射到用于 Update 和 Delete 命令的原始属性（*PropertyName* （原始））。

    > [!NOTE]
    > 默认情况下，名称匹配时方法自变量映射到类属性。 如果更改的属性名称在表和实体类之间不再匹配，而设计器无法确定正确的映射，您可能需要选择等效的类属性进行映射。

10. 单击“确定”或“应用”。

    > [!NOTE]
    > 只要在每次更改后单击“应用”，就可以继续为每个类/行为组合配置行为。 如果在单击 "**应用**" 之前更改类或行为，则会出现一个警告对话框，其中显示了应用任何更改的机会。

     要恢复为使用默认的运行时逻辑，请在 "**属性**" 窗口中单击 "插入"、"更新" 或 "删除" 命令旁边的省略号，然后在 "**配置行为**" 对话框中选择 "**使用运行时**"。

## <a name="see-also"></a>请参阅
 [LINQ to SQL Visual Studio](../data-tools/linq-to-sql-tools-in-visual-studio2.md) [DataContext 方法（o/R 设计器）](../data-tools/datacontext-methods-o-r-designer.md)中的工具[演练：创建 LINQ to SQL 类（o-r 设计器）](https://msdn.microsoft.com/library/35aad4a4-2e8a-46e2-ae09-5fbfd333c233) [LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655) [插入、更新和删除操作](https://msdn.microsoft.com/library/26a43a4f-83c9-4732-806d-bb23aad0ff6b)
