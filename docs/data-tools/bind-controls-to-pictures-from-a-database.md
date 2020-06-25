---
title: 将控件绑定到数据库中的图片
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- images [Visual Basic], displaying on Windows Forms
- data binding [Windows Forms], pictures
- images [Visual Basic], data binding
- pictures, data binding
- pictures, dragging from Data Sources window
- Data Sources Window, setting controls to display images
- PictureBox control [Windows Forms], data binding
- images [Visual Basic], dragging from Data Sources window
ms.assetid: 9748815e-3556-49e8-86b1-c6aa593c6163
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: e9093c2a2d7cec95e4fdd08ff4273ae8f8126a36
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/23/2020
ms.locfileid: "85282979"
---
# <a name="bind-controls-to-pictures-from-a-database"></a>将控件绑定到数据库中的图片

您可以使用 "**数据源**" 窗口将数据库中的图像绑定到应用程序中的控件。 例如，可以将图像绑定到 <xref:System.Windows.Controls.Image> WPF 应用程序中的控件或 <xref:System.Windows.Forms.PictureBox> Windows 窗体应用程序中的控件。

数据库中的图片通常作为字节数组存储。 默认情况下，作为字节数组存储的 "**数据源**" 窗口中的项的控件类型默认设置为 "**无**"，因为字节数组可以包含从简单字节数组到大型应用程序的可执行文件的任何内容。 若要为表示图像的 "**数据源**" 窗口中的字节数组项创建数据绑定控件，你必须选择要创建的控件。

下面的过程假定 "**数据源**" 窗口已经用绑定到图像的项填充。

## <a name="to-bind-a-picture-in-a-database-to-a-control"></a>将数据库中的图片绑定到控件

1. 请确保要将控件添加到的设计图面在 WPF 设计器或 Windows 窗体设计器中处于打开状态。

2. 在 "**数据源**" 窗口中，展开所需的表或对象以显示其列或属性。

   > [!TIP]
   > 如果 "**数据源**" 窗口未打开，请选择 "**查看**  >  **其他 Windows**  >  **数据源**" 将其打开。

3. 选择包含图像数据的列或属性，并从其下拉控件列表中选择以下控件之一：

    - 如果 WPF 设计器处于打开状态，请选择 "**图像**"。

    - 如果 Windows 窗体设计器处于打开状态，请选择**PictureBox**。

    - 此外，还可以选择支持数据绑定的其他控件，并可以显示图像。 如果要使用的控件不在可用控件列表中，则可以将其添加到列表中，然后选择它。 有关详细信息，请参阅[将自定义控件添加到 "数据源" 窗口](../data-tools/add-custom-controls-to-the-data-sources-window.md)。

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 中将 WPF 控件绑定到数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)
