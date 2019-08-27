---
title: 设置从数据源窗口中拖动时创建的控件 |Microsoft Docs
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
- Data Sources Window, select controls
- Windows Forms, displaying data
- data [Visual Studio], displaying on Windows Forms
- data [Visual Studio], Data Sources window
ms.assetid: 20597ff8-0c98-43ec-8fb1-05376804ba48
caps.latest.revision: 34
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 3c9902080ae501c1d77a59f152d7d272462d2264
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62563215"
---
# <a name="set-the-control-to-be-created-when-dragging-from-the-data-sources-window"></a>设置从“数据源”窗口中拖动时要创建的控件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以通过将项从创建数据绑定控件**数据源**窗口拖到 WPF 设计器或 Windows 窗体设计器。 中的每项**数据源**窗口具有时将其拖到设计器中创建一个默认控件。 但是，您可以选择创建一个不同的控件。  
  
## <a name="set-the-controls-to-be-created-for-data-tables-or-objects"></a>设置为数据表或对象创建的控件  
 拖动这些项表示数据表或对象从之前**数据源**窗口中，可以选择一个控件中显示的所有数据或要在一个单独的控件中都显示每个列或属性。  
  
 在此上下文中，术语*对象*指的是自定义业务对象、 实体 （在实体数据模型中） 或由服务返回的对象。  
  
#### <a name="to-set-the-controls-to-be-created-for-data-tables-or-objects"></a>若要设置为数据表或对象创建的控件  
  
1. 请确保在 WPF 设计器或 Windows 窗体设计器处于打开状态。  
  
2. 在中**数据源**窗口中，选择表示数据表的项或要设置对象。  
  
3. 单击项的下拉列表菜单，然后单击菜单中的以下项之一：  
  
   - 若要在单独控件中显示每个数据字段，请单击**详细信息**。 将数据项拖到设计器中，此操作将创建每个列或属性的父数据的表或对象，以及为每个控件的标签的不同数据绑定控件。  
  
   - 若要在单个控件中显示的所有数据，请选择一个不同的控件在列表中，如**DataGrid**或**列表**在 WPF 应用程序中，或**DataGridView**在 Windows 窗体中应用程序。  
  
     可用控件列表取决于所在的设计器上已打开，.NET Framework 的版本将项目目标，以及是否已添加自定义控件支持数据绑定到的**工具箱**。 如果你想要创建的控件的可用控件列表中，可以将控件添加到列表。 有关详细信息，请参阅[将自定义控件添加到数据源窗口](../data-tools/add-custom-controls-to-the-data-sources-window.md)。  
  
     若要了解如何创建可添加到的控件中数据的表或对象列表的自定义 Windows 窗体控件**数据源**窗口中，请参阅[创建支持复杂数据的 Windows 窗体用户控件绑定](../data-tools/create-a-windows-forms-user-control-that-supports-complex-data-binding.md)。  
  
## <a name="set-the-controls-to-be-created-for-data-columns-or-properties"></a>设置要创建的数据列或属性的控件  
 拖动项表示某一列或从对象的属性之前**数据源**到设计器窗口中的，可以设置要创建的控件。  
  
#### <a name="to-set-the-controls-to-be-created-for-columns-or-properties"></a>若要设置为列或属性创建的控件  
  
1. 请确保在 WPF 设计器或 Windows 窗体设计器处于打开状态。  
  
2. 在中**数据源**窗口中，展开所需的表，或要显示其列或属性的对象。  
  
3. 选择你想要设置的控件创建每个列或属性。  
  
4. 单击列或属性的下拉列表菜单，然后选择你想要创建一项拖动到设计器时的控件。  
  
     可用控件列表取决于所在的设计器上已打开，.NET Framework 的版本将项目目标，以及的自定义控件的支持的数据绑定，已添加到**工具箱**。 如果你想要创建的控件的可用控件列表中，可以将控件添加到列表。 有关详细信息，请参阅[将自定义控件添加到数据源窗口](../data-tools/add-custom-controls-to-the-data-sources-window.md)。  
  
     若要了解如何创建可添加到的数据列或属性中的控件列表的自定义控件**数据源**窗口中，请参阅[创建支持简单数据绑定的Windows窗体用户控件](../data-tools/create-a-windows-forms-user-control-that-supports-simple-data-binding.md).  
  
     如果不想要创建的列或属性的控件，请选择**None**下拉列表菜单中。 如果你想要将父表或对象拖动到设计器中，但不是希望包含的特定列或属性，这非常有用。  
  
## <a name="see-also"></a>请参阅  
 [在 Visual Studio 中将控件绑定到数据](../data-tools/bind-controls-to-data-in-visual-studio.md)
