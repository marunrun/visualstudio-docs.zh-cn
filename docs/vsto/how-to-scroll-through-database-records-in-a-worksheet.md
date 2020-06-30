---
title: 如何：在工作表中滚动查看数据库记录
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- databases [Office development in Visual Studio], scrolling records
- records [Office development in Visual Studio], scrolling
- data [Office development in Visual Studio], scrolling database records
- worksheets [Office development in Visual Studio], scrolling records
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 8127a5f61e292fb777be4854796535bbe01226aa
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545790"
---
# <a name="how-to-scroll-through-database-records-in-a-worksheet"></a>如何：在工作表中滚动查看数据库记录
  下面的过程演示如何使用设计器在 Microsoft Office Excel 工作表中的数据库表中显示单个字段，以及使最终用户能够滚动浏览所有记录的控件。

 仅可在文档级项目中使用设计器。 但是，还可以在运行时以编程方式添加控件并将其绑定到数据。 有关详细信息，请参阅[演练： VSTO 外接程序项目中的简单数据绑定](../vsto/walkthrough-simple-data-binding-in-vsto-add-in-project.md)。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

## <a name="to-scroll-through-database-records-in-a-worksheet"></a>在工作表中滚动查看数据库记录

1. 在 Visual Studio 中打开 Excel 应用程序项目。

2. 打开 "**数据源**" 窗口并从数据库创建数据源。 有关详细信息，请参阅[添加新连接](../data-tools/add-new-connections.md)。

3. 展开包含要显示的数据的表，然后选择特定列。

4. 打开控件列表并选择 " **NamedRange**"。

5. 将 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件拖动到要在其中显示数据的单元。

6. 从 "**工具箱**" 的 " **Windows 窗体**" 选项卡中，将 <xref:System.Windows.Forms.BindingNavigator> 控件添加到工作表中，并设置要使用的控件。 有关详细信息，请参阅[BindingNavigator 控件概述 &#40;Windows 窗体&#41;](/dotnet/framework/winforms/controls/bindingnavigator-control-overview-windows-forms)。

## <a name="see-also"></a>另请参阅
- [将数据绑定到 Office 解决方案中的控件](../vsto/binding-data-to-controls-in-office-solutions.md)
