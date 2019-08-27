---
title: Excel:文档级自定义项编程入门
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Excel solutions in Visual Studio
- Excel projects [Office development in Visual Studio], getting started
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 2c1ff264eb1a4ca7afdc424cef7edf15bae06554
ms.sourcegitcommit: 25570fb5fb197318a96d45160eaf7def60d49b2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/30/2019
ms.locfileid: "66402162"
---
# <a name="get-started-programming-document-level-customizations-for-excel"></a>用于 Excel 的文档级自定义项编程入门
  如果你刚开始使用 Visual Studio 创建 Microsoft Office Excel 文档级自定义项，下面是您需要了解。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

## <a name="understand-how-document-level-customizations-for-excel-work"></a>了解如何使用文档级自定义项的 Excel 工作
 基于 Excel 的文档级自定义项的是单个工作簿。 若要开始使用自定义项，最终用户打开该工作簿或 Excel 模板从创建该工作簿。 工作簿，例如在单元格中键入或单击按钮和菜单项中的事件可以在程序集中调用事件处理方法。 关闭工作簿后，不再在 Excel 中，仅在包含它们的文档中提供自定义项提供的功能。

 有关详细信息，请参阅[的文档级自定义体系结构](../vsto/architecture-of-document-level-customizations.md)。

## <a name="create-document-level-projects-for-excel"></a>创建 Excel 文档级项目
 若要创建 Excel 文档级自定义，请使用中的 Excel 工作簿或 Excel 模板项目模板**新的项目**对话框。 这些模板包括所需程序集引用和项目文件。

 有关如何创建 Excel 文档级项目的详细信息，请参阅[如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。 有关项目模板的详细信息，请参阅[Office 项目模板概述](../vsto/office-project-templates-overview.md)。

## <a name="program-excel-workbooks-by-using-host-items-and-host-controls"></a>通过使用程序 Excel 工作簿主机项和主机控件
 *主机项*并*承载控件*是提供用于使用 Visual Studio 创建的文档级自定义项编程模型的类。

 宿主项提供的入口点为你的代码，并且它们还可以充当宿主控件和 Windows 窗体控件的容器。 在 excel 文档级项目中，这些主机项由`ThisWorkbook`， `Sheet1`， `Sheet2`，和`Sheet3`类。

 主机控件基于本机 Excel 对象，例如对象列表和范围。 宿主控件提供本机 Excel 对象，与类似的功能，但它们还具有新的事件、 设计器支持和数据绑定功能。 它们显示为在你的项目代码和 IntelliSense，因此可以轻松地引用直接在代码中的特定对象，而无需导航 Excel 对象模型中的第一类对象。

 有关详细信息，请参阅下列主题：

- [文档级自定义项进行编程](../vsto/programming-document-level-customizations.md)

- [通过使用扩展的对象自动化 Excel](../vsto/automating-excel-by-using-extended-objects.md)

- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)

## <a name="customize-the-user-interface-of-excel"></a>自定义 Excel 的用户界面
 大多数 Microsoft Office 解决方案的 Office 应用程序提供用户交互的解决方案某种方式修改用户界面 (UI)。 有许多方法通过使用文档级自定义可以在其中修改 UI Excel。 例如，可以将控件添加到功能区中，或者，可以显示操作窗格。 有关详细信息，请参阅[Office UI 自定义](../vsto/office-ui-customization.md)。

 此外可以打开与你直接在 Visual Studio 中的项目相关联的工作簿。 在 Visual Studio 中打开工作簿时，可以通过使用 Excel 用户界面来修改该工作簿。 此外可以为设计图面上，这样就可以将控件拖到工作表上使用该工作簿。 有关详细信息，请参阅[Visual Studio 环境中的 Office 项目](../vsto/office-projects-in-the-visual-studio-environment.md)。

## <a name="use-data-binding"></a>使用数据绑定
 主机控件的控件，您可以拖动它从列表中也存在**数据源**窗口。 在此方法会自动添加宿主控件将将它们绑定到设置使用在窗口的数据源。 无需编写任何代码，可以显示来自数据库、 web 服务和业务对象数据。 有关详细信息，请参阅[将数据绑定到 Office 解决方案中的控件](../vsto/binding-data-to-controls-in-office-solutions.md)。

## <a name="next-steps"></a>后续步骤
 若要了解如何创建 Excel 文档级自定义，请参阅[演练：创建在第一个文档级自定义 excel](../vsto/walkthrough-creating-your-first-document-level-customization-for-excel.md)。 本演练向您介绍 Visual Studio 和 Excel 文档级自定义项的编程模型中的 Office 开发工具。

 有关指导你完成某些 Excel 项目中的常见任务的主题的列表，请参阅[Office 编程中的常见任务](../vsto/common-tasks-in-office-programming.md)。

## <a name="see-also"></a>请参阅
- [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [文档级自定义项进行编程](../vsto/programming-document-level-customizations.md)
- [Excel 解决方案](../vsto/excel-solutions.md)
- [演练：创建 excel 在第一个文档级自定义项](../vsto/walkthrough-creating-your-first-document-level-customization-for-excel.md)
- [Excel 用法演练](../vsto/walkthroughs-using-excel.md)
- [Excel 对象模型概述](../vsto/excel-object-model-overview.md)
- [在 Office 解决方案中编写代码](../vsto/writing-code-in-office-solutions.md)
