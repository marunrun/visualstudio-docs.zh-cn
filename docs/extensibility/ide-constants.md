---
title: IDE 常量 |Microsoft Docs
ms.date: 03/22/2018
ms.topic: conceptual
helpviewer_keywords:
- IDE, errors
- logical views
- errors [Visual Studio], IDE
- UI context constants
- constants, Visual Studio IDE
- IDE, constants
- physical views
ms.assetid: 5030e70a-241d-474a-ba8c-e3b1cf947ff0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bc2eddac1cc7d7e616deb197752adf41a4d68d15
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80710506"
---
# <a name="ide-constants"></a>IDE 常量

<xref:Microsoft.VisualStudio.VSConstants>类提供特定于集成开发环境 (IDE) 并且以前仅在头文件中定义的常量。

## <a name="logical-and-physical-views"></a>逻辑和物理视图

|值|说明|
|-----------|-----------------|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Code_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>`cmdidOpenWith`处理程序应将此值传递给 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> 方法以获取 "**打开方式**" 对话框，在本例中为可能的代码视图。|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Debugging_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>`cmdidOpenWith`处理程序将此值传递给 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> 方法以获取 "**打开方式**" 对话框，在此示例中，用 <xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Debugging_guid> 映射到与相同视图的可能调试视图填充 <xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Code_guid> 。|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Designer_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>`cmdidOpenWith`处理程序将此值传递给 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> 方法以获取 "**打开方式**" 对话框，在本例中，可以**查看窗体**设计器视图。|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Primary_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>`cmdidOpenWith`处理程序将此值传递给 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> 方法以获取 "**打开方式**" 对话框，在本例中为编辑器工厂的默认/主视图。|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.TextView_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>`cmdidOpenWith`处理程序将此值传递给 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> 方法以获取 "**打开方式**" 对话框，在此对话框中用于文档或数据文本编辑器视图。|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.UserChooseView_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>`cmdidOpenWith`处理程序将此值传递给方法，该 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A> 方法提示用户选择要使用的用户定义的视图。|

## <a name="editor-factory-flags"></a>编辑器工厂标志

|值|说明|
|-----------|-----------------|
|[CEF.CloneFile](<xref:Microsoft.VisualStudio.VSConstants.CEF#Microsoft_VisualStudio_VSConstants_CEF_CloneFile>)|与方法的第一个参数组合在一起的过时标志 <xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A> 。|
|[CEF.OpenAsNew](<xref:Microsoft.VisualStudio.VSConstants.CEF#Microsoft_VisualStudio_VSConstants_CEF_OpenAsNew>)|按位组合为方法的第一个参数 <xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A> ，这表示编辑器工厂应执行必要的修复。|
|[CEF.OpenFile](<xref:Microsoft.VisualStudio.VSConstants.CEF#Microsoft_VisualStudio_VSConstants_CEF_OpenFile>)|按位组合作为方法的第一个参数 <xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A> ，此标志与 [CEF 互斥。CloneFile](<xref:Microsoft.VisualStudio.VSConstants.CEF#Microsoft_VisualStudio_VSConstants_CEF_CloneFile>)。|
|[CEF.自行](<xref:Microsoft.VisualStudio.VSConstants.CEF#Microsoft_VisualStudio_VSConstants_CEF_Silent>)|按位组合为方法的第一个参数 <xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A> ，这表示编辑器工厂应创建编辑器，而不显示用户界面)  (UI。|

## <a name="visual-studio-errors"></a>Visual Studio 错误

|值|说明|
|-----------|-----------------|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_BUSY>|当相关对象已处于繁忙状态时，接口返回的常量|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_INCOMPATIBLEDOCDATA>|特定于 Visual Studio 的错误 HRESULT "文档数据不兼容"。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_PACKAGENOTLOADED>|特定于 Visual Studio 并显示 "未加载包" 的错误 HRESULT。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_PROJECTALREADYEXISTS>|特定于 Visual Studio 的错误 HRESULT，指示 "项目已存在"。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_PROJECTMIGRATIONFAILED>|特定于 Visual Studio 的错误 HRESULT，指示 "项目配置失败"。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_PROJECTNOTLOADED>|特定于 Visual Studio 的错误 HRESULT，指示 "项目未加载"。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_SOLUTIONALREADYOPEN>|特定于 Visual Studio 的错误 HRESULT，指示 "解决方案已打开"。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_SOLUTIONNOTOPEN>|特定于 Visual Studio 的错误 HRESULT，指示 "解决方案未打开"。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_SPECIFYING_OUTPUT_UNSUPPORTED>|由生成接口返回，该接口具有用于从接口指定数组的参数 <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutput> ，但实现只能将方法应用于所有输出。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_UNSUPPORTEDFORMAT>|<xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A>如果文档的格式不能在编辑器中打开，则该方法返回此值。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_WIZARDBACKBUTTONPRESS>|一个 HRESULT 值，该值指示用户在 Visual Studio 向导中按 "后退" 按钮。|

## <a name="visual-studio-constants"></a>Visual Studio 常量

|值|说明|
|-----------|-----------------|
|<xref:Microsoft.VisualStudio.VSConstants.VS_S_PROJECTFORWARDED>|特定于 Visual Studio 的错误 HRESULT，指示 "项目已转发"。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_S_TBXMARKER>|一个特定于 Visual Studio 的常量，用于 "工具箱标记"。|
|<xref:Microsoft.VisualStudio.VSConstants.VSM_ENTERMODAL>|一个特定于 Visual Studio 的常数，用于通过 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBroadcastMessageEvents.OnBroadcastMessage%2A> 指示模态开始的方法广播通知消息。|
|<xref:Microsoft.VisualStudio.VSConstants.VSM_EXITMODAL>|一个特定于 Visual Studio 的常数，用于通过 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBroadcastMessageEvents.OnBroadcastMessage%2A> 指示模态结束的方法广播通知消息。|
|<xref:Microsoft.VisualStudio.VSConstants.VSM_TOOLBARMETRICSCHANGE>|一个特定于 Visual Studio 的常数，用于通过 <xref:Microsoft.VisualStudio.Shell.Interop.IVsBroadcastMessageEvents.OnBroadcastMessage%2A> 指示命令栏度量值已更改的方法广播通知消息。|
|<xref:Microsoft.VisualStudio.VSConstants.VSCOOKIE_NIL>|特定于 Visual Studio 的常数，指示尚未设置 cookie。|
|[VSITEMID.牌](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID#Microsoft_VisualStudio_VSConstants_VSITEMID_Nil>)|表示缺少项目项的 Visual Studio 项标识符。 如果当前没有选定内容，则使用此值。|
|[VSITEMID.Root](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID#Microsoft_VisualStudio_VSConstants_VSITEMID_Root>)|表示项目层次结构的根的 Visual Studio 项标识符，用于标识整个层次结构，而不是单个项。|
|[VSITEMID.选择](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID#Microsoft_VisualStudio_VSConstants_VSITEMID_Selection>)|一个 Visual Studio 项标识符，它表示当前选定的项，这些项可以包括层次结构的根。|

## <a name="ivsselectionevents"></a>IVsSelectionEvents
 描述在调用中刚选择了 IDE 的哪个组件， <xref:Microsoft.VisualStudio.Shell.Interop.IVsSelectionEvents.OnElementValueChanged%2A> 例如。

|返回的常量|Value|
|--------------|-----------|
|[SelectionElement.DocumentFrame](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_DocumentFrame>)|0x2|
|[SelectionElement.PropertyBrowserSID](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_PropertyBrowserSID>)|0x4|
|[SelectionElement. StartupProject](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_StartupProject>)|0x3|
|[SelectionElement. UndoManager](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_UndoManager>)|0x0|
|[SelectionElement. UserContext](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_UserContext>)|0x5|
|[SelectionElement. WindowFrame](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_WindowFrame>)|0x1|

## <a name="vsselelemid"></a>VSSELELEMID
 用于指示新的选择状态的常量。

|返回的常量|Value|
|--------------|-----------|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|2|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|7|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|4|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|6|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|3|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|0|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|5|
|<xref:Microsoft.VisualStudio.VSConstants.VSSELELEMID>|1|

## <a name="component-selector-dialog-constants"></a>组件选择器对话框常量

|返回的常量|Value|
|--------------|-----------|
|<xref:Microsoft.VisualStudio.VSConstants.CPDN_SELCHANGED>|WM_USER + 1280|
|<xref:Microsoft.VisualStudio.VSConstants.CPDN_SELDBLCLICK>|WM_USER + 1281|
|<xref:Microsoft.VisualStudio.VSConstants.CPPM_CLEARSELECTION>|WM_USER + 1290|
|<xref:Microsoft.VisualStudio.VSConstants.CPPM_GETSELECTION>|WM_USER + 1287|
|<xref:Microsoft.VisualStudio.VSConstants.CPPM_INITIALIZELIST>|WM_USER + 1285|
|<xref:Microsoft.VisualStudio.VSConstants.CPPM_INITIALIZETAB>|WM_USER + 1288|
|<xref:Microsoft.VisualStudio.VSConstants.CPPM_QUERYCANSELECT>|WM_USER + 1286|
|<xref:Microsoft.VisualStudio.VSConstants.CPPM_SETMULTISELECT>|WM_USER + 1289|

## <a name="see-also"></a>另请参阅

- [IDE 定义的用于扩展项目系统的命令](../extensibility/internals/ide-defined-commands-for-extending-project-systems.md)
