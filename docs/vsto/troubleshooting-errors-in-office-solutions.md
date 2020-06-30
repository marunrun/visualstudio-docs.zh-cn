---
title: 排查 Office 解决方案中的错误
ms.date: 02/02/2017
ms.topic: troubleshooting
f1_keywords:
- VST.Project.DesignerDisabled
- VST.Designer.CannotActivate
- VST.Project.ExcelBusy
- VST.SelectDocWizard.AlreadyCustomized
- VST.SelectDocWizard.DocPath
- VST.Project.CannotOpen
- VST.Designer.ErrorsOccurred
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- troubleshooting [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 8d73dadd10342d3616291fb93efbb447bd7ecaee
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85537314"
---
# <a name="troubleshoot-errors-in-office-solutions"></a>排查 Office 解决方案中的错误
  在 Visual Studio 中开发 Office 解决方案时，如果执行下面的任务，可能会遇到问题：

- [创建、升级和打开项目](#creating)

- [使用设计器](#designers)

- [编写代码](#code)

- [生成项目](#building)

- [调试项目](#debugging)

## <a name="create-upgrade-and-open-projects"></a><a name="creating"></a>创建、升级和打开项目
 创建或打开 Office 项目时，可能会遇到以下错误。

### <a name="the-project-cannot-be-created"></a>无法创建该项目
 尝试创建或打开 Office 项目时出现错误，而 Visual Studio 没有足够的信息确定导致错误的原因。 请尝试关闭项目，退出 Visual Studio，然后重新启动。

 如果你正在尝试创建文档级项目，则可能已在 Excel 或 Word 中打开与新项目中的文档同名的另一个文档。 请确保 Excel 或 Word 的所有其他实例均已关闭。

### <a name="control-properties-are-lost-when-you-create-a-new-project-based-on-a-document-from-an-existing-project"></a>基于现有项目中的文档创建新项目时，控件属性将丢失
 如果基于现有项目中的文档创建新 Office 项目，则不会将该文档中任何控件的属性复制到新项目中。 必须为任何先前存在的控件手动重置其属性。 或者，可以通过以下方法保留控件属性：创建现有项目的副本（而不是创建新项目）；或者将现有项目加载到新解决方案（在设计器中），然后将控件从现有文档复制并粘贴到新文档中。

### <a name="errors-when-you-create-an-excel-workbook-project-based-on-an-existing-workbook"></a>基于现有工作簿创建 Excel 工作簿项目时出现的错误
 如果基于现有工作簿创建新的 Excel 工作簿项目，可能会看到以下错误的组合。

 来自 Excel：“隐私问题警告: 此文档中包含宏、ActiveX 控件、XML 扩展包信息或 Web 组件。 其中可能包含个人信息，并且这些信息不能通过“文档检查器”删除。”

 来自 Visual Studio：“设计器未能正确加载。”

 如果尝试创建的项目基于其个人信息已使用文档检查器删除的工作簿，则可能会发生这些错误。 若要避免此错误，请在创建项目之前执行以下步骤：

1. 在 Excel 中打开工作簿。

2. 在 Excel 中打开“信任中心”。

3. 在 "**隐私选项**" 选项卡上，清除 "**保存时从文件属性中删除个人信息**" 复选框。

4. 保存工作簿并关闭 Excel。

### <a name="cannot-open-a-project-after-migration"></a>迁移后无法打开项目
 在将 Office 解决方案迁移到 Microsoft Office 2010 之后，无法在仅安装了 2007 Microsoft Office system 的开发计算机中打开项目。 可以会出现下列错误。

 “解决方案中的一个或多个项目未能正确加载。 请参阅输出窗口获取有关的详细信息。”

 “无法创建项目，因为此计算机上未安装与此项目类型关联的应用程序。 必须安装与此项目类型关联的 Microsoft Office 应用程序。”

 若要解决此问题，请编辑 *.vbproj*或 *.csproj*文件。 对于 Word 项目，将 HostPackage="{763FDC83-64E5-4651-AC9B-28C4FEB985A1}" 替换为 HostPackage="{6CE98B71-D55A-4305-87A8-0D6E368D9600}"。 对于 Excel 项目，将 HostPackage="{B284B16A-C42C-4438-BDCD-B72F4AC43CFB}" 替换为 HostPackage="{825100CF-0BA7-47EA-A084-DCF3308DAF74}"。 对于 Outlook 项目，将 HostPackage="{D2B20FF5-A6E5-47E1-90E8-463C6860CB05}" 替换为 HostPackage="{20A848B8-E01F-4801-962E-25DB0FF57389}"。

 或者，确保仅在安装了 Microsoft Office 2010 的开发计算机上打开迁移的项目。

### <a name="errors-in-upgraded-office-2003-document-level-projects-that-contain-windows-forms-controls"></a>升级的 Office 2003 文档级项目中包含 Windows 窗体控件的错误
 如果升级 Microsoft Office 2003 文档级项目，并且该文档包含 Windows 窗体控件，则升级后的项目可能包含编译或运行时错误。 若要避免此问题，请在升级项目之前在开发计算机上安装 Visual Studio 2005 Tools for Office Second Edition Runtime。 可以从 Microsoft 下载中心（网址为： [Microsoft Visual Studio 2005 Tools for Office Second Edition Runtime (VSTO 2005 SE) (x86)](https://www.microsoft.com/download/details.aspx?id=2392)）下载此版本的运行时作为可再发行组件包。

 完成项目升级后，如果它未被任何其他 Office 解决方案使用，你可以将 Visual Studio 2005 Tools for Office Second Edition Runtime 从开发计算机上卸载。

## <a name="use-the-designers"></a><a name="designers"></a>使用设计器
 在文档级项目中使用文档、工作簿或工作表设计器时，可能会遇到以下错误。

### <a name="designer-failed-to-load-correctly"></a>设计器未能正确加载
 在以下情况下，Visual Studio 无法打开设计器：

- Excel 或 Word 已打开且显示模式对话框。 若要打开设计器，请查看 Excel 或 Word 是否有已打开的模式对话框，然后关闭所有打开的模式对话框。 如果没有打开的模式对话框，则可能需要先执行一些其他操作 Excel 或 Word 才可做出响应。

- 当前正在调试项目。 若要打开设计器，请停止或完成调试。

- Excel 启动时，开发计算机上安装的某个 Excel VSTO 外接程序正在显示一个对话框。 若要创建 Excel 文档级项目，则必须首先禁用该 VSTO 外接程序。

### <a name="controls-appear-as-black-rectangles-on-the-document-or-worksheet"></a>控件在文档或工作表中显示为黑色矩形
 如果对文档或工作表中的控件进行分组，则 Visual Studio 不再识别这些控件。 在 "**属性**" 窗口中无法访问已分组的控件，它们在文档或工作表中显示为黑色矩形。 若要还原控件的功能，必须取消对控件进行分组。

### <a name="controls-on-a-word-template-are-not-visible-in-visual-studio"></a>Word 模板上的控件在 Visual Studio 中不可见
 如果在 Visual Studio 设计器中打开 Word 模板，则该模板中未嵌入文本中的控件可能不可见。 这是因为 Visual Studio 在**普通**视图中打开 Word 模板。 若要查看控件，请单击 "**视图**" 菜单，指向**Microsoft Office Word "视图**，然后单击"**打印布局**"。

### <a name="insert-clip-art-command-does-nothing-in-the-visual-studio-designer"></a>在 Visual Studio 设计器中插入剪贴画命令不执行任何操作
 当在 Visual Studio 设计器中打开 Excel 或 Word 时，单击功能区中的 "**图例**" 选项卡上的 "**剪贴画**" 按钮不会打开 "**剪贴画**" 任务窗格。 若要添加 "剪贴画"，必须在 Visual Studio 外部打开主项目文件夹（不是*\bin*文件夹中的副本）的工作簿或文档的副本，添加剪贴画，然后保存该工作簿或文档。

## <a name="write-code"></a><a name="code"></a>编写代码
 在 Office 项目中编写代码时，可能会遇到以下错误。

### <a name="some-events-of-office-objects-are-not-accessible-when-using-c"></a>使用 C 时，无法访问 Office 对象的某些事件\#
 在某些情况下，当你尝试在 Visual C# 项目中访问 Office 主互操作程序集 (PIA) 类型的实例的特定事件时，可能会看到类似于以下形式的编译器错误。

 “‘Microsoft.Office.Interop.Excel._Application.NewWorkbook’与‘Microsoft.Office.Interop.Excel.AppEvents_Event.NewWorkbook’之间存在二义性”

 此错误意味着你正尝试访问的事件与对象的其他属性或方法同名。 若要访问该事件，必须将该对象强制转换为其*事件接口*。

 具有事件的 Office PIA 类型实现两种接口：核心接口和事件接口；前者包含所有属性和方法，后者则包含由对象公开的事件。 这些事件接口使用命名约定*objectname*事件*n*_Event，例如 <xref:Microsoft.Office.Interop.Excel.AppEvents_Event> 和 <xref:Microsoft.Office.Interop.Word.ApplicationEvents2_Event> 。 如果无法访问应在某一对象中找到的事件，请将该对象强制转换为其事件接口。

 例如，<xref:Microsoft.Office.Interop.Excel.Application> 对象具有一个<xref:Microsoft.Office.Interop.Excel.AppEvents_Event.NewWorkbook> 事件和一个 <xref:Microsoft.Office.Interop.Excel._Application.NewWorkbook%2A> 属性。 若要处理 <xref:Microsoft.Office.Interop.Excel.AppEvents_Event.NewWorkbook> 事件，请将 <xref:Microsoft.Office.Interop.Excel.Application> 强制转换为 <xref:Microsoft.Office.Interop.Excel.AppEvents_Event> 接口。 下面的代码示例演示了如何在 Excel 的文档级项目中进行此操作。

 [!code-csharp[Trin_VstcoreTroubleshootingExcel#1](../vsto/codesnippet/CSharp/Trin_VstcoreTroubleshootingExcelCS/ThisWorkbook.cs#1)]

 有关 Office Pia 中的事件接口的详细信息，请参阅[office 主互操作程序集中的类和接口概述](/previous-versions/office/office-12//ms247299(v=office.12))。

### <a name="cannot-reference-office-pia-classes-in-projects-that-target-the-net_v40_short-or-the-net_v45"></a>无法引用面向或的项目中的 Office PIA 类 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)][!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)]
 在面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或 [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] 的项目中，默认情况下 Office PIA 中定义的类的代码不进行编译。 Pia 中的类使用命名约定*objectname*类，如 <xref:Microsoft.Office.Interop.Word.DocumentClass> 和 <xref:Microsoft.Office.Interop.Excel.WorkbookClass> 。 例如，Word VSTO 外接程序项目中的以下代码将不进行编译。

```vb
Dim document As Word.DocumentClass = Globals.ThisAddIn.Application.ActiveDocument
```

```csharp
Word.DocumentClass document = (Word.DocumentClass) Globals.ThisAddIn.Application.ActiveDocument;
```

 此代码将导致以下编译错误：

- Visual Basic：当使用无 PIA 模式链接的程序集时，不允许对类 "DocumentClass" 的引用。

- Visual c #：无法嵌入 "互操作类型" Microsoft.Office.Interop.Word.DocumentClass "。 请改用适用的接口。”

  若要解决此错误，请修改代码以改为引用相应的接口。 例如，应引用 <xref:Microsoft.Office.Interop.Word.Document> 接口的实例，而不是引用 <xref:Microsoft.Office.Interop.Word.DocumentClass> 对象。

```vb
Dim document As Word.Document = Globals.ThisAddIn.Application.ActiveDocument
```

```csharp
Word.Document document = Globals.ThisAddIn.Application.ActiveDocument;
```

 默认情况下，面向 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] 或 [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] 的项目会自动嵌入 Office PIA 中的所有互操作类型。 发生此编译错误的原因是嵌入互操作类型功能仅适用于接口，而不适用于类。 有关 Office Pia 中的接口和类的详细信息，请参阅[office 主互操作程序集中的类和接口概述](/previous-versions/office/office-12/ms247299(v=office.12))。 有关 Office 项目中嵌入的互操作类型功能的详细信息，请参阅[设计和创建 office 解决方案](../vsto/designing-and-creating-office-solutions.md)。

### <a name="references-to-office-classes-are-not-recognized"></a>无法识别对 Office 类的引用
 某些类名（例如应用程序）位于多个命名空间中，例如 <xref:Microsoft.Office.Interop.Word> 和 <xref:System.Windows.Forms> 。 出于此原因，项目模板顶部**的 import** / **using**语句包含简写的限定常数，例如：

 [!code-csharp[Trin_VstcoreTroubleshootingWord#2](../vsto/codesnippet/CSharp/Trin_VstcoreTroubleshootingWordCS/ThisDocument.cs#2)]
 [!code-vb[Trin_VstcoreTroubleshootingWord#2](../vsto/codesnippet/VisualBasic/Trin_VstcoreTroubleshootingWordVB/ThisDocument.vb#2)]

 此**Imports** / **使用 import using**语句的情况要求使用 Word 或 Excel 限定符区分对 Office 类的引用，例如：

 [!code-csharp[Trin_VstcoreTroubleshootingWord#3](../vsto/codesnippet/CSharp/Trin_VstcoreTroubleshootingWordCS/ThisDocument.cs#3)]
 [!code-vb[Trin_VstcoreTroubleshootingWord#3](../vsto/codesnippet/VisualBasic/Trin_VstcoreTroubleshootingWordVB/ThisDocument.vb#3)]

 如果使用非限定性声明，将出现错误，例如：

 [!code-csharp[Trin_VstcoreTroubleshootingWord#4](../vsto/codesnippet/CSharp/Trin_VstcoreTroubleshootingWordCS/ThisDocument.cs#4)]
 [!code-vb[Trin_VstcoreTroubleshootingWord#4](../vsto/codesnippet/VisualBasic/Trin_VstcoreTroubleshootingWordVB/ThisDocument.vb#4)]

 即使您已经导入了 Word 或 Excel 命名空间并有权访问其中的所有类，也必须使用 Word 或 Excel 完全限定所有类型，以消除命名空间的歧义。

## <a name="build-projects"></a><a name="building"></a>生成项目
 生成 Office 项目时，可能会遇到以下错误。

### <a name="cannot-build-a-document-level-project-that-is-based-on-a-document-with-restricted-permissions"></a>无法生成基于具有受限权限的文档的文档级项目
 如果文档具有受限权限，则 Visual Studio 无法生成文档级项目。 如果你的项目包含具有受限权限的文档，该项目将不会进行编译，并且你将在 "**错误列表**" 窗口中收到以下消息。

 “未能添加自定义项。”

 如果要包括具有受限权限的文档，请在开发和生成解决方案时使用无限制的文档。 然后，在发布解决方案之后对发布位置中的文档应用受限权限。

### <a name="compiler-errors-occur-after-a-namedrange-control-is-deleted"></a>删除 NamedRange 控件后发生编译器错误
 如果从设计器中的非活动工作表的工作表中删除 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件，则可能不会从项目中移除自动生成的代码，并可能发生编译器错误。 为了确保删除这些代码，应在删除 <xref:Microsoft.Office.Tools.Excel.NamedRange> 控件前总是选中包含该控件的工作表，使其成为活动工作表。 如果在删除该控件时没有删除自动生成的代码，可激活该工作表并进行更改以将该工作表标记为已修改，从而令设计器删除这些代码。 重新生成项目时，将删除这些代码。

## <a name="debug-projects"></a><a name="debugging"></a>调试项目
 调试 Office 项目时，可能会遇到以下错误。

### <a name="prompt-to-uninstall-appears-when-you-publish-and-install-a-solution-on-the-development-computer"></a>当您在开发计算机上发布和安装解决方案时，将显示 "提示进行卸载"
 调试 Office 解决方案时，可能会出现以下错误。

 “由于当前已安装另一个版本的自定义项且无法从该位置升级，无法安装该自定义项。”

 此错误指示以前在开发计算机上发布和安装了 Office 解决方案。 若要避免出现此消息，请在调试解决方案之前从计算机上的已安装程序列表中卸载该解决方案。 或者，可以在开发计算机上创建另一个用户帐户以测试已发布解决方案的安装。

### <a name="document-level-projects-created-at-unc-network-locations-do-not-run-from-visual-studio"></a>在 UNC 网络位置创建的文档级项目不会从 Visual Studio 运行
 如果在 UNC 网络位置为 Excel 或 Word 创建文档级项目，则必须将文档的位置添加到 Excel 或 Word 中的受信任位置列表中。 否则，尝试在 Visual Studio 中运行或调试该项目时，将不会加载自定义项。 有关可信位置的详细信息，请参阅[向文档授予信任](../vsto/granting-trust-to-documents.md)。

### <a name="threads-are-not-stopped-correctly-after-debugging"></a>调试后，线程无法正确停止
 Visual Studio 中的 Office 项目遵循能够使调试器正确关闭程序的线程命名约定。 如果在解决方案中创建线程，则应使用前缀 VSTA_ 为每个线程命名，以确保在停止调试时会正确处理这些线程。 例如，可以设置 `Name` 等待网络事件**VSTA_NetworkListener**的线程的属性。

### <a name="cannot-run-or-debug-any-office-solution-on-the-development-computer"></a>无法在开发计算机上运行或调试任何 Office 解决方案
 如果无法在开发计算机上运行或开发 Office 项目，则可能会出现下面的错误消息。

 “无法加载自定义项，原因是无法创建应用程序域。”

 在加载 Office 解决方案之前，Visual Studio 使用 Fusion（.NET Framework 程序集加载程序）来缓存程序集。 请确保 Visual Studio 可以写入 Fusion 缓存，然后重试。 有关详细信息，请参阅[卷影副本程序集](/dotnet/framework/app-domains/shadow-copy-assemblies)。

### <a name="error-when-stopping-the-debugger-in-a-document-level-project-after-using-edit-and-continue"></a>使用 "编辑并继续" 后在文档级项目中停止调试器时出错
 如果您在项目处于中断模式时使用 "**编辑**并**继续**" 对 Excel 或 Word 的文档级项目中的代码进行更改，则您可能会看到一个对话框，如果您随后停止调试器，会显示以下错误消息。

 “在当前状态下终止进程可能导致意外结果，包括数据丢失和系统不稳定。”

 无论是在对话框中单击 **"是" 还是 "** **否**"，Visual Studio 都将终止 Excel 或 Word 进程并停止调试器。 若要停止调试项目而不显示此对话框，请直接退出 Excel 或 Word，而不是在 Visual Studio 中停止调试器。

## <a name="see-also"></a>另请参阅
- [排查 Office 解决方案问题](../vsto/troubleshooting-office-solutions.md)
- [Office 解决方案安全性疑难解答](../vsto/troubleshooting-office-solution-security.md)
- [Office 解决方案部署疑难解答](../vsto/troubleshooting-office-solution-deployment.md)
