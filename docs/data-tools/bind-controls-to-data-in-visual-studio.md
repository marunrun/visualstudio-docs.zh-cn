---
title: 将控件绑定到数据
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- data, displaying
- data sources, displaying data
- Data Sources window
- displaying data
ms.assetid: be8b6623-86a6-493e-ab7a-050de4661fd6
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 32b392f59fb0ac587730d2aa432ca11d91d5a9ea
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62824822"
---
# <a name="bind-controls-to-data-in-visual-studio"></a>在 Visual Studio 中将控件绑定到数据

通过将数据绑定到控件，可以向应用程序的用户显示数据。 可以通过将项从创建这些数据绑定控件**数据源**窗口拖到设计图面上或在 Visual Studio 中的图面上的控件。

本主题描述可用于创建数据绑定控件的数据源。 它还描述了数据绑定中涉及的一些常规任务。 有关如何创建数据绑定控件的更多具体详细信息，请参阅[绑定 Windows 窗体控件添加到 Visual Studio 中的数据](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)并[控件添加到 Visual Studio 中的数据绑定 WPF](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)。

## <a name="data-sources"></a>数据源

在数据绑定的上下文中，数据源表示可绑定到您的用户界面的内存中的数据。 在实践中，数据源可以是实体框架类、 数据集、 封装.NET 代理对象、 LINQ to SQL 类或任何.NET 对象或集合中的服务终结点。 某些数据源支持通过从“数据源”窗口拖动项来创建数据绑定控件，而其他数据源则不能。 下表显示了支持的数据源。

| 数据源 | Windows 窗体设计器中的拖放支持 | WPF 设计器中的拖放支持 | Silverlight 设计器中的拖放支持 |
| - | - | - | - |
| 数据集 | 是 | 是 | 否 |
| 实体数据模型 | 是<sup>1</sup> | 是 | 是 |
| LINQ to SQL 类 | 否<sup>2</sup> | 否<sup>2</sup> | 否<sup>2</sup> |
| 服务（包括 [!INCLUDE[ssAstoria](../data-tools/includes/ssastoria_md.md)]、WCF 服务和 Web 服务） | 是 | 是 | 是 |
| 对象 | 是 | 是 | 是 |
| SharePoint | 是 | 是 | 是 |

1. 生成模型使用**实体数据模型**向导中，然后将这些对象拖到设计器。

2. LINQ to SQL 类不会出现在“数据源”窗口中。 不过，你可以添加基于 LINQ to SQL 类的新对象数据源，然后将这些对象拖到设计器来创建数据绑定控件。 有关详细信息，请参见[演练：创建 LINQ to SQL 类（O-R 设计器）](how-to-create-linq-to-sql-classes-mapped-to-tables-and-views-o-r-designer.md)。

## <a name="data-sources-window"></a>“数据源”窗口

数据源以“数据源”窗口中的项的形式提供给项目。 窗体设计图面是活动窗口在项目中，或可以通过选择打开它 （如果项目处于打开状态） 时，此窗口是否可见**视图** > **其他 Windows**  >  **数据源**。 可以将项从此窗口来创建绑定到基础数据的控件，还可以通过右键单击配置数据源。

![“数据源”窗口](../data-tools/media/raddata-data-sources-window.png)

对于显示在“数据源”窗口中的每个数据类型，将该项拖到设计器时，都会创建一个默认控件。 中的项拖之前**数据源**窗口中，你可以创建的控件。 有关详细信息，请参阅[设置从数据源窗口中拖动时创建的控件](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)。

## <a name="tasks-involved-in-binding-controls-to-data"></a>将控件绑定到数据所涉及的任务

下表列出了一些最常见的任务所需执行将控件绑定到数据。

|任务|详细信息|
|----------| - |
|打开“数据源”窗口。|在编辑器中打开设计图面，然后选择**视图** > **数据源**。|
|将数据源添加到项目中。|[添加新数据源](../data-tools/add-new-data-sources.md)|
|设置在将项从“数据源”窗口拖到设计器时创建的控件。|[设置从“数据源”窗口中拖动时要创建的控件](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)|
|修改与“数据源”窗口中的项关联的控件的列表。|[向“数据源”窗口添加自定义控件](../data-tools/add-custom-controls-to-the-data-sources-window.md)|
|创建数据绑定控件。|[在 Visual Studio 中将 Windows 窗体控件绑定到数据](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)<br /><br /> [在 Visual Studio 中将 WPF 控件绑定到数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)|
|将绑定到对象或集合。|[Visual Studio 中的绑定对象](../data-tools/bind-objects-in-visual-studio.md)|
|在 UI 中显示的数据进行筛选。|[在 Windows 窗体应用程序中对数据进行筛选和排序](../data-tools/filter-and-sort-data-in-a-windows-forms-application.md)|
|自定义控件的标题。|[自定义 Visual Studio 创建数据绑定控件的标题的方式](../data-tools/customize-how-visual-studio-creates-captions-for-data-bound-controls.md)|

## <a name="see-also"></a>请参阅

- [适用于 NET 的 Visual Studio Data Tools](../data-tools/visual-studio-data-tools-for-dotnet.md)
- [Windows 窗体数据绑定](/dotnet/framework/winforms/windows-forms-data-binding)