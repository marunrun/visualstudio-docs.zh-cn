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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 6c788e422ea8613b77d7d0c0460d7c026916baa3
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65697158"
---
# <a name="add-code-to-datasets-in-n-tier-applications"></a>向 n 层应用程序中的数据集添加代码
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以通过创建数据集的分部类文件并将代码添加到该扩展数据集的功能 (而不是将代码添加到*DatasetName*。Dataset.Designer 文件）。 分部类启用划分到多个物理文件的特定类代码。 有关详细信息，请参阅[分部](https://msdn.microsoft.com/library/7adaef80-f435-46e1-970a-269fff63b448)或[分部类和方法](https://msdn.microsoft.com/library/804cecb7-62db-4f97-a99f-60975bd59fa1)。

每次对数据集定义进行更改，则生成的代码定义数据集。 任何修改的数据集配置的向导运行期间进行更改时，还会生成此代码。 若要防止在数据集重新生成过程中删除你的代码，请将代码添加到数据集的分部类文件。

默认情况下之后将数据集, 和`TableAdapter`代码，结果是每个项目中的离散类文件。 原始项目将包含 filenamed *DatasetName*。Designer.vb (或*DatasetName*。Designer.cs)，其中包含`TableAdapter`代码。 中指定的项目**数据集项目**属性具有名为的文件*DatasetName*。DataSet.Designer.vb (或*DatasetName*。DataSet.Designer.cs)。此文件包含的数据集代码。

> [!NOTE]
> 分离数据集时， `TableAdapter`s (通过设置**数据集项目**属性)，将不会自动移动项目中的现有数据集分部类。 向数据集项目，必须手动移动现有数据集分部类。

> [!NOTE]
> 当需要添加验证代码时，数据集设计器提供了用于生成功能<xref:System.Data.DataTable.ColumnChanging>和<xref:System.Data.DataTable.RowChanging>事件处理程序。 有关详细信息，请参阅[向 n 层数据集添加验证](../data-tools/add-validation-to-an-n-tier-dataset.md)。

## <a name="add-code-to-datasets-in-n-tier-applications"></a>向 n 层应用程序中的数据集添加代码

1. 找到包含.xsd 文件 （数据集） 的项目。

2. 选择 **.xsd**文件打开数据集。

3. 右键单击你想要添加代码 （表中的标题栏名称），并选择的数据表**查看代码**。

     分部类将创建并在代码编辑器中打开。

4. 添加代码的分部类声明。

     下面的示例显示了将代码添加到 NorthwindDataSet 中 CustomersDataTable 的位置：

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
- [TableAdapters](https://msdn.microsoft.com/library/09416de9-134c-4dc7-8262-6c8d81e3f364)
- [TableAdapterManager 概述](https://msdn.microsoft.com/library/33076d42-6b41-491a-ac11-6c6339aea650)
- [分层更新概述](https://msdn.microsoft.com/library/c4f8e8b9-e4a5-4a02-8462-d03d1e8222d6)
- [Visual Studio 中的数据集工具](../data-tools/dataset-tools-in-visual-studio.md)