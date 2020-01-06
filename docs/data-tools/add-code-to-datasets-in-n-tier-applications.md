---
title: 向 n 层应用程序中的数据集添加代码
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- n-tier applications, extending DataSets
ms.assetid: d43c2ccd-4902-43d8-b1a8-d10ca5d3210c
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 3d35ff68144e92af12f2ee6284076118493c6be9
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75587116"
---
# <a name="add-code-to-datasets-in-n-tier-applications"></a>向 n 层应用程序中的数据集添加代码

您可以扩展数据集的功能，方法是为数据集创建一个分部类文件并向其添加代码（而不是将代码添加到*DatasetName*中。数据集. 设计器文件）。 分部类使特定类的代码可以在多个物理文件之间进行分隔。 有关详细信息，请参阅[分部](/dotnet/visual-basic/language-reference/modifiers/partial)或[分部类和方法](/dotnet/csharp/programming-guide/classes-and-structs/partial-classes-and-methods)。

每次对数据集定义进行更改（在类型化数据集中），都将生成定义数据集的代码。 当你在运行任何修改数据集配置的向导期间进行更改时，也会生成此代码。 若要防止在重新生成数据集的过程中删除代码，请将代码添加到数据集的分部类文件中。

默认情况下，在分离数据集和 TableAdapter 代码后，结果是每个项目中的离散类文件。 原始项目包含一个名为*DatasetName* （或*DatasetName.Designer.cs*）的文件，该文件包含 TableAdapter 代码。 **数据集项目**属性中指定的项目包含一个名为*DatasetName* （或*DatasetName.DataSet.Designer.cs*）的文件。此文件包含数据集代码。

> [!NOTE]
> 分离数据集和 Tableadapter （通过设置 "**数据集项目**" 属性）时，不会自动移动项目中的现有部分数据集类。 必须将现有数据集分部类手动移动到 dataset 项目。

> [!NOTE]
> 需要添加验证代码时，类型化数据集提供生成 <xref:System.Data.DataTable.ColumnChanging> 和 <xref:System.Data.DataTable.RowChanging> 事件处理程序的功能。 有关详细信息，请参阅[将验证添加到 n 层数据集](../data-tools/add-validation-to-an-n-tier-dataset.md)。

## <a name="to-add-code-to-datasets-in-n-tier-applications"></a>将代码添加到 n 层应用程序中的数据集

1. 找到包含 *.xsd*文件的项目。

2. 选择 **.xsd**文件以打开数据集。

3. 右键单击要向其添加代码的数据表（标题栏中的表名称），然后选择 "**查看代码**"。

     将创建一个分部类并在代码编辑器中打开它。

4. 将代码添加到分部类声明中。

     下面的示例演示在 NorthwindDataSet 中将代码添加到 CustomersDataTable 的位置：

    ```vb
    Partial Public Class CustomersDataTable
        ' Add code here to add functionality
        ' to the CustomersDataTable.
    End Class
    ```

    ```csharp
    partial class CustomersDataTable
    {
        // Add code here to add functionality
        // to the CustomersDataTable.
    }
    ```

## <a name="see-also"></a>另请参阅

- [N 层数据应用程序概述](../data-tools/n-tier-data-applications-overview.md)
- [向 N 层应用程序中的 TableAdapter 添加代码](../data-tools/add-code-to-tableadapters-in-n-tier-applications.md)
- [创建和配置 Tableadapter](create-and-configure-tableadapters.md)
- [分层更新概述](hierarchical-update.md)
- [Visual Studio 中的数据集工具](../data-tools/dataset-tools-in-visual-studio.md)
