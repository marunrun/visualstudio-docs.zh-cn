---
title: 将代码添加到 n 层应用程序中的 Tableadapter |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- TableAdapters, n-tier applications
- n-tier applications, extending TableAdapters
ms.assetid: dafac00e-df9d-4d4a-95a6-e34b4d099425
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 942850e776cdd493afaad56b782b417db2040625
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72673107"
---
# <a name="add-code-to-tableadapters-in-n-tier-applications"></a>向 n 层应用程序中的 TableAdapter 添加代码
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以 `TableAdapter` 通过为创建一个分部类文件 `TableAdapter` 并向其添加代码 (而不是将代码添加到 *DatasetName*，来扩展的功能。DataSet 文件) 。 分部类使特定类的代码可以在多个物理文件之间进行分隔。 有关详细信息，请参阅 [部分](https://msdn.microsoft.com/library/7adaef80-f435-46e1-970a-269fff63b448) 或 [部分 (类型) ](https://msdn.microsoft.com/library/27320743-a22e-4c7b-b0b3-53afe3607334)。

 每次对进行更改时，都将生成定义为的代码 `TableAdapter` `TableAdapter` 。 如果在修改的配置的任何向导运行期间进行了更改，也会生成此代码 `TableAdapter` 。 若要防止在重新生成过程中删除代码 `TableAdapter` ，请将代码添加到的分部类文件中 `TableAdapter` 。

 默认情况下，在分离数据集和 `TableAdapter` 代码后，结果是每个项目中的离散类文件。 原始项目包含一个名为 " *DatasetName*" 的文件。设计器 .vb (或 *DatasetName*。包含代码的 Designer.cs) `TableAdapter` 。 **数据集项目**属性中指定的项目包含一个名为 " *DatasetName*" 的文件。 (或*DatasetName*的数据集。包含数据集代码的 DataSet.Designer.cs) 。

> [!NOTE]
> `TableAdapter`通过将**数据集项目**属性设置) 分离数据集和 (时，项目中的现有部分数据集类将不会自动移动。 必须将现有数据集分部类手动移动到 dataset 项目。

> [!NOTE]
> 数据集设计器提供 <xref:System.Data.DataTable.ColumnChanging> <xref:System.Data.DataTable.RowChanging> 在需要验证时生成和事件处理程序的功能。 有关详细信息，请参阅 [将验证添加到 n 层数据集](../data-tools/add-validation-to-an-n-tier-dataset.md)。

 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]

### <a name="to-add-user-code-to-a-tableadapter-in-an-n-tier-application"></a>将用户代码添加到 n 层应用程序中的 TableAdapter

1.  (数据集) 中找到包含 .xsd 文件的项目。

2. 双击 **.xsd** 文件打开该数据集。

3. 右键单击要向其添加代码的，然后 `TableAdapter` 选择 "**查看代码**"。

     将创建一个分部类并在代码编辑器中打开它。

4. 将代码添加到分部类声明中。

5. 下面的示例演示了在中将代码添加到的位置 `CustomersTableAdapter` `NorthwindDataSet` ：

    ```vb
    Partial Public Class CustomersTableAdapter
        ' Add code here to add functionality
        ' to the CustomersTableAdapter.
    End Class
    ```

    ```csharp
    public partial class CustomersTableAdapter
    {
        // Add code here to add functionality
        // to the CustomersTableAdapter.
    }
    ```

## <a name="see-also"></a>另请参阅
 [N 层数据应用程序概述](../data-tools/n-tier-data-applications-overview.md)[向 N 层应用程序中的数据集添加代码](../data-tools/add-code-to-datasets-in-n-tier-applications.md) [Tableadapter](https://msdn.microsoft.com/library/09416de9-134c-4dc7-8262-6c8d81e3f364) [TableAdapterManager 概述](https://msdn.microsoft.com/library/33076d42-6b41-491a-ac11-6c6339aea650)[分层更新概述](https://msdn.microsoft.com/library/c4f8e8b9-e4a5-4a02-8462-d03d1e8222d6)