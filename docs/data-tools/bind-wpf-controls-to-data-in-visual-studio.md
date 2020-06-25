---
title: 将 WPF 控件绑定到数据-第1部分
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- data [WPF], displaying
- WPF, data binding in Visual Studio
- WPF data binding [Visual Studio]
- displaying data, WPF
- WPF [WPF], data
- WPF Designer, data binding
- data binding, WPF
ms.assetid: e05a1e0c-5082-479d-bbc9-d395b0bc6580
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 27d0c14bcf09a3b0d30cd23dea0f8348c45fcab7
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85282876"
---
# <a name="bind-wpf-controls-to-data-in-visual-studio"></a>在 Visual Studio 中将 WPF 控件绑定到数据

通过将数据绑定到 [!INCLUDE[TLA#tla_titlewinclient](../data-tools/includes/tlasharptla_titlewinclient_md.md)] 控件，可以向应用程序的用户显示数据。 若要创建这些数据绑定控件，可以将项从 "**数据源**" 窗口拖动到 [!INCLUDE[wpfdesigner_current_short](../data-tools/includes/wpfdesigner_current_short_md.md)] Visual Studio 中的。 本主题将介绍一些您可用于创建数据绑定 [!INCLUDE[TLA#tla_titlewinclient](../data-tools/includes/tlasharptla_titlewinclient_md.md)] 应用程序的最常见的任务、工具和类。

有关如何在 Visual Studio 中创建数据绑定控件的一般信息，请参阅[在 Visual studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)。 有关数据绑定的详细信息 [!INCLUDE[TLA#tla_titlewinclient](../data-tools/includes/tlasharptla_titlewinclient_md.md)] ，请参阅[数据绑定概述](/dotnet/desktop-wpf/data/data-binding-overview)。

## <a name="tasks-involved-in-binding-wpf-controls-to-data"></a>将 WPF 控件绑定到数据所涉及的任务

下表列出了可以通过将项从“数据源”窗口拖到 [!INCLUDE[wpfdesigner_current_short](../data-tools/includes/wpfdesigner_current_short_md.md)] 来完成的任务****。

|任务|详细信息|
|----------| - |
|新建数据绑定控件。<br /><br /> 将现有控件绑定到数据。|[将 WPF 控件绑定到数据集](../data-tools/bind-wpf-controls-to-a-dataset.md)|
|创建按父子关系显示相关数据的控件：当用户选择一个控件中的父数据记录时，另一个控件将显示所选记录的相关子数据。|[在 WPF 应用程序中显示相关数据](../data-tools/display-related-data-in-wpf-applications.md)|
|创建“查找表”，此表根据一个表的外键字段的值显示另一个表中的信息**。|[在 WPF 应用程序中创建查找表](../data-tools/create-lookup-tables-in-wpf-applications.md)|
|将控件绑定到数据库中的图像。|[将控件绑定到数据库中的图片](../data-tools/bind-controls-to-pictures-from-a-database.md)|

## <a name="valid-drop-targets"></a>有效放置目标

只能将“数据源”窗口中的项拖动到 [!INCLUDE[wpfdesigner_current_short](../data-tools/includes/wpfdesigner_current_short_md.md)] 中的有效放置目标****。 有两种主要的有效放置目标：容器和控件。 容器是通常包含控件的用户界面元素。 例如，网格是容器，窗口也是容器。

## <a name="generated-xaml-and-code"></a>生成的 XAML 和代码

将项从 "**数据源**" 窗口拖到时 [!INCLUDE[wpfdesigner_current_short](../data-tools/includes/wpfdesigner_current_short_md.md)] ，Visual Studio 将生成 [!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] 定义新的数据绑定控件（或将现有控件绑定到数据源）的。 对于某些数据源，Visual Studio 还会在代码隐藏文件中生成用数据填充数据源的代码。

下表列出了 [!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] Visual Studio 为 "**数据源**" 窗口中的每种类型的数据源生成的和代码。

| 数据源 | 生成将控件绑定到数据源的 XAML | 生成用数据填充数据源的代码 |
| - | - | - |
| 数据集 | 是 | 是 |
| [!INCLUDE[adonet_edm](../data-tools/includes/adonet_edm_md.md)] | 是 | 是 |
| 服务 | 是 | 否 |
| Object | 是 | 否 |

### <a name="datasets"></a>数据集

将表或列从 "**数据源**" 窗口拖到设计器中时，Visual Studio 将生成 [!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] 以下内容：

- 将数据集和新的 <xref:System.Windows.Data.CollectionViewSource> 添加到将项拖至的容器的资源中。 <xref:System.Windows.Data.CollectionViewSource> 是可用于导航和显示数据集中的数据的对象。

- 为控件创建数据绑定。 如果将项拖动到设计器中的一个现有控件上，则 XAML 会将该控件绑定到该项。 如果将项拖动到容器中，则 XAML 会创建为拖动项选择的控件，并将该控件绑定到该项。 将在新的 <xref:System.Windows.Controls.Grid> 内创建该控件。

Visual Studio 还将对代码隐藏文件做出以下更改：

- 为包含该控件的 <xref:System.Windows.FrameworkElement.Loaded> 元素创建 [!INCLUDE[TLA2#tla_ui](../data-tools/includes/tla2sharptla_ui_md.md)] 事件处理程序。 该事件处理程序用数据填充表，从容器的资源中检索 <xref:System.Windows.Data.CollectionViewSource>，然后使第一个数据项成为当前项。 如果 <xref:System.Windows.FrameworkElement.Loaded> 事件处理程序已存在，则 Visual Studio 会将此代码添加到现有的事件处理程序。

### <a name="entity-data-models"></a>实体数据模型

将实体或实体属性从 "**数据源**" 窗口拖到设计器中时，Visual Studio 将生成 [!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] 执行以下操作的：

- 将新的 <xref:System.Windows.Data.CollectionViewSource> 添加到将项拖至的容器的资源中。 <xref:System.Windows.Data.CollectionViewSource> 是可用于导航和显示实体中的数据的对象。

- 为控件创建数据绑定。 如果将项拖动到设计器中的一个现有控件上，则 [!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] 会将该控件绑定到该项。 如果将项拖动到容器中，则 [!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] 会创建为拖动项选择的控件，并将该控件绑定到该项。 将在新的 <xref:System.Windows.Controls.Grid> 内创建该控件。

Visual Studio 还将对代码隐藏文件做出以下更改：

- 添加一种新方法，该方法返回对拖动到设计器中的实体（或包含拖动到设计器中的属性的实体）的查询。 新方法具有名称 `Get<EntityName>Query` ，其中 `\<EntityName>` 是实体的名称。

- 为包含该控件的 <xref:System.Windows.FrameworkElement.Loaded> 元素创建 [!INCLUDE[TLA2#tla_ui](../data-tools/includes/tla2sharptla_ui_md.md)] 事件处理程序。 该事件处理程序调用 `Get<EntityName>Query` 方法以用数据填充实体， <xref:System.Windows.Data.CollectionViewSource> 从容器的资源中检索，然后使第一个数据项成为当前项。 如果 <xref:System.Windows.FrameworkElement.Loaded> 事件处理程序已存在，则 Visual Studio 会将此代码添加到现有的事件处理程序。

### <a name="services"></a>服务

将服务对象或属性从 "**数据源**" 窗口拖到设计器中时，Visual Studio 将生成以 [!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] 创建数据绑定控件（或将现有控件绑定到该对象或属性）。 但是，Visual Studio 不会生成用数据填充代理服务对象的代码。 你必须自己编写此代码。 有关演示如何执行此操作的示例，请参阅[将 WPF 控件绑定到 WCF 数据服务](../data-tools/bind-wpf-controls-to-a-wcf-data-service.md)。

Visual Studio 将生成执行以下操作的 XAML：

- 将新的 <xref:System.Windows.Data.CollectionViewSource> 添加到将项拖至的容器的资源中。 <xref:System.Windows.Data.CollectionViewSource> 是一个对象，它可用于导航和显示服务返回的对象中的数据。

- 为控件创建数据绑定。 如果将项拖动到设计器中的一个现有控件上，则 [!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] 会将该控件绑定到该项。 如果将项拖动到容器中，则 [!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] 会创建为拖动项选择的控件，并将该控件绑定到该项。 将在新的 <xref:System.Windows.Controls.Grid> 内创建该控件。

### <a name="objects"></a>对象

将对象或属性从 "**数据源**" 窗口拖到设计器中时，Visual Studio 将生成以 [!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] 创建数据绑定控件（或将现有控件绑定到该对象或属性）。 但是，Visual Studio 不会生成代码来用数据填充对象。 你必须自己编写此代码。

> [!NOTE]
> 自定义类必须是公共的，并且默认情况下，具有不带参数的构造函数。 它们不能是其语法中包含 "dot" 的嵌套类。 有关详细信息，请参阅[WPF 的 XAML 和自定义类](/dotnet/framework/wpf/advanced/xaml-and-custom-classes-for-wpf)。

Visual Studio 生成 [!INCLUDE[TLA#tla_titlexaml](../data-tools/includes/tlasharptla_titlexaml_md.md)] 以下内容：

- 将新的 <xref:System.Windows.Data.CollectionViewSource> 添加到将项拖至的容器的资源中。 <xref:System.Windows.Data.CollectionViewSource> 是可用于导航和显示对象中的数据的对象。

- 为控件创建数据绑定。 如果将项拖动到设计器中的一个现有控件上，则 XAML 会将该控件绑定到该项。 如果将项拖动到容器中，则 XAML 会创建为拖动项选择的控件，并将该控件绑定到该项。 将在新的 <xref:System.Windows.Controls.Grid> 内创建该控件。

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)
