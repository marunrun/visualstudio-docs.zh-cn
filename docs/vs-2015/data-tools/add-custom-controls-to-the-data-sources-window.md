---
title: 将自定义控件添加到数据源窗口 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
f1_keywords:
- vs.datasource.howtoaddcustomcontrol
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- Data Sources Window, adding controls
- controls [Visual Studio], adding to Data Sources Window
- DefaultBindingPropertyAttribute class, using
- LookupBindingPropertiesAttribute class, using
- ComplexBindingPropertiesAttribute class, using
- Data Sources Window, selecting controls
ms.assetid: 8c43e7d2-ba94-4d9b-96de-3aa971955afd
caps.latest.revision: 45
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 28476c454dc78f30e33c0b37e8319bfe5a65df2d
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65699390"
---
# <a name="add-custom-controls-to-the-data-sources-window"></a>向“数据源”窗口添加自定义控件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

当将某项从**数据源**到设计图面来创建数据绑定控件的窗口，可以选择你创建的控件的类型。 在窗口中的每个项具有下拉列表，其中显示您可以从选择的控件。 通过项的数据类型确定的每个项与相关联的控件的集合。 如果你想要创建该控件不会出现在列表中，可以按照本主题中的说明将控件添加到列表。  
  
 有关选择数据绑定控件中项创建的详细信息**数据源**窗口中，请参阅[设置从数据源窗口中拖动时创建的控件](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md)。  
  
> [!NOTE]
> 显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你的当前设置或版本。 若要更改您的设置，在**工具**菜单中，选择**导入和导出设置**。 有关详细信息，请参阅 [在 Visual Studio 中自定义开发设置](https://msdn.microsoft.com/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
## <a name="customizinglist"></a> 自定义数据类型可绑定控件的列表  
 若要添加或删除控件，从列表中的可用控件中的项**数据源**窗口具有特定的数据类型，请执行以下步骤。  
  
#### <a name="to-select-the-controls-to-be-listed-for-a-data-type"></a>若要选择要为数据类型列出的控件  
  
1. 请确保在 WPF 设计器或 Windows 窗体设计器处于打开状态。  
  
2. 在中**数据源**窗口中，单击的是添加到窗口中，数据源的一部分的项目，然后单击下拉列表菜单项。  
  
3. 在下拉列表菜单中，单击**自定义**。 将打开下列对话框之一：  
  
    - Windows 窗体设计器处于打开状态，如果**数据 UI 自定义**页**选项**对话框随即打开。  
  
    - WPF 设计器处于打开状态，如果**自定义控件绑定**对话框随即打开。  
  
4. 在对话框中，选择数据类型从**数据类型**下拉列表。  
  
    - 若要自定义的表或对象的控件列表，请选择 **[列表]**。  
  
    - 若要自定义控件的列的表或对象的属性列表，请选择基础数据存储区中的列或属性的数据类型。  
  
    - 若要自定义控件以显示具有用户定义的形状的数据对象的列表，请选择 **[其他]**。 例如，选择 **[其他]** 如果你的应用程序具有的自定义控件，显示来自多个特定对象的属性的数据。  
  
5. 在中**关联的控件**框中，选择你想要将适用于所选的数据类型，每个控件或清除你想要从列表中删除任何控件的选择。  
  
    > [!NOTE]
    > 如果你想要选择该控件不会出现在**关联的控件**框中，必须将控件添加到列表。 有关详细信息，请参阅[将控件添加到数据类型的关联控件列表](#addingcontrols)。  
  
6. 单击 **“确定”**。  
  
7. 在中**数据源**窗口中，单击数据的项键入您刚刚关联一个或多个控件，然后单击项的下拉列表菜单。  
  
     在中选择的控件**关联的控件**框现在显示在下拉列表菜单项。  
  
## <a name="addingcontrols"></a> Addcontrols 到关联控件的数据类型的列表  
 如果你想要将某个控件与数据类型，但该控件不会出现在**关联的控件**框中，必须将控件添加到列表。 该控件必须位于当前解决方案中或引用的程序集。 它还必须提供**工具箱**，并且具有一个属性，指定控件的数据绑定行为。  
  
#### <a name="to-add-controls-to-the-list-of-associated-controls"></a>若要将控件添加到关联控件的列表  
  
1. 添加到所需的控制**工具箱**通过右击**工具箱**，然后选择**选择项**。  
  
     控件必须具有以下属性之一。  
  
    |特性|描述|  
    |---------------|-----------------|  
    |<xref:System.ComponentModel.DefaultBindingPropertyAttribute>|此属性显示的数据，单个列 （或属性） 的简单控件上实现如<xref:System.Windows.Forms.TextBox>。|  
    |<xref:System.ComponentModel.ComplexBindingPropertiesAttribute>|此属性显示数据列表 （或表） 的控件上实现如<xref:System.Windows.Forms.DataGridView>。|  
    |<xref:System.ComponentModel.LookupBindingPropertiesAttribute>|此属性显示的数据，但还需要提供单个列或属性列表 （或表） 的控件上实现如<xref:System.Windows.Forms.ComboBox>。|  
  
2. Windows 窗体上**选项**对话框中，打开**数据 UI 自定义**页。 或者，对于 WPF 中，打开**自定义控件绑定**对话框。 有关详细信息，请参阅[自定义数据类型的可绑定控件列表的](#customizinglist)。  
  
3. 在中**关联的控件**框中，只需添加到该控件**工具箱**现在应出现。  
  
    > [!NOTE]
    > 是位于当前解决方案中引用的程序集中的唯一控件可以添加到关联控件的列表。 （控件还必须实现数据绑定特性之一上表中。）若要将数据绑定到在中不可用的自定义控件**数据源**窗口中，将从控件**工具箱**拖动到设计图面上，然后拖动要将绑定到中的项**数据源**窗口拖动到控件。  
  
## <a name="see-also"></a>请参阅  
 [在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)
