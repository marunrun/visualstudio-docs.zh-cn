---
title: 如何：在打印时隐藏工作表上的控件
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- printing [Office development in Visual Studio], worksheets
- controls [Office development in Visual Studio], hiding while printing
- printing [Office development in Visual Studio], hiding controls
- worksheets, hiding controls when printing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 336723f60a2cd90dc63db24e981dd06e0388cb9c
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544802"
---
# <a name="how-to-hide-controls-on-worksheets-when-printing"></a>如何：在打印时隐藏工作表上的控件
  打印 Microsoft Office 包含 Windows 窗体控件的 Excel 文档时，这些控件在打印的工作表中可见。 打印工作表时，可以隐藏控件。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

> [!NOTE]
> 如果隐藏显示数据的控件（如），则 <xref:Microsoft.Office.Tools.Excel.Controls.TextBox> 控件中的数据将不会显示在打印的工作表中。

> [!NOTE]
> 以下说明中的某些 Visual Studio 用户界面元素在计算机上出现的名称或位置可能会不同。 这些元素取决于你所使用的 Visual Studio 版本和你所使用的设置。 有关详细信息，请参阅[个性化设置 Visual Studio IDE](../ide/personalizing-the-visual-studio-ide.md)。

## <a name="to-hide-controls-when-a-worksheet-is-printed"></a>打印工作表时隐藏控件

1. 在 Visual Studio 中创建或打开 Excel 项目，并验证**Sheet1**在设计器中是否可见。 有关创建项目的信息，请参阅[如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。

2. 从 "**工具箱**" 的 "**公共控件**" 选项卡中，将 <xref:Microsoft.Office.Tools.Excel.Controls.Button> 控件拖动到上的单元 `Sheet1` 。

3. 在 "**属性**" 窗口中，将 <xref:Microsoft.Office.Tools.Excel.Controls.Button.PrintObject%2A> 属性设置为**False**。

## <a name="see-also"></a>请参阅
- [Office 文档上的控件](../vsto/controls-on-office-documents.md)
- [Office 文档上的 Windows 窗体控件概述](../vsto/windows-forms-controls-on-office-documents-overview.md)
- [如何：向 Office 文档添加 Windows 窗体控件](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)
- [如何：调整工作表单元格中的控件大小](../vsto/how-to-resize-controls-within-worksheet-cells.md)
