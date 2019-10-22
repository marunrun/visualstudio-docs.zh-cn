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
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 24c3549cf98e49f3419ef0e7387a6c236c15e9e6
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72648845"
---
# <a name="bind-windows-forms-controls-to-data-in-visual-studio"></a>在 Visual Studio 中将 Windows 窗体控件绑定到数据

可以通过将数据绑定到 Windows 窗体来向应用程序的用户显示数据。 若要创建这些数据绑定控件，请将项从 "**数据源**" 窗口拖动到 Visual Studio 中的 Windows 窗体设计器。

![数据源拖动操作](../data-tools/media/raddata-data-source-drag-operation.png)

> [!TIP]
> 如果 "**数据源**" 窗口不可见，可以通过选择 "**视图**"  > **其他 Windows**  > **数据源**，或按**Shift** +**Alt** +**D**来打开它。 若要查看 "**数据源**" 窗口，必须在 Visual Studio 中打开一个项目。

在拖动项之前，您可以设置要绑定到的控件的类型。 显示不同的值，具体取决于您选择的是表本身还是单独的列。  还可以设置自定义值。 对于表，**详细信息**意味着每个列绑定到一个单独的控件。

![将数据源绑定到 DataGridView](../data-tools/media/raddata-bind-data-source-to-datagridview.png)

## <a name="bindingsource-and-bindingnavigator-controls"></a>BindingSource 和 BindingNavigator 控件

<xref:System.Windows.Forms.BindingSource> 组件有两个用途。 首先，在将控件绑定到数据时，它提供抽象层。 窗体上的控件绑定到 <xref:System.Windows.Forms.BindingSource> 组件，而不是直接绑定到数据源。 其次，它可以管理对象的集合。 将类型添加到 <xref:System.Windows.Forms.BindingSource> 会创建该类型的列表。

有关 <xref:System.Windows.Forms.BindingSource> 组件的详细信息，请参阅：

- [BindingSource 组件](/dotnet/framework/winforms/controls/bindingsource-component)

- [BindingSource 组件概述](/dotnet/framework/winforms/controls/bindingsource-component-overview)

- [BindingSource 组件体系结构](/dotnet/framework/winforms/controls/bindingsource-component-architecture)

[BindingNavigator 控件](/dotnet/framework/winforms/controls/bindingnavigator-control-windows-forms)提供一个用户界面，用于浏览 Windows 应用程序所显示的数据。

## <a name="bind-to-data-in-a-datagridview-control"></a>绑定到 DataGridView 控件中的数据

对于[DataGridView 控件](/dotnet/framework/winforms/controls/datagridview-control-overview-windows-forms)，整个表将绑定到该单个控件。 将**DataGridView**拖到窗体时，还会出现用于导航记录的工具条（<xref:System.Windows.Forms.BindingNavigator>）。 [数据集](../data-tools/dataset-tools-in-visual-studio.md)、 [TableAdapter](../data-tools/create-and-configure-tableadapters.md)、<xref:System.Windows.Forms.BindingSource> 和 <xref:System.Windows.Forms.BindingNavigator> 出现在组件栏中。 在下图中，还添加了一个[TableAdapterManager](https://msdn.microsoft.com/library/bb384426.aspx) ，因为 Customers 表与 Orders 表有一个关系。 这些变量都在自动生成的代码中声明为 form 类中的私有成员。 用于填充**DataGridView**的自动生成的代码位于 `Form_Load` 事件处理程序中。 用于保存用于更新数据库的数据的代码位于**BindingNavigator**的 `Save` 事件处理程序中。 您可以根据需要移动或修改此代码。

![BindingNavigator 与 BindingNavigator](../data-tools/media/raddata-gridview-with-bindingnavigator.png)

可以通过单击每个 DataGridView 的右上角的智能标记来自定义**DataGridView**和**BindingNavigator**的行为：

![DataGridView 和绑定导航器智能标记](../data-tools/media/raddata-datagridview-and-binding-navigator-smart-tags.png)

如果你的应用程序所需的控件在 "**数据源**" 窗口中不可用，则可以添加控件。 有关详细信息，请参阅[将自定义控件添加到 "数据源" 窗口](../data-tools/add-custom-controls-to-the-data-sources-window.md)。

您还可以将项从 "**数据源**" 窗口拖到窗体上的控件上，以将控件绑定到数据。 已绑定到数据的控件的数据绑定将重置为最近拖放到它上面的项。 若要成为有效的拖放目标，控件必须能够显示从 "**数据源**" 窗口拖放到它上面的项的基础数据类型。 例如，将数据类型为 <xref:System.DateTime> 的项拖到 <xref:System.Windows.Forms.CheckBox> 中是无效的，因为 <xref:System.Windows.Forms.CheckBox> 不能显示日期。

## <a name="bind-to-data-in-individual-controls"></a>绑定到各个控件中的数据

将数据源绑定到**详细信息**时，数据集中的每一列都将绑定到一个单独的控件。

![将数据源绑定到详细信息](../data-tools/media/raddata-bind-data-source-to-details.png)

> [!IMPORTANT]
> 请注意，在上图中，从 Customers 表的 Orders 属性中进行拖动，而不是从 Orders 表中进行拖动。 通过绑定到 `Customer.Orders` 属性， **DataGridView**中生成的导航命令会立即反映在详细信息控件中。 如果从 Orders 表中拖动，控件仍将绑定到数据集，但不会与**DataGridView**同步。

下图显示了在 Customers 表中的 Orders 属性绑定到 "**数据源**" 窗口中的 "**详细信息**" 之后，添加到窗体中的默认数据绑定控件。

![绑定到详细信息的订单表](../data-tools/media/raddata-orders-table-bound-to-details.png)

另请注意，每个控件都有一个智能标记。 此标记启用仅适用于该控件的自定义项。

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)
- [Windows 窗体（.NET Framework）中的数据绑定](/dotnet/framework/winforms/windows-forms-data-binding)