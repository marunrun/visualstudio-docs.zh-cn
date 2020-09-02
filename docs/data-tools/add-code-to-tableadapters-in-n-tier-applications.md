---
title: 向 n 层应用程序中的 TableAdapter 添加代码
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- TableAdapters, n-tier applications
- n-tier applications, extending TableAdapters
ms.assetid: dafac00e-df9d-4d4a-95a6-e34b4d099425
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 3ea451ac60de971677ee2f7910b28b334c67dff3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85283094"
---
# <a name="add-code-to-tableadapters-in-n-tier-applications"></a>向 n 层应用程序中的 TableAdapter 添加代码
可以通过为 TableAdapter 创建分部类文件并向其添加代码 (而不是将代码添加到 *DatasetName* 文件) 来扩展 tableadapter 的功能。 分部类使特定类的代码可以在多个物理文件之间进行分隔。 有关详细信息，请参阅 [部分](/dotnet/visual-basic/language-reference/modifiers/partial) 或 [部分 (类型) ](/dotnet/csharp/language-reference/keywords/partial-type)。

每次对数据集中的 TableAdapter 进行更改时，都将生成定义 TableAdapter 的代码。 如果在修改 TableAdapter 的配置的任何向导运行期间进行了更改，也会生成此代码。 若要防止在重新生成 TableAdapter 时删除代码，请将代码添加到 TableAdapter 的分部类文件中。

默认情况下，在分离数据集和 TableAdapter 代码后，结果是每个项目中的离散类文件。 原始项目包含一个名为 *DatasetName* 的文件 (或包含 TableAdapter 代码的 *DatasetName.Designer.cs*) 。 **数据集项目**属性中指定的项目包含一个名为*DatasetName*的文件 (或包含数据集代码的*DatasetName.DataSet.Designer.cs*) 。

> [!NOTE]
> 分离数据集与 TableAdapter（通过设置“数据集项目”属性）时，将不会自动移动项目中现有的数据集分部类****。 必须将现有部分数据集类手动移动到数据集项目。

> [!NOTE]
> 数据集提供了 <xref:System.Data.DataTable.ColumnChanging> <xref:System.Data.DataTable.RowChanging> 在需要验证时生成和事件处理程序的功能。 有关详细信息，请参阅 [将验证添加到 n 层数据集](../data-tools/add-validation-to-an-n-tier-dataset.md)。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="to-add-user-code-to-a-tableadapter-in-an-n-tier-application"></a>将用户代码添加到 n 层应用程序中的 TableAdapter

1. 找到包含 *.xsd* 文件的项目。

2. 双击 *.xsd* 文件以打开 **数据集设计器**。

3. 右键单击要向其添加代码的 TableAdapter，然后选择 " **查看代码**"。

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

- [N 层数据应用程序概述](../data-tools/n-tier-data-applications-overview.md)
- [将代码添加到 n 层应用程序中的数据集](../data-tools/add-code-to-datasets-in-n-tier-applications.md)
- [创建和配置 TableAdapter](create-and-configure-tableadapters.md)
- [分层更新概述](hierarchical-update.md)
