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
ms.openlocfilehash: 39cf3e8d59a2ced26f878da979fa87fc663b5bab
ms.sourcegitcommit: e98db44f3a33529b0ba188d24390efd09e548191
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71253581"
---
# <a name="get-started-programming-vsto-add-ins"></a>VSTO 外接程序编程入门
  你可以使用 VSTO 外接程序来实现 Microsoft Office 应用程序自动化、扩展应用程序的功能，以及自定义应用程序的用户界面 (UI)。 有关 VSTO 外接程序如何与可以使用 Visual Studio 创建的其他类型的 Office 解决方案进行比较的信息，请参阅[Office 解决方案开发&#40;概述&#41;VSTO](../vsto/office-solutions-development-overview-vsto.md)。

 [!INCLUDE[appliesto_allapp](../vsto/includes/appliesto-allapp-md.md)]

## <a name="create-vsto-add-in-projects"></a>创建 VSTO 外接程序项目
 使用 "**新建项目**" 对话框中的一个 vsto 外接程序项目模板创建 vsto 外接程序项目。 这些模板包括所需程序集引用和项目文件。 Visual Studio 为 Office 中的大多数应用程序提供 VSTO 外接程序项目模板。

 有关如何创建 VSTO 外接程序项目的详细信息，请参阅[如何：在 Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)中创建 Office 项目。 有关项目模板的详细信息，请参阅[Office 项目模板概述](../vsto/office-project-templates-overview.md)。

## <a name="develop-vsto-add-in-projects"></a>开发 VSTO 外接程序项目
 创建 VSTO 外接程序项目时，Visual Studio 将自动创建*ThisAddIn* （在中[!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)]）或*ThisAddIn.cs* （在中C#为）代码文件。 此文件包含`ThisAddIn`类，该类为 VSTO 外接程序提供基础。 在加载或卸载 VSTO 外接程序时，可以使用此类的成员运行代码，以访问主机应用程序的对象模型，以及扩展应用程序的功能。 有关详细信息，请参阅[PROGRAM VSTO 外接程序](../vsto/programming-vsto-add-ins.md)。

## <a name="automate-applications-by-using-the-object-models"></a>使用对象模型自动执行应用程序
 Microsoft Office 应用程序的对象模型公开许多类型，可在 VSTO 外接程序中依据这些类型进行编程。 可以使用这些类型来实现应用程序自动化。 例如，可以通过编程方式在 Outlook 中创建和发送电子邮件，也可以在 Word 中打开文档和添加内容。 有关如何在代码中访问主机应用程序的对象模型的详细信息，请参阅[PROGRAM VSTO 外](../vsto/programming-vsto-add-ins.md)接程序。

 有关特定 Microsoft Office 应用程序的对象模型的详细信息，请参阅以下主题：

- [Excel 对象模型概述](../vsto/excel-object-model-overview.md)

- [Word 对象模型概述](../vsto/word-object-model-overview.md)

- [Outlook 对象模型概述](../vsto/outlook-object-model-overview.md)

- [InfoPath 解决方案](../vsto/infopath-solutions.md)

- [PowerPoint 解决方案](../vsto/powerpoint-solutions.md)

- [项目解决方案](../vsto/project-solutions.md)

- [Visio 对象模型概述](../vsto/visio-object-model-overview.md)

## <a name="customize-the-user-interface-of-applications"></a>自定义应用程序的用户界面
 使用 VSTO 外接程序可通过多种不同的方式自定义主机应用程序的 UI：

- 对于 Excel 和 Word，可以向文档中添加托管控件。 有关详细信息，请参阅[在运行时在 VSTO 外接程序中扩展 Word 文档和 Excel 工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)。

- 如果应用程序支持功能区，则你可以自定义它。 有关详细信息，请参阅[功能区概述](../vsto/ribbon-overview.md)。

- 如果应用程序支持自定义任务窗格，则你可以创建它。 有关详细信息，请参阅[自定义任务窗格](../vsto/custom-task-panes.md)。

- 对于 Outlook，你可以创建自定义窗体区域。 有关详细信息，请参阅[创建 Outlook 窗体区域](../vsto/creating-outlook-form-regions.md)。

- 对于所有 Microsoft Office 应用程序，可以在 VSTO 外接程序中显示 Windows 窗体。

  有关如何自定义 Microsoft Office 应用程序的 UI 的详细信息，请参阅[OFFICE UI 自定义](../vsto/office-ui-customization.md)。

## <a name="next-steps"></a>后续步骤
 若要了解如何创建 VSTO 外接程序，请参阅下面的演练：

- [演练：创建你的第一个 Excel VSTO 外接程序](../vsto/walkthrough-creating-your-first-vsto-add-in-for-excel.md)

- [演练：创建你的第一个 Outlook VSTO 外接程序](../vsto/walkthrough-creating-your-first-vsto-add-in-for-outlook.md)

- [演练：创建您的第一个 PowerPoint VSTO 外接程序](../vsto/walkthrough-creating-your-first-vsto-add-in-for-powerpoint.md)

- [演练：为项目创建第一个 VSTO 外接程序](../vsto/walkthrough-creating-your-first-vsto-add-in-for-project.md)

- [演练：创建您的第一个 Word VSTO 外接程序](../vsto/walkthrough-creating-your-first-vsto-add-in-for-word.md)

  这些演练介绍 Visual Studio 中的 Office开发工具和 VSTO 外接程序的编程模型。

  有关指导你完成 Office 项目中某些常见任务的主题列表，请参阅[office 编程中的常见任务](../vsto/common-tasks-in-office-programming.md)。

## <a name="see-also"></a>请参阅
- [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [Visual Studio &#40;中的 Office 开发入门&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [在 Office 解决方案中编写代码](../vsto/writing-code-in-office-solutions.md)
- [VSTO 外接程序的体系结构](../vsto/architecture-of-vsto-add-ins.md)
- [程序 VSTO 外接程序](../vsto/programming-vsto-add-ins.md)
