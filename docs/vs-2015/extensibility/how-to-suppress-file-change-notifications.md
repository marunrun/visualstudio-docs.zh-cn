---
title: 如何：禁止显示文件更改通知 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - suppress file change notification
ms.assetid: 891c1eb4-f6d0-4073-8df0-2859dbd417ca
caps.latest.revision: 19
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3f045175eae165b75a887ada2716b19f34fc228b
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68204083"
---
# <a name="how-to-suppress-file-change-notifications"></a>如何：禁止显示文件更改通知
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

表示文本缓冲区的物理文件更改后，对话框将显示与消息**是否要保存对以下各项的更改？** 这称为文件更改通知。 如果很多更改将为到该文件，但是，反复地显示此对话框中可以快速变得令人讨厌。  
  
 以编程方式可以禁止显示此对话框，使用以下过程。 通过执行此操作，您可以重新加载文件立即而无需提示用户每次保存所做的更改。  
  
### <a name="to-suppress-file-change-notification"></a>若要禁止显示文件更改通知  
  
1. 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsRunningDocumentTable.FindAndLockDocument%2A>方法，以确定哪些文本缓冲区对象是与你打开的文件相关联。  
  
2. 直接<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer>对象，它内存中要忽略监视文件更改通过获取<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocDataFileChangeControl>从接口<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer>（文档数据） 对象，然后实现<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocDataFileChangeControl.IgnoreFileChanges%2A>方法替换`fIgnore`参数设置为`true`。  
  
3. 调用对象方法<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextLines>并<xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextBuffer>接口，以便更新在内存<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer>对象 （例如，当将字段添加到你的组件） 的文件更改。  
  
4. 使用更改更新磁盘上的文件而不考虑任何挂起的编辑用户可能正在进行中。  
  
     这样一来，当您直接时<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer>对象就可以继续监视文件更改通知，请在内存中的文本缓冲区中显示的生成，以及所有其他挂起的编辑更改。 磁盘上的文件反映了由你生成的最新代码和任何以前保存在用户编辑代码中的用户所做的更改。  
  
5. 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsDocDataFileChangeControl.IgnoreFileChanges%2A>方法以通知<xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer>对象就可以继续通过设置监视文件更改通知`fIgnore`参数`false`。  
  
6. 如果你打算进行几项更改到文件中，如下所示的源代码管理 (SCC)，这种情况，您必须告诉全局文件更改服务以暂时挂起文件更改通知。  
  
     例如，如果您重写该文件，然后更改时间戳，您必须挂起文件更改通知，如的重写和 timestample 操作每个计为一个单独的文件更改事件。 若要启用全局文件更改通知应改为调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsFileChangeEx.IgnoreFile%2A>方法。  
  
## <a name="example"></a>示例  
 下面演示了如何禁止显示文件更改通知。  
  
```cpp#  
//Misc. helper classes  
  
CSuspendFileChanges::CSuspendFileChanges(  
    /* [in] */ const CString& strMkDocument,   
    /* [in] */ BOOL fSuspendNow /* = TRUE */)   
:  
    m_strMkDocument(strMkDocument),  
    m_fFileChangeSuspended(FALSE)  
{  
    if(fSuspendNow)  
        Suspend();  
}  
CSuspendFileChanges::~CSuspendFileChanges()  
{  
    Resume();  
}  
void CSuspendFileChanges::Suspend()  
{  
    USES_CONVERSION;  
  
    // Prevent suspend from suspending more than once.  
    if(m_fFileChangeSuspended)  
        return;  
  
    IVsRunningDocumentTable* pRDT =   
      _VxModule.GetIVsRunningDocumentTable();  
    ASSERT(pRDT);  
    if (!pRDT)  
        return;  
  
    CComPtr<IUnknown> srpDocData;  
    VSCOOKIE vscookie = VSCOOKIE_NIL;  
    pRDT->FindAndLockDocument(RDT_NoLock, T2COLE(m_strMkDocument),    
      NULL, NULL, &srpDocData, &vscookie);  
    if ( (vscookie == VSCOOKIE_NIL) || !srpDocData)  
        return;  
    CComPtr<IVsFileChangeEx> srpIVsFileChangeEx;  
    HRESULT hr = _VxModule.QueryService(SID_SVsFileChangeEx,   
      IID_IVsFileChangeEx, (void **)&srpIVsFileChangeEx);  
    if (SUCCEEDED(hr) && srpIVsFileChangeEx)  
    {  
        m_fFileChangeSuspended = TRUE;  
        srpIVsFileChangeEx->IgnoreFile(NULL, m_strMkDocument, TRUE);   
        srpDocData->QueryInterface(IID_IVsDocDataFileChangeControl,   
          (void**)&m_srpIVsDocDataFileChangeControl);  
        if(m_srpIVsDocDataFileChangeControl)  
            m_srpIVsDocDataFileChangeControl->IgnoreFileChanges(TRUE);  
    }  
}  
void CSuspendFileChanges::Resume()  
{  
    if(!m_fFileChangeSuspended)  
        return;  
  
    CComPtr<IVsFileChangeEx> srpIVsFileChangeEx;  
    HRESULT hr = _VxModule.QueryService(SID_SVsFileChangeEx,   
      IID_IVsFileChangeEx, (void **)&srpIVsFileChangeEx);  
    if (SUCCEEDED(hr) && srpIVsFileChangeEx)  
  
    srpIVsFileChangeEx->IgnoreFile(NULL, m_strMkDocument, FALSE);   
    if(m_srpIVsDocDataFileChangeControl)  
        m_srpIVsDocDataFileChangeControl->IgnoreFileChanges(FALSE);  
    m_fFileChangeSuspended = FALSE;  
    m_srpIVsDocDataFileChangeControl.Release();  
}  
// Misc. helper classes  
```  
  
## <a name="robust-programming"></a>可靠编程  
 如果您的案例涉及多项更改的文件，如下所示的 SCC，这种情况然后务必继续发出警报的文档数据，就可以继续监视文件更改前执行全局文件更改通知。
