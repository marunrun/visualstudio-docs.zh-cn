---
title: 将 WPF 控件绑定到数据 |Microsoft Docs
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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: e37d17cbe67bd1e4e64e306831f38996a7f93c80
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65697957"
---
# <a name="bind-wpf-controls-to-data-in-visual-studio"></a>在 Visual Studio 中将 WPF 控件绑定到数据
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以创建数据绑定[!INCLUDE[TLA#tla_titlewinclient](../includes/tlasharptla-titlewinclient-md.md)]通过使用控件**数据源**窗口。 首先，将添加到的数据源**数据源**窗口。 然后，将项从**数据源**到窗口**WPF 设计器**。

## <a name="adding"></a> 将数据源添加到数据源窗口
 创建数据绑定控件之前，必须首先将添加到的数据源**数据源**窗口。

#### <a name="to-add-a-data-source-to-the-data-sources-window"></a>将数据源添加到“数据源”窗口中

1. 上**视图**菜单，依次指向**其他 Windows**，然后单击**数据源**。

2. 单击“添加新数据源”，然后完成“数据源配置”向导。

3. 执行以下任务之一以创建数据绑定控件：

    - [创建控件绑定到单个字段的数据](#simple)。

    - [创建一个控件绑定到多个数据字段的](#complex)。

    - [创建一组控件绑定到多个字段的数据](#details)。

    - [数据绑定到设计器中的现有控件](#existing)。

## <a name="simple"></a> 创建绑定到单个字段的数据的控件
 添加到的数据源后**数据源**窗口中，可以创建新的数据绑定控件用于显示单个字段的数据，如<xref:System.Windows.Controls.ComboBox>或<xref:System.Windows.Controls.TextBox>。

#### <a name="to-create-a-control-that-is-bound-to-a-single-field-of-data"></a>创建绑定到单个数据字段的控件

1. 在中**数据源**窗口中，展开一个表示表或对象的项。 查找表示要绑定到的列或属性的子项。 有关示例，请参阅[数据源窗口](https://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992)。

2. （可选）选择要创建的控件。 中的每项**数据源**窗口具有时将项拖动到设计器中创建一个默认控件。 默认控件将取决于项的基础数据类型。

     若要选择一个不同的控件，请单击项旁边的下拉箭头，然后选择一个控件。 有关详细信息，请参阅[设置从数据源窗口中拖动时创建的控件](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)。

3. 将项拖动到设计器中是有效的容器。 有关有效容器的详细信息，请参阅[控件添加到 Visual Studio 中的数据绑定 WPF](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)。

     [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 创建新的数据绑定控件和一个具有适当标题<xref:System.Windows.Controls.Label>容器中。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 还会生成 [!INCLUDE[TLA#tla_titlexaml](../includes/tlasharptla-titlexaml-md.md)] 和代码以将控件绑定到数据。 有关详细信息，请参阅[控件添加到 Visual Studio 中的数据绑定 WPF](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)。

## <a name="complex"></a> 创建绑定到多个字段的数据的控件
 添加到的数据源后**数据源**窗口中，可以创建新的数据绑定控件显示多个字段的数据，如<xref:System.Windows.Controls.DataGrid>或<xref:System.Windows.Controls.ListView>。

#### <a name="to-create-a-control-that-is-bound-to-multiple-fields-of-data"></a>创建绑定到多个数据字段的控件

1. 在中**数据源**窗口中，选择一个表示表或对象的项目。 有关示例，请参阅[数据源窗口](https://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992)。

2. （可选）选择要创建的控件。 默认情况下，每个项目中**数据源**表示数据表或对象的窗口已设置为创建<xref:System.Windows.Controls.DataGrid>（如果项目面向.NET Framework 4） 或<xref:System.Windows.Controls.ListView>（适用于.NET framework 的早期版本）。

     若要选择一个不同的控件，请单击项旁边的下拉箭头，然后选择一个控件。 有关详细信息，请参阅[设置从数据源窗口中拖动时创建的控件](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)。

    > [!NOTE]
    > 如果你不希望显示特定的列或属性，请展开该项以显示其子级。 单击列或你不想要显示，然后再单击属性旁边的下拉箭头**None**。

3. 在设计器中将项拖动到有效容器（例如 <xref:System.Windows.Controls.Grid>）中。 有关有效容器的详细信息，请参阅[控件添加到 Visual Studio 中的数据绑定 WPF](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)。

     [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 会在容器中创建新的数据绑定控件。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 还会生成 [!INCLUDE[TLA#tla_titlexaml](../includes/tlasharptla-titlexaml-md.md)] 和代码以将控件绑定到数据。 有关详细信息，请参阅[控件添加到 Visual Studio 中的数据绑定 WPF](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)。

## <a name="details"></a> 创建一组绑定到多个字段的数据的控件
 添加到的数据源后**数据源**窗口中，可以将数据表或对象绑定到一组控件。 这将为表或对象中的每个列或属性创建一个不同的控件。

#### <a name="to-create-a-set-of-controls-that-are-bound-to-multiple-fields-of-data"></a>创建一组绑定到多个数据字段的控件

1. 在中**数据源**窗口中，选择一个表示表或对象的项目。 有关示例，请参阅[数据源窗口](https://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992)。

2. 单击项目并选择旁边的下拉箭头**详细信息**。

    > [!NOTE]
    > 如果你不希望显示特定的列或属性，请展开该项以显示其子级。 单击列或你不想要显示，然后再单击属性旁边的下拉箭头**None**。

3. 在设计器中将项拖动到有效容器（例如 <xref:System.Windows.Controls.Grid>）中。 有关有效容器的详细信息，请参阅[控件添加到 Visual Studio 中的数据绑定 WPF](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)。

     [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 会在容器中创建新的数据绑定控件。 每个控件将绑定到不同的列或属性，而且每个控件都带有一个具有适当标题的 <xref:System.Windows.Controls.Label> 控件。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 还会生成 [!INCLUDE[TLA#tla_titlexaml](../includes/tlasharptla-titlexaml-md.md)] 和代码以便将控件绑定到数据。 有关详细信息，请参阅[控件添加到 Visual Studio 中的数据绑定 WPF](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)。

## <a name="existing"></a> 在设计器中的现有控件到 Binddata
 添加到的数据源后**数据源**窗口中，可以添加数据绑定到现有控件设计器中。

#### <a name="to-bind-data-to-an-existing-control-in-the-designer"></a>在设计器中将数据绑定到现有控件

1. 在中**数据源**窗口中，使用以下过程之一：

    - 若要将数据绑定添加到显示多个数据字段的现有控件（例如 <xref:System.Windows.Controls.DataGrid> 或 <xref:System.Windows.Controls.ListView>），请选择表示要绑定到该控件的表或对象的项。

    - 若要将数据绑定添加到显示单个数据字段的现有控件（例如 <xref:System.Windows.Controls.ComboBox> 或 <xref:System.Windows.Controls.TextBox>），请展开表示包含数据的表或对象的项，然后选择表示要绑定到该控件的数据的项。

2. 将从选定的项**数据源**窗口拖到设计器中的现有控件。 该控件必须是有效的放置目标。 有关详细信息，请参阅[控件添加到 Visual Studio 中的数据绑定 WPF](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)。

     [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 生成[!INCLUDE[TLA#tla_titlexaml](../includes/tlasharptla-titlexaml-md.md)]和代码以将控件绑定到数据。 有关详细信息，请参阅[控件添加到 Visual Studio 中的数据绑定 WPF](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)。

    > [!NOTE]
    > 如果该控件已绑定到数据，则会将该控件的数据绑定重置为最近拖动到该控件上的项。

## <a name="see-also"></a>请参阅
 [将 WPF 控件绑定到 Visual Studio 中的数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md) [WPF 应用程序中创建查找表](../data-tools/create-lookup-tables-in-wpf-applications.md) [WPF 应用程序中显示相关的数据](../data-tools/display-related-data-in-wpf-applications.md)[绑定 WPF 控件添加到数据集](../data-tools/bind-wpf-controls-to-a-dataset.md)[绑定 WPF 控件添加到 WCF 数据服务](../data-tools/bind-wpf-controls-to-a-wcf-data-service.md)[演练：在 WPF 应用程序中显示相关的数据](../data-tools/walkthrough-displaying-related-data-in-a-wpf-application.md)
