---
title: 将 Windows 窗体控件绑定到数据 |Microsoft Docs
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
- displaying data, Windows Forms controls
- Windows Forms, displaying data
- data sources, displaying
- data [Windows Forms], displaying
ms.assetid: 0163a34a-38cb-40b9-8f38-3058a90caf21
caps.latest.revision: 31
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 3541dada6167bd2f0a95913d9ccc385dc3e5ccc3
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63439474"
---
# <a name="bind-windows-forms-controls-to-data"></a>将 Windows 窗体控件绑定到数据
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以将数据源绑定到控件中通过将对象从拖**数据源**窗口拖到 Windows 窗体或拖动到窗体上现有控件上。 拖动项之前，您可以设置想要将绑定到控件的类型。 具体取决于您选择表本身，或单独的列显示不同的值。  此外可以设置自定义值。 对于表中，"详细信息"意味着，每个列绑定到一个单独的控件。  
  
 ![将数据源绑定到 DataGridView](../data-tools/media/raddata-bind-data-source-to-datagridview.png "到 DataGridView raddata 绑定数据源")  
  
 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
## <a name="bind-to--data-in-a-datagridview-control"></a>将绑定到 DataGridView 控件中的数据  
 DataGridView，为整个表绑定到该单个控件。 将 DataGridView 拖到窗体后，一种工具条带用于导航记录 (<xref:System.Windows.Forms.BindingNavigator>) 也会出现。 一个[数据集](../data-tools/dataset-tools-in-visual-studio.md)，TableAdapter <xref:System.Windows.Forms.BindingSource>，和<xref:System.Windows.Forms.BindingNavigator>组件栏中出现。 在下图中，因为客户表具有与 Orders 表的关系也添加 TableAdapterManager。 这些变量被所有声明自动生成的代码中为窗体类中的私有成员。 用于填充 DataGridView 的自动生成的代码位于 form_load 事件处理程序。 用于保存数据，以更新数据库的代码位于 BindingNavigator 保存的事件处理程序。 您可以移动或根据需要修改此代码。  
  
 ![使用 BindingNavigator GridView](../data-tools/media/raddata-gridview-with-bindingnavigator.png "raddata 使用 BindingNavigator 的 GridView")  
  
 通过单击每个的右上角中的智能标记，可以自定义 DataGridView 和 BindingNavigator 的行为：  
  
 ![DataGridView 控件和绑定的导航器智能标记](../data-tools/media/raddata-datagridview-and-binding-navigator-smart-tags.png "raddata DataGridView 和绑定的导航器智能标记")  
  
 如果控件在应用程序需求中不能从**数据源**窗口中，你可以添加控件。 有关详细信息，请参阅[将自定义控件添加到数据源窗口](../data-tools/add-custom-controls-to-the-data-sources-window.md)。  
  
 此外可以将项从**数据源**窗口拖动到已在要将控件绑定到数据的窗体上的控件。 已绑定到数据的控件具有其数据绑定重置为最近拖动到它上面的项。 若要有效放置目标，控件必须能够显示的项拖动到它从基础数据类型**数据源**窗口。 例如，不能用来将数据类型为某项拖<xref:System.DateTime>拖到<xref:System.Windows.Forms.CheckBox>，这是因为<xref:System.Windows.Forms.CheckBox>不能显示日期。  
  
## <a name="bind-to--data-in-individual-controls"></a>将绑定到在单独控件中的数据  
 当将数据源绑定到"详细信息"时，在数据集中每个列绑定到一个单独的控件。  
  
 ![将数据源绑定到详细信息](../data-tools/media/raddata-bind-data-source-to-details.png "raddata 绑定数据源详细信息")  
  
> [!IMPORTANT]
> 请注意，在上图中，将从客户表不能从 Orders 表的 Orders 属性。 通过绑定到 Customer.Orders 属性，在详细信息控件中立即反映在 DataGridView 中进行导航命令中。 如果您从订单表拖动，仍会将控件绑定到数据集，但不是它们将不会与同步 DataGridView。  
  
 下图中显示的默认的客户表中的 Orders 属性绑定到"详细信息"后，添加到窗体数据绑定控件**数据源**窗口。  
  
 ![订单表绑定到详细信息](../data-tools/media/raddata-orders-table-bound-to-details.png "raddata 订单表绑定到详细信息")  
  
 另请注意，每个控件包含一个智能标记。 此标记启用适用于仅该控件的自定义项。  
  
## <a name="see-also"></a>请参阅  
 [在 Visual Studio 中将 Windows 窗体控件绑定到数据](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
