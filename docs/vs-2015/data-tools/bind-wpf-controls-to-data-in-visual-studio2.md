---
title: 将 WPF 控件绑定到数据（第2部分） |Microsoft Docs
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
- data [WPF], displaying
- WPF, data binding in Visual Studio
- WPF data binding [Visual Studio]
- displaying data, WPF
- WPF [WPF], data
- WPF Designer, data binding
- data binding, WPF
ms.assetid: 00dd5147-db0b-4b59-8d6c-8229b09ca9dd
caps.latest.revision: 29
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 06428a633aec41489a8a77655d6ea9442ffffaa0
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85540083"
---
# <a name="bind-wpf-controls-to-data-in-visual-studio"></a>在 Visual Studio 中将 WPF 控件绑定到数据
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以 [!INCLUDE[TLA#tla_titlewinclient](../includes/tlasharptla-titlewinclient-md.md)] 使用 "**数据源**" 窗口创建数据绑定控件。 首先，将数据源添加到 "**数据源**" 窗口。 然后，将项从 "**数据源**" 窗口拖到**WPF 设计器**。

## <a name="add-a-data-source-to-the-data-sources-window"></a><a name="adding"></a>将数据源添加到 "数据源" 窗口
 必须先将数据源添加到 "**数据源**" 窗口中，然后才能创建数据绑定控件。

#### <a name="to-add-a-data-source-to-the-data-sources-window"></a>将数据源添加到“数据源”窗口中

1. 在 "**视图**" 菜单上，指向 "**其他窗口**"，再单击 "**数据源**"。

2. 单击“添加新数据源”，然后完成“数据源配置”向导********。

3. 执行以下任务之一以创建数据绑定控件：

    - [创建绑定到单个数据字段的控件](#simple)。

    - [创建绑定到多个数据字段的控件](#complex)。

    - [创建一组绑定到多个数据字段的控件](#details)。

    - [在设计器中将数据绑定到现有控件](#existing)。

## <a name="create-a-control-that-is-bound-to-a-single-field-of-data"></a><a name="simple"></a>创建绑定到单个数据字段的控件
 在将数据源添加到 "**数据源**" 窗口后，可以创建一个新的数据绑定控件，该控件显示单个数据字段，例如 <xref:System.Windows.Controls.ComboBox> 或 <xref:System.Windows.Controls.TextBox> 。

#### <a name="to-create-a-control-that-is-bound-to-a-single-field-of-data"></a>创建绑定到单个数据字段的控件

1. 在 "**数据源**" 窗口中，展开表示表或对象的项。 查找表示要绑定到的列或属性的子项。 有关可视化示例，请参阅 "[数据源" 窗口](https://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992)。

2. （可选）选择要创建的控件。 "**数据源**" 窗口中的每个项都有一个默认控件，该控件在您将项拖到设计器中时创建。 默认控件将取决于项的基础数据类型。

     若要选择一个不同的控件，请单击项旁边的下拉箭头，然后选择一个控件。 有关详细信息，请参阅[设置在从 "数据源" 窗口中拖动时要创建的控件](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)。

3. 将该项拖动到设计器中的有效容器。 有关有效容器的详细信息，请参阅[在 Visual Studio 中将 WPF 控件绑定到数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)。

     [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]在容器中创建新的数据绑定控件和适当的标题 <xref:System.Windows.Controls.Label> 。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]还会生成 [!INCLUDE[TLA#tla_titlexaml](../includes/tlasharptla-titlexaml-md.md)] 和代码以将控件绑定到数据。 有关详细信息，请参阅[在 Visual Studio 中将 WPF 控件绑定到数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)。

## <a name="create-a-control-that-is-bound-to-multiple-fields-of-data"></a><a name="complex"></a>创建绑定到多个数据字段的控件
 在将数据源添加到 "**数据源**" 窗口后，可以创建一个新的数据绑定控件，该控件显示多个数据字段，例如 <xref:System.Windows.Controls.DataGrid> 或 <xref:System.Windows.Controls.ListView> 。

#### <a name="to-create-a-control-that-is-bound-to-multiple-fields-of-data"></a>创建绑定到多个数据字段的控件

1. 在 "**数据源**" 窗口中，选择表示表或对象的项。 有关可视化示例，请参阅 "[数据源" 窗口](https://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992)。

2. （可选）选择要创建的控件。 默认情况下，"**数据源**" 窗口中表示数据表或对象的每一项都设置为创建 <xref:System.Windows.Controls.DataGrid> （如果您的项目面向 .NET Framework 4）或 <xref:System.Windows.Controls.ListView> （对于早期版本的 .NET Framework）。

     若要选择一个不同的控件，请单击项旁边的下拉箭头，然后选择一个控件。 有关详细信息，请参阅[设置在从 "数据源" 窗口中拖动时要创建的控件](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)。

    > [!NOTE]
    > 如果你不希望显示特定的列或属性，请展开该项以显示其子级。 单击不想显示的列或属性旁边的下拉箭头，然后单击 "**无**"。

3. 在设计器中将项拖动到有效容器（例如 <xref:System.Windows.Controls.Grid>）中。 有关有效容器的详细信息，请参阅[在 Visual Studio 中将 WPF 控件绑定到数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)。

     [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]在容器中创建新的数据绑定控件。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]还会生成 [!INCLUDE[TLA#tla_titlexaml](../includes/tlasharptla-titlexaml-md.md)] 和代码以将控件绑定到数据。 有关详细信息，请参阅[在 Visual Studio 中将 WPF 控件绑定到数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)。

## <a name="create-a-set-of-controls-that-are-bound-to-multiple-fields-of-data"></a><a name="details"></a>创建一组绑定到多个数据字段的控件
 在将数据源添加到 "**数据源**" 窗口后，可以将数据表或对象绑定到一组控件。 这将为表或对象中的每个列或属性创建一个不同的控件。

#### <a name="to-create-a-set-of-controls-that-are-bound-to-multiple-fields-of-data"></a>创建一组绑定到多个数据字段的控件

1. 在 "**数据源**" 窗口中，选择表示表或对象的项。 有关可视化示例，请参阅 "[数据源" 窗口](https://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992)。

2. 单击项旁边的下拉箭头，然后选择 "**详细信息**"。

    > [!NOTE]
    > 如果你不希望显示特定的列或属性，请展开该项以显示其子级。 单击不想显示的列或属性旁边的下拉箭头，然后单击 "**无**"。

3. 在设计器中将项拖动到有效容器（例如 <xref:System.Windows.Controls.Grid>）中。 有关有效容器的详细信息，请参阅[在 Visual Studio 中将 WPF 控件绑定到数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)。

     [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]在容器中创建新的数据绑定控件。 每个控件将绑定到不同的列或属性，而且每个控件都带有一个具有适当标题的 <xref:System.Windows.Controls.Label> 控件。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]还会生成 [!INCLUDE[TLA#tla_titlexaml](../includes/tlasharptla-titlexaml-md.md)] 和代码以将控件绑定到数据。 有关详细信息，请参阅[在 Visual Studio 中将 WPF 控件绑定到数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)。

## <a name="binddata-to-existing-controls-in-the-designer"></a><a name="existing"></a>Binddata 到设计器中的现有控件
 将数据源添加到 "**数据源**" 窗口后，可以将数据绑定添加到设计器中的现有控件。

#### <a name="to-bind-data-to-an-existing-control-in-the-designer"></a>在设计器中将数据绑定到现有控件

1. 在 "**数据源**" 窗口中，使用以下过程之一：

    - 若要将数据绑定添加到显示多个数据字段的现有控件（例如 <xref:System.Windows.Controls.DataGrid> 或 <xref:System.Windows.Controls.ListView>），请选择表示要绑定到该控件的表或对象的项。

    - 若要将数据绑定添加到显示单个数据字段的现有控件（例如 <xref:System.Windows.Controls.ComboBox> 或 <xref:System.Windows.Controls.TextBox>），请展开表示包含数据的表或对象的项，然后选择表示要绑定到该控件的数据的项。

2. 将选择的项从 "**数据源**" 窗口拖到设计器中的现有控件上。 该控件必须是有效的放置目标。 有关详细信息，请参阅[在 Visual Studio 中将 WPF 控件绑定到数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)。

     [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]生成 [!INCLUDE[TLA#tla_titlexaml](../includes/tlasharptla-titlexaml-md.md)] 和代码以将控件绑定到数据。 有关详细信息，请参阅[在 Visual Studio 中将 WPF 控件绑定到数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)。

    > [!NOTE]
    > 如果该控件已绑定到数据，则会将该控件的数据绑定重置为最近拖动到该控件上的项。

## <a name="see-also"></a>另请参阅
 [在 Visual Studio 中将 wpf 控件绑定到数据在 wpf](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md) [应用程序中创建查找表在](../data-tools/create-lookup-tables-in-wpf-applications.md) [wpf 应用程序中显示相关数据](../data-tools/display-related-data-in-wpf-applications.md)将[WPF 控件绑定到数据集](../data-tools/bind-wpf-controls-to-a-dataset.md)将[wpf 控件绑定到 WCF 数据服务](../data-tools/bind-wpf-controls-to-a-wcf-data-service.md)[演练：在 WPF 应用程序中显示相关数据](../data-tools/walkthrough-displaying-related-data-in-a-wpf-application.md)
