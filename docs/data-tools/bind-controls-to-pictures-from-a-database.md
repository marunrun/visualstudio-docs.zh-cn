---
title: 将控件绑定到数据库中的图片
ms.date: 11/04/2016
ms.topic: conceptual
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
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: 4e41cb7bf747a1c083dc1728d7ea26f47ad8fa48
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62818158"
---
# <a name="bind-controls-to-pictures-from-a-database"></a>将控件绑定到数据库中的图片

可以使用**数据源**窗口将在数据库中的图像绑定到你的应用程序中的控件。 例如，将绑定到图像<xref:System.Windows.Controls.Image>控制在 WPF 应用程序中，或为<xref:System.Windows.Forms.PictureBox>Windows 窗体应用程序中的控件。

作为字节数组通常存储在数据库中的图片。 中的项**数据源**将存储为字节数组具有键入其控件的窗口将设置为**None**默认情况下，原因是字节数组可以包含任何内容，从简单的可执行文件的字节数组大型应用程序。 若要创建数据绑定控件中的字节数组项**数据源**表示的图像的窗口中，您必须选择要创建的控件。

以下过程假设**数据源**窗口已填充的项的绑定到你的映像。

## <a name="to-bind-a-picture-in-a-database-to-a-control"></a>若要在数据库中的图片绑定到控件

1. 请确保你想要将控件添加到设计图面是在 WPF 设计器或 Windows 窗体设计器中打开。

2. 在中**数据源**窗口中，展开所需的表，或要显示其列或属性的对象。

   > [!TIP]
   > 如果**数据源**窗口未打开，选择打开**视图** > **其他 Windows** > **数据源**.

3. 选择列或属性，其中包含您的图像数据，并从其下拉列表控件列表中选择以下控件之一：

    - 如果 WPF 设计器打开，请选择**图像**。

    - 如果 Windows 窗体设计器打开，请选择**PictureBox**。

    - 或者，可以选择一个不同的控件的支持数据绑定和可显示图像。 如果你想要使用的控件不在可用控件列表中，您可以将其添加到列表，然后选择它。 有关详细信息，请参阅[将自定义控件添加到数据源窗口](../data-tools/add-custom-controls-to-the-data-sources-window.md)。

## <a name="see-also"></a>请参阅

- [在 Visual Studio 中将 WPF 控件绑定到数据](../data-tools/bind-wpf-controls-to-data-in-visual-studio.md)