---
title: 将 Windows 窗体控件绑定到数据
ms.date: 11/03/2017
ms.topic: conceptual
helpviewer_keywords:
- data [Windows Forms], data sources
- Windows Forms, data binding
- Windows Forms, displaying data
- displaying data on forms
- forms, displaying data
- data sources, displaying data
- displaying data, Windows Forms
- data [Windows Forms], displaying
ms.assetid: 243338ef-41af-4cc5-aff7-1e830236f0ec
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 6b961af0bf35bb4476f9f336fcf5298bb0bd3651
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62818723"
---
# <a name="bind-windows-forms-controls-to-data-in-visual-studio"></a>在 Visual Studio 中将 Windows 窗体控件绑定到数据

通过将数据绑定到 Windows 窗体，可以向应用程序的用户显示数据。 若要创建这些数据绑定控件，将项从**数据源**窗口拖到 Visual Studio 中的 Windows 窗体设计器。

![数据源拖放操作](../data-tools/media/raddata-data-source-drag-operation.png)

> [!TIP]
> 如果**数据源**窗口不可见，请打开，请选择**视图** > **其他 Windows** > **数据源**，或按**Shift**+**Alt**+**D**。 必须具有在 Visual Studio 中查看打开的项目**数据源**窗口。

拖动项之前，您可以设置想要将绑定到控件的类型。 具体取决于您选择表本身，或单独的列显示不同的值。  此外可以设置自定义值。 对于表，**详细信息**意味着每个列将绑定到一个单独的控件。

![将数据源绑定到 DataGridView](../data-tools/media/raddata-bind-data-source-to-datagridview.png)

## <a name="bindingsource-and-bindingnavigator-controls"></a>BindingSource 和 BindingNavigator 控件

<xref:System.Windows.Forms.BindingSource> 组件有两个用途。 首先，当控件绑定到数据时提供一个抽象层。 窗体控件绑定到<xref:System.Windows.Forms.BindingSource>组件而不是直接与数据源。 其次，它可以管理的对象的集合。 添加到类型<xref:System.Windows.Forms.BindingSource>创建该类型的列表。

有关详细信息<xref:System.Windows.Forms.BindingSource>组件，请参阅：

- [BindingSource 组件](/dotnet/framework/winforms/controls/bindingsource-component)

- [BindingSource 组件概述](/dotnet/framework/winforms/controls/bindingsource-component-overview)

- [BindingSource 组件体系结构](/dotnet/framework/winforms/controls/bindingsource-component-architecture)

[BindingNavigator 控件](/dotnet/framework/winforms/controls/bindingnavigator-control-windows-forms)提供用于在由 Windows 应用程序显示的数据中导航用户界面。

## <a name="bind-to-data-in-a-datagridview-control"></a>将绑定到 DataGridView 控件中的数据

有关[DataGridView 控件](/dotnet/framework/winforms/controls/datagridview-control-overview-windows-forms)，整个表绑定到该单个控件。 当拖动**DataGridView**窗体，用于导航记录的条带一个工具 (<xref:System.Windows.Forms.BindingNavigator>) 也会出现。 一个[数据集](../data-tools/dataset-tools-in-visual-studio.md)， [TableAdapter](../data-tools/create-and-configure-tableadapters.md)， <xref:System.Windows.Forms.BindingSource>，并<xref:System.Windows.Forms.BindingNavigator>组件栏中出现。 在下图中， [TableAdapterManager](https://msdn.microsoft.com/library/bb384426.aspx)还会添加它，因为客户表具有与 Orders 表的关系。 这些变量被所有声明自动生成的代码中为窗体类中的私有成员。 为填充自动生成的代码**DataGridView**位于`Form_Load`事件处理程序。 用于保存数据，以更新数据库的代码位于`Save`事件处理程序**BindingNavigator**。 您可以移动或根据需要修改此代码。

![使用 BindingNavigator 的 GridView](../data-tools/media/raddata-gridview-with-bindingnavigator.png)

您可以自定义的行为**DataGridView**并**BindingNavigator**通过单击右上角的每个智能标记：

![DataGridView 控件和绑定的导航器的智能标记](../data-tools/media/raddata-datagridview-and-binding-navigator-smart-tags.png)

如果控件在应用程序需求中不能从**数据源**窗口中，你可以添加控件。 有关详细信息，请参阅[将自定义控件添加到数据源窗口](../data-tools/add-custom-controls-to-the-data-sources-window.md)。

此外可以将项从**数据源**窗口拖动到已在要将控件绑定到数据的窗体上的控件。 已绑定到数据的控件具有其数据绑定重置为最近拖动到它上面的项。 若要有效放置目标，控件必须能够显示的项拖动到它从基础数据类型**数据源**窗口。 例如，不能用来将数据类型为某项拖<xref:System.DateTime>拖到<xref:System.Windows.Forms.CheckBox>，这是因为<xref:System.Windows.Forms.CheckBox>不能显示日期。

## <a name="bind-to-data-in-individual-controls"></a>将绑定到在单独控件中的数据

当您将绑定到的数据源**详细信息**，在数据集中每个列绑定到一个单独的控件。

![将数据源绑定到详细信息](../data-tools/media/raddata-bind-data-source-to-details.png)

> [!IMPORTANT]
> 请注意，在上图中，将从客户表不能从 Orders 表的 Orders 属性。 通过绑定到`Customer.Orders`属性中，导航命令中所做**DataGridView**立即反映在详细信息控件中。 如果从订单表拖动，仍会将控件绑定到数据集，但不是它们将不会与同步**DataGridView**。

下图显示的默认的客户表中的 Orders 属性绑定到后，添加到窗体数据绑定控件**详细信息**中**数据源**窗口。

![Orders 表绑定到详细信息](../data-tools/media/raddata-orders-table-bound-to-details.png)

另请注意，每个控件包含一个智能标记。 此标记启用适用于仅该控件的自定义项。

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)
- [在 Windows 窗体 (.NET Framework) 中的数据绑定](/dotnet/framework/winforms/windows-forms-data-binding)