---
title: 向 n 层应用程序中的 TableAdapter 添加代码
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- TableAdapters, n-tier applications
- n-tier applications, extending TableAdapters
ms.assetid: dafac00e-df9d-4d4a-95a6-e34b4d099425
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: e61b9e35464c4200581f6859b2f394911d266d44
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63402909"
---
# <a name="add-code-to-tableadapters-in-n-tier-applications"></a>向 n 层应用程序中的 TableAdapter 添加代码
您可以通过为 TableAdapter 创建分部类文件并向其中添加代码来扩展 TableAdapter 的功能 (而不是将代码添加到*DatasetName.DataSet.Designer*文件)。 分部类启用划分到多个物理文件的特定类代码。 有关详细信息，请参阅[分部](/dotnet/visual-basic/language-reference/modifiers/partial)或[分部 （类型）](/dotnet/csharp/language-reference/keywords/partial-type)。

每次对在数据集中的 TableAdapter 的更改，则生成的代码，用于定义 TableAdapter。 修改的 TableAdapter 配置任何向导运行期间发生更改时，还会生成此代码。 若要防止在 TableAdapter 的重新生成过程中删除你的代码，请将代码添加到 TableAdapter 的分部类文件。

默认情况下，单独的数据集和 TableAdapter 代码后结果将是每个项目中的离散类文件。 原始项目将包含名为的文件*DatasetName.Designer.vb* (或*DatasetName.Designer.cs*)，其中包含 TableAdapter 代码。 中指定的项目**数据集项目**属性具有名为的文件*DatasetName.DataSet.Designer.vb* (或*DatasetName.DataSet.Designer.cs*)，包含的数据集代码。

> [!NOTE]
> 分离数据集与 TableAdapter（通过设置“数据集项目”属性）时，将不会自动移动项目中现有的数据集分部类。 向数据集项目，必须手动移动现有数据集分部类。

> [!NOTE]
> 数据集提供了用于生成功能<xref:System.Data.DataTable.ColumnChanging>和<xref:System.Data.DataTable.RowChanging>事件处理程序时需要验证。 有关详细信息，请参阅[向 n 层数据集添加验证](../data-tools/add-validation-to-an-n-tier-dataset.md)。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

## <a name="to-add-user-code-to-a-tableadapter-in-an-n-tier-application"></a>若要将用户代码添加到 TableAdapter 中的 n 层应用程序

1. 找到包含项目 *.xsd*文件。

2. 双击 *.xsd*文件以打开**数据集设计器**。

3. 右键单击你想要将代码添加到，然后选择 TableAdapter**查看代码**。

     分部类将创建并在代码编辑器中打开。

4. 添加代码的分部类声明。

5. 下面的示例显示了将代码添加到的位置`CustomersTableAdapter`在`NorthwindDataSet`:

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

## <a name="see-also"></a>请参阅

- [N 层数据应用程序概述](../data-tools/n-tier-data-applications-overview.md)
- [向 N 层应用程序的数据集添加代码](../data-tools/add-code-to-datasets-in-n-tier-applications.md)
- [创建和配置 Tableadapter](create-and-configure-tableadapters.md)
- [分层更新概述](hierarchical-update.md)
