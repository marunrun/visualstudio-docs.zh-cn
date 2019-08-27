---
title: 单个和多选项卡视图 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - single and multi-tab views
ms.assetid: e3611704-349f-4323-b03c-f2b0a445d781
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: def68627223ba082f5ec6a3ef571e314feae33f3
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66332047"
---
# <a name="single-and-multi-tab-views"></a>单选项卡和多选项卡视图
编辑器可以创建不同类型的视图。 例如，代码编辑器窗口，另一个窗体设计器。

 多个选项卡视图是具有多个选项卡的视图。 例如，HTML 编辑器有两个选项卡在底部：**设计**并**源**，每个逻辑视图。 设计视图显示呈现的网页上，而另一个显示包含网页的 HTML。

## <a name="accessing-physical-views"></a>访问物理视图
 物理视图承载文档视图对象，每个元素表示的数据缓冲区，例如代码或窗体中的数据的视图。 相应地，每个文档视图对象已 （通过称为物理查看字符串标识） 的物理视图，并通常单一的逻辑视图。

 但是，在某些情况下，物理视图可以具有两个或多个逻辑视图。 一些示例包括一个编辑器，具有与通过并行视图拆分窗口或具有 GUI/设计视图和代码隐藏的窗体视图窗体设计器。

 若要启用您编辑器来访问所有可用的物理视图，必须创建每种类型的编辑器工厂可以创建的文档视图对象的唯一物理视图字符串。 例如，[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]编辑器工厂可以创建文档的代码窗口和窗体设计器窗口的视图对象。

## <a name="creating-multi-tabbed-views"></a>创建多个选项卡视图
 尽管文档视图对象必须与通过唯一的物理视图字符串的物理视图相关联，您可以将启用不同的方式查看数据的物理视图中的多个选项卡。 在此多个选项卡配置中，所有选项卡与相关联的相同的物理视图字符串，但每个选项卡提供不同的逻辑视图 GUID。

 若要创建多个选项卡视图编辑器，实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsMultiViewDocumentView>接口，然后将关联的不同的逻辑视图 GUID (<xref:Microsoft.VisualStudio.Shell.Interop.LogicalViewID>) 创建与每个选项卡。

 Visual Studio HTML 编辑器是一个多选项卡视图编辑器的一个示例。 它具有**设计**并**源**选项卡。 若要启用此功能，不同的逻辑视图是与每个选项卡上，相关联`LOGICALVIEWID_TextView`有关**设计**选项卡和`LOGICALVIEWID_Code`为**源**选项卡。

 通过指定适当的逻辑视图，VSPackage 可以访问的视图，对应于某种特定用途，如设计窗体、 编辑代码，或调试代码。 但是，windows 之一必须由 NULL 字符串标识，这必须与对应的主逻辑视图 (`LOGVIEWID_Primary`)。

 下表列出了可用的逻辑视图值和其用法。

|LOGVIEWID GUID|建议的使用|
|--------------------|---------------------|
|`LOGVIEWID_Primary`|编辑器工厂的默认/主视图。<br /><br /> 所有编辑器工厂必须都支持此值。 此视图必须使用 NULL 字符串作为其物理视图字符串。 至少一个逻辑视图必须设置为此值。|
|`LOGVIEWID_Debugging`|调试视图。 通常情况下，`LOGVIEWID_Debugging`映射到同一个视图作为`LOGVIEWID_Code`。|
|`LOGVIEWID_Code`|视图由启动**查看代码**命令。|
|`LOGVIEWID_Designer`|视图由启动**查看窗体**命令。|
|`LOGVIEWID_TextView`|文本编辑器视图。 这是返回的视图<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow>，从可以访问<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>。|
|`LOGVIEWID_UserChooseView`|提示用户选择要使用哪个视图。|
|`LOGVIEWID_ProjectSpecificEditor`|通过传递**打开**到对话框<br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.OpenItem%2A><br /><br /> 当用户选择"（项目默认编辑器）"条目。|

 尽管逻辑视图 Guid 是可扩展的可以使用仅在你的 VSPackage 中定义的逻辑视图 Guid。

 关闭时，Visual Studio 将保留编辑器工厂和与文档窗口中，以便它可用于重新打开解决方案时重新打开文档窗口关联的物理视图字符串的 GUID。 关闭解决方案时所打开的 windows 将保留在解决方案 (.suo) 文件。 这些值对应于`VSFPROPID_guidEditorType`并`VSFPROPID_pszPhysicalView`传入的值`propid`中的参数<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A>方法。

## <a name="example"></a>示例
 此代码段说明了如何<xref:Microsoft.VisualStudio.Shell.Interop.LogicalViewID.TextView>对象用于访问视图实现`IVsCodeWindow`。 在这种情况下，<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShellOpenDocument>服务用来调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenDocumentViaProject%2A>和请求`LOGVIEWID_TextView`，用于获取指向窗口框架的指针。 通过调用获取指向文档视图对象的指针<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A>并将值指定为`VSFPROPID_DocView`。 文档视图对象，从`QueryInterface`为调用`IVsCodeWindow`。 预期结果在这种情况下是返回文本编辑器，并在返回文档视图对象。 因此<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A>方法是代码窗口。

```cpp
HRESULT CFindTool::GotoFileLocation(const WCHAR * szFile, long iLine, long iStart, long iLen)
{
  HRESULT hr;
  if (NULL == szFile || !*szFile)
    return E_INVALIDARG;

  if (iLine == -1L)
    return S_FALSE;

  VSITEMID                  itemid;
  VARIANT                   var;
  RECT                      rc;
  IVsUIShellOpenDocument *  pOpenDoc    = NULL;
  IVsCodeWindow *           pCodeWin    = NULL;
  IVsTextView *             pTextView   = NULL;
  IVsUIHierarchy *          pHierarchy  = NULL;
  IVsWindowFrame *          pFrame      = NULL;
  IUnknown *                pUnk        = NULL;
  IVsHighlight *            pHighlight  = NULL;

  IfFailGo(CGlobalServiceProvider::HrQueryService(SID_SVsUIShellOpenDocument, IID_IVsUIShellOpenDocument, (void **)&pOpenDoc));
  IfFailGo(pOpenDoc->OpenDocumentViaProject(szFile, LOGVIEWID_TextView, NULL, &pHierarchy, &itemid, &pFrame));
  pFrame->Show();
  VariantInit(&var);
  IfFailGo(pFrame->GetProperty(VSFPROPID_DocView, &var));
  if (VT_UNKNOWN != var.vt) { hr = E_FAIL; goto Error; }
  pUnk = V_UNKNOWN(&var);
  if (NULL != pUnk)
  {
    IfFailGo(pUnk->QueryInterface(IID_IVsCodeWindow, (void **)&pCodeWin));
    if (SUCCEEDED(hr = pCodeWin->GetLastActiveView(&pTextView)) ||
        SUCCEEDED(hr = pCodeWin->GetPrimaryView(&pTextView)) )
    {
      pTextView->SetSelection(iLine, iStart, iLine, iStart + iLen);
      // uncover selection
      IfFailGo(pTextView->QueryInterface(IID_IVsHighlight, (void**)&pHighlight));
      IfFailGo(SUCCEEDED(pHighlight->GetHighlightRect(&rc)));
      UncoverSelectionRect(&rc);
    }
  }

Error:
  CLEARINTERFACE(pHighlight);
  CLEARINTERFACE(pTextView);
  CLEARINTERFACE(pCodeWin);
  CLEARINTERFACE(pUnk);
  CLEARINTERFACE(pFrame);
  CLEARINTERFACE(pOpenDoc);
  CLEARINTERFACE(pHierarchy);
  RedrawWindow(m_hwndResults, NULL, NULL, RDW_ERASE|RDW_FRAME|RDW_INVALIDATE|RDW_ALLCHILDREN);
  return hr;
}
```

## <a name="see-also"></a>请参阅
- [支持多个文档视图](../extensibility/supporting-multiple-document-views.md)
- [如何：将视图附加到文档数据](../extensibility/how-to-attach-views-to-document-data.md)
- [创建自定义编辑器和设计器](../extensibility/creating-custom-editors-and-designers.md)