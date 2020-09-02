---
title: 单个和多个选项卡视图 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80699979"
---
# <a name="single-and-multi-tab-views"></a>单选项卡和多选项卡视图
编辑器可以创建不同类型的视图。 一个示例是代码编辑器窗口，另一个是窗体设计器。

 多选项卡式视图是具有多个选项卡的视图。 例如，HTML 编辑器在底部有两个选项卡： **设计** 和 **源**，每个选项卡都为逻辑视图。 "设计" 视图显示呈现的网页，而另一个显示包含网页的 HTML。

## <a name="accessing-physical-views"></a>访问物理视图
 物理视图宿主文档视图对象，每个对象表示缓冲区中的数据视图，如代码或窗体。 相应地，每个文档视图对象都有一个物理视图 (由称为物理视图字符串) 的对象标识，通常是一个逻辑视图。

 但在某些情况下，物理视图可以有两个或多个逻辑视图。 例如，有一个具有并排视图的拆分窗口的编辑器，或一个具有 GUI/设计视图和代码隐藏视图的窗体设计器。

 若要使编辑器能够访问所有可用的物理视图，必须为编辑器工厂可以创建的每种类型的文档视图对象创建唯一的物理视图字符串。 例如， [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] 编辑器工厂可以为代码窗口和窗体设计器窗口创建文档视图对象。

## <a name="creating-multi-tabbed-views"></a>创建多选项卡式视图
 尽管文档视图对象必须通过唯一的物理视图字符串与物理视图关联，但您可以将多个选项卡置于物理视图中，以不同的方式查看数据。 在此多选项卡式配置中，所有选项卡都与相同的物理视图字符串关联，但每个选项卡都有不同的逻辑视图 GUID。

 若要为编辑器创建多选项卡式视图，请实现 <xref:Microsoft.VisualStudio.Shell.Interop.IVsMultiViewDocumentView> 接口，然后将不同的逻辑视图 GUID (<xref:Microsoft.VisualStudio.Shell.Interop.LogicalViewID>) 与创建的每个选项卡关联。

 Visual Studio HTML 编辑器是包含多选项卡视图的编辑器的示例。 它具有 **设计** 和 **源** 选项卡。 若要启用此选项，不同的逻辑视图与每个选项卡、 `LOGICALVIEWID_TextView` " **设计** " 选项卡和 `LOGICALVIEWID_Code` " **源** " 选项卡相关联。

 通过指定适当的逻辑视图，VSPackage 可以访问与特定用途（如设计窗体、编辑代码或调试代码）对应的视图。 但是，必须使用 NULL 字符串标识其中一个窗口，这必须与主逻辑视图 `LOGVIEWID_Primary`)  (。

 下表列出了可用的逻辑视图值及其用法。

|LOGVIEWID GUID|建议使用|
|--------------------|---------------------|
|`LOGVIEWID_Primary`|编辑器工厂的默认/主视图。<br /><br /> 所有编辑器工厂必须支持此值。 此视图必须使用 NULL 字符串作为其物理视图字符串。 至少必须将一个逻辑视图设置为此值。|
|`LOGVIEWID_Debugging`|调试视图。 通常， `LOGVIEWID_Debugging` 映射到与相同的视图 `LOGVIEWID_Code` 。|
|`LOGVIEWID_Code`|视图 **代码** 命令启动的视图。|
|`LOGVIEWID_Designer`|视图 **窗体** 命令启动的视图。|
|`LOGVIEWID_TextView`|文本编辑器视图。 这是返回的视图 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow> ，可从中进行访问 <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> 。|
|`LOGVIEWID_UserChooseView`|提示用户选择要使用的视图。|
|`LOGVIEWID_ProjectSpecificEditor`|通过 " **打开方式** " 对话框传递到<br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject.OpenItem%2A><br /><br /> 当用户选择 " (项目默认编辑器) " 项时。|

 尽管逻辑视图 Guid 是可扩展的，但只能使用在 VSPackage 中定义的逻辑视图 Guid。

 关闭时，Visual Studio 将保留编辑器工厂的 GUID 和与文档窗口关联的物理视图字符串，以便在重新打开解决方案时，可以使用它来重新打开文档窗口。 只有解决方案关闭时打开的窗口将保留在解决方案 ( .suo) 文件中。 这些值对应于 `VSFPROPID_guidEditorType` `VSFPROPID_pszPhysicalView` `propid` 方法中参数中传递的和值 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> 。

## <a name="example"></a>示例
 此代码段演示如何 <xref:Microsoft.VisualStudio.Shell.Interop.LogicalViewID.TextView> 使用对象来访问实现的视图 `IVsCodeWindow` 。 在这种情况下，该 <xref:Microsoft.VisualStudio.Shell.Interop.SVsUIShellOpenDocument> 服务用于调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShellOpenDocument.OpenDocumentViaProject%2A> 和请求 `LOGVIEWID_TextView` ，后者将获取指向窗口框架的指针。 指向文档视图对象的指针通过调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> 并指定的值获得 `VSFPROPID_DocView` 。 从文档视图对象中， `QueryInterface` 为调用 `IVsCodeWindow` 。 在这种情况下的假定是返回文本编辑器，因此在方法中返回的文档视图对象 <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowFrame.GetProperty%2A> 是一个代码窗口。

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

## <a name="see-also"></a>另请参阅
- [支持多个文档视图](../extensibility/supporting-multiple-document-views.md)
- [如何：将视图附加到文档数据](../extensibility/how-to-attach-views-to-document-data.md)
- [创建自定义编辑器和设计器](../extensibility/creating-custom-editors-and-designers.md)
