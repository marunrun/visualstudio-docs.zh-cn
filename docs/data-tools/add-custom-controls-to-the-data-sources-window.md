---
title: 向“数据源”窗口添加自定义控件
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.datasource.howtoaddcustomcontrol
helpviewer_keywords:
- Data Sources Window, adding controls
- controls [Visual Studio], adding to Data Sources Window
- DefaultBindingPropertyAttribute class, using
- LookupBindingPropertiesAttribute class, using
- ComplexBindingPropertiesAttribute class, using
- Data Sources Window, selecting controls
ms.assetid: 8c43e7d2-ba94-4d9b-96de-3aa971955afd
author: ghogen
ms.author: ghogen
manager: jillfra
ms.openlocfilehash: 39ff272581793be9b456bbc404119a488850b3c4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "85283068"
---
# <a name="add-custom-controls-to-the-data-sources-window"></a>向“数据源”窗口添加自定义控件

将项从 "数据源" 窗口拖到设计图面以创建数据绑定控件时，可以选择您创建的控件类型。 窗口中的每个项都有一个下拉列表，其中显示了您可以选择的控件。 与每个项关联的控件集由项的数据类型确定。 如果您要创建的控件未出现在列表中，则可以按照本主题中的说明将该控件添加到列表中。

有关选择要为 "数据源" 窗口中的项创建的数据绑定控件的详细信息，请参阅 [设置从 "数据源" 窗口中拖动时要创建的控件](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)。

## <a name="customize-the-bindable-controls-list"></a>自定义可绑定控件列表

若要从 "数据源" 窗口中具有特定数据类型的项的可用控件列表中添加或删除控件，请执行以下步骤。

### <a name="to-select-the-controls-to-be-listed-for-a-data-type"></a>选择要为数据类型列出的控件

1. 确保 WPF 设计器或 Windows 窗体设计器处于打开状态。

2. 在 " **数据源** " 窗口中，单击作为添加到窗口的数据源的一部分的项，然后单击该项的下拉菜单。

   > [!TIP]
   > 如果 "数据源" 窗口未打开，请选择 "**查看**  >  **其他 Windows**  >  **数据源**" 将其打开。

3. 在下拉菜单中，单击 " **自定义**"。 此时将打开下列对话框之一：

    - 如果**Windows 窗体设计器**处于打开状态，则会打开 "**选项**" 对话框的 "**数据 UI 自定义**" 页。 有关详细信息，请参阅 " [数据 UI 自定义选项" 对话框](../ide/reference/options-windows-forms-designer-data-ui-customization.md)。

    - 如果 **WPF 设计器** 处于打开状态，则 " **自定义控件绑定** " 对话框将打开。

4. 在对话框中，从 " **数据类型** " 下拉列表中选择一种数据类型。

    - 若要自定义表或对象的控件列表，请选择 " **列表**"。

    - 若要为表的列或对象的属性自定义控件列表，请选择基础数据存储区中的列或属性的数据类型。

    - 若要自定义控件列表以显示具有用户定义的形状的数据对象，请选择 " **[其他]**"。 例如，如果您的应用程序具有可显示特定对象的多个属性的数据的自定义控件，则选择 " **[其他]** "。

5. 在 " **关联的控件** " 框中，选择要用于所选数据类型的每个控件，或取消选择要从列表中删除的任何控件。

    > [!NOTE]
    > 如果要选择的控件未出现在 " **关联的控件** " 框中，则必须将该控件添加到该列表中。 有关详细信息，请参阅 [添加关联控件](#add-associated-controls)。

6. 单击“确定”。

7. 在 " **数据源** " 窗口中，单击与一个或多个控件关联的数据类型的项，然后单击该项的下拉菜单。

     此时，在 "关联的 **控件** " 框中选择的控件将显示在该项的下拉菜单中。

## <a name="add-associated-controls"></a>添加关联控件

如果要将控件与数据类型相关联，但控件未出现在 " **关联的控件** " 框中，则必须将该控件添加到列表中。 控件必须位于当前解决方案或引用的程序集中。 它还必须在 " **工具箱** " 中提供，并且具有指定控件的数据绑定行为的特性。

若要将控件添加到关联控件列表：

1. 右键单击**工具箱**并选择 "**选择项**"，将所需的控件添加到 "**工具箱**"。

     控件必须具有以下属性之一：

    |特性|说明|
    |---------------|-----------------|
    |<xref:System.ComponentModel.DefaultBindingPropertyAttribute>|在显示单列 (或属性) 数据的简单控件上实现此特性，例如 <xref:System.Windows.Forms.TextBox> 。|
    |<xref:System.ComponentModel.ComplexBindingPropertiesAttribute>|在显示列表 (或表) 数据的控件（如）中实现此特性 <xref:System.Windows.Forms.DataGridView> 。|
    |<xref:System.ComponentModel.LookupBindingPropertiesAttribute>|在 (或表) 显示列表的控件上实现此属性，但也需要显示单个列或属性，例如 <xref:System.Windows.Forms.ComboBox> 。|

2. 对于 Windows 窗体，请在 " **选项** " 对话框中打开 " **数据 UI 自定义** " 页。 或者，对于 WPF，打开 " **自定义控件绑定** " 对话框。 有关详细信息，请参阅 [自定义数据类型的可绑定控件列表](#customize-the-bindable-controls-list)。

3. 在 " **关联的控件** " 框中，刚刚添加到 " **工具箱** " 中的控件现在应显示。

    > [!NOTE]
    > 只有位于当前解决方案或被引用程序集中的控件才能添加到关联控件列表中。  (控件还必须实现上一个表中的一个数据绑定属性。 ) 要将数据绑定到 "数据源" 窗口中不可用的自定义控件，请将该控件从 " **工具箱** " 拖到设计图面上，然后从 " **数据源** " 窗口中将该项拖到控件上。

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)
- ["数据 UI 自定义选项" 对话框](../ide/reference/options-windows-forms-designer-data-ui-customization.md)
