---
title: 演练：在数据集设计器中创建数据表
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- DataTable objects, creating
- Dataset Designer, creating data tables
- tables [Visual Studio], creating
- data [Visual Studio], Dataset Designer
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 1526a5f4137ece5b76c282255af3da4ab20ac119
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75585998"
---
# <a name="walkthrough-create-a-datatable-in-the-dataset-designer"></a>演练：在数据集设计器中创建 DataTable

本演练说明如何使用**数据集设计器**创建 <xref:System.Data.DataTable> （不包含 TableAdapter）。 有关创建包含 Tableadapter 的数据表的信息，请参阅[创建和配置 tableadapter](../data-tools/create-and-configure-tableadapters.md)。

## <a name="create-a-new-windows-forms-application"></a>创建新的 Windows 窗体应用程序

1. 在 Visual Studio 的“文件”菜单中，依次选择“新建” > “项目”。

2. 在左侧窗格中展开 "**视觉对象C#**  " 或 " **Visual Basic** "，然后选择 " **Windows 桌面**"。

3. 在中间窗格中，选择 " **Windows 窗体应用程序**" 项目类型。

4. 将项目命名为**DataTableWalkthrough**，然后选择 **"确定"** 。

     创建**DataTableWalkthrough**项目并将其添加到**解决方案资源管理器**。

## <a name="add-a-new-dataset-to-the-application"></a>向应用程序添加新的数据集

1. 在“项目”菜单上，选择“添加新项”。

     “添加新项”对话框随即出现。

2. 在左侧窗格中，选择 "**数据**"，然后在中间窗格中选择 "数据**集**"。

3. 选择“添加”。

     Visual Studio 会将名为**DataSet1**的文件添加到项目中，并在**数据集设计器**中打开它。

## <a name="add-a-new-datatable-to-the-dataset"></a>向数据集添加新 DataTable

1. 将**DataTable**从 "**工具箱**" 的 "**数据集**" 选项卡拖动到**数据集设计器**。

     名为**DataTable1**的表将添加到数据集。

2. 单击**DataTable1**的标题栏，并将其重命名 `Music`。

## <a name="add-columns-to-the-datatable"></a>将列添加到 DataTable

1. 右键单击**音乐**表。 指向 "**添加**"，然后单击 "**列**"。

2. 将列命名为 `SongID`。

3. 在“属性” 窗口中，将 <xref:System.Data.DataColumn.DataType%2A> 属性设置为 <xref:System.Int16?displayProperty=fullName>。

4. 重复此过程并添加以下列：

     `SongTitle`: <xref:System.String?displayProperty=fullName>

     `Artist`: <xref:System.String?displayProperty=fullName>

     `Genre`: <xref:System.String?displayProperty=fullName>

## <a name="set-the-primary-key-for-the-table"></a>设置表的主键

所有数据表都应有一个主键。 主键唯一标识数据表中的特定记录。

若要设置主密钥，请右键单击**SongID**列，然后单击 "**设置主键**"。 **SongID**列的旁边将显示一个钥匙图标。

## <a name="save-your-project"></a>保存项目

若要保存**DataTableWalkthrough**项目，请在 "**文件**" 菜单上，选择 "**全部保存**"。

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 中创建和配置数据集](../data-tools/create-and-configure-datasets-in-visual-studio.md)
- [在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)
- [验证数据](../data-tools/validate-data-in-datasets.md)
