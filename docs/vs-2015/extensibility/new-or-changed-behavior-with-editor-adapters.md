---
title: 新的或更改了编辑器适配器的行为 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - adapter behavior
ms.assetid: 5555b116-cfdb-4773-ba62-af80fda64abd
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: fc7ddaf7ec67a1e33248d5ce424868849200d3e6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68194182"
---
# <a name="new-or-changed-behavior-with-editor-adapters"></a>编辑器适配器的新增或更改行为
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

如果要更新的代码是针对 Visual Studio 核心编辑器的早期版本编写的，并且计划使用编辑器适配器 (或填充程序) 而不是使用新的 API，则应该注意编辑器适配器的行为与以前的核心编辑器的不同之处。  
  
## <a name="features"></a>功能  
  
#### <a name="using-setsite"></a>使用 SetSite ( # A1  
 在对 <xref:Microsoft.VisualStudio.OLE.Interop.IObjectWithSite.SetSite%2A> 文本缓冲区、文本视图和代码 windows 执行任何其他操作之前，必须调用共同 iopalisserverextension。 但是，如果你使用来创建它们，则不需要这样做 <xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService> ，因为此服务的 create ( # A1 方法本身会调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.SetSite%2A> 。  
  
#### <a name="hosting-ivscodewindow-and-ivstextview-in-your-own-content"></a>将 IVsCodeWindow 和 IVsTextView 托管在你自己的内容中  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 使用 Win32 模式或 WPF 模式，可以在自己的内容中承载和。 但请记住，这两种模式之间存在一些差异。  
  
##### <a name="using-win32-and-wpf-versions-of-ivscodewindow"></a>使用 IVsCodeWindow 的 Win32 和 WPF 版本  
 编辑器代码窗口派生于 <xref:Microsoft.VisualStudio.Shell.WindowPane> ，后者实现了较旧的 Win32 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane> 接口以及新的 WPF <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIElementPane> 接口。 您可以使用 <xref:Microsoft.VisualStudio.Shell.WindowPane.Microsoft%23VisualStudio%23Shell%23Interop%23IVsWindowPane%23CreatePaneWindow%2A> 方法创建基于 HWND 的宿主环境，或使用 <xref:Microsoft.VisualStudio.Shell.WindowPane.Microsoft%23VisualStudio%23Shell%23Interop%23IVsUIElementPane%23CreateUIElementPane%2A> 方法来创建 WPF 宿主环境。 基础编辑器始终使用 WPF，但是，如果您将此窗口窗格直接嵌入到自己的内容中，则可以创建符合托管要求的窗口窗格的类型。  
  
##### <a name="using-win32-and-wpf-versions-of-ivstextview"></a>使用 IVsTextView 的 Win32 和 WPF 版本  
 可以将设置 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 为 Win32 模式或 WPF 模式。  
  
 当编辑器工厂创建文本视图时，默认情况下，该视图承载于 HWND 中，并 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.GetWindowHandle%2A> 返回 hwnd。 不应使用此模式将编辑器嵌入到 WPF 控件中。  
  
 若要将文本视图设置为 WPF 模式，必须调用 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.Initialize%2A> 并传入 <xref:Microsoft.VisualStudio.TextManager.Interop.TextViewInitFlags3> 作为参数中的一个初始化标志 `InitView` 。 可以 <xref:System.Windows.FrameworkElement> 通过调用获取 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIElementPane.CreateUIElementPane%2A> 。  
  
 WPF 模式在两个方面与 Win32 模式不同。 首先，可以在 WPF 上下文中承载文本视图。 您可以通过将强制转换 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 为并调用来访问 WPF 窗格 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIElementPane> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIElement.GetUIObject%2A> 。 其次， <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.GetWindowHandle%2A> 仍返回 hwnd，但此 hwnd 只能用于检查其位置并将焦点设置到它上面。 不能使用此 HWND 来响应 WM_PAINT 消息，因为它不会影响编辑器绘制窗口的方式。 此 HWND 仅用于通过适配器实现到新编辑器代码的转换。 `VIF_NO_HWND_SUPPORT`如果组件要求 hwnd 工作，则强烈建议不要使用，因为 `GetWindowHandle` 在此模式下，中从返回的 hwnd 中的限制。  
  
#### <a name="passing-arrays-as-parameters-in-native-code"></a>在本机代码中将数组作为参数传递  
 旧编辑器 API 中有很多方法，这些方法的参数包含数组及其计数。 示例如下：  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewEx.AppendViewOnlyMarkerTypes%2A>  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewEx.RemoveViewOnlyMarkerTypes%2A>  
  
 如果在本机代码中调用这些方法，则一次只能传入一个元素。 如果传递多个元素，则会由于主互操作实现问题而拒绝调用。  
  
 此问题对等方法更复杂 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewEx.SetIgnoreMarkerTypes%2A> 。 每次调用此方法时，它会清除以前的忽略标记类型列表，因此，不可能只是用三个不同的标记类型调用此方法三次。 唯一的补救方法是仅在托管代码中调用此方法。  
  
#### <a name="threading"></a>线程  
 应始终从 UI 线程调用缓冲区适配器。 缓冲区适配器是托管对象，这意味着从托管代码调用到该对象将绕过 COM 封送处理，并且不会自动将调用封送到 UI 线程。  如果是从后台线程调用缓冲区适配器，则必须使用 <xref:System.Windows.Threading.Dispatcher.Invoke%2A> 或类似的方法。  
  
#### <a name="lockbuffer-methods"></a>LockBuffer 方法  
 所有 LockBuffer ( # A1 方法已弃用。 示例如下：  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer.LockBuffer%2A>  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStream.LockBuffer%2A>  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines.LockBuffer%2A>  
  
#### <a name="commit-events"></a>提交事件  
 不支持提交事件。 调用建议这些事件的方法将导致方法返回失败代码。  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsPreliminaryTextChangeCommitEvents>  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFinalTextChangeCommitEvents>  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsUndoRedoClusterWithCommitEvents>  
  
#### <a name="texteditorevents"></a>TextEditorEvents  
 <xref:EnvDTE.TextEditorEvents>提交 ( # A1 时不再激发。 而是在每次文本更改时激发。  
  
#### <a name="text-markers"></a>文本标记  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarker.Invalidate%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarker> 删除对象时，必须对其调用。 在以前的版本中，只需要发布标记。  
  
#### <a name="line-numbers"></a>行号  
 对于和上的各种方法 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewEx> ，行号对应于基础缓冲区行号，而不是对应于在 Visual Studio 2008 中用于分级显示和自动换行的行号。  
  
 受影响的方法包括以下 (列表并非详尽) ：  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.CenterLines%2A>  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.GetCaretPos%2A>  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.GetLineAndColumn%2A>  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.GetNearestPosition%2A>  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.GetPointOfLineColumn%2A>  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.GetTextStream%2A>  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.GetWordExtent%2A>  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.PositionCaretForEditing%2A>  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.ReplaceTextOnLine%2A>  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.SetCaretPos%2A>  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.SetSelection%2A>  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.SetTopLine%2A>  
  
#### <a name="outlining"></a>大纲显示  
 的客户端 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> 将仅看到使用或添加的那些大纲显示区域 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession.AddHiddenRegions%2A> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSessionEx.AddHiddenRegionsEx%2A> 。 它们不会看到即席区域，因为它们不是通过编辑器适配器添加的。 同样，这些客户端将不会看到按语言添加的大纲区域 (包括使用新编辑器代码的 c # 和 c + +) ，而不是编辑器适配器。  
  
#### <a name="line-heights"></a>行高  
 在新编辑器中，文本线条的高度可能不同，具体取决于可以移动线条相对于其他线条的字号和可能的行转换。 方法返回的行高度 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.GetLineHeight%2A> 是使用默认字体大小的行高度，未应用线条转换。 此高度一定会反映视图中线条的实际高度。  
  
#### <a name="eventing-and-undo"></a>事件和撤消  
 在新编辑器中，视图将继续执行操作（例如，即使在撤消群集处于打开状态时也会持续呈现和引发事件）。 此行为与旧视图的行为不同，后者在关闭撤消群集之前不会执行这些操作。  
  
#### <a name="intellisense"></a>IntelliSense  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.UpdateTipWindow%2A>如果传入的类未实现或，则方法将失败 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextTipWindow2> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow3> 。 不再支持自定义的 Win32 所有者描述的弹出窗口。  
  
#### <a name="smarttags"></a>标记  
 没有适配器支持通过、 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsSmartTagData> 、和接口创建的智能标记 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsSmartTagTipWindow> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsSmartTagTipWindow2> 。  
  
#### <a name="dte"></a>DTE  
 <xref:EnvDTE80.IncrementalSearch> 未实现。  
  
## <a name="unimplemented-methods"></a>未实现的方法  
 某些方法尚未在文本缓冲区适配器、文本视图适配器和文本层适配器上实现。  
  
|接口|未实现|  
|---------------|---------------------|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>|`Reload(false)` 未实现。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator.EnumSpans%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator.SetBufferMappingModes%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBufferCoordinator.SetSpanMappings%2A>|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines.GetMarkerData%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines.ReleaseMarkerData%2A>|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.CanReplaceLines%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.CopyLineText%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.CreateTrackingPoint%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.EnumLayerMarkers%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.GetBaseBuffer%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.GetLengthOfLine%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.GetLineCount%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.GetLineText%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.GetMarkerData%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.LockBufferEx%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.MapLocalSpansToTextOriginatingLayer%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.ReleaseMarkerData%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.ReplaceLines%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.ReplaceLinesEx%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLayer.UnlockBufferEx%2A>|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget.Find%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFindTarget.Replace%2A>|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLayeredTextView>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsLayeredTextView.GetSelectedAtom%2A>|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.GetSelectionDataObject%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.PositionCaretForEditing%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.RestrictViewRange%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.UpdateViewFrameCaption%2A>|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewEx>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewEx.GetSmartTagRect%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewEx.InvokeInsertionUI%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewEx.SetHoverWaitTimer%2A>|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow.SetViewClassID%2A>|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.AfterCompletorCommit%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.BeforeCompletorCommit%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.Exec%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.GetContextLocation%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.GetServiceProvider%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.GetSmartTagRect%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.GetSubjectCaretPos%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.GetSubjectSelection%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.GetSubjectText%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.QueryStatus%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.ReplaceSubjectTextSpan%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.SetSubjectCaretPos%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.SetSubjectSelection%2A><br /><br /> <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.UpdateSmartTagWindow%2A>|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewIntellisenseHost>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewIntellisenseHost.SetSubjectFromPrimaryBuffer%2A> 在适配器中实现，但在大纲 UI 中被忽略。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenRegionEx>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenRegionEx.GetBannerAttr%2A> 在适配器中实现，但在大纲 UI 中被忽略。|
