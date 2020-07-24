---
title: 程序 VSTO 外接程序
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VST.ProjectItem.Addin
- VST.ProjectItem.AddinProject
- thisAddIn
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ICustomTaskPaneConsumer interface
- add-ins [Office development in Visual Studio], programming
- IRibbonExtensibility interface
- UI customizing [Office development in Visual Studio]
- Office applications [Office development in Visual Studio], application-level add-ins
- programming [Office development in Visual Studio], application-level add-ins
- ThisAddIn class
- user interfaces [Office development in Visual Studio], customizing
- writing code for Office solutions
- host items [Office development in Visual Studio], AddIn
- application development [Office development in Visual Studio], application-level add-ins
- add-ins [Office development in Visual Studio], ThisAddIn class
- application-level add-ins [Office development in Visual Studio], ThisAddIn class
- FormRegionStartup interface
- ThisAddIn_Startup
- application-level add-ins [Office development in Visual Studio], programming
- ThisAddIn_Shutdown
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 240995eb744f8107503c108cbcdbbb8522748b79
ms.sourcegitcommit: 8c4dc60b665e7065a5231d6b61380731221d9fc5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2020
ms.locfileid: "87115329"
---
# <a name="program-vsto-add-ins"></a>程序 VSTO 外接程序
  通过创建 VSTO 外接程序扩展 Microsoft Office 应用程序时，可以直接接针对项目中的 `ThisAddIn` 类编写代码。 此类可用于执行下列任务，例如：访问 Microsoft Office 主机应用程序的对象模型、自定义应用程序的用户界面 (UI) 和向其他 Office 解决方公开 VSTO 外接程序中的对象。

 [!INCLUDE[appliesto_allapp](../vsto/includes/appliesto-allapp-md.md)]

 在 VSTO 外接程序项目中编写代码与在 Visual Studio 中编写其他类型项目的代码在某些方面存在不同。 其中许多差异是由 Office 对象模型公开给托管代码的方式引起的。 有关详细信息，请参阅[在 Office 解决方案中编写代码](../vsto/writing-code-in-office-solutions.md)。

 有关可以通过使用 Visual Studio 中的 Office 开发工具创建的 VSTO 外接程序和其他类型的解决方案的常规信息，请参阅[office 解决方案开发概述 &#40;VSTO&#41;](../vsto/office-solutions-development-overview-vsto.md)。

## <a name="use-the-thisaddin-class"></a>使用 ThisAddIn 类
 你可以在 `ThisAddIn` 类中开始编写 VSTO 外接程序代码。 Visual Studio 会自动在 VSTO 外接程序项目中的*ThisAddIn* （在中 [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] ）或*ThisAddIn.cs* （在 c # 中）代码文件中生成此类。 当 Microsoft Office 应用程序加载 VSTO 外接程序时， [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 将为你自动实例化此类。

 `ThisAddIn` 类中有两个默认的事件处理程序。 若要在加载 VSTO 外接程序后运行代码，请将代码添加到 `ThisAddIn_Startup` 事件处理程序。 若要在卸载 VSTO 外接程序前运行代码，请将代码添加到 `ThisAddIn_Shutdown` 事件处理程序。 有关这些事件处理程序的详细信息，请参阅[Office 项目中的事件](../vsto/events-in-office-projects.md)。

> [!NOTE]
> 在 Outlook 中，卸载 VSTO 外接程序时默认情况下不会始终调用 `ThisAddIn_Shutdown` 事件处理程序。 有关详细信息，请参阅[Office 项目中的事件](../vsto/events-in-office-projects.md)。

### <a name="access-the-object-model-of-the-host-application"></a>访问主机应用程序的对象模型
 若要访问主机应用程序的对象模型，请使用 `Application` 类的 `ThisAddIn` 字段。 此字段会返回一个表示主机程序当前实例的对象。 下表列出了每个 VSTO 外接程序项目中 `Application` 字段的返回值类型。

|主机应用程序|返回值类型|
|----------------------|-----------------------|
|Microsoft Office Excel|<xref:Microsoft.Office.Interop.Excel.Application>|
|Microsoft Office InfoPath|<xref:Microsoft.Office.Interop.InfoPath.Application>|
|Microsoft Office Outlook|<xref:Microsoft.Office.Interop.Outlook.Application>|
|Microsoft Office PowerPoint|[应用程序](/previous-versions/office/developer/office-2010/ff764034(v=office.14))|
|Microsoft Office Project|Microsoft.Office.Interop.MSProject.Application|
|Microsoft Office Visio|Microsoft.Office.Interop.Visio.Application|
|Microsoft Office Word|<xref:Microsoft.Office.Interop.Word.Application>|

 下面的代码示例演示如何使用 `Application` 字段在 Microsoft Office Excel 的 VSTO 外接程序中创建新的工作簿。 此示例应从 `ThisAddIn` 类运行。

```vb
Dim newWorkbook As Excel.Workbook = Me.Application.Workbooks.Add()
```

```csharp
Excel.Workbook newWorkbook = this.Application.Workbooks.Add(System.Type.Missing);
```

 若要从 `ThisAddIn` 类的外部执行相同操作，请使用 `Globals` 对象访问 `ThisAddIn` 类。 有关对象的详细信息 `Globals` ，请参阅[对 Office 项目中对象的全局访问](../vsto/global-access-to-objects-in-office-projects.md)。

```vb
Dim newWorkbook As Excel.Workbook = Globals.ThisAddIn.Application.Workbooks.Add()
```

```csharp
Excel.Workbook newWorkbook = Globals.ThisAddIn.Application.Workbooks.Add(System.Type.Missing);
```

 有关特定 Microsoft Office 应用程序的对象模型的详细信息，请参阅以下主题：

- [Excel 对象模型概述](../vsto/excel-object-model-overview.md)

- [Word 对象模型概述](../vsto/word-object-model-overview.md)

- [Outlook 对象模型概述](../vsto/outlook-object-model-overview.md)

- [InfoPath 解决方案](../vsto/infopath-solutions.md)

- [PowerPoint 解决方案](../vsto/powerpoint-solutions.md)

- [项目解决方案](../vsto/project-solutions.md)

- [Visio 对象模型概述](../vsto/visio-object-model-overview.md)

### <a name="access-a-document-when-the-office-application-starts"></a><a name="AccessingDocuments"></a>在 Office 应用程序启动时访问文档
 并非所有 [!INCLUDE[office14_long](../vsto/includes/office14-long-md.md)] 应用程序都会在启动时自动打开文档，任何 [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] 应用程序在启动时都不会打开文档。 因此， `ThisAdd-In_Startup` 如果代码要求打开文档，请不要在事件处理程序中添加代码。 相反，请将该代码添加到用户创建或打开文档时 Office 应用程序引发的事件。 这样，可以保证在代码执行对文档的操作前，该文档已打开。

 仅当在用户创建一个文档或打开现有文档时，以下代码示例才会使用 Word 中的文档。

 [!code-csharp[Trin_WordAddIn_Menus#3](../vsto/codesnippet/CSharp/trin_wordaddin_menus.cs/thisaddin.cs#3)]
 [!code-vb[Trin_WordAddIn_Menus#3](../vsto/codesnippet/VisualBasic/trin_wordaddin_menus.vb/thisaddin.vb#3)]

### <a name="thisaddin-members-to-use-for-other-tasks"></a>用于其他任务的 ThisAddIn 成员
 下表描述了其他常见任务，并显示了你可以用以执行这些任务的 `ThisAddIn` 类的成员类型。

|任务|供使用的成员|
|----------|-------------------|
|运行代码以在加载 VSTO 外接程序时初始化 VSTO 外接程序。|将代码添加到 `ThisAddIn_Startup` 方法。 这是 <xref:Microsoft.Office.Tools.AddInBase.Startup> 事件的默认事件处理程序。 有关详细信息，请参阅[Office 项目中的事件](../vsto/events-in-office-projects.md)。|
|运行代码以清理 VSTO 外接程序在被卸载前使用的资源。|将代码添加到 `ThisAddIn_Shutdown` 方法。 这是 <xref:Microsoft.Office.Tools.AddInBase.Shutdown> 事件的默认事件处理程序。 有关详细信息，请参阅[Office 项目中的事件](../vsto/events-in-office-projects.md)。 **注意：** 在 Outlook 中，默认情况下， `ThisAddIn_Shutdown` 当卸载 VSTO 外接程序时，不会始终调用事件处理程序。 有关详细信息，请参阅[Office 项目中的事件](../vsto/events-in-office-projects.md)。|
|显示自定义任务窗格。|使用 `CustomTaskPanes` 字段。 有关详细信息，请参阅[自定义任务窗格](../vsto/custom-task-panes.md)。|
|向其他 Microsoft Office 解决方案公开 VSTO 外接程序中的对象。|重写 <xref:Microsoft.Office.Tools.AddInBase.RequestComAddInAutomationService%2A> 方法。 有关详细信息，请参阅[从其他 Office 解决方案调用 VSTO 外接程序中的代码](../vsto/calling-code-in-vsto-add-ins-from-other-office-solutions.md)。|
|通过实现可扩展性接口，在 Microsoft Office 系统中自定义功能。|重写 <xref:Microsoft.Office.Tools.AddInBase.RequestService%2A> 方法以返回实现该接口的类的实例。 有关详细信息，请参阅[使用扩展性接口自定义 UI 功能](../vsto/customizing-ui-features-by-using-extensibility-interfaces.md)。 **注意：** 若要自定义功能区 UI，还可以重写 <xref:Microsoft.Office.Tools.AddInBase.CreateRibbonExtensibilityObject%2A> 方法。|

### <a name="understand-the-design-of-the-thisaddin-class"></a>了解 ThisAddIn 类的设计
 在面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]的项目中， <xref:Microsoft.Office.Tools.AddIn> 是一个接口。 `ThisAddIn` 类是从 <xref:Microsoft.Office.Tools.AddInBase> 类派生的。 此基类会将对其成员的所有调用都重定向到 <xref:Microsoft.Office.Tools.AddIn> 中 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)]接口的内部实现。

 在 Outlook 的 VSTO 外接程序项目中，`ThisAddIn` 类派生自面向 .NET Framework 3.5 的项目中的 `Microsoft.Office.Tools.Outlook.OutlookAddIn` 类，以及面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 的项目中的 <xref:Microsoft.Office.Tools.Outlook.OutlookAddInBase>。 这些基类提供了一些附加功能以支持窗体区域。 有关窗体区域的详细信息，请参阅[创建 Outlook 窗体区域](../vsto/creating-outlook-form-regions.md)。

## <a name="customize-the-user-interface-of-microsoft-office-applications"></a>自定义 Microsoft Office 应用程序的用户界面
 通过使用 VSTO 外接程序，你能以编程方式自定义 Microsoft Office 应用程序的 UI。 例如，你可以在 Outlook 中自定义功能区、显示自定义任务窗格或创建自定义窗体区域。 有关详细信息，请参阅[OFFICE UI 自定义](../vsto/office-ui-customization.md)。

 Visual Studio 提供了可用于创建自定义任务窗格、功能区自定义和 Outlook 窗体区域的设计器和类。 这些设计器和类有助于简化自定义这些功能的过程。 有关详细信息，请参阅[自定义任务窗格](../vsto/custom-task-panes.md)、[功能区设计器](../vsto/ribbon-designer.md)和[创建 Outlook 窗体区域](../vsto/creating-outlook-form-regions.md)。

 如果你想要以类和设计器不支持的方式自定义这些功能之一，则还可以通过在 VSTO 外接程序中实现 *扩展性接口* 来自定义这些功能。 有关详细信息，请参阅[使用扩展性接口自定义 UI 功能](../vsto/customizing-ui-features-by-using-extensibility-interfaces.md)。

 此外，你还可以通过生成扩展文档和工作簿的行为的主机项来修改 Word 文档和 Excel 工作簿的 UI。 这样，你便可以将托管控件添加到文档和工作表。 有关详细信息，请参阅[在运行时在 VSTO 外接程序中扩展 Word 文档和 Excel 工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)。

## <a name="call-code-in-vsto-add-ins-from-other-solutions"></a>从其他解决方案调用 VSTO 外接程序中的代码
 你可以向其他解决方案（包括其他 Office 解决方案）公开 VSTO 外接程序中的对象。 如果 VSTO 外接程序提供了你希望使其他解决方案能够使用的服务，这一点非常有用。 例如，如果您有 Microsoft Office Excel 的 VSTO 外接程序从 web 服务中执行财务数据计算，则其他解决方案可以通过在运行时调用 Excel VSTO 外接程序来执行这些计算。

 有关详细信息，请参阅[从其他 Office 解决方案调用 VSTO 外接程序中的代码](../vsto/calling-code-in-vsto-add-ins-from-other-office-solutions.md)。

## <a name="see-also"></a>另请参阅
- [开发 Office 解决方案](../vsto/developing-office-solutions.md)
- [在运行时在 VSTO 外接程序中扩展 Word 文档和 Excel 工作簿](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [从其他 Office 解决方案调用 VSTO 外接程序中的代码](../vsto/calling-code-in-vsto-add-ins-from-other-office-solutions.md)
- [演练：从 VBA 调用 VSTO 外接程序中的代码](../vsto/walkthrough-calling-code-in-a-vsto-add-in-from-vba.md)
- [使用扩展性接口自定义 UI 功能](../vsto/customizing-ui-features-by-using-extensibility-interfaces.md)
- [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [Architecture of VSTO Add-ins](../vsto/architecture-of-vsto-add-ins.md)
- [在 Office 解决方案中编写代码](../vsto/writing-code-in-office-solutions.md)
