---
title: 演练：数据集设计器中创建数据表
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- DataTable objects, creating
- Dataset Designer, creating data tables
- tables [Visual Studio], creating
- data [Visual Studio], Dataset Designer
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 1126117cb1fc26c4f61bfb0f6ed0e19e86ce9323
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62564917"
---
# <a name="walkthrough-create-a-datatable-in-the-dataset-designer"></a>演练：在数据集设计器中创建数据表

本演练说明了如何创建<xref:System.Data.DataTable>（不带 TableAdapter) 使用**数据集设计器**。 有关创建包含 Tableadapter 的数据表的信息，请参阅[创建和配置 Tableadapter](../data-tools/create-and-configure-tableadapters.md)。

## <a name="create-a-new-windows-forms-application"></a>创建新的 Windows 窗体应用程序

1. 在 Visual Studio 中，在**文件**菜单中，选择**新建** > **项目**。

2. 展开**Visual C#** 或**Visual Basic**在左侧窗格中，然后选择**Windows 桌面**。

3. 在中间窗格中，选择**Windows 窗体应用**项目类型。

4. 将项目命名**DataTableWalkthrough**，然后选择**确定**。

     **DataTableWalkthrough**创建项目并将其添加到**解决方案资源管理器**。

## <a name="add-a-new-dataset-to-the-application"></a>将新的数据集添加到应用程序

1. 在“项目”菜单上，选择“添加新项”。

     “添加新项”对话框随即出现。

2. 在左侧窗格中，选择**数据**，然后选择**数据集**在中间窗格中。

3. 选择“添加”。

     Visual Studio 将添加名为的文件**DataSet1.xsd**到该项目并将其在中打开**数据集设计器**。

## <a name="add-a-new-datatable-to-the-dataset"></a>将一个新的 DataTable 添加到数据集

1. 拖动**DataTable**从**数据集**选项卡**工具箱**拖到**数据集设计器**。

     名为的表**DataTable1**添加到数据集。

2. 单击的标题栏**DataTable1**并将其重命名`Music`。

## <a name="add-columns-to-the-datatable"></a>向数据表添加列

1. 右键单击**音乐**表。 指向**外**，然后单击**列**。

2. 名称列`SongID`。

3. 在“属性”  窗口中，将 <xref:System.Data.DataColumn.DataType%2A> 属性设置为 <xref:System.Int16?displayProperty=fullName>。

4. 重复此过程，并添加以下列：

     `SongTitle`: <xref:System.String?displayProperty=fullName>

     `Artist`: <xref:System.String?displayProperty=fullName>

     `Genre`: <xref:System.String?displayProperty=fullName>

## <a name="set-the-primary-key-for-the-table"></a>设置表的主键

数据的所有表应都具有主键。 主键唯一标识数据表中的特定记录。

若要设置为主键，右键单击**SongID**列中，并单击**设置主键**。 旁边会显示密钥图标**SongID**列。

## <a name="save-your-project"></a>保存项目

若要保存**DataTableWalkthrough**项目，在**文件**菜单中，选择**全部保存**。

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中创建和配置数据集](../data-tools/create-and-configure-datasets-in-visual-studio.md)
- [在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)
- [验证数据](../data-tools/validate-data-in-datasets.md)