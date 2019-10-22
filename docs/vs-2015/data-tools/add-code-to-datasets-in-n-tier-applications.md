---
title: 将代码添加到 n 层应用程序中的数据集 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- n-tier applications, extending datasets
ms.assetid: d43c2ccd-4902-43d8-b1a8-d10ca5d3210c
caps.latest.revision: 23
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: aed37ee9cdd8c221fcfb114db426a6286ee8ad6f
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72673119"
---
# <a name="add-code-to-datasets-in-n-tier-applications"></a>向 n 层应用程序中的数据集添加代码
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以扩展数据集的功能，方法是为数据集创建一个分部类文件并向其添加代码（而不是将代码添加到*DatasetName*中。数据集. 设计器文件）。 分部类使特定类的代码可以在多个物理文件之间进行分隔。 有关详细信息，请参阅[分部](https://msdn.microsoft.com/library/7adaef80-f435-46e1-970a-269fff63b448)或[分部类和方法](https://msdn.microsoft.com/library/804cecb7-62db-4f97-a99f-60975bd59fa1)。

每次对数据集定义进行更改时，都会生成定义数据集的代码。 当你在运行任何修改数据集配置的向导期间进行更改时，也会生成此代码。 若要防止在重新生成数据集的过程中删除代码，请将代码添加到数据集的分部类文件中。

默认情况下，在将数据集和 `TableAdapter` 代码分离后，结果为每个项目中的离散类文件。 原始项目有一个 filenamed *DatasetName*。设计器 .vb （或*DatasetName*。Designer.cs）包含 `TableAdapter` 代码。 **数据集项目**属性中指定的项目包含一个名为 " *DatasetName*" 的文件。数据集 .vb （或*DatasetName*。DataSet.Designer.cs）。此文件包含数据集代码。

> [!NOTE]
> 分离数据集和 `TableAdapter`s （通过设置 "**数据集项目**" 属性）时，不会自动移动项目中的现有部分数据集类。 必须将现有数据集分部类手动移动到 dataset 项目。

> [!NOTE]
> 需要添加验证代码时，数据集设计器提供生成 <xref:System.Data.DataTable.ColumnChanging> 和 <xref:System.Data.DataTable.RowChanging> 事件处理程序的功能。 有关详细信息，请参阅[将验证添加到 n 层数据集](../data-tools/add-validation-to-an-n-tier-dataset.md)。

## <a name="add-code-to-datasets-in-n-tier-applications"></a>向 n 层应用程序中的数据集添加代码

1. 找到包含 .xsd 文件的项目（数据集）。

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

## <a name="see-also"></a>请参阅

- [N 层数据应用程序概述](../data-tools/n-tier-data-applications-overview.md)
- [向 N 层应用程序中的 TableAdapter 添加代码](../data-tools/add-code-to-tableadapters-in-n-tier-applications.md)
- [Tableadapter](https://msdn.microsoft.com/library/09416de9-134c-4dc7-8262-6c8d81e3f364)
- [TableAdapterManager 概述](https://msdn.microsoft.com/library/33076d42-6b41-491a-ac11-6c6339aea650)
- [分层更新概述](https://msdn.microsoft.com/library/c4f8e8b9-e4a5-4a02-8462-d03d1e8222d6)
- [Visual Studio 中的数据集工具](../data-tools/dataset-tools-in-visual-studio.md)