---
title: 在 Windows 窗体应用程序中创建查找表
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- lookup tables
- lookup tables, creating
ms.assetid: 0edd5385-c381-4b17-9096-74e2778db9d5
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 9fe49ee90dba3edd0e2777817c4903c6101a1b47
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75586765"
---
# <a name="create-lookup-tables-in-windows-forms-applications"></a>在 Windows 窗体应用程序中创建查找表

字词*查找表*描述绑定到两个相关数据表的控件。 这些查找控件根据第二个表中所选的值显示第一个表中的数据。

您可以通过将父表的主节点从 "[数据源" 窗口](add-new-data-sources.md#data-sources-window)拖到窗体上已经绑定到相关子表中的列的控件来创建查找表。

例如，假设有一个表在 sales 数据库中 `Orders`。 `Orders` 表中的每条记录都包括一个 `CustomerID`，指示下订单的客户。 `CustomerID` 是指向 `Customers` 表中的客户记录的外键。 在此方案中，将展开 "**数据源**" 窗口中的 "`Orders`" 表，并将主节点设置为 "**详细信息**"。 然后，设置 `CustomerID` 列以使用 <xref:System.Windows.Forms.ComboBox> （或支持查找绑定的任何其他控件），然后将 `Orders` 节点拖到窗体上。 最后，将 `Customers` 节点拖动到绑定到相关列的控件上（在本例中，绑定到 `CustomerID` 列的 <xref:System.Windows.Forms.ComboBox>）。

## <a name="to-databind-a-lookup-control"></a>对查找控件进行 databind

1. 打开项目后，通过选择 "**视图**" > **其他 Windows** > **数据源**打开 "**数据源**" 窗口。

    > [!NOTE]
    > 查找表要求在 "**数据源**" 窗口中提供两个相关的表或对象。 有关详细信息，请参阅[数据集中的关系](relationships-in-datasets.md)。

2. 展开 "**数据源**" 窗口中的节点，直到看到父表及其所有列、相关子表及其所有列。

    > [!NOTE]
    > 子表节点是在父表中显示为可展开子节点的节点。

3. 通过从子表节点上的控件列表中选择 "**详细信息**"，将子表的 "删除" 类型更改为 "**详细**信息"。 有关详细信息，请参阅[设置在从 "数据源" 窗口中拖动时要创建的控件](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)。

4. 找到关联两个表的节点（上一示例中的 `CustomerID` 节点）。 从控件列表中选择**ComboBox** ，将其放置类型更改为 <xref:System.Windows.Forms.ComboBox>。

5. 将主子表节点从 "**数据源**" 窗口拖到窗体上。

     数据绑定控件（具有描述性标签）和工具条（<xref:System.Windows.Forms.BindingNavigator>）显示在窗体上。 [数据集](../data-tools/dataset-tools-in-visual-studio.md)、 [TableAdapter](../data-tools/create-and-configure-tableadapters.md)、<xref:System.Windows.Forms.BindingSource>和 <xref:System.Windows.Forms.BindingNavigator> 出现在组件栏中。

6. 现在，将主父表节点从 "**数据源**" 窗口直接拖到查找控件（<xref:System.Windows.Forms.ComboBox>）上。

     查找绑定现已建立。 对于在控件上设置的特定属性，请参阅下表。

    |Property|设置说明|
    |--------------| - |
    |**数据源**|Visual Studio 将此属性设置拖到控件上的表所创建的 <xref:System.Windows.Forms.BindingSource>（相对于创建该控件时所创建的 <xref:System.Windows.Forms.BindingSource>）。<br /><br /> 如果需要进行调整，请将此设置为包含要显示的列的表的 <xref:System.Windows.Forms.BindingSource>。|
    |**DisplayMember**|对于你拖动到控件上的表，则 Visual Studio 将此属性设置为该主键后的具有字符串数据类型的第一列。<br /><br /> 如果需要进行调整，请将此设置为要显示的列名称。|
    |**ValueMember**|Visual Studio 将此属性设置为参与主键的第一列，或表中的第一列（如果未定义任何键）。<br /><br /> 如果需要进行调整，请将此项设置为包含要显示的列的表中的主键。|
    |**SelectedValue**|Visual Studio 将此属性设置为从 "**数据源**" 窗口中删除的原始列。<br /><br /> 如果需要进行调整，请将此项设置为相关表中的外键列。|

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 中将 Windows 窗体控件绑定到数据](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
