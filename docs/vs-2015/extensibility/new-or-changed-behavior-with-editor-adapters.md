---
title: 新的或更改行为与编辑器适配器 |Microsoft Docs
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
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68194182"
---
# <a name="new-or-changed-behavior-with-editor-adapters"></a>编辑器适配器的新增或更改行为
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

如果要更新已针对早期版本的 Visual Studio 核心编辑器，编写的代码，并且你打算使用的编辑器适配器 （或填充程序） 而不是使用新的 API，你应注意的以下编辑器适配器的行为差异相对于以前的核心编辑器。  
  
## <a name="features"></a>功能  
  
#### <a name="using-setsite"></a>使用 SetSite()  
 必须调用<xref:Microsoft.VisualStudio.OLE.Interop.IObjectWithSite.SetSite%2A>共同创建文本缓冲区，文本视图和代码窗口之前执行任何其他操作在其上的时。 但是，这不是必需的如果您使用<xref:Microsoft.VisualStudio.Editor.IVsEditorAdaptersFactoryService>来创建它们，因为此服务的 create （） 方法自身调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory.SetSite%2A>。  
  
#### <a name="hosting-ivscodewindow-and-ivstextview-in-your-own-content"></a>在您自己的内容中承载 IVsCodeWindow 和 IVsTextView  
 你可托管<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow>和<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>内容使用 Win32 模式或 WPF 模式中。 但是，您应记住有两种模式中的一些差异。  
  
##### <a name="using-win32-and-wpf-versions-of-ivscodewindow"></a>使用 Win32 和 WPF 版本的 IVsCodeWindow  
 编辑器代码窗口派生自<xref:Microsoft.VisualStudio.Shell.WindowPane>，它可实现较旧的 Win32<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>接口以及新的 WPF<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIElementPane>接口。 可以使用<xref:Microsoft.VisualStudio.Shell.WindowPane.Microsoft%23VisualStudio%23Shell%23Interop%23IVsWindowPane%23CreatePaneWindow%2A>方法来创建基于 HWND 的宿主环境中，或<xref:Microsoft.VisualStudio.Shell.WindowPane.Microsoft%23VisualStudio%23Shell%23Interop%23IVsUIElementPane%23CreateUIElementPane%2A>方法来创建 WPF 宿主环境。 基础编辑器始终使用 WPF，但您可以创建适合自己的托管要求，如果要直接在您自己的内容嵌入此窗口窗格的窗口窗格的类。  
  
##### <a name="using-win32-and-wpf-versions-of-ivstextview"></a>使用 Win32 和 WPF 版本的 IVsTextView  
 可以设置<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>为 Win32 模式或 WPF 模式。  
  
 当编辑器工厂创建文本视图中，默认情况下位于 HWND，和<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.GetWindowHandle%2A>返回 HWND。 不应使用此模式下嵌入在 WPF 控件内部的编辑器。  
  
 若要设置为 WPF 模式下文本视图，必须调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.Initialize%2A>，并传入<xref:Microsoft.VisualStudio.TextManager.Interop.TextViewInitFlags3>如初始化之一在标记`InitView`参数。 可以获取<xref:System.Windows.FrameworkElement>通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIElementPane.CreateUIElementPane%2A>。  
  
 WPF 模式与 Win32 模式下通过两种方式不同。 首先，在文本视图可以承载 WPF 上下文中。 可以通过强制转换访问 WPF 窗格<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>到<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIElementPane>并调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIElement.GetUIObject%2A>。 第二个，<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.GetWindowHandle%2A>仍的返回 HWND，但此 HWND 可用于仅检查它的位置并对其设置焦点。 不必须使用此 HWND 响应 WM_PAINT 消息，因为它不会影响编辑器如何绘制窗口。 存在仅为了便于转换到新的编辑器代码适配器通过此 HWND。 强烈建议，不应使用`VIF_NO_HWND_SUPPORT`如果你的组件需要 HWND 工作，由于在从返回 HWND 中限制`GetWindowHandle`在处于此模式。  
  
#### <a name="passing-arrays-as-parameters-in-native-code"></a>将数组作为参数传递在本机代码中  
 有许多旧编辑器 API 的方法具有参数，包括数组和其计数。 示例包括：  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewEx.AppendViewOnlyMarkerTypes%2A>  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewEx.RemoveViewOnlyMarkerTypes%2A>  
  
 如果要在本机代码中调用这些方法，则必须一次传递中只有一个元素。 如果传递多个元素中，调用将被拒绝，由于存在问题的主互操作实现。  
  
 问题是更复杂的方法，如<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewEx.SetIgnoreMarkerTypes%2A>。 每次调用此方法时，它会清除已忽略的标记类型的以前列表，因此不可能只是为了使用三种不同的标记类型调用此方法三次。 唯一的补救措施是只能在托管代码中调用此方法。  
  
#### <a name="threading"></a>线程  
 始终应从 UI 线程调用缓冲区适配器。 缓冲区适配器是一个托管的对象，这意味着它调用从托管代码将绕过 COM 封送处理的调用将不会自动封送到 UI 线程。  如果正在从后台线程调用缓冲区适配器，则必须使用<xref:System.Windows.Threading.Dispatcher.Invoke%2A>或类似方法。  
  
#### <a name="lockbuffer-methods"></a>LockBuffer 方法  
 所有 LockBuffer() 方法已都弃用。 示例包括：  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer.LockBuffer%2A>  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextStream.LockBuffer%2A>  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines.LockBuffer%2A>  
  
#### <a name="commit-events"></a>提交事件  
 提交不支持这些事件。 调用这些事件的建议的方法会导致此方法返回了失败代码。  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsPreliminaryTextChangeCommitEvents>  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsFinalTextChangeCommitEvents>  
  
 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsUndoRedoClusterWithCommitEvents>  
  
#### <a name="texteditorevents"></a>TextEditorEvents  
 <xref:EnvDTE.TextEditorEvents>不再激发 commit （） 上。 而是它们会激发上每个文本更改。  
  
#### <a name="text-markers"></a>文本标记  
 必须调用<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarker.Invalidate%2A>上<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextMarker>对象时删除它们。 在上一版本中，您只需发布标记。  
  
#### <a name="line-numbers"></a>行号  
 上的方法有多种<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>和<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewEx>、 行号对应于基础缓冲区行号、 不行号大纲显示和自动换行，如下所示 Visual Studio 2008 中的身份。  
  
 受影响的方法包括的以下 （列表并不详尽）：  
  
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
 客户端<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession>会看到仅使用已添加这些大纲区域<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession.AddHiddenRegions%2A>或<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSessionEx.AddHiddenRegionsEx%2A>。 它们不会看到临时区域，因为它们未添加通过编辑器适配器。 同样，这些客户端不会看到添加的语言的区域的大纲显示 (包括C#和C++) 使用的新的编辑器代码而不是编辑器适配器。  
  
#### <a name="line-heights"></a>行的高度  
 在新的编辑器中，可以具有不同高度，具体取决于字体大小和可能的行转换可能会移动相对于其他行的行的文本行。 如由方法返回的行高度<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.GetLineHeight%2A>是应用的任何行转换中使用的默认字体大小的行的高度。 此高度可能或可能不会反映在视图中的行的实际高度。  
  
#### <a name="eventing-and-undo"></a>事件记录和撤消  
 在新的编辑器中，视图将继续执行操作，如呈现和连续引发事件，即使撤消群集处于打开状态。 此行为是不同于未执行之前关闭之后撤消群集的这些操作的旧视图。  
  
#### <a name="intellisense"></a>IntelliSense  
  
- <xref:Microsoft.VisualStudio.TextManager.Interop.IVsIntellisenseHost.UpdateTipWindow%2A>方法将失败，如果没有实现的类中传递<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextTipWindow2>或<xref:Microsoft.VisualStudio.TextManager.Interop.IVsMethodTipWindow3>。 不再支持自定义 Win32 所有者描述弹出窗口。  
  
#### <a name="smarttags"></a>SmartTags  
 没有适配器支持的智能标记，创建<xref:Microsoft.VisualStudio.TextManager.Interop.IVsSmartTagData>， <xref:Microsoft.VisualStudio.TextManager.Interop.IVsSmartTagTipWindow>，和<xref:Microsoft.VisualStudio.TextManager.Interop.IVsSmartTagTipWindow2>接口。  
  
#### <a name="dte"></a>DTE  
 <xref:EnvDTE80.IncrementalSearch> 未实现。  
  
## <a name="unimplemented-methods"></a>未实现的方法  
 某些方法尚未实现文本缓冲区适配器、 文本视图适配器和文本层适配器上。  
  
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
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewIntellisenseHost>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextViewIntellisenseHost.SetSubjectFromPrimaryBuffer%2A> 实现，但会将其忽略大纲显示 UI 的适配器。|  
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenRegionEx>|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenRegionEx.GetBannerAttr%2A> 实现，但会将其忽略大纲显示 UI 的适配器。|
