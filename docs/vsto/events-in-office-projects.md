---
title: Office 项目中的事件
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Sheet1_Startup
- ThisDocument_Shutdown
- ThisDocument_Startup
- application-level add-ins [Office development in Visual Studio], events
- event handlers [Office development in Visual Studio]
- ThisWorkbook_Startup
- Sheet2_Startup
- ThisWorkbook_Shutdown
- document-level customizations [Office development in Visual Studio], events
- Sheet2_Shutdown
- Startup event
- Sheet3_Shutdown
- add-ins [Office development in Visual Studio], events
- Shutdown event
- ThisAddIn_Startup
- Sheet3_Startup
- Startup method [Office development in Visual Studio]
- Shutdown method [Office development in Visual Studio]
- Sheet1_Shutdown
- events [Office development in Visual Studio]
- ThisAddIn_Shutdown
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: c8e8aca881ba25df134c675ac504ea0794c4b051
ms.sourcegitcommit: dcbb876a5dd598f2538e62e1eabd4dc98595b53a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72986119"
---
# <a name="events-in-office-projects"></a>Office 项目中的事件
  每个 Office 项目模板都会自动生成若干事件处理程序。 文档级自定义项的事件处理程序与 VSTO 外接程序的事件处理程序略有不同。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="document-level-projects"></a>文档级项目
 Visual Studio 在文档级自定义项中新的或现有的文档或工作表之后提供生成的代码。 此代码引发两个不同的事件： **Startup** 和 **Shutdown**。

### <a name="startup-event"></a>Startup 事件
 在文档正在运行和程序集中的所有初始化代码均已运行之后，将为每个主机项（文档、工作簿或工作表）引发 **Startup** 事件。 它是要在你的代码在其中运行的类的构造函数中运行的最后一步。 有关宿主项的详细信息，请参阅[主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)。

 当创建文档级项目时，Visual Studio 将在生成的代码文件中创建 **Startup** 事件的事件处理程序：

- 对于 Microsoft Office Word 项目，事件处理程序命名为 `ThisDocument_Startup`。

- 对于 Microsoft Office Excel 项目，事件处理程序具有以下名称：

  - `Sheet1_Startup`

  - `Sheet2_Startup`

  - `Sheet3_Startup`

  - `ThisWorkbook_Startup`

### <a name="shutdown-event"></a>Shutdown 事件
 当你的代码加载在其中的应用程序域即将卸载时，将为每个主机项（文档或工作表）引发 **Shutdown** 事件。 这是当其卸载时要在类中调用的最后一项。

 当创建文档级项目时，Visual Studio 将在生成的代码文件中创建 **Shutdown** 事件的事件处理程序：

- 对于 Microsoft Office Word 项目，事件处理程序命名为 `ThisDocument_Shutdown`。

- 对于 Microsoft Office Excel 项目，事件处理程序具有以下名称：

  - `Sheet1_Shutdown`

  - `Sheet2_Shutdown`

  - `Sheet3_Shutdown`

  - `ThisWorkbook_Shutdown`

> [!NOTE]
> 请不要在文档的 **Shutdown** 事件处理程序过程中以编程方式删除控件。 发生 **Shutdown** 事件时，文档的 UI 元素将不再可用。 如果要在应用程序关闭之前删除控件，请将你的代码添加到另一个事件处理程序中，如 **BeforeClose** 或 **BeforeSave**。

### <a name="event-handler-method-declarations"></a>事件处理程序方法声明
 每个事件处理程序方法声明都具有传递给它的相同参数： *sender* 和 *e*。 在 Excel 中， *sender* 参数引用工作表，如 `Sheet1` 或 `Sheet2`；在 Word 中， *sender* 参数引用文档。 *e* 参数引用事件的标准参数，此情况下不使用该事件。

 下面的代码示例演示 Word 的文档级项目中的默认事件处理程序。

 [!code-vb[Trin_VstcoreWordAutomation#121](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#121)]
 [!code-csharp[Trin_VstcoreWordAutomation#121](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#121)]

 下面的代码示例演示 Excel 的文档级项目中的默认事件处理程序。

> [!NOTE]
> 下面的代码示例演示 `Sheet1` 类中的事件处理程序。 其他主机项类中的事件处理程序的名称对应于类名。 例如，在 `Sheet2` 类中， **Startup** 事件处理程序命名为 `Sheet2_Startup`。 在 `ThisWorkbook` 类中， **Startup** 事件处理程序命名为 `ThisWorkbook_Startup`。

 [!code-csharp[Trin_VstcoreExcelAutomation#83](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#83)]
 [!code-vb[Trin_VstcoreExcelAutomation#83](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#83)]

### <a name="order-of-events-in-document-level-excel-projects"></a>文档级 Excel 项目中事件的顺序
 Excel 项目中 **Startup** 事件处理程序的调用顺序如下：

1. `ThisWorkbook_Startup`

2. `Sheet1_Startup`

3. `Sheet2_Startup`

4. `Sheet3_Startup`

5. 按顺序排列的其他工作表。

   工作簿解决方案中 **Shutdown** 事件处理程序的调用顺序如下：

6. `ThisWorkbook_Shutdown`

7. `Sheet1_Shutdown`

8. `Sheet2_Shutdown`

9. `Sheet3_Shutdown`

10. 按顺序排列的其他工作表。

    在编译项目时确定顺序。 如果用户在运行时重新排列工作表，则不会更改下次打开或关闭该工作簿时引发事件的顺序。

## <a name="vsto-add-in-projects"></a>VSTO 外接程序项目
 Visual Studio 在 VSTO 外接程序中提供生成的代码。此代码引发两个不同的事件： <xref:Microsoft.Office.Tools.AddInBase.Startup> 和 <xref:Microsoft.Office.Tools.AddInBase.Shutdown>。

### <a name="startup-event"></a>Startup 事件
 在已加载 VSTO 外接程序并且已运行程序集中的所有初始化代码之后，将引发 <xref:Microsoft.Office.Tools.AddIn.Startup> 事件。 此事件由生成的代码文件中的 `ThisAddIn_Startup` 方法处理。

 `ThisAddIn_Startup` 事件处理程序中的代码是要运行的第一个用户代码，除非你的 VSTO 外接程序替代 <xref:Microsoft.Office.Tools.AddInBase.RequestComAddInAutomationService%2A> 方法。 在这种情况下，将在 `ThisAddIn_Startup` 之后调用 <xref:Microsoft.Office.Tools.AddInBase.RequestComAddInAutomationService%2A>事件处理程序。

 如果代码要求打开文档，请不要在 `ThisAdd-In_Startup` 事件处理程序中添加代码。 相反，请将该代码添加到用户创建或打开文档时 Office 应用程序引发的事件。 有关详细信息，请参阅在[Office 应用程序启动时访问文档](../vsto/programming-vsto-add-ins.md#AccessingDocuments)。

 有关 VSTO 外接程序的启动顺序的详细信息，请参阅[Vsto 外接程序的体系结构](../vsto/architecture-of-vsto-add-ins.md)。

### <a name="shutdown-event"></a>Shutdown 事件
 即将卸载你的代码加载在其中的应用程序域时，将引发 <xref:Microsoft.Office.Tools.AddInBase.Shutdown> 事件。 此事件由生成的代码文件中的 `ThisAddIn_Shutdown` 方法处理。 此事件处理程序是在卸载 VSTO 外接程序时要运行的最后一个用户代码。

#### <a name="shutdown-event-in-outlook-vsto-add-ins"></a>Outlook VSTO 外接程序中的 Shutdown 事件
 仅当用户使用 Outlook 中的 COM 外接程序对话框禁用 VSTO 外接程序时才引发 <xref:Microsoft.Office.Tools.AddInBase.Shutdown> 事件。 在 Outlook 退出时不引发该事件。 如果具有在 Outlook 退出时必须运行的代码，请处理任一以下事件：

- <xref:Microsoft.Office.Interop.Outlook.ApplicationEvents_11_Event.Quit> 对象的 <xref:Microsoft.Office.Interop.Outlook.Application> 事件。

- <xref:Microsoft.Office.Interop.Outlook.ExplorerEvents_10_Event.Close> 对象的 <xref:Microsoft.Office.Interop.Outlook.Explorer> 事件。

> [!NOTE]
> 当 Outlook 通过修改注册表退出时，可以强制它引发 <xref:Microsoft.Office.Tools.AddInBase.Shutdown> 事件。 但是，如果管理员还原了此设置，则当 Outlook 退出时，你添加到 `ThisAddIn_Shutdown` 方法的任何代码均将不再运行。 有关详细信息，请参阅[Outlook 2010 的关闭更改](/previous-versions/office/developer/office-2010/ee720183(v=office.14))。

## <a name="see-also"></a>请参阅
- [开发 Office 解决方案](../vsto/developing-office-solutions.md)
- [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [程序文档级自定义项](../vsto/programming-document-level-customizations.md)
- [程序 VSTO 外接程序](../vsto/programming-vsto-add-ins.md)
- [Office 项目模板概述](../vsto/office-project-templates-overview.md)
