---
title: Word 文档级自定义项编程入门
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Word solutions in Visual Studio
- Word projects [Office development in Visual Studio], getting started
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 2b2872ca6496444cbb3878dc39800a8661400a76
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "62971792"
---
# <a name="get-started-programming-document-level-customizations-for-word"></a>Word 文档级自定义项编程入门
  如果只是开始使用 Visual Studio 创建 Microsoft Office Word 的文档级自定义项，则需要了解以下内容。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

## <a name="understand-how-document-level-customizations-for-word-work"></a>了解 Word 文档级自定义项的工作原理
 你创建的每个 Word 自定义项都基于单个文档。 若要开始使用自定义，最终用户将打开文档或从 Word 模板创建文档。 文档中的事件（例如，将光标移到特定区域或单击按钮和菜单项）可以调用程序集中的事件处理方法。 当文档关闭时，自定义项所提供的功能将不再可用于 Word。

 有关详细信息，请参阅 [文档级自定义项的体系结构](../vsto/architecture-of-document-level-customizations.md)。

## <a name="create-document-level-projects-for-word"></a>为 Word 创建文档级项目
 若要为 Word 创建文档级自定义项，请使用 " **新建项目** " 对话框中的 "word 文档" 或 "word 模板" 项目模板。 这些模板包括所需程序集引用和项目文件。

 有关如何创建 Word 文档级项目的详细信息，请参阅 [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)。 有关项目模板的详细信息，请参阅 [Office 项目模板概述](../vsto/office-project-templates-overview.md)。

## <a name="program-word-documents-by-using-host-items-host-controls"></a>使用宿主项和宿主控件来编写 Word 文档
 *宿主项* 和 *宿主控件* 是为文档级自定义项提供编程模型的类。

 宿主项提供代码的入口点，并且它们还可以充当宿主控件和 Windows 窗体控件的容器。 在 Word 的文档级项目中，宿主项由 `ThisDocument` 类表示。

 宿主控件基于本机 Word 对象，如内容控件、书签和 XML 节点。 宿主控件向本机 Word 对象提供类似的功能，但它们还具有新的事件、设计器支持和数据绑定功能。 它们在你的项目代码和 IntelliSense 中显示为第一类对象，使你可以更轻松地直接在代码中引用特定对象，而无需导航 Word 对象模型。

 有关详细信息，请参阅下列主题：

- [程序文档级自定义项](../vsto/programming-document-level-customizations.md)

- [使用扩展对象实现 Word 自动化](../vsto/automating-word-by-using-extended-objects.md)

- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)

## <a name="customize-the-user-interface-of-word"></a>自定义 Word 的用户界面
 大多数 Microsoft Office 解决方案会修改 Office 应用程序的用户界面 (UI) ，以提供某种方式让用户与解决方案交互。 可以通过多种方式使用文档级自定义项来修改 Word 的 UI。 例如，你可以将控件添加到功能区，并且可以显示操作窗格。 有关详细信息，请参阅 [OFFICE UI 自定义](../vsto/office-ui-customization.md)。

 你还可以直接在 Visual Studio 中打开与你的项目关联的文档。 当文档在 Visual Studio 中打开时，可以使用 Word 用户界面修改文档。 你还可以使用文档作为设计图面，以便将控件拖到它上面。 有关详细信息，请参阅 [Visual Studio 环境中的 Office 项目](../vsto/office-projects-in-the-visual-studio-environment.md)。

## <a name="bind-controls-to-data"></a>将控件绑定到数据
 内容控件和控件位于 <xref:Microsoft.Office.Tools.Word.Bookmark> 可从 " **数据源** " 窗口拖动的控件列表中。 以这种方式添加内容控件和书签会自动将其绑定到通过使用窗口设置的数据源。 在不编写任何代码的情况下，可以显示数据库、服务和业务对象中的数据。 有关详细信息，请参阅 [将数据绑定到 Office 解决方案中的控件](../vsto/binding-data-to-controls-in-office-solutions.md)。

## <a name="next-steps"></a>后续步骤
 若要了解如何创建 Word 的文档级自定义项，请参阅 [演练：创建您的第一个 word 文档级自定义项](../vsto/walkthrough-creating-your-first-document-level-customization-for-word.md)。 本演练介绍了 Visual Studio 中的 Office 开发工具和 Word 文档级自定义项的编程模型。

 有关演练 Word 项目中的一些常见任务的主题列表，请参阅 [Office 编程中的常见任务](../vsto/common-tasks-in-office-programming.md)。

## <a name="see-also"></a>另请参阅
- [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [程序文档级自定义项](../vsto/programming-document-level-customizations.md)
- [Word 解决方案](../vsto/word-solutions.md)
- [演练：创建您的第一个 Word 文档级自定义项](../vsto/walkthrough-creating-your-first-document-level-customization-for-word.md)
- [使用 Word 的演练](../vsto/walkthroughs-using-word.md)
- [Word 对象模型概述](../vsto/word-object-model-overview.md)
- [在 Office 解决方案中编写代码](../vsto/writing-code-in-office-solutions.md)
