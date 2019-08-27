---
title: 在 WPF 应用程序中创建查找表
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- data [WPF], displaying
- WPF, data binding in Visual Studio
- WPF data binding [Visual Studio]
- displaying data, WPF
- WPF [WPF], data
- WPF Designer, data binding
- data binding, WPF
ms.assetid: 56a1fbff-c7e8-4187-a1c1-ffd17024bc1b
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 1631f1b93f79c21914f990620f7e0047c301163f
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62567814"
---
# <a name="create-lookup-tables-in-wpf-applications"></a>在 WPF 应用程序中创建查找表

术语*查找表*(有时称为*查找绑定*) 介绍了一个控件，显示来自一个数据表基于另一个表中的外键字段的值的信息。 可以通过拖动对主节点的父表中创建查找表或对象中**数据源**窗口拖到已绑定到列或相关的子表中的属性的控件。

例如，考虑一个表的`Orders`销售数据库中。 中的每条`Orders`表包含`CustomerID`，该值指示哪个客户下达订单。 `CustomerID`是指向客户记录中的外键`Customers`表。 当显示从订单的列表`Orders`表中，您可能希望显示实际的客户名称而不是`CustomerID`。 因为客户名称在`Customers`表，需要创建一个查找表来显示客户名称。 查找表使用`CustomerID`中的值`Orders`记录导航关系，并返回客户名称。

## <a name="to-create-a-lookup-table"></a>创建查找表的步骤

1. 向项目中添加具有相关数据的数据源的以下类型之一：

    - 数据集或实体数据模型。

    - WCF 数据服务，WCF 服务或 web 服务。 有关详细信息，请参阅[如何：连接到服务中的数据](../data-tools/how-to-connect-to-data-in-a-service.md)。

    - 对象。 有关详细信息，请参阅[绑定到 Visual Studio 中的对象](bind-objects-in-visual-studio.md)。

    > [!NOTE]
    > 创建查找表之前，必须存在两个相关的表或对象作为项目的数据源。

2. 打开**WPF 设计器**，并确保该设计器包含有效的放置目标中的项容器**数据源**窗口。

     有关有效放置目标的详细信息，请参阅[控件添加到 Visual Studio 中的数据绑定 WPF](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)。

3. 在“数据”菜单上单击“显示数据源”，打开“数据源”窗口。

4. 展开中的节点**数据源**窗口中，直至你可看到父表或对象和相关的子表或对象。

    > [!NOTE]
    > 相关的子表或对象是显示为父表或对象下可展开子节点的节点。

5. 单击子节点的下拉列表菜单，然后选择**详细信息**。

6. 展开子节点。

7. 下的子节点，单击与相关的子和父数据的项的下拉列表菜单。 (在前面的示例中，这是**CustomerID**节点。)选择支持查找绑定的控件的以下类型之一：

    - **组合框**

    - **ListBox**

    - **ListView**

        > [!NOTE]
        > 如果**ListBox**或**ListView**控件不会出现在列表中，可以将这些控件添加到列表。 有关信息，请参阅[设置从数据源窗口中拖动时创建的控件](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)。

    - 任何自定义控件派生自<xref:System.Windows.Controls.Primitives.Selector>。

        > [!NOTE]
        > 了解如何添加自定义控件添加到的控件列表您可以选择中的项**数据源**窗口中，请参阅[将自定义控件添加到数据源窗口](../data-tools/add-custom-controls-to-the-data-sources-window.md)。

8. 将从子节点**数据源**窗口拖到 WPF 设计器中的容器。 (在上述示例中，子节点是**订单**节点。)

     Visual Studio 将生成为每个拖动的项创建新的数据绑定控件的 XAML。 XAML 还添加了一个新<xref:System.Windows.Data.CollectionViewSource>子表或对象的拖放目标资源。 对于某些数据源，Visual Studio 还会生成代码以将数据加载到表或对象。 有关详细信息，请参阅[控件添加到 Visual Studio 中的数据绑定 WPF](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)。

9. 将从父节点**数据源**窗口拖到前面创建的查找绑定控件。 (在上述示例中，该父节点是**客户**节点)。

     Visual Studio 来配置查找绑定在控件上设置某些属性。 下表列出了 Visual Studio 会修改的属性。 如果有必要，您可以更改这些属性在 XAML 中或在**属性**窗口。

    |属性|设置说明|
    |--------------| - |
    |<xref:System.Windows.Controls.ItemsControl.ItemsSource%2A>|此属性指定的集合或用于获取在控件中显示的数据的绑定。 Visual Studio 将此属性设置为<xref:System.Windows.Data.CollectionViewSource>拖到控件的父数据。|
    |<xref:System.Windows.Controls.ItemsControl.DisplayMemberPath%2A>|此属性指定的控件中显示的数据项的路径。 Visual Studio 后为主键，具有字符串数据类型将此属性设置为第一列或父数据中的属性。<br /><br /> 如果你想要在父数据中显示不同的列或属性，此属性更改为不同的属性的路径。|
    |<xref:System.Windows.Controls.Primitives.Selector.SelectedValue%2A>|Visual Studio 将此属性绑定到列或拖动到设计器中的子数据的属性。 这是父数据的外键。|
    |<xref:System.Windows.Controls.Primitives.Selector.SelectedValuePath%2A>|Visual Studio 将此属性设置为列的路径或子数据的父数据的外键的属性。|

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中将 WPF 控件绑定到数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)
- [在 WPF 应用程序中显示相关数据](../data-tools/display-related-data-in-wpf-applications.md)
- [演练：在 WPF 应用程序中显示相关数据](../data-tools/display-related-data-in-wpf-applications.md)