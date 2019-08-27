---
title: 如何：向工作表添加 XMLMappedRange 控件
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XMLMappedRange control, adding to worksheets
- controls [Office development in Visual Studio], adding to worksheets
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 60f1fe8330e3a40676738c4187273ee60215db6d
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63427433"
---
# <a name="how-to-add-xmlmappedrange-controls-to-worksheets"></a>如何：向工作表添加 XMLMappedRange 控件
  在将 XML 元素映射到 Microsoft Office Excel 中的单元格时，Visual Studio 会自动添加<xref:Microsoft.Office.Tools.Excel.XmlMappedRange>到工作表中的控件。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

> [!NOTE]
> <xref:Microsoft.Office.Tools.Excel.XmlMappedRange>控件上不可用**工具箱**或**数据源**窗口。 此外，不能创建<xref:Microsoft.Office.Tools.Excel.XmlMappedRange>以编程方式控制。

## <a name="to-add-an-xmlmappedrange-control-to-a-worksheet"></a>若要向工作表添加 XMLMappedRange 控件

1. 在 Visual Studio 设计器中打开 Excel 工作簿。

2. 打开你想要将控件添加的工作表。

3. 上**开发人员**选项卡上，单击**源**。

    > [!NOTE]
    > 如果**开发人员**选项卡不在功能区上可见，则必须启用它。 有关详细信息，请参阅[如何：功能区上显示开发人员选项卡](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)。

     **XML 源**此时将显示任务窗格。

4. 在中**XML 源**任务窗格中，单击**XML 映射**。

5. 在中**XML 映射**对话框中，单击**添加**。

     **XML 源**对话框随即出现。

6. 选择从 XML 架构**XML 源**对话框中，单击**打开**。

     该架构添加到**XML 映射**对话框。

7. 在中**XML 映射**对话框中，单击**确定**。

8. 将从一个元素**XML 源**到工作表上的单元的任务窗格。

     <xref:Microsoft.Office.Tools.Excel.XmlMappedRange>被创建并添加到项目。

    > [!NOTE]
    > 如果您将从父元素拖**XML 源**任务窗格中，<xref:Microsoft.Office.Tools.Excel.ListObject>创建控件。

## <a name="see-also"></a>请参阅
- [XmlMappedRange 控件](../vsto/xmlmappedrange-control.md)
- [通过使用扩展的对象自动化 Excel](../vsto/automating-excel-by-using-extended-objects.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [主机项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
- [如何：将架构映射到 Visual Studio 内部的工作表](../vsto/how-to-map-schemas-to-worksheets-inside-visual-studio.md)
