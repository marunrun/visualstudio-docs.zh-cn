---
title: IDE 常量 |微软文档
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710506"
---
# <a name="ide-constants"></a>IDE 常量

类<xref:Microsoft.VisualStudio.VSConstants>提供特定于集成开发环境 （IDE） 且以前仅在标头文件中定义的常量。

## <a name="logical-and-physical-views"></a>逻辑视图和物理视图

|值|说明|
|-----------|-----------------|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Code_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>`cmdidOpenWith`处理程序应将此值传递给<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>方法，以获得 **"打开使用"** 对话框，在这种情况下，请处理可能的代码视图。|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Debugging_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>`cmdidOpenWith`处理程序将此值传递给<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>方法，以获得 **"打开使用"** 对话框，在这种情况下，填充了可能<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Debugging_guid>映射到 的相同视图的<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Code_guid>调试视图。|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Designer_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>`cmdidOpenWith`处理程序将此值传递给<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>方法以获取 **"打开使用"** 对话框，在这种情况下，用于**查看窗体**设计器视图。|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.Primary_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>`cmdidOpenWith`处理程序将此值传递给<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>方法以获取 **"打开使用"** 对话框，在这种情况下，编辑器工厂的默认/主视图。|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.TextView_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>`cmdidOpenWith`处理程序将此值传递给<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>方法，以获得文档或数据文本编辑器视图中的 **"打开"** 对话框。|
|<xref:Microsoft.VisualStudio.VSConstants.LOGVIEWID.UserChooseView_guid>|<xref:Microsoft.VisualStudio.VSConstants.GUID_VSStandardCommandSet97>`cmdidOpenWith`处理程序将此值传递给方法，<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenStandardEditor%2A>该方法提示用户选择要使用的用户定义的视图。|

## <a name="editor-factory-flags"></a>编辑器工厂标志

|值|说明|
|-----------|-----------------|
|[Cef。克隆文件](<xref:Microsoft.VisualStudio.VSConstants.CEF#Microsoft_VisualStudio_VSConstants_CEF_CloneFile>)|过时的标志按位方式组合为<xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A>方法的第一个参数。|
|[Cef。开放AsNew](<xref:Microsoft.VisualStudio.VSConstants.CEF#Microsoft_VisualStudio_VSConstants_CEF_OpenAsNew>)|按位方式组合为<xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A>方法的第一个参数，这表明编辑器工厂应执行必要的修复。|
|[Cef。打开文件](<xref:Microsoft.VisualStudio.VSConstants.CEF#Microsoft_VisualStudio_VSConstants_CEF_OpenFile>)|此标志作为<xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A>方法的第一个参数按位组合，是 CEF 的互斥[。克隆文件](<xref:Microsoft.VisualStudio.VSConstants.CEF#Microsoft_VisualStudio_VSConstants_CEF_CloneFile>)。|
|[Cef。沉默](<xref:Microsoft.VisualStudio.VSConstants.CEF#Microsoft_VisualStudio_VSConstants_CEF_Silent>)|按位方式组合为<xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A>方法的第一个参数，这表明编辑器工厂应创建编辑器而不显示用户界面 （UI）。|

## <a name="visual-studio-errors"></a>视觉工作室错误

|值|说明|
|-----------|-----------------|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_BUSY>|当有问题的对象在已经忙时，接口返回到异步行为的常量|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_INCOMPATIBLEDOCDATA>|特定于 Visual Studio 的"不兼容文档数据"的错误 HRESULT。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_PACKAGENOTLOADED>|特定于 Visual Studio 并指示"未加载包"的错误 HRESULT。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_PROJECTALREADYEXISTS>|特定于 Visual Studio 并指示"项目已存在"的错误 HRESULT。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_PROJECTMIGRATIONFAILED>|特定于 Visual Studio 并指示"项目配置失败"的错误 HRESULT。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_PROJECTNOTLOADED>|特定于 Visual Studio 并指示"项目未加载"的错误 HRESULT。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_SOLUTIONALREADYOPEN>|特定于 Visual Studio 并指示"解决方案已打开"的错误 HRESULT。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_SOLUTIONNOTOPEN>|特定于 Visual Studio 并指示"解决方案未打开"的错误 HRESULT。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_SPECIFYING_OUTPUT_UNSUPPORTED>|由具有用于从<xref:Microsoft.VisualStudio.Shell.Interop.IVsOutput>接口指定数组的参数的生成接口返回，但实现只能将该方法应用于所有输出。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_UNSUPPORTEDFORMAT>|如果<xref:Microsoft.VisualStudio.Package.EditorFactory.CreateEditorInstance%2A>文档的格式无法在编辑器中打开，则该方法将返回此值。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_E_WIZARDBACKBUTTONPRESS>|HRESULT 值，指示用户点击可视化工作室向导中的后退按钮。|

## <a name="visual-studio-constants"></a>可视化工作室常数

|值|说明|
|-----------|-----------------|
|<xref:Microsoft.VisualStudio.VSConstants.VS_S_PROJECTFORWARDED>|特定于 Visual Studio 并指示"项目转发"的错误 HRESULT。|
|<xref:Microsoft.VisualStudio.VSConstants.VS_S_TBXMARKER>|特定于"工具箱标记"的可视化工作室的常量。|
|<xref:Microsoft.VisualStudio.VSConstants.VSM_ENTERMODAL>|特定于 Visual Studio 的常量，用于通过指示模式开始<xref:Microsoft.VisualStudio.Shell.Interop.IVsBroadcastMessageEvents.OnBroadcastMessage%2A>的方法广播通知消息。|
|<xref:Microsoft.VisualStudio.VSConstants.VSM_EXITMODAL>|特定于 Visual Studio 的常量，用于通过指示模式结束<xref:Microsoft.VisualStudio.Shell.Interop.IVsBroadcastMessageEvents.OnBroadcastMessage%2A>的方法广播通知消息。|
|<xref:Microsoft.VisualStudio.VSConstants.VSM_TOOLBARMETRICSCHANGE>|特定于 Visual Studio 的常量，用于通过指示命令栏<xref:Microsoft.VisualStudio.Shell.Interop.IVsBroadcastMessageEvents.OnBroadcastMessage%2A>指标已更改的方法广播通知消息。|
|<xref:Microsoft.VisualStudio.VSConstants.VSCOOKIE_NIL>|特定于 Visual Studio 的常量，指示尚未设置 Cookie。|
|[VSITEMID。零](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID#Microsoft_VisualStudio_VSConstants_VSITEMID_Nil>)|表示缺少项目项的可视化工作室项标识符。 当没有当前选择时，将使用此值。|
|[VSITEMID。根](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID#Microsoft_VisualStudio_VSConstants_VSITEMID_Root>)|表示项目层次结构的根目录的 Visual Studio 项标识符，用于标识整个层次结构，而不是单个项。|
|[VSITEMID。选择](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID#Microsoft_VisualStudio_VSConstants_VSITEMID_Selection>)|表示当前选定的项或项的 Visual Studio 项标识符，可以包括层次结构的根目录。|

## <a name="ivsselectionevents"></a>IV 选择事件
 例如，在<xref:Microsoft.VisualStudio.Shell.Interop.IVsSelectionEvents.OnElementValueChanged%2A>调用中描述刚刚选择的 IDE 的哪些组件。

|返回的常量|值|
|--------------|-----------|
|[选择元素.文档框架](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_DocumentFrame>)|0x2|
|[选择元素.属性浏览器SID](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_PropertyBrowserSID>)|0x4|
|[选择元素.启动项目](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_StartupProject>)|0x3|
|[选择元素.撤消管理器](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_UndoManager>)|0x0|
|[选择元素.用户上下文](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_UserContext>)|0 x 5|
|[选择元素.窗口框架](<xref:Microsoft.VisualStudio.VSConstants.SelectionElement#Microsoft_VisualStudio_VSConstants_SelectionElement_WindowFrame>)|0x1|

## <a name="vsselelemid"></a>VSSELELEMID
 用于指示新选择状态的常量。

|返回的常量|值|
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

|返回的常量|值|
|--------------|-----------|
|<xref:Microsoft.VisualStudio.VSConstants.CPDN_SELCHANGED>|WM_USER = 1280|
|<xref:Microsoft.VisualStudio.VSConstants.CPDN_SELDBLCLICK>|WM_USER = 1281|
|<xref:Microsoft.VisualStudio.VSConstants.CPPM_CLEARSELECTION>|WM_USER = 1290|
|<xref:Microsoft.VisualStudio.VSConstants.CPPM_GETSELECTION>|WM_USER = 1287|
|<xref:Microsoft.VisualStudio.VSConstants.CPPM_INITIALIZELIST>|WM_USER = 1285|
|<xref:Microsoft.VisualStudio.VSConstants.CPPM_INITIALIZETAB>|WM_USER = 1288|
|<xref:Microsoft.VisualStudio.VSConstants.CPPM_QUERYCANSELECT>|WM_USER = 1286|
|<xref:Microsoft.VisualStudio.VSConstants.CPPM_SETMULTISELECT>|WM_USER = 1289|

## <a name="see-also"></a>请参阅

- [用于扩展项目系统的 IDE 定义命令](../extensibility/internals/ide-defined-commands-for-extending-project-systems.md)
