---
title: VSTO 外接程序编程入门
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VST.ProjectItem.Outlook
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application-level add-ins [Office development in Visual Studio], getting started
- add-ins [Office development in Visual Studio], getting started
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 7b709012dafe0db3dcc0959908a1e6b4d9e07e21
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62788762"
---
# <a name="get-started-programming-vsto-add-ins"></a>VSTO 外接程序编程入门
  你可以使用 VSTO 外接程序来实现 Microsoft Office 应用程序自动化、扩展应用程序的功能，以及自定义应用程序的用户界面 (UI)。 可以使用 Visual Studio 创建 VSTO 外接程序如何与其他类型的 Office 解决方案进行比较的有关信息，请参阅[Office 解决方案开发概述&#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)。

 [!INCLUDE[appliesto_allapp](../vsto/includes/appliesto-allapp-md.md)]

## <a name="create-vsto-add-in-projects"></a>创建 VSTO 外接程序项目
 使用中的 VSTO 外接程序项目模板之一创建 VSTO 外接程序项目**新的项目**对话框。 这些模板包括所需程序集引用和项目文件。 Visual Studio 为 Office 中的大多数应用程序提供 VSTO 外接程序项目模板。

 有关如何创建 VSTO 外接程序项目的详细信息，请参阅[如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。 有关项目模板的详细信息，请参阅[Office 项目模板概述](../vsto/office-project-templates-overview.md)。

## <a name="develop-vsto-add-in-projects"></a>开发 VSTO 外接程序项目
 Visual Studio 时创建 VSTO 外接程序项目时，会自动创建*ThisAddIn.vb* (在[!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)]) 或*ThisAddIn.cs* （在 C# 中) 代码文件。 此文件包含`ThisAddIn`类，该类为 VSTO 外接程序中提供了基础。 在加载或卸载 VSTO 外接程序时，可以使用此类的成员运行代码，以访问主机应用程序的对象模型，以及扩展应用程序的功能。 有关详细信息，请参阅[程序 VSTO 外接程序](../vsto/programming-vsto-add-ins.md)。

## <a name="automate-applications-by-using-the-object-models"></a>通过使用对象模型来自动执行应用程序
 Microsoft Office 应用程序的对象模型公开许多类型，可在 VSTO 外接程序中依据这些类型进行编程。 可以使用这些类型来实现应用程序自动化。 例如，可以通过编程方式在 Outlook 中创建和发送电子邮件，也可以在 Word 中打开文档和添加内容。 有关如何访问主机应用程序代码中的对象模型的详细信息，请参阅[程序 VSTO 外接程序](../vsto/programming-vsto-add-ins.md)。

 有关特定 Microsoft Office 应用程序的对象模型的详细信息，请参阅以下主题：

- [Excel 对象模型概述](../vsto/excel-object-model-overview.md)

- [Word 对象模型概述](../vsto/word-object-model-overview.md)

- [Outlook 对象模型概述](../vsto/outlook-object-model-overview.md)

- [InfoPath 解决方案](../vsto/infopath-solutions.md)

- [PowerPoint 解决方案](../vsto/powerpoint-solutions.md)

- [项目解决方案](../vsto/project-solutions.md)

- [Visio 对象模型概述](../vsto/visio-object-model-overview.md)

## <a name="customize-the-user-interface-of-applications"></a>自定义应用程序的用户界面
 有几种方式将 VSTO 外接程序中使用自定义主机应用程序的 UI:

- 对于 Excel 和 Word，可以向文档中添加托管控件。 有关详细信息，请参阅[扩展 Word 文档和 Excel 工作簿中运行时在 VSTO 加载项](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)。

- 如果应用程序支持功能区，则你可以自定义它。 有关详细信息，请参阅[功能区概述](../vsto/ribbon-overview.md)。

- 如果应用程序支持自定义任务窗格，则你可以创建它。 有关详细信息，请参阅[自定义任务窗格](../vsto/custom-task-panes.md)。

- 对于 Outlook，你可以创建自定义窗体区域。 有关详细信息，请参阅[创建 Outlook 窗体区域](../vsto/creating-outlook-form-regions.md)。

- 对于所有 Microsoft Office 应用程序，可以在 VSTO 外接程序中显示 Windows 窗体。

  有关如何自定义 UI 的 Microsoft Office 应用程序的详细信息，请参阅[Office UI 自定义](../vsto/office-ui-customization.md)。

## <a name="next-steps"></a>后续步骤
 若要了解如何创建 VSTO 外接程序，请参阅下面的演练：

- [演练：为 Excel 创建第一个 VSTO 外接程序](../vsto/walkthrough-creating-your-first-vsto-add-in-for-excel.md)

- [演练：在第一个 VSTO 外接程序为 Outlook 创建](../vsto/walkthrough-creating-your-first-vsto-add-in-for-outlook.md)

- [演练：为 PowerPoint 中创建第一个 VSTO 外接程序](../vsto/walkthrough-creating-your-first-vsto-add-in-for-powerpoint.md)

- [演练：创建在第一个 VSTO 外接程序项目](../vsto/walkthrough-creating-your-first-vsto-add-in-for-project.md)

- [演练：为 Word 创建第一个 VSTO 外接程序](../vsto/walkthrough-creating-your-first-vsto-add-in-for-word.md)

  这些演练介绍 Visual Studio 中的 Office开发工具和 VSTO 外接程序的编程模型。

  有关指导你完成某些 Office 项目中的常见任务的主题的列表，请参阅[Office 编程中的常见任务](../vsto/common-tasks-in-office-programming.md)。

## <a name="see-also"></a>请参阅
- [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [开始&#40;Visual Studio 中的 Office 开发&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [在 Office 解决方案中编写代码](../vsto/writing-code-in-office-solutions.md)
- [VSTO 外接程序的体系结构](../vsto/architecture-of-vsto-add-ins.md)
- [VSTO 外接程序](../vsto/programming-vsto-add-ins.md)
