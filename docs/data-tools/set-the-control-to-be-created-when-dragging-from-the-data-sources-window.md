---
title: 设置从 "数据源" 窗口拖动时要创建的控件
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Data Sources Window, select controls
- Windows Forms, displaying data
- data [Visual Studio], displaying on Windows Forms
- data [Visual Studio], Data Sources window
ms.assetid: 20597ff8-0c98-43ec-8fb1-05376804ba48
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: b5c57b73656f75ae9d99211ba28e38935d3164cb
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72641043"
---
# <a name="set-the-control-to-be-created-when-dragging-from-the-data-sources-window"></a>设置从“数据源”窗口中拖动时要创建的控件

可以通过将项从 "**数据源**" 窗口拖到 WPF 设计器或 Windows 窗体设计器来创建数据绑定控件。 "**数据源**" 窗口中的每个项都有一个默认控件，该控件是在将其拖到设计器时创建的。 不过，您可以选择创建不同的控件。

## <a name="set-the-controls-to-be-created-for-data-tables-or-objects"></a>设置要为数据表或对象创建的控件

在从 "**数据源**" 窗口中拖动表示数据表或对象的项之前，您可以选择在一个控件中显示所有数据，或者在单独的控件中显示每个列或属性。

在此上下文中，术语 "*对象*" 指的是自定义业务对象、实体（在实体数据模型中）或服务返回的对象。

### <a name="to-set-the-controls-to-be-created-for-data-tables-or-objects"></a>设置要为数据表或对象创建的控件

1. 确保**WPF**设计器或**Windows 窗体**设计器处于打开状态。

2. 在 "**数据源**" 窗口中，选择表示要设置的数据表或对象的项。

   > [!TIP]
   > 如果 "**数据源**" 窗口未打开，可以通过选择 "**视图**"  > **其他 Windows**  > **数据源**打开它。

3. 单击该项的下拉菜单，然后在菜单中单击以下项之一：

    - 若要在单独的控件中显示每个数据字段，请单击 "**详细信息**"。 将数据项拖到设计器中时，此操作将为父数据表或对象的每个列或属性以及每个控件的标签创建一个不同的数据绑定控件。

    - 若要在单个控件中显示所有数据，请在列表中选择一个不同的控件，例如 WPF 应用程序中的**DataGrid**或**列表**，或 Windows 窗体应用程序中的**DataGridView** 。

    可用控件的列表取决于你已打开的设计器、你的项目面向的 .NET 版本，以及你是否已将支持数据绑定的自定义控件添加到 "**工具箱**"。 如果您要创建的控件不在可用控件列表中，则可以将该控件添加到该列表中。 有关详细信息，请参阅[将自定义控件添加到 "数据源" 窗口](../data-tools/add-custom-controls-to-the-data-sources-window.md)。

    若要了解如何创建自定义 Windows 窗体控件，该控件可以添加到 "**数据源**" 窗口中的数据表或对象的控件列表中，请参阅[创建支持复杂数据绑定的 Windows 窗体用户控件](../data-tools/create-a-windows-forms-user-control-that-supports-complex-data-binding.md)。

## <a name="set-the-controls-to-be-created-for-data-columns-or-properties"></a>设置要为数据列或属性创建的控件

将表示对象的列或属性的项从 "**数据源**" 窗口拖到设计器之前，可以设置要创建的控件。

### <a name="to-set-the-controls-to-be-created-for-columns-or-properties"></a>设置要为列或属性创建的控件

1. 确保**WPF**设计器或**Windows 窗体**设计器处于打开状态。

2. 在 "**数据源**" 窗口中，展开所需的表或对象以显示其列或属性。

3. 选择要为其设置要创建的控件的每个列或属性。

4. 单击列或属性的下拉菜单，然后选择要在将项拖动到设计器时创建的控件。

     可用控件的列表取决于你已打开的设计器、你的项目面向的 .NET 版本以及支持你已添加到**工具箱**中的数据绑定的自定义控件。 如果要创建的控件位于可用控件列表中，则可以将该控件添加到该列表中。 有关详细信息，请参阅[将自定义控件添加到 "数据源" 窗口](../data-tools/add-custom-controls-to-the-data-sources-window.md)。

     若要了解如何创建可添加到 "**数据源**" 窗口中数据列或属性的控件列表中的自定义控件，请参阅[创建支持简单数据绑定的 Windows 窗体用户控件](../data-tools/create-a-windows-forms-user-control-that-supports-simple-data-binding.md)。

     如果不想创建列或属性的控件，请在下拉菜单中选择 "**无**"。 如果要将父表或对象拖到设计器中，但又不想包含特定列或属性，这会很有用。

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)