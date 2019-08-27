---
title: 在 Windows 窗体应用程序中创建查找表 |Microsoft Docs
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
- lookup tables
- lookup tables, creating
ms.assetid: 0edd5385-c381-4b17-9096-74e2778db9d5
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: af9777667bef466dc97ea3a3d239f83f766816da
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65693957"
---
# <a name="create-lookup-tables-in-windows-forms-applications"></a>在 Windows 窗体应用程序中创建查找表
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

术语*查找表*描述了绑定到两个相关的数据表的控件。 这些查找的控件显示基于所选第二个表中的值的第一个表中的数据。  
  
 可以通过拖动对主节点的父表中创建查找表 (从[数据源窗口](https://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992)) 拖到窗体已绑定到相关的子表中的列上的控件。  
  
 例如，考虑一个表的`Orders`销售数据库中。 中的每条`Orders`表包含`CustomerID`，指示哪个客户下达订单。 `CustomerID`是指向客户记录中的外键`Customers`表。 在此方案中，展开`Orders`表中**数据源**窗口并将主节点设置为**详细信息**。 然后设置`CustomerID`要使用的列<xref:System.Windows.Forms.ComboBox>（或任何其他支持查找绑定的控件），并将其拖`Orders`节点拖到窗体上的。 最后，将`Customers`拖动到控件绑定到的相关列上的节点，在这种情况下，<xref:System.Windows.Forms.ComboBox>绑定到`CustomerID`列。  
  
## <a name="to-databind-a-lookup-control"></a>数据绑定查找控件  
  
1. 打开“数据源”窗口。  
  
    > [!NOTE]
    > 查找表需要两个相关的表或对象均位于**数据源**窗口。
  
2. 展开中的节点**数据源**窗口，直到您所见的父表和所有列，以及相关的子表和所有它的列。  
  
    > [!NOTE]
    > 子表节点是显示为父表中可展开子节点的节点。  
  
3. 更改到子表的拖放类型**详细信息**通过选择**详细信息**从子表节点上的控件列表。 有关详细信息，请参阅[设置从数据源窗口中拖动时创建的控件](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)。  
  
4. 查找两个表相关的节点 (`CustomerID`上一示例中的节点)。为其拖放类型更改<xref:System.Windows.Forms.ComboBox>通过选择**组合框**从控件列表。  
  
5. 将从主要子表节点拖**数据源**窗口拖到窗体上的。  
  
     数据绑定控件 （带有描述性标签） 和一个工具条 (<xref:System.Windows.Forms.BindingNavigator>) 窗体中显示。 一个[数据集](../data-tools/dataset-tools-in-visual-studio.md)，TableAdapter <xref:System.Windows.Forms.BindingSource>，和<xref:System.Windows.Forms.BindingNavigator>组件栏中出现。  
  
6. 现在将从主要的父表节点**数据源**窗口直接拖到查找控件 ( <xref:System.Windows.Forms.ComboBox>)。  
  
     查找绑定现在已建立。 请参阅下表中的设置在控件的特定属性。  
  
    |属性|设置说明|  
    |--------------|----------------------------|  
    |**数据源**|Visual Studio 将此属性设置为你拖到控件上的表所创建的 <xref:System.Windows.Forms.BindingSource>（相对于创建该控件时所创建的 <xref:System.Windows.Forms.BindingSource>）。<br /><br /> 如果你需要进行调整，则设置此为<xref:System.Windows.Forms.BindingSource>具有你想要显示的列的表。|  
    |**DisplayMember**|对于你拖动到控件上的表，则 Visual Studio 将此属性设置为该主键后的具有字符串数据类型的第一列。<br /><br /> 如果你需要进行调整，然后将此设置为你想要显示的列名称。|  
    |**ValueMember**|Visual Studio 将此属性设置为参与主键的第一列，或表中的第一列（如果未定义任何键）。<br /><br /> 如果你需要进行调整，然后将此设置为具有你想要显示的列的表中的主键。|  
    |**SelectedValue**|Visual Studio 将此属性设置为从删除的原始列**数据源**窗口。<br /><br /> 如果你需要进行调整，然后将此设置为相关表中的外键列。|  
  
## <a name="see-also"></a>请参阅  
 [在 Visual Studio 中将 Windows 窗体控件绑定到数据](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
