---
title: 单选项卡和多选项卡视图 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - single and multi-tab views
ms.assetid: e3611704-349f-4323-b03c-f2b0a445d781
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c308b4d6c7b90456255019ef57c6b9d544aefc77
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80699979"
---
# <a name="single-and-multi-tab-views"></a>单选项卡和多选项卡视图
编辑器可以创建不同类型的视图。 一个示例是代码编辑器窗口，另一个是窗体设计器。

 多选项卡视图是具有多个选项卡的视图。 例如，HTML 编辑器底部有两个选项卡：**设计和****源**，每个选项卡都是逻辑视图。 设计视图显示呈现的网页，而另一个显示包含网页的 HTML。

## <a name="accessing-physical-views"></a>访问物理视图
 物理视图承载文档视图对象，每个对象表示缓冲区中数据视图，如代码或窗体。 因此，每个文档视图对象都有一个物理视图（由称为物理视图字符串的东西标识），通常只有一个逻辑视图。

 但是，在某些情况下，物理视图可以具有两个或多个逻辑视图。 一些示例是具有并行视图的拆分窗口的编辑器，或者具有 GUI/设计视图和代码后窗体视图的窗体设计器。

 要使编辑器能够访问所有可用的物理视图，必须为编辑器工厂可以创建的每种类型的文档视图对象创建唯一的物理视图字符串。 例如，[!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)]编辑器工厂可以为代码窗口和窗体设计器窗口创建文档视图对象。

## <a name="creating-multi-tabbed-views"></a>创建多选项卡视图
 尽管文档视图对象必须通过唯一的物理视图字符串与物理视图关联，但您可以在物理视图中放置多个选项卡，以便以不同的方式查看数据。 在此多选项卡配置中，所有选项卡都与同一物理视图字符串相关联，但每个选项卡都给定不同的逻辑视图 GUID。

 要为编辑器创建多选项卡视图，请实现接口，<xref:Microsoft.VisualStudio.Shell.Interop.IVsMultiViewDocumentView>然后将不同的逻辑视图 GUID （<xref:Microsoft.VisualStudio.Shell.Interop.LogicalViewID>） 与创建的每个选项卡相关联。

 Visual Studio HTML 编辑器是具有多选项卡视图的编辑器的示例。 它有 **"设计和****源**"选项卡。 为此，不同的逻辑视图与每个选项卡`LOGICALVIEWID_TextView`**、"设计"** 选项卡和`LOGICALVIEWID_Code`**"源"** 选项卡相关联。

 通过指定适当的逻辑视图，VSPackage 可以访问对应于特定用途的视图，例如设计窗体、编辑代码或调试代码。 但是，其中一个窗口必须由 NULL 字符串标识，并且必须对应于主逻辑视图 （）。`LOGVIEWID_Primary`

 下表列出了可用的逻辑视图值及其使用。

|日志 GUID|推荐使用|
|--------------------|---------------------|
|`LOGVIEWID_Primary`|编辑器工厂的默认/主视图。<br /><br /> 所有编辑器工厂都必须支持此值。 此视图必须使用 NULL 字符串作为其物理视图字符串。 必须至少将一个逻辑视图设置为此值。|
|`LOGVIEWID_Debugging`|调试视图。 通常，`LOGVIEWID_Debugging`映射到与 的相同视图`LOGVIEWID_Code`。|
|`LOGVIEWID_Code`|**查看由"查看代码"** 命令启动的视图。|
|`LOGVIEWID_Designer`|**视图由"查看窗体"** 命令启动。|
|`LOGVIEWID_TextView`|文本编辑器视图。 这是返回<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow>的视图，可以从中访问<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView>。|
|`LOGVIEWID_UserChooseView`|提示用户选择要使用的视图。|
|`LOGVIEWID_ProjectSpecificEditor`|通过 **"打开使用"** 对话框传递到<br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.OpenItem%2A><br /><br /> 当用户选择"（项目默认编辑器）"条目时。|

 尽管逻辑视图 GUID 是可扩展的，但只能使用 VSPackage 中定义的逻辑视图 GUID。

 关闭后，Visual Studio 会保留编辑器工厂的 GUID 以及与文档窗口关联的物理视图字符串，以便在重新打开解决方案时使用它重新打开文档窗口。 只有关闭解决方案时打开的窗口才会保留在解决方案 （.suo） 文件中。 这些`VSFPROPID_guidEditorType`值对应于`VSFPROPID_pszPhysicalView``propid`<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A>方法中参数中传递的 和 值。

## <a name="example"></a>示例
 此代码段说明了如何使用<xref:Microsoft.VisualStudio.Shell.Interop.LogicalViewID.TextView>对象访问实现`IVsCodeWindow`的视图。 在这种情况下，<xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShellOpenDocument>服务用于调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenDocumentViaProject%2A>和请求`LOGVIEWID_TextView`，获取指向窗口框的指针。 通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A>和指定 的值`VSFPROPID_DocView`，获得指向文档视图对象的指针。 从文档视图对象中，`QueryInterface`调用 。 `IVsCodeWindow` 在这种情况下，期望返回文本编辑器，因此<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A>在方法中返回的文档视图对象是一个代码窗口。

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
