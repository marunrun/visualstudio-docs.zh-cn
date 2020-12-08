---
title: Excel：文档级自定义项编程入门
description: 了解开始使用 Visual Studio 创建 Microsoft Office Excel 的文档级自定义项时需要了解的知识。
ms.custom: SEO-VS-2020
titleSuffix: ''
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
ms.openlocfilehash: 1fb048fd015126e5438a007be1950cddffbac9e1
ms.sourcegitcommit: ce85cff795df29e2bd773b4346cd718dccda5337
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2020
ms.locfileid: "96846033"
---
# <a name="get-started-programming-document-level-customizations-for-excel"></a>开始编程 Excel 文档级自定义项
  如果只是开始使用 Visual Studio 创建 Microsoft Office Excel 的文档级自定义项，则需要了解以下内容。

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

## <a name="understand-how-document-level-customizations-for-excel-work"></a>了解 Excel 文档级自定义项的工作原理
 Excel 的文档级自定义项基于单个工作簿。 若要开始使用自定义，最终用户将打开工作簿或从 Excel 模板创建工作簿。 工作簿中的事件（例如，在单元格中键入或单击按钮和菜单项）可以调用程序集中的事件处理方法。 关闭工作簿后，自定义项所提供的功能将不再可在 Excel 中使用，只能在包含它们的文档中使用。

 有关详细信息，请参阅 [文档级自定义项的体系结构](../vsto/architecture-of-document-level-customizations.md)。

## <a name="create-document-level-projects-for-excel"></a>为 Excel 创建文档级项目
 若要为 Excel 创建文档级自定义项，请使用 " **新建项目** " 对话框中的 "Excel 工作簿" 或 "excel 模板" 项目模板。 这些模板包括所需程序集引用和项目文件。

 有关如何创建 Excel 文档级项目的详细信息，请参阅 [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。 有关项目模板的详细信息，请参阅 [Office 项目模板概述](../vsto/office-project-templates-overview.md)。

## <a name="program-excel-workbooks-by-using-host-items-and-host-controls"></a>使用宿主项和宿主控件来编写 Excel 工作簿
 *宿主项* 和 *宿主控件* 是为使用 Visual Studio 创建的文档级自定义项提供编程模型的类。

 宿主项提供代码的入口点，并且它们还可以充当宿主控件和 Windows 窗体控件的容器。 在 Excel 文档级项目中，这些主机项由 `ThisWorkbook` 、 `Sheet1` 、 `Sheet2` 和 `Sheet3` 类表示。

 宿主控件基于本机 Excel 对象，如列表对象和范围。 宿主控件向本机 Excel 对象提供类似的功能，但它们还具有新的事件、设计器支持和数据绑定功能。 它们在你的项目代码和 IntelliSense 中显示为第一类对象，这使你可以更轻松地直接在代码中引用特定对象，而无需导航到 Excel 对象模型。

 有关详细信息，请参阅下列主题：

- [程序文档级自定义项](../vsto/programming-document-level-customizations.md)

- [使用扩展对象实现 Excel 自动化](../vsto/automating-excel-by-using-extended-objects.md)

- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)

## <a name="customize-the-user-interface-of-excel"></a>自定义 Excel 的用户界面
 大多数 Microsoft Office 解决方案会修改 Office 应用程序的用户界面 (UI) ，以提供某种方式让用户与解决方案交互。 可以通过多种方式使用文档级自定义项修改 Excel 的 UI。 例如，可以将控件添加到功能区中，也可以显示操作窗格。 有关详细信息，请参阅 [OFFICE UI 自定义](../vsto/office-ui-customization.md)。

 你还可以直接在 Visual Studio 中打开与你的项目关联的工作簿。 在 Visual Studio 中打开工作簿后，可以使用 Excel 用户界面修改工作簿。 您还可以将该工作簿用作设计图面，以便将控件拖到工作表上。 有关详细信息，请参阅 [Visual Studio 环境中的 Office 项目](../vsto/office-projects-in-the-visual-studio-environment.md)。

## <a name="use-data-binding"></a>使用数据绑定
 宿主控件也位于可从 " **数据源** " 窗口拖动的控件列表中。 以这种方式添加主机控件会自动将它们绑定到使用窗口设置的数据源。 在不编写任何代码的情况下，可以显示数据库、web 服务和业务对象中的数据。 有关详细信息，请参阅 [将数据绑定到 Office 解决方案中的控件](../vsto/binding-data-to-controls-in-office-solutions.md)。

## <a name="next-steps"></a>后续步骤
 若要了解如何创建 Excel 文档级自定义项，请参阅 [演练：创建您的第一个 excel 文档级自定义项](../vsto/walkthrough-creating-your-first-document-level-customization-for-excel.md)。 本演练介绍了 Visual Studio 中的 Office 开发工具和 Excel 文档级自定义项的编程模型。

 有关演练 Excel 项目中的一些常见任务的主题列表，请参阅 [Office 编程中的常见任务](../vsto/common-tasks-in-office-programming.md)。

## <a name="see-also"></a>请参阅
- [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [程序文档级自定义项](../vsto/programming-document-level-customizations.md)
- [Excel 解决方案](../vsto/excel-solutions.md)
- [演练：创建您的第一个 Excel 文档级自定义项](../vsto/walkthrough-creating-your-first-document-level-customization-for-excel.md)
- [使用 Excel 的演练](../vsto/walkthroughs-using-excel.md)
- [Excel 对象模型概述](../vsto/excel-object-model-overview.md)
- [在 Office 解决方案中编写代码](../vsto/writing-code-in-office-solutions.md)
