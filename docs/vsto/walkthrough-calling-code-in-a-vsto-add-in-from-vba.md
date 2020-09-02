---
title: 演练：从 VBA 调用 VSTO 外接程序中的代码
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- VBA [Office development in Visual Studio], calling code in application-level add-ins
- application-level add-ins [Office development in Visual Studio], calling code from other solutions
- Video How tos, Office development in Visual Studio
- calling add-in code
- add-ins [Office development in Visual Studio], calling code from other solutions
- interoperability [Office development in Visual Studio]
- calling code from VBA
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 6fdbd2cf85086bac0aa7bb56c128a7ad6fe36f94
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72650788"
---
# <a name="walkthrough-call-code-in-a-vsto-add-in-from-vba"></a>演练：从 VBA 调用 VSTO 外接程序中的代码
  本演练演示如何向其他 Microsoft Office 解决方案（包括 Visual Basic for Applications (VBA) 和 COM VSTO 外接程序）公开 VSTO 外接程序中的对象。

 [!INCLUDE[appliesto_allapp](../vsto/includes/appliesto-allapp-md.md)]

 尽管本演练中特别使用了 Excel，但本演练演示的概念适用于 Visual Studio 提供的任何 VSTO 外接程序项目模板。

 本演练演示以下任务：

- 定义可向其他 Office 解决方案公开的类。

- 向其他 Office 解决方案公开类。

- 从 VBA 代码调用类的方法。

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>先决条件
 您需要满足以下条件才能完成本演练：

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Excel

## <a name="create-the-vsto-add-in-project"></a>创建 VSTO 外接程序项目
 第一步是针对 Excel 创建一个 VSTO 外接程序项目。

### <a name="to-create-a-new-project"></a>创建新项目的步骤

1. 使用 Excel VSTO 外接程序项目模板，创建一个名为 **ExcelImportData**的 Excel VSTO 外接程序项目。 有关详细信息，请参阅 [How to: Create Office Projects in Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md)。

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 打开 **ThisAddIn.cs** 或 **ThisAddIn** 代码文件，并将 **ExcelImportData** 项目添加到 **解决方案资源管理器**。

## <a name="define-a-class-that-you-can-expose-to-other-office-solutions"></a>定义可向其他 Office 解决方案公开的类
 本演练的目的是从 VBA 代码中调入 VSTO 外接程序中名为 `ImportData` 的类的 `AddInUtilities` 方法。 此方法将字符串写入活动工作表中的 A1 单元格。

 若要向其他 Office 解决方案公开 `AddInUtilities` 类，必须使该类成为公共类并对 COM 可见。 还必须在类中公开 [IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) 接口。 以下过程中的代码演示了一种可满足这些要求的方式。 有关更多信息，请参见 [Calling Code in VSTO Add-ins from Other Office Solutions](../vsto/calling-code-in-vsto-add-ins-from-other-office-solutions.md)。

### <a name="to-define-a-class-that-you-can-expose-to-other-office-solutions"></a>定义可向其他 Office 解决方案公开的类

1. 在 **“项目”** 菜单上，单击 **“添加类”**。

2. 在 **“添加新项”** 对话框中，将新类的名称更改为 **AddInUtilities**，然后单击 **“添加”**。

     **AddInUtilities.cs** 或 **AddInUtilities.vb** 文件将在代码编辑器中打开。

3. 将以下指令添加到文件顶部。

     [!code-csharp[Trin_AddInInteropWalkthrough#2](../vsto/codesnippet/CSharp/Trin_AddInInteropWalkthrough/AddInUtilities.cs#2)]
     [!code-vb[Trin_AddInInteropWalkthrough#2](../vsto/codesnippet/VisualBasic/Trin_AddInInteropWalkthrough/AddInUtilities.vb#2)]

4. 将 `AddInUtilities` 类替换为以下代码。

     [!code-csharp[Trin_AddInInteropWalkthrough#3](../vsto/codesnippet/CSharp/Trin_AddInInteropWalkthrough/AddInUtilities.cs#3)]
     [!code-vb[Trin_AddInInteropWalkthrough#3](../vsto/codesnippet/VisualBasic/Trin_AddInInteropWalkthrough/AddInUtilities.vb#3)]

     此代码使 `AddInUtilities` 类对于 COM 可见，并向该类中添加 `ImportData` 方法。 为了公开 [IDispatch](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-idispatch) 接口， `AddInUtilities` 类还具有 <xref:System.Runtime.InteropServices.ClassInterfaceAttribute> 特性，并且该类实现对 COM 可见的接口。

## <a name="expose-the-class-to-other-office-solutions"></a>向其他 Office 解决方案公开类
 若要向其他 Office 解决方案公开 `AddInUtilities` 类，请替代 <xref:Microsoft.Office.Tools.AddInBase.RequestComAddInAutomationService%2A> 类中的 `ThisAddIn` 方法。 在替代中，返回 `AddInUtilities` 类的一个实例。

### <a name="to-expose-the-addinutilities-class-to-other-office-solutions"></a>向其他 Office 解决方案公开 AddInUtilities 类

1. 在 **“解决方案资源管理器”** 中，展开 **“Excel”**。

2. 右键单击 **“ThisAddIn.cs”** 或 **“ThisAddIn.vb”**，然后单击 **“查看代码”**。

3. 将以下代码添加到 `ThisAddIn` 类。

     [!code-csharp[Trin_AddInInteropWalkthrough#1](../vsto/codesnippet/CSharp/Trin_AddInInteropWalkthrough/ThisAddIn.cs#1)]
     [!code-vb[Trin_AddInInteropWalkthrough#1](../vsto/codesnippet/VisualBasic/Trin_AddInInteropWalkthrough/ThisAddIn.vb#1)]

4. 在“生成”菜单中，单击“生成解决方案”。

     验证解决方案已生成且未发生错误。

## <a name="test-the-vsto-add-in"></a>测试 VSTO 外接程序
 可以从多种不同类型的 Office 解决方案中调入 `AddInUtilities` 类。 在本演练中，你将在 Excel 工作簿中使用 VBA 代码。 有关其他类型的 Office 解决方案的详细信息，请参阅 [从其他 Office 解决方案调用 VSTO 外接程序中的代码](../vsto/calling-code-in-vsto-add-ins-from-other-office-solutions.md)。

### <a name="to-test-your-vsto-add-in"></a>测试 VSTO 外接程序

1. 按 **F5** 运行项目。

2. 在 Excel 中，将活动工作簿另存为启用宏的 Excel 工作簿 (*.xlsm)。 将它保存在一个方便的位置，例如桌面。

3. 在功能区上，单击 **“开发人员”** 选项卡。

    > [!NOTE]
    > 如果看不到 **“开发人员”** 选项卡，则必须首先显示它。 有关详细信息，请参阅 [如何：在功能区上显示 "开发人员" 选项卡](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)。

4. 在 **“代码”** 组中，单击 **“Visual Basic”**。

     将打开 Visual Basic 编辑器。

5. 在 **“项目”** 窗口中，双击 **“ThisWorkbook”**。

     将打开 `ThisWorkbook` 对象的代码文件。

6. 将下面的 VBA 代码添加到代码文件。 此代码首先获取一个 COMAddIn 对象，该对象表示 **ExcelImportData** VSTO 外接程序。 然后，该代码使用 COMAddIn 对象的对象属性调用 `ImportData` 方法。

    ```vb
    Sub CallVSTOMethod()
        Dim addIn As COMAddIn
        Dim automationObject As Object
        Set addIn = Application.COMAddIns("ExcelImportData")
        Set automationObject = addIn.Object
        automationObject.ImportData
    End Sub
    ```

7. 按 **F5**。

8. 验证是否已将新的 **Imported Data** 表添加到工作簿。 此外，请验证 A1 单元格是否包含字符串 **This is my data**。

9. 退出 Excel。

## <a name="next-steps"></a>后续步骤
 可以从以下主题了解有关 VSTO 外接程序编程的详细信息：

- 使用 `ThisAddIn` 类实现主机应用程序自动化并在 VSTO 外接程序项目中执行其他任务。 有关详细信息，请参阅 [PROGRAM VSTO 外接程序](../vsto/programming-vsto-add-ins.md)。

- 在 VSTO 外接程序中创建自定义任务窗格。 有关详细信息，请参阅 [自定义任务窗格](../vsto/custom-task-panes.md) 和 [如何：向应用程序添加自定义任务窗格](../vsto/how-to-add-a-custom-task-pane-to-an-application.md)。

- 在 VSTO 外接程序中自定义功能区。 有关详细信息，请参阅 [功能区概述](../vsto/ribbon-overview.md) 和 [如何：开始自定义功能区](../vsto/how-to-get-started-customizing-the-ribbon.md)。

## <a name="see-also"></a>另请参阅
- [程序 VSTO 外接程序](../vsto/programming-vsto-add-ins.md)
- [从其他 Office 解决方案调用 VSTO 外接程序中的代码](../vsto/calling-code-in-vsto-add-ins-from-other-office-solutions.md)
- [开发 Office 解决方案](../vsto/developing-office-solutions.md)
- [如何：在 Visual Studio 中创建 Office 项目](../vsto/how-to-create-office-projects-in-visual-studio.md)
- [Architecture of VSTO Add-ins](../vsto/architecture-of-vsto-add-ins.md)
- [使用扩展性接口自定义 UI 功能](../vsto/customizing-ui-features-by-using-extensibility-interfaces.md)
